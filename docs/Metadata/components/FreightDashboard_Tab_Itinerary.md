---
layout: default
title: FreightDashboard_Tab_Itinerary
parent: components
grand_parent: Metadata
---
# Metadata Type
components


# Filename 
FreightDashboard_Tab_Itinerary


# Raw XML
```
<apex:component layout="block" controller="FreightDashboardController">
    <apex:attribute name="vopportunity" type="Opportunity" description="opportunity master" assignTo="{!opportunity}" />
    <apex:attribute name="vopportunityid" type="String" description="opportunity id" assignTo="{!opportunityId}" />
    <apex:attribute name="vdateToday" type="String" description="date today" assignTo="{!dateToday}" />
    <apex:attribute name="itineraryfiltr" type="Itinerary__c" description="itinerary filter" assignTo="{!itineraryFilter}" />
    <apex:attribute name="itinerarylst" type="Itinerary__c[]" description="itinerary list" assignTo="{!itineraryList}" />
    <apex:attribute name="vnewtrip" type="Freight__c" description="new trip" assignTo="{!newtrip}" />
    <apex:attribute name="vnewitinerary" type="Itinerary__c" description="new itinerary" assignTo="{!newitinerary}" />
    <apex:attribute name="vnewtrip_startcity" type="String" description="city name" assignTo="{!newtrip_startcity}" />
    <apex:attribute name="vnewtrip_endcity" type="String" description="city name" assignTo="{!newtrip_endcity}" />
    <apex:attribute name="vnewtrip_clear" type="Boolean" description="new trip clear" assignTo="{!newtrip_clear}" />
    <apex:attribute name="vehiclesByTripMap" type="map" description="vehicles by trip map" />
    <apex:attribute name="vstatusItineraryPL" type="SelectOption[]" description="status itinerary picklist" assignTo="{!statusItineraryPL}" />
    <apex:attribute name="vgrouptypeJson" type="String" description="group type json" assignTo="{!grouptypeJson}" />
    <apex:attribute name="tripsItineraryMap" type="map" description="trip itinerary map" />
    <apex:attribute name="tripsItineraryCountMap" type="map" description="trip itinerary count map" />
    <apex:attribute name="travelsItineraryMap" type="map" description="travel itinerary map" />
    <apex:attribute name="travelsItineraryCountMap" type="map" description="travel itinerary count map" />
    <apex:attribute name="ratesByBidMap" type="map" description="rate map" />
    <apex:attribute name="bidContractByGTMap" type="map" description="bid by gt map" />
    <apex:attribute name="itinerarySummary_congaQueriesJson" type="String" description="Conga queries"/>
    <apex:attribute name="itinerarySummary_congaTemplateId" type="String" description="Conga template id for Itinerary Summary"/>
    <apex:attribute name="vlimitItinerary" type="Integer" description="limit itineraries" assignTo="{!limitItinerary}" />
    <apex:attribute name="voffsetItinerary" type="Integer" description="offset itineraries" assignTo="{!offsetItinerary}" />
    <apex:attribute name="vtotalPagesItinerary" type="Integer" description="total pages itineraries" assignTo="{!totalPagesItinerary}" />
    <apex:attribute name="vorderFieldItinerary" type="String" description="order field itinerary" assignTo="{!orderFieldItinerary}" />
    <apex:attribute name="vorderOrientationItinerary" type="String" description="order orientation itinerary" assignTo="{!orderOrientationItinerary}" />
    
    <apex:inputHidden id="date_today" value="{!dateToday}" />
    <div class="expand">
        <div class="row">
            <div class="col-md-12 text-right">
                <button type="button" class="btn btn-danger btn-sm btn-custom" onclick="congaPreviewItinerarySummary('{!opportunityId}', '{!JSENCODE(itinerarySummary_congaQueriesJson)}', '{!itinerarySummary_congaTemplateId}')" >Preview Itinerary Summary</button>
                <!--<button type="button" class="btn btn-danger btn-sm btn-custom" onclick="congaItineraryDetailsJs()" >Preview Itinerary Details</button>-->
                <button type="button" class="btn btn-success btn-sm btn-custom" onclick="newTrip();" ><i class="fa fa-plus"></i> Add New Trip</button>
                <button type="button" class="btn btn-secondary btn-sm btn-custom btn-expand-all-itinerary" onclick="expandAllItinerary();">Expand All</button>
                <span style="font-size:15px;margin-left:15px;">Production ID: </span><span style="font-weight:bold;font-size:15px;">{!opportunity.Production_ID__c}</span>
            </div>
        </div>
        <div class="row">
            <div class="col-md-2">
                <label>Start Date</label><br/>
                <apex:inputField id="itinerarystart" value="{!itineraryFilter.Start_Date__c}" styleClass="form-control form-control-sm" />
            </div>
            <div class="col-md-2">
                <label>End Date</label><br/>
                <apex:inputField id="itineraryend" value="{!itineraryFilter.End_Date__c}" styleClass="form-control form-control-sm" />
            </div>
            <div class="col-md-3">
                <label>Vendor</label>
                <!--<apex:inputField id="itineraryvendor" value="{!itineraryFilter.Freight__r.Vendor_lookup__c}" styleClass="form-control form-control-sm" />-->
                <input id="itineraryvendor" class="form-control form-control-sm gtitinerary-vendor" onkeyup="setInputItineraryVendor();" />
                <script>
                createAutocompleteItineraryVendor = false;
                </script>
            </div>
            <div class="col-md-2">
                <label>City</label>
                <!--<apex:inputField id="itinerarycity" value="{!itineraryFilter.City__c}" styleClass="form-control form-control-sm" />-->
                <input id="gtitinerary_city" class="form-control form-control-sm gtitinerary-city" onkeyup="setInputItineraryCity();" />
                <script>
                createAutocompleteItineraryCity = false;
                </script>
            </div>
            <div class="col-md-3">
                <label>Status</label>
                <apex:inputField id="itinerarystatus" value="{!itineraryFilter.Status__c}" styleClass="form-control form-control-sm" />
            </div>
        </div>
        <div class="row">
            <div class="col-md-9">
                <span style="margin-left: 10px;">
                    <input class="form-check-input" type="checkbox" value="" id="itinerary_showprior" style="margin-left: -5px;margin-top: 3px;" /> <label style="margin-left:12px;">Show Prior Trips</label>
                </span>
                <span style="margin-left: 35px;">
                    <input class="form-check-input" type="checkbox" value="" id="itinerary_showcontracted" style="margin-left: -5px;margin-top: 3px;" /> <label style="margin-left:12px;">Show Contracted on own</label>
                </span>
                <span style="margin-left: 35px;">
                    <input class="form-check-input" type="checkbox" value="" id="itinerary_showcancelled" style="margin-left: -5px;margin-top: 3px;" /> <label style="margin-left:12px;">Show Cancelled</label>
                </span>
            </div>
            <div class="col-md-3">
                <button type="button" class="btn btn-info btn-sm btn-custom" onclick="searchItinerary();">Search</button>
                <button type="button" class="btn btn-info btn-sm btn-custom" onclick="clearItineraryFields();">Clear</button>
            </div>
        </div>
    </div>
    <div>
        <apex:outputPanel id="itineraryPanel">
            <div class="row">
                <div class="col-md-12">
                    <input type="hidden" value="{!limitItinerary}" id="listtrip_limitItinerary" />
                    <input type="hidden" value="{!offsetItinerary}" id="listtrip_offsetItinerary" />
                    <input type="hidden" value="{!totalPagesItinerary}" id="listtrip_totalPagesItinerary" />
                    <div style="display: flex; padding: 4px; background-color:#e9ecef; border: 1px solid #dee2e6;">
                        <div style="flex: 1; display: flex; align-items: center;">
                            <button class="btn btn-secondary btn-sm filePaginator btn-nav-modal btn-listtrip-first" type="button" onclick="GotoPageItinerary('first');">
                                <i class="fas fa-step-backward"></i>
                            </button>
                            <button class="btn btn-secondary btn-sm btn-nav-modal btn-listtrip-previous" type="button" style="padding-right: 3px;" onclick="GotoPageItinerary('previous');">
                                <i class="fas fa-caret-left fa-lg"></i>
                            </button>
                            <button class="btn btn-secondary btn-sm btn-nav-modal btn-listtrip-next" type="button" style="padding-left: 3px;" onclick="GotoPageItinerary('next');">
                                <i class="fas fa-caret-right fa-lg"></i>
                            </button>
                            <button class="btn btn-secondary btn-sm btn-nav-modal btn-listtrip-last" type="button" onclick="GotoPageItinerary('last');">
                                <i class="fas fa-step-forward"></i>
                            </button>
                        </div>
                        <div style="display: flex;">
                            <div class="fileNavigatorMessage" style="display: flex; flex: 1; align-self: center;">Page {!IF(OR(offsetItinerary == null,offsetItinerary <= 0),1,(offsetItinerary/limitItinerary)+1)} of {!totalPagesItinerary}</div>
                        </div>
                    </div>
                    <table class="table table-sm" style="margin-top:0;margin-bottom:0;">
                        <thead class="thead-light">
                            <tr>
                                <th style="width:2%;"></th>
                                <th style="width:9%;">Start Date</th>
                                <th style="width:9%;">End Date</th>
                                <th style="width:10%;">Description</th>
                                <th style="width:10%;">Service Type</th>
                                <th style="width:10%;">Vendor</th>
                                <th style="width:10%;">Group</th>
                                <th style="width:10%;">Status</th>
                                <th style="width:10%;">Deadline Date</th>
                                <th style="width:10%;">Rate</th>
                                <th style="width:10%;">Action</th>
                            </tr>
                        </thead>
                        <tbody>
                            <apex:repeat value="{!itineraryList}" var="itinerary">
                                <tr>
                                    <td style="text-align:center;">
                                    	<a href="javascript:void(0);" onclick="expandItinerary(this);" class="view-itinerary-detail icon-right"><i class="fa fa-caret-right"></i></a>
                                    </td>
                                    <td>
                                        <apex:outputField value="{!itinerary.Start_Date__c}" />
                                    </td>
                                    <td>
                                        <apex:outputField value="{!itinerary.End_Date__c}" />
                                    </td>
                                    <td>
                                    	{!itinerary.Freight__r.Description__c}
                                    </td>
                                    <td>
                                    	{!itinerary.Freight__r.Service_Type__c}
                                    </td>
                                    <td>
                                    	{!IF(itinerary.Freight__r.Vendor_lookup__c <> null,itinerary.Freight__r.Vendor_lookup__r.Name,'')} <span style="color:red;{!IF(itinerary.Freight__r.Vendor_lookup__c <> null,'display:none;','')}">Vendor TBD</span>
                                    </td>
                                    <td>
                                    	{!itinerary.Freight__r.Group_Type__c}
                                    </td>
                                    <td>
                                    	{!itinerary.Freight__r.Status__c}
                                    </td>
                                    <td>
                                        <apex:outputField value="{!itinerary.Freight__r.Deadline_Date__c}" />
                                    </td>
                                    <td>
                                        <apex:outputText value="${0,number,###,##0.00}">
                                            <apex:param value="{!ratesByBidMap[itinerary.Freight__c].Total_Price__c}"/>
                                        </apex:outputText>
                                    </td>
                                    <td>
                                    	<button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="editItinerary('{!itinerary.Id}','{!itinerary.Freight__r.Name}');"><i class="fa fa-pencil"></i> Edit</button>
                                    </td>
                                </tr>
                                <tr class="itinerary-hidden" style="display:none;">
                                    <td></td>
                                	<td colspan="10">
                                    	<div class="fieldset" style="margin-top: 0 !important;">
                                            <div>
                                                <div>
                                                    <span style="font-weight:bold;">Trip ID: {!itinerary.Freight__r.Name} (<a href="javascript:void(0);" onclick="viewTripDetailByItinerary('{!itinerary.Freight__c}')">Freight Dashboard</a>)</span>
                                                    <span style="font-weight:bold;{!IF(bidContractByGTMap[itinerary.Freight__c].id <> null,'','display:none;')}">- Bid ID: {!bidContractByGTMap[itinerary.Freight__c].Name} (<a href="javascript:void(0);" onclick="viewContractingDetailByItinerary('{!bidContractByGTMap[itinerary.Freight__c].Id}','{!bidContractByGTMap[itinerary.Freight__c].Freight__c}');">Contracting Dashboard</a>)</span>
                                                </div>
                                                <br/>
                                                <span style="color:red;{!IF(tripsItineraryCountMap[itinerary.Freight__c] > 0,'display:none;','')}">No Trips found</span>
                                                <div style="margin-bottom:5px;{!IF(tripsItineraryCountMap[itinerary.Freight__c] > 0,'','display:none;')}">
                                                    <apex:repeat value="{!tripsItineraryMap[itinerary.Freight__c]}" var="tripitinerary">
                                                    	<span style="font-weight:bold;">Trip Type : {!tripitinerary.Sub_Trip_Type__c} | Description: {!tripitinerary.Description__c}</span>
                                                        <br/><span>Travel Information:</span>
                                                        <br/><span style="color:red;{!IF(travelsItineraryCountMap[tripitinerary.Id] > 0,'display:none;','')}">No Travel Information Records Found</span>
                                                        <div style="{!IF(travelsItineraryCountMap[tripitinerary.Id] > 0,'','display:none;')}">
                                                            <table class="table table-sm" style="margin-bottom:0;">
                                                                <thead class="thead-light">
                                                                    <tr>
                                                                        <th style="width:15%;">Equipment</th>
                                                                        <th style="width:10%;">Start Date</th>
                                                                        <th style="width:10%;">End Date</th>
                                                                        <th style="width:10%;">Type</th>
                                                                        <th style="width:10%;">Location Type</th>
                                                                        <th style="width:10%;">Group</th>
                                                                        <th style="width:10%;">Location Details</th>
                                                                        <th style="width:15%;">Notes</th>
                                                                        <th style="width:10%;">Trip Notes</th>
                                                                    </tr>
                                                                </thead>
                                                                <tbody>
                                                                    <apex:repeat value="{!travelsItineraryMap[tripitinerary.Id]}" var="travelitinerary">
                                                                        <tr>
                                                                            <td>{!travelitinerary.Equipment__c}</td>
                                                                            <td>
                                                                                <apex:outputField value="{!travelitinerary.Start_Date__c}" />
                                                                            </td>
                                                                            <td>
                                                                                <apex:outputField value="{!travelitinerary.End_Date__c}" />
                                                                            </td>
                                                                            <td>{!travelitinerary.Travel_Type__c}</td>
                                                                            <td>{!travelitinerary.Location_Type__c}</td>
                                                                            <td>{!travelitinerary.Group_Type__c}</td>
                                                                            <td>{!travelitinerary.Location_Details__c}</td>
                                                                            <td>{!travelitinerary.Airline_Info_Special_Notes__c}</td>
                                                                            <td>{!travelitinerary.Sub_Trip_Notes__c}</td>
                                                                        </tr>
                                                                    </apex:repeat>
                                                                </tbody>
                                                            </table>
                                                        </div>
                                                    </apex:repeat>
                                                </div>
                                                <br/><span>Vehicle Details</span>
                                                <table class="table table-sm" style="margin-top:5px;margin-bottom:0;">
                                                    <thead class="thead-light">
                                                        <tr>
                                                            <th style="width:20%;">Equipment</th>
                                                            <th style="width:20%;">Description</th>
                                                            <th style="width:60%;">Amenities</th>
                                                        </tr>
                                                    </thead>
                                                    <tbody>
                                                        <apex:repeat value="{!vehiclesByTripMap[itinerary.Freight__c]}" var="vehiclebytrip">
                                                            <tr>
                                                                <td>{!vehiclebytrip.Equipment__c}</td>
                                                                <td>{!vehiclebytrip.Make__c} {!vehiclebytrip.Model__c}</td>
                                                                <td>{!vehiclebytrip.Amenities__c}</td>
                                                            </tr>
                                                        </apex:repeat>
                                                    </tbody>
                                                </table>
                                            </div>
                                        </div>
                                    </td>
                                </tr>
                            </apex:repeat>
                            <tr style="{!IF(itineraryList.size > 0,'display:none;','')}">
                            	<td colspan="11" style="text-align:center;color:red">No records found</td>
                            </tr>
                        </tbody>
                    </table>
                    <div style="display: flex; padding: 4px; background-color:#e9ecef; border: 1px solid #dee2e6;">
                        <div style="flex: 1; display: flex; align-items: center;">
                            <button class="btn btn-secondary btn-sm filePaginator btn-nav-modal btn-listtrip-first" type="button" onclick="GotoPageItinerary('first');">
                                <i class="fas fa-step-backward"></i>
                            </button>
                            <button class="btn btn-secondary btn-sm btn-nav-modal btn-listtrip-previous" type="button" style="padding-right: 3px;" onclick="GotoPageItinerary('previous');">
                                <i class="fas fa-caret-left fa-lg"></i>
                            </button>
                            <button class="btn btn-secondary btn-sm btn-nav-modal btn-listtrip-next" type="button" style="padding-left: 3px;" onclick="GotoPageItinerary('next');">
                                <i class="fas fa-caret-right fa-lg"></i>
                            </button>
                            <button class="btn btn-secondary btn-sm btn-nav-modal btn-listtrip-last" type="button" onclick="GotoPageItinerary('last');">
                                <i class="fas fa-step-forward"></i>
                            </button>
                        </div>
                        <div style="display: flex;">
                            <div class="fileNavigatorMessage" style="display: flex; flex: 1; align-self: center;">Page {!IF(OR(offsetItinerary == null,offsetItinerary <= 0),1,(offsetItinerary/limitItinerary)+1)} of {!totalPagesItinerary}</div>
                        </div>
                    </div>
                </div>
            </div>
        </apex:outputPanel>
    </div>
    <!-- Modal content-->
    <div class="modal fade" id="newTripModal" role="dialog">
        <div class="modal-dialog modal-xl">
            <div class="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title">New Trip</h4>
                    <button type="button" class="close" data-dismiss="modal">&times;</button>
                </div>
                <apex:outputPanel id="newTripPanel">
                    <span class="create-trip-id" style="display:none;">{!newtrip.Id}</span>
                    <div class="modal-body">
                        <div class="row">
                            <div class="col-md-6">
                                <label>Start Date <span style="color:red;">*</span></label><br/>
                                <apex:inputField id="newtrip_startdate" value="{!newtrip.Start_Date__c}" styleClass="form-control form-control-sm" />
                            </div>
                            <div class="col-md-6">
                                <label>End Date <span style="color:red;">*</span></label><br/>
                                <apex:inputField id="newtrip_enddate" value="{!newtrip.End_Date__c}" styleClass="form-control form-control-sm" />
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-6">
                                <label>Start City</label> <br/>
                                <apex:inputText id="newtrip_startcity" value="{!newtrip_startcity}" styleClass="form-control form-control-sm startCitySearch" onkeyup="setInput();" />
                                <input type="hidden" class="form-control form-control-sm" id="newtrip_startcityid" value="{!newtrip.Start_City__c}" />
                            </div>
                            <div class="col-md-6">
                                <label>End City</label> <br/>
                                <apex:inputText id="newtrip_endcity" value="{!newtrip_endcity}" styleClass="form-control form-control-sm endCitySearch" onkeyup="setInput();" />
                                <input type="hidden" class="form-control form-control-sm" id="newtrip_endcityid" value="{!newtrip.End_City__c}" />
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-6">
                                <label>Description</label><br/>
                                <apex:inputText id="newtrip_description" value="{!newtrip.Description__c}" styleClass="form-control form-control-sm" />
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-6">
                                <label>Freight Preferences <span style="color:red;">*</span></label><br/>
                                <apex:inputField value="{!newtrip.Freight_Preferences__c}" id="newtrip_gtpreferences" styleClass="form-control form-control-sm" />
                            </div>
                            <div class="col-md-6">
                                <label>Status</label><br/>
                                <!--<apex:inputField id="newtrip_status" value="{!newtrip.Status__c}" styleClass="form-control form-control-sm" />-->
                                <apex:selectList size="1" id="newtrip_status" value="{!newtrip.Status__c}" styleClass="form-control form-control-sm">
                                    <apex:selectOptions value="{!statusItineraryPL}" />
                                </apex:selectList>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-6">
                                <label>Trace Date</label><br/>
                                <apex:inputField id="newtrip_tracedate" value="{!newtrip.Trace_Date__c}" styleClass="form-control form-control-sm" />
                            </div>
                            <div class="col-md-6">
                                <label>Deadline Date</label><br/>
                                <apex:inputField id="newtrip_deadlinedate" value="{!newtrip.Deadline_Date__c}" styleClass="form-control form-control-sm" />
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-6">
                                <label>Group Type</label><br/>
                                <input type="hidden" class="data-original-grouptype" value="{!newtrip.Group_Type__c}"  style="display:none;" />
                                <input class="form-control form-control-sm new-trip-grouptype" id="newtrip_grouptype" value="{!newtrip.Group_Type__c}"/>
                                <script>
                                $('input[id$=newtrip_grouptype]').inputpicker({
                                    data: {!grouptypeJson},
                                    fields:[
                                        {name:'dataname',text:'Name'}
                                    ],
                                    fieldText: 'dataname',
                                    fieldValue: 'dataid',
                                    headShow: false,
                                    filterOpen: true,
                                    autoOpen: false
                                });
                                </script>
                            </div>
                            <div class="col-md-6">
                                <label>Service Type <span style="color:red;">*</span></label><br/>
                                <apex:inputField id="newtrip_servicetype" value="{!newtrip.Service_Type__c}" styleClass="form-control form-control-sm" />
                            </div>
                        </div>
                    </div>
                    <script>
                    createAutocomplete = false;
                    </script>
                </apex:outputPanel>
                <div class="modal-footer" style="display: block;">
                    <apex:outputPanel id="newTripButtonsPanel">
                        <button type="button" class="btn btn-danger btn-sm btn-save-new-trip" onclick="saveAndNewTrip();" >Save &amp; New</button>
                        <button type="button" class="btn btn-danger btn-sm btn-save-close-trip" onclick="saveAndCloseTrip();" >Save &amp; Close</button>
                        <button type="button" class="btn btn-danger btn-sm btn-delete-trip" onclick="deleteTrip('{!newtrip.Id}');" style="{!IF(AND(newtrip.Id <> NULL,newtrip.Status__c=='Itinerary Received'),'','display:none;')}">Delete</button>
                        <button type="button" class="btn btn-danger btn-sm btn-create-trip-journal" onclick="openCreateJournal('','trip');" >Trip Journal</button>
                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-close-new-trip" onclick="javascript:void(0);" data-dismiss="modal" >Close</button>
                    </apex:outputPanel>
                </div>
            </div>
        </div>
    </div>
    <!-- End Modal -->
    <script>
    $(function(){
        verifyButtonsListItinerary();
    });
    function verifyButtonsListItinerary(){
        var limit = $('input[id$=listtrip_limitItinerary]').val();
        var offset = parseInt($('input[id$=listtrip_offsetItinerary]').val()) || 0;
        var totalpages = $('input[id$=listtrip_totalPagesItinerary]').val();
        $('.btn-listtrip-first').prop('disabled',false);
        $('.btn-listtrip-previous').prop('disabled',false);
        $('.btn-listtrip-next').prop('disabled',false);
        if(offset == null || offset <= 0){
            $('.btn-listtrip-first').prop('disabled',true);
            $('.btn-listtrip-previous').prop('disabled',true);
        }
        var actual_page = 1;
        if(offset == null || offset <= 0) actual_page = 1; else actual_page = (offset/limit)+1;
        if(totalpages == actual_page){
            $('.btn-listtrip-next').prop('disabled',true);
            $('.btn-listtrip-last').prop('disabled',true);
        }
    }
    function viewContractingDetailByItinerary(bidid,parentid){
        viewContractingDetailByItineraryJs(bidid,parentid);
    }
    function viewTripDetailByItinerary(val){
        viewTripDetailByItineraryJs(val);
    }
    function deleteTrip(val){
        deleteTripJs(val);
    }
    function setInputItineraryVendor(){
        if(createAutocompleteItineraryVendor == false){
            createAutocompleteItineraryVendor = true;
            $('.gtitinerary-vendor').autocomplete({
                lookup: function (query, done) {
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.FreightDashboardController.searchAccount}',query,'Freight Vendor',
                        function(result, event){
                            if (event.status) {
                                var t1 = result;
                                var results = t1.replace(/(&quot\;)/g,"\"").replace(/&#39;/g,"'").replace(/(&amp\;)/g,"&");
                                console.log('HERE: ' + results);
                                var resultAuto = {
                                    suggestions: JSON.parse(results)
                                };
                                done(resultAuto);
                            } else if (event.type === 'exception') {
                                
                            } else {
                                alert('other');
                            }
                        }, 
                        {escape: true}
                    );
                }
            });
        }
    }
    function setInputItineraryCity(){
        if(createAutocompleteItineraryCity == false){
            createAutocompleteItineraryCity = true;
            $('.gtitinerary-city').autocomplete({
                lookup: function (query, done) {
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.FreightDashboardController.searchCity}',query,
                        function(result, event){
                            if (event.status) {
                                var t1 = result;
                                var results = t1.replace(/(&quot\;)/g,"\"").replace(/&#39;/g,"'").replace(/(&amp\;)/g,"&");
                                console.log('HERE: ' + results);
                                var resultAuto = {
                                    suggestions: JSON.parse(results)
                                };
                                done(resultAuto);
                            } else if (event.type === 'exception') {
                                
                            } else {
                                alert('other');
                            }
                        }, 
                        {escape: true}
                    );
                }
            });
        }
    }
    function blockEditTrip(){
        $('input[id$=newtrip_startdate]').attr('disabled','disabled');
        $('input[id$=newtrip_enddate]').attr('disabled','disabled');
        var data_original = $('.data-original-grouptype').val();
        $('.new-trip-grouptype.inputpicker-input').val(data_original);
    }
    function openEditTrip(){
        blockEditTrip();
        openModal('newTripModal');
    }
    function editItinerary(val1,val2){
        $('#newTripModal').find('.modal-title').text('Edit Trip ' + val2);
        $('#newTripModal').find('.modal-footer .btn-close-new-trip').show();
        editTripJs(val1);
    }
    function expandAllItinerary(){
        if($('.btn-expand-all-itinerary').text() == 'Expand All'){
            $(".view-itinerary-detail").each(function(){ 
                $(this).html('<i class="fa fa-caret-down"></i>');
                $(this).removeClass('icon-right');
                $(this).addClass('icon-down');
                $(this).parents('tr').next('.itinerary-hidden').show('slow');
            });
            $('.btn-expand-all-itinerary').text('Collapse All');
        }else{
            $(".view-itinerary-detail").each(function(){ 
                $(this).html('<i class="fa fa-caret-right"></i>');
                $(this).removeClass('icon-down');
                $(this).addClass('icon-right');
                $(this).parents('tr').next('.itinerary-hidden').hide('slow');
            });
            $('.btn-expand-all-itinerary').text('Expand All');
        }
    }
    function expandItinerary(val){
        if($(val).hasClass('icon-right')){
            $(val).html('<i class="fa fa-caret-down"></i>');
            $(val).removeClass('icon-right');
            $(val).addClass('icon-down');
        }else{
            $(val).html('<i class="fa fa-caret-right"></i>');
            $(val).removeClass('icon-down');
            $(val).addClass('icon-right');
        }
        $(val).parents('tr').next('.itinerary-hidden').toggle('slow');
    }
    function newTrip(){
        $('#newTripModal').find('.modal-footer .btn-save-new-trip').text('Save & New');
        $('#newTripModal').find('.modal-footer .btn-save-close-trip').text('Save & Close');
        $('input[id$=newtrip_startdate]').removeClass('error-custom');
        $('input[id$=newtrip_enddate]').removeClass('error-custom');
        $('select[id$=newtrip_gtpreferences]').removeClass('error-custom');
        $('select[id$=newtrip_servicetype]').removeClass('error-custom');
        $('#newTripModal').find('.modal-title').text('New Trip');
        $('#newTripModal').find('.modal-footer .btn-create-trip-journal').text('Trip Journal');
        $('#newTripModal').find('.modal-footer .btn-close-new-trip').show();
        newTripJs();
    }
    function saveAndNewTrip(){
        $('input[id$=newtrip_startdate]').removeClass('error-custom');
        $('input[id$=newtrip_enddate]').removeClass('error-custom');
        $('select[id$=newtrip_gtpreferences]').removeClass('error-custom');
        $('select[id$=newtrip_servicetype]').removeClass('error-custom');
        if($('input[id$=newtrip_startdate]').val() != ''){
            if($('input[id$=newtrip_enddate]').val() != ''){
                var date_today = new Date($('input[id$=date_today]').val());
                var datein = $('input[id$=newtrip_startdate]').val();
                var dateout = $('input[id$=newtrip_enddate]').val();
                //var date1 = new Date(datein);
                //var date2 = new Date(dateout);
                var dataidtrip = $('span.create-trip-id').html();
                
                Visualforce.remoting.Manager.invokeAction(
                    '{!$RemoteAction.FreightDashboardController.validateDates}',datein,dateout,
                    function(result, event){
                        if (event.status) {
                            console.log(result);
                            if(result != ''){
                                if(result == 'Cannot post-date Start or End Date') $('input[id$=newtrip_enddate]').addClass('error-custom');
                                alert(result);
                            }else{
                                if($('select[id$=newtrip_gtpreferences]').val() != ''){
                                    if($('select[id$=newtrip_servicetype]').val() != ''){
                                        var startcityid = $('input[id$=newtrip_startcityid]').val();
                                        var endcityid = $('input[id$=newtrip_endcityid]').val();
                                        var newtrip_grouptype = $('.new-trip-grouptype.inputpicker-input').val();
                                        saveAndNewTripJs(startcityid,endcityid,newtrip_grouptype);
                                    }else{
                                        $('select[id$=newtrip_servicetype]').addClass('error-custom');
                                        alert('Service Type is required.');
                                    }
                                }else{
                                    $('select[id$=newtrip_gtpreferences]').addClass('error-custom');
                                    alert('Select Freight Preferences.');
                                }
                            }
                        } else if (event.type === 'exception') {
                            
                        } else {
                            alert('other');
                        }
                    }, 
                    {escape: true}
                );
            }else{
                $('input[id$=newtrip_enddate]').addClass('error-custom');
                alert('The End Date field is required');
            }
        }else{
            $('input[id$=newtrip_startdate]').addClass('error-custom');
            alert('The Start Date field is required');
        }
    }
    function saveAndCloseTrip(){
        $('input[id$=newtrip_startdate]').removeClass('error-custom');
        $('input[id$=newtrip_enddate]').removeClass('error-custom');
        $('select[id$=newtrip_gtpreferences]').removeClass('error-custom');
        $('select[id$=newtrip_servicetype]').removeClass('error-custom');
        if($('input[id$=newtrip_startdate]').val() != ''){
            if($('input[id$=newtrip_enddate]').val() != ''){
                var date_today = new Date($('input[id$=date_today]').val());
                var datein = $('input[id$=newtrip_startdate]').val();
                var dateout = $('input[id$=newtrip_enddate]').val();
                //var date1 = new Date(datein);
                //var date2 = new Date(dateout);
                var dataidtrip = $('span.create-trip-id').html();
                Visualforce.remoting.Manager.invokeAction(
                    '{!$RemoteAction.FreightDashboardController.validateDates}',datein,dateout,
                    function(result, event){
                        if (event.status) {
                            console.log(result);
                            if(result != ''){
                                if(result == 'Cannot post-date Start or End Date') $('input[id$=newtrip_enddate]').addClass('error-custom');
                                alert(result);
                            }else{
                                if($('select[id$=newtrip_gtpreferences]').val() != ''){
                                    if($('select[id$=newtrip_servicetype]').val() != ''){
                                        var startcityid = $('input[id$=newtrip_startcityid]').val();
                                        var endcityid = $('input[id$=newtrip_endcityid]').val();
                                        var newtrip_grouptype = $('.new-trip-grouptype.inputpicker-input').val();
                                        saveTripJs(startcityid,endcityid,newtrip_grouptype);
                                    }else{
                                        $('select[id$=newtrip_servicetype]').addClass('error-custom');
                                        alert('Service Type is required.');
                                    }
                                }else{
                                    $('select[id$=newtrip_gtpreferences]').addClass('error-custom');
                                    alert('Select Freight Preferences.');
                                }
                            }
                        } else if (event.type === 'exception') {
                            
                        } else {
                            alert('other');
                        }
                    }, 
                    {escape: true}
                );
            }else{
                $('input[id$=newtrip_enddate]').addClass('error-custom');
                alert('The End Date field is required');
            }
        }else{
            $('input[id$=newtrip_startdate]').addClass('error-custom');
            alert('The Start Date field is required');
        }
    }
    function setInput(){
        if(createAutocomplete == false){
            createAutocomplete = true;
            $('.startCitySearch').autocomplete({
                lookup: function (query, done) {
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.FreightDashboardController.searchCity}',query,
                        function(result, event){
                            if (event.status) {
                                var t1 = result;
                                var results = t1.replace(/(&quot\;)/g,"\"").replace(/&#39;/g,"'").replace(/(&amp\;)/g,"&");
                                console.log('HERE: ' + results);
                                var resultAuto = {
                                    suggestions: JSON.parse(results)
                                };
                                done(resultAuto);
                            } else if (event.type === 'exception') {
                                
                            } else {
                                alert('other');
                            }
                        }, 
                        {escape: true}
                    );
                },
                onSelect: function (suggestion) {
                    $('input[id$=newtrip_startcityid]').val(suggestion.data);
                    $('input[id$=newtrip_startcity]').val(suggestion.value);
                }
            });
            $('.endCitySearch').autocomplete({
                lookup: function (query, done) {
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.FreightDashboardController.searchCity}',query,
                        function(result, event){
                            if (event.status) {
                                var t1 = result;
                                var results = t1.replace(/(&quot\;)/g,"\"").replace(/&#39;/g,"'").replace(/(&amp\;)/g,"&");
                                console.log('HERE: ' + results);
                                var resultAuto = {
                                    suggestions: JSON.parse(results)
                                };
                                done(resultAuto);
                            } else if (event.type === 'exception') {
                                
                            } else {
                                alert('other');
                            }
                        }, 
                        {escape: true}
                    );
                },
                onSelect: function (suggestion) {
                    $('input[id$=newtrip_endcityid]').val(suggestion.data);
                    $('input[id$=newtrip_endcity]').val(suggestion.value);
                }
            });
        }
    }
    function searchItinerary(){
        var itinerary_start = $('input[id$=itinerarystart]').val();
        var itinerary_end = $('input[id$=itineraryend]').val();
        //var itinerary_city = $('input[id$=itinerarycity_lkid]').val() != '000000000000000' ? $('input[id$=itinerarycity_lkid]').val() : '';
        var itinerary_city = $('input[id$=gtitinerary_city]').val();
        //var itinerary_vendor = $('input[id$=itineraryvendor_lkid]').val() != '000000000000000' ? $('input[id$=itineraryvendor_lkid]').val() : '';
        var itinerary_vendor = $('input[id$=itineraryvendor]').val();
        var itinerary_status = $('select[id$=itinerarystatus]').val();
        var itinerary_showprior = $("input[id$=itinerary_showprior]").prop("checked");
        var itinerary_showcontracted = $("input[id$=itinerary_showcontracted]").prop("checked");
        var itinerary_showcancelled = $("input[id$=itinerary_showcancelled]").prop("checked");
        searchItineraryJs(itinerary_start,itinerary_end,itinerary_city,itinerary_vendor,itinerary_status,itinerary_showprior,itinerary_showcontracted,itinerary_showcancelled);
    }
    function clearItineraryFields(){
        $('input[id$=itinerarystart]').val('');
        $('input[id$=itineraryend]').val('');
        $('input[id$=gtitinerary_city]').val('');
        //$('input[id$=itinerarycity]').val('');
        //$('input[id$=itinerarycity_lkid]').val('');
        $('input[id$=itineraryvendor]').val('');
        //$('input[id$=itineraryvendor_lkid]').val('');
        $("input[id$=itinerary_showprior]").prop("checked", false);
        $("input[id$=itinerary_showcontracted]").prop("checked", false);
        $("input[id$=itinerary_showcancelled]").prop("checked", false);
        $('select[id$=itinerarystatus]').val('');
    }
    /*---@Conga: Update for Conga---*/
    function congaPreviewItinerarySummary(opportunityId, congaQueriesJson, congaTemplateId) { 
        var congaQueriesMap = JSON.parse(congaQueriesJson);
        window.open('/apex/APXTConga4__Conga_Composer?id=' + opportunityId + (congaQueriesMap.hasOwnProperty('Freight - ItineraryByOppId') ? '&QueryId=[Itinerary]' + congaQueriesMap['Freight - ItineraryByOppId'].Id + '?pv0=' + opportunityId : '') + '&TemplateId=' + congaTemplateId + '&OFN=Freight+Itinerary+Summary&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=800, resizable=yes, toolbar=no, location=no, status=yes');
    }
    </script>
</apex:component>
```


# Last Modified


# Usage
