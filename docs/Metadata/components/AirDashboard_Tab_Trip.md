---
layout: default
title: AirDashboard_Tab_Trip
parent: components
grand_parent: Metadata
---
# Metadata Type
components


# Filename 
AirDashboard_Tab_Trip


# Raw XML
```
<apex:component layout="block" controller="AirDashboardController" allowDML="true">
    <apex:attribute name="variables" type="DashboardConfigurationWrapper" assignTo="{!vfpConfiguration}" description="The variables of the VFP" required="true" />
    <apex:attribute name="vopportunity" type="Opportunity" description="opportunity master" assignTo="{!opportunity}" />
    <apex:attribute name="vopportunityid" type="String" description="opportunity id" assignTo="{!opportunityId}" />
    <apex:attribute name="vdateToday" type="String" description="today date" assignTo="{!dateToday}" />
    <apex:attribute name="vnewItineraryTrip" type="Air__c" description="new itinerary trip" assignTo="{!newItineraryTrip}" />
    <apex:attribute name="vitineraryTripList" type="Air__c[]" description="itinerary by trip" assignTo="{!itineraryTripList}" />
    <apex:attribute name="groundfiltr" type="Ground__c" description="itinerary filter" assignTo="{!groundFilter}" />
    <apex:attribute name="tripList" type="Air__c[]" description="trip list" />
    <apex:attribute name="vorderFieldTrip" type="String" description="order field trip" assignTo="{!orderFieldTrip}" />
    <apex:attribute name="vorderOrientationTrip" type="String" description="order orientation trip" assignTo="{!orderOrientationTrip}" />
    <apex:attribute name="vtripView" type="Air__c" description="trip view" assignTo="{!tripView}" />
    <apex:attribute name="vtripViewId" type="String" description="trip view id" assignTo="{!tripViewId}" />
    <apex:attribute name="vdocumentTripList" type="ContentDocument[]" description="document trip list" assignTo="{!documentTripList}" />
    <apex:attribute name="vbodytrip" type="String" description="body trip attachment" assignTo="{!bodytrip}" />
    <apex:attribute name="vjournalByTripList" type="Journal__c[]" description="journal by trip list" assignTo="{!journalByTripList}" />
    <apex:attribute name="journalByTripMap" type="map" description="journal by trip map" />
    <apex:attribute name="vclientsByProduction" type="SelectOption[]" description="clients by production list" assignTo="{!clientsByProduction}" />
    <apex:attribute name="vclientByProduction" type="Contact" description="client by production" assignTo="{!clientByProduction}" />
    <apex:attribute name="vcoordinatorGTName" type="String" description="coordinator GT name" assignTo="{!coordinatorGTName}" />
    <apex:attribute name="vteamMembers" type="SelectOption[]" description="team members list" assignTo="{!teamMembers}" />
    <apex:attribute name="vbackendcoordinatorGT" type="String" description="back end coordinator GT name" assignTo="{!backendcoordinatorGT}" />
    <apex:attribute name="vtabGroundDefault" type="String" description="tab ground default" assignTo="{!tabGroundDefault}" />
    <apex:attribute name="vbAuxWrapper" type="BidWrapper[]" description="trip aux list" assignTo="{!bAuxWrapper}" />    
    <apex:attribute name="vbidsByTripShowList" type="BidWrapper[]" description="trip list" assignTo="{!bidsByTripShowList}" />    
    <apex:attribute name="vOffsetSizeBids" type="Integer" description="off size bids" assignTo="{!OffsetSizeBids}"  />
    <apex:attribute name="vLimitSizeBids" type="Integer" description="limit size bids" assignTo="{!LimitSizeBids}"  />
    <apex:attribute name="vtotalRecsBids" type="Integer" description="total records bids" assignTo="{!totalRecsBids}"  />
    <apex:attribute name="vorderFieldBid" type="String" description="order field bid" assignTo="{!orderFieldBid}" />
    <apex:attribute name="vorderOrientationBid" type="String" description="order orientation bid" assignTo="{!orderOrientationBid}" />
    <apex:attribute name="vprevShowBid" type="Boolean" description="prev bids" assignTo="{!prevShowBid}" />
    <apex:attribute name="vnextShowBid" type="Boolean" description="prev bids" assignTo="{!nextShowBid}" />
    <apex:attribute name="vsearchVendorList" type="Account[]" description="search vendor list" assignTo="{!searchVendorList}" />
    <apex:attribute name="vdetailId" type="String" description="detail id vendor" assignTo="{!detailId}" />
    <apex:attribute name="vorderFieldVendor" type="String" description="order field vendor" assignTo="{!orderFieldVendor}" />
    <apex:attribute name="vorderOrientationVendor" type="String" description="order orientation vendor" assignTo="{!orderOrientationVendor}" />
    <apex:attribute name="vservicetypesPL" type="SelectOption[]" description="service type by account" assignTo="{!servicetypesPL}" />
    <apex:attribute name="vvendorFilter" type="Account" description="account filter" assignTo="{!vendorFilter}" />
    <apex:attribute name="sendBidRequestMap" type="map" description="send bid request map" />
    <apex:attribute name="sendBidRequestMapSelected" type="map" description="send bid request map selected" />
    <apex:attribute name="vsendBidRequestMapSize" type="Integer" description="send bid request map size" assignTo="{!sendBidRequestMapSize}" />
    <apex:attribute name="contactsByVendor_bidRequestMap" type="map" description="contacts by vendor bid request map" />
    <apex:attribute name="contactsByVendorParent_bidRequestMap" type="map" description="contacts by vendor parent bid request map" />
    <apex:attribute name="contactSelectOption_bidRequestMap" type="map" description="select option bid request map" />
    <apex:attribute name="contactSelectOption_bidRequestSizeMap" type="map" description="select option bid request size map" />
    <apex:attribute name="vbidSendBidFirstTime" type="Boolean" description="send bid first time boolean" assignTo="{!bidSendBidFirstTime}" />
    <apex:attribute name="vmessageCreateContact" type="String" description="message create contact" assignTo="{!messageCreateContact}" />
    <apex:attribute name="sendBidRequestMapRelease" type="map" description="release bid request map" />
    <apex:attribute name="sendBidRequestMapReleaseSelected" type="map" description="release bid request map selected" />
    <apex:attribute name="vsendBidRequestMapReleaseSize" type="Integer" description="release bid request map size" assignTo="{!sendBidRequestMapReleaseSize}" />  
    <apex:attribute name="contactsByVendor_releaseMap" type="map" description="contacts by vendor release bid map" />
    <apex:attribute name="contactsByVendorParent_releaseMap" type="map" description="contacts by vendor parent release bid map" />
    <apex:attribute name="contactSelectOption_releaseMap" type="map" description="select option release bid map" />
    <apex:attribute name="contactSelectOption_releaseSizeMap" type="map" description="select option release bid size map" />
    <apex:attribute name="vbidReleaseActive" type="Boolean" description="bid release active" assignTo="{!bidReleaseActive}" />  
    <apex:attribute name="vnewConcessionTrip" type="Concessions__c" description="new concession trip" assignTo="{!newConcessionTrip}" />
    <apex:attribute name="vconcessionsRequestedTrip" type="Concessions__c[]" description="concessions by trip list" assignTo="{!concessionsRequestedTrip}" />
    <apex:attribute name="vconcessions_concessionTypePL" type="SelectOption[]" description="concession type picklist" assignTo="{!concessions_concessionTypePL}" />
    <apex:attribute name="sendBidRequest_congaQueriesJson" type="String" description="Conga queries for sending bid request"/>
    <apex:attribute name="sendBidRequest_congaEmailTemplateId" type="String" description="Conga email template id for sending bid request"/>
    <apex:attribute name="sendBidRequest_congaEmailSubject" type="String" description="Conga email subject for sending bid request"/>
    <apex:attribute name="sendBidRequest_congaTemplateId1" type="String" description="Conga template id for sending bid request"/>
    <apex:attribute name="sendBidRequest_congaTemplateId2" type="String" description="Conga template id for sending bid request"/>
    <apex:attribute name="vnewAircraftTrip" type="Air__c" description="new aircraft trip" assignTo="{!newAircraftTrip}" />
    <apex:attribute name="vaircraftsByTripList" type="Air__c[]" description="aircrafts by trip list" assignTo="{!aircraftsByTripList}" />
    <apex:attribute name="vsubTripList" type="Ground__c[]" description="subtrip by trip list" assignTo="{!subTripList}" />
    <apex:attribute name="hasFreightMap" type="map" description="has freight map" />
    <apex:attribute name="travelsBySubTripMap" type="map" description="travels by subtrip map" />
    <apex:attribute name="vnewTravel" type="Ground__c" description="new travel" assignTo="{!newTravel}" />
    <apex:attribute name="vtravelActualId" type="String" description="travel actual id" assignTo="{!travelActualId}" />
    <apex:attribute name="vtravelActualOrder" type="String" description="travel actual id" assignTo="{!travelActualOrder}" />
    <apex:attribute name="vsearchLocationList" type="wrapperLocation[]" description="search location list" assignTo="{!searchLocationList}" />
    <apex:attribute name="vsearchlocation_type" type="String" description="search location type" assignTo="{!searchlocation_type}" />
    <apex:attribute name="vsearchLocationRelatedList" type="wrapperLocation[]" description="search location related list" assignTo="{!searchLocationRelatedList}" />
    <apex:attribute name="vstatusItineraryPL" type="SelectOption[]" description="status itinerary picklist" assignTo="{!statusItineraryPL}" />
    <apex:attribute name="vconcessionJson" type="String" description="additional fees values" assignTo="{!concessionJson}" />
    <apex:attribute name="vsearchVendor_CityGoogle" type="String" description="google value" assignTo="{!searchVendor_CityGoogle}" />
    <apex:attribute name="vbidsCreated" type="Integer" description="total bids created" assignTo="{!bidsCreated}" />  
    <apex:attribute name="bidRevenueMap" type="map" description="revenue by bid map" />
    <apex:attribute name="vdecisionDueDateContact" type="Contact" description="decision due date contact" assignTo="{!decisionDueDateContact}" />
    <apex:attribute name="vdraft" type="Draft__c" description="decision due date draft" assignTo="{!draft}" />
    <apex:attribute name="vbidDataDecision" type="Bid__c" description="decision due date bid" assignTo="{!bidDataDecision}" />
    <apex:attribute name="vattachDocumentList" type="ContentDocument[]" description="attach doc list" assignTo="{!attachDocumentList}" />
    <apex:attribute name="vbody" type="String" description="attach body" assignTo="{!body}" />
    <apex:attribute name="vnewattachment_id" type="String" description="new attach id" assignTo="{!newattachment_id}" />
    <apex:attribute name="vnewattachment_name" type="String" description="new attach name" assignTo="{!newattachment_name}" />
    <apex:attribute name="vtripview_option" type="Integer" description="trip view option" assignTo="{!tripview_option}" />
    <apex:attribute name="symbolMap" type="map" description="symbol map" />
    <apex:attribute name="visBidRequestRendered" type="Boolean" description="is bid request sent rendered" assignTo="{!isBidRequestRendered}" />
    <apex:attribute name="visBidReleaseRendered" type="Boolean" description="is bid release rendered" assignTo="{!isBidReleaseRendered}" />
    <apex:attribute name="vlimitTrip" type="Integer" description="limit trips" assignTo="{!limitTrip}" />
    <apex:attribute name="voffsetTrip" type="Integer" description="offset trips" assignTo="{!offsetTrip}" />
    <apex:attribute name="vtotalPagesTrip" type="Integer" description="total pages trips" assignTo="{!totalPagesTrip}" />
    <apex:attribute name="vlimitVendor" type="Integer" description="limit vendors" assignTo="{!limitVendor}" />
    <apex:attribute name="voffsetVendor" type="Integer" description="offset vendors" assignTo="{!offsetVendor}" />
    <apex:attribute name="vtotalPagesVendor" type="Integer" description="total pages vendors" assignTo="{!totalPagesVendor}" />
    
    <div class="row">
        <div class="col-md-12 text-right">
            <button type="button" class="btn btn-danger btn-sm btn-custom" onclick="createMultipleBids();" >Multi Bids to Vendor</button>
            <button type="button" class="btn btn-danger btn-sm btn-custom" onclick="loadTabContent('gt-itinerary');" >All Events</button>
            <apex:outputPanel id="tripInformationHeaderPanel">
            	<span style="font-size:15px;margin-left:15px;">Production ID: </span><span style="font-weight:bold;font-size:15px;">{!opportunity.Production_ID__c}</span> | 
                <span style="font-size:15px;margin-left:5px;">Trip ID: </span><span style="font-weight:bold;font-size:15px;">{!tripView.Name}</span>
            </apex:outputPanel>
        </div>
    </div>
    <div class="expand">
        <div class="row">
            <div class="col-md-2">
                <label>From Date</label><br/>
                <apex:inputField id="tripstart" value="{!groundFilter.Start_Date__c}" styleClass="form-control form-control-sm" />
            </div>
            <div class="col-md-2">
                <label>To Date</label><br/>
                <apex:inputField id="tripend" value="{!groundFilter.End_Date__c}" styleClass="form-control form-control-sm" />
            </div>
            
            <div class="col-md-2">
                <span style="margin-top: 25px;display: block;">
                    <label style="margin-left:12px;">Show Prior Trips</label> <input class="form-check-input" type="checkbox" value="" id="trip_showprior" style="margin-left: -5px;margin-top: 3px;" />
                </span>
            </div>
        </div>
        <div class="row">
            <div class="col-md-2">
                <label>City</label>
                <!--<apex:inputField id="tripcity" value="{!groundFilter.Start_City__c}" styleClass="form-control form-control-sm" />-->
                <input id="tripcity" class="form-control form-control-sm gttrip-city" onkeyup="setInputTripCity();" />
                <script>
                createAutocompleteTripCity = false;
                </script>
            </div>
            <div class="col-md-2">
                <label>Vendor</label>
                <!--<apex:inputField id="tripvendor" value="{!groundFilter.Vendor_lookup__c}" styleClass="form-control form-control-sm" />-->
                <input id="tripvendor" class="form-control form-control-sm gttrip-vendor" onkeyup="setInputTripVendor();" />
                <script>
                createAutocompleteTripVendor = false;
                </script>
            </div>
            <div class="col-md-2">
                <div style="margin-top: 25px;">
                    <label style="margin-left:12px;">Show Cancelled</label> <input class="form-check-input" type="checkbox" value="" id="trip_showcancelled" style="margin-left: -5px;margin-top: 3px;" />
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col-md-3">
                <button type="button" class="btn btn-info btn-sm btn-custom" onclick="searchTrip();">Search</button>
                <button type="button" class="btn btn-info btn-sm btn-custom" onclick="clearTripFields();">Clear</button>
            </div>
        </div>
        <apex:outputPanel id="tripListPanel">
            <div class="row">
                <div class="col-md-12">
                    <apex:inputHidden id="orderFieldTripActual" value="{!orderFieldTrip}" />
                    <input type="hidden" value="{!limitTrip}" id="listtrip_limitTrip" />
                    <input type="hidden" value="{!offsetTrip}" id="listtrip_offsetTrip" />
                    <input type="hidden" value="{!totalPagesTrip}" id="listtrip_totalPagesTrip" />
                    <div style="display: flex; padding: 4px; background-color:#e9ecef; border: 1px solid #dee2e6;">
                        <div style="flex: 1; display: flex; align-items: center;">
                            <button class="btn btn-secondary btn-sm filePaginator btn-nav-modal btn-listtrip-first" type="button" onclick="GotoPageTrip('first');">
                                <i class="fas fa-step-backward"></i>
                            </button>
                            <button class="btn btn-secondary btn-sm btn-nav-modal btn-listtrip-previous" type="button" style="padding-right: 3px;" onclick="GotoPageTrip('previous');">
                                <i class="fas fa-caret-left fa-lg"></i>
                            </button>
                            <button class="btn btn-secondary btn-sm btn-nav-modal btn-listtrip-next" type="button" style="padding-left: 3px;" onclick="GotoPageTrip('next');">
                                <i class="fas fa-caret-right fa-lg"></i>
                            </button>
                            <button class="btn btn-secondary btn-sm btn-nav-modal btn-listtrip-last" type="button" onclick="GotoPageTrip('last');">
                                <i class="fas fa-step-forward"></i>
                            </button>
                        </div>
                        <div style="display: flex;">
                            <div class="fileNavigatorMessage" style="display: flex; flex: 1; align-self: center;">Page {!IF(OR(offsetTrip == null,offsetTrip <= 0),1,(offsetTrip/limitTrip)+1)} of {!totalPagesTrip}</div>
                        </div>
                    </div>
                    <table id="dataTrips" class="table table-sm" style="margin-top:0;margin-bottom:0;">
                        <thead class="thead-light">
                            <tr>
                                <th style="width:10%;">
                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortTrips('Departure_Date__c','{!orderOrientationTrip}');">
                                        <span style="float:left;">Departure Date</span>
                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldTrip == 'Departure_Date__c',orderOrientationTrip == 'DESC'),'','display:none;')}"></i>
                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldTrip == 'Departure_Date__c',orderOrientationTrip == 'ASC'),'','display:none;')}"></i>
                                    </a>
                                </th>
                                <th style="width:10%;">
                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortTrips('Dep_Arr__c','{!orderOrientationTrip}');">
                                        <span style="float:left;">Dep/Arr</span>
                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldTrip == 'Dep_Arr__c',orderOrientationTrip == 'DESC'),'','display:none;')}"></i>
                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldTrip == 'Dep_Arr__c',orderOrientationTrip == 'ASC'),'','display:none;')}"></i>
                                    </a>
                                </th>
                                <th style="width:10%;">
                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortTrips('Return_Date__c','{!orderOrientationTrip}');">
                                        <span style="float:left;">RT Date</span>
                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldTrip == 'Return_Date__c',orderOrientationTrip == 'DESC'),'','display:none;')}"></i>
                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldTrip == 'Return_Date__c',orderOrientationTrip == 'ASC'),'','display:none;')}"></i>
                                    </a>
                                </th>
                                <th style="width:10%;">
                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortTrips('RT_Dep_Arr__c','{!orderOrientationTrip}');">
                                        <span style="float:left;">RT Dep/Arr</span>
                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldTrip == 'RT_Dep_Arr__c',orderOrientationTrip == 'DESC'),'','display:none;')}"></i>
                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldTrip == 'RT_Dep_Arr__c',orderOrientationTrip == 'ASC'),'','display:none;')}"></i>
                                    </a>
                                </th>
                                <th style="width:10%;">
                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortTrips('Trip_Type__c','{!orderOrientationTrip}');">
                                        <span style="float:left;">Trip Type</span>
                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldTrip == 'Trip_Type__c',orderOrientationTrip == 'DESC'),'','display:none;')}"></i>
                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldTrip == 'Trip_Type__c',orderOrientationTrip == 'ASC'),'','display:none;')}"></i>
                                    </a>
                                </th>
                                <th style="width:18%;">
                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortTrips('Vendor__r.Name','{!orderOrientationTrip}');">
                                        <span style="float:left;">Vendor</span>
                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldTrip == 'Vendor__r.Name',orderOrientationTrip == 'DESC'),'','display:none;')}"></i>
                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldTrip == 'Vendor__r.Name',orderOrientationTrip == 'ASC'),'','display:none;')}"></i>
                                    </a>
                                </th>
                                <th style="width:6%;">
                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortTrips('PAX__c','{!orderOrientationTrip}');">
                                        <span style="float:left;">#PAX</span>
                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldTrip == 'PAX__c',orderOrientationTrip == 'DESC'),'','display:none;')}"></i>
                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldTrip == 'PAX__c',orderOrientationTrip == 'ASC'),'','display:none;')}"></i>
                                    </a>
                                </th>
                                <th style="width:8%;">
                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortTrips('Baggage__c','{!orderOrientationTrip}');">
                                        <span style="float:left;">Baggage</span>
                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldTrip == 'Baggage__c',orderOrientationTrip == 'DESC'),'','display:none;')}"></i>
                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldTrip == 'Baggage__c',orderOrientationTrip == 'ASC'),'','display:none;')}"></i>
                                    </a>
                                </th>
                                <th style="width:8%;">
                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortTrips('Decision_Due_Date__c','{!orderOrientationTrip}');">
                                        <span style="float:left;">Decision Due Date</span>
                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldTrip == 'Decision_Due_Date__c',orderOrientationTrip == 'DESC'),'','display:none;')}"></i>
                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldTrip == 'Decision_Due_Date__c',orderOrientationTrip == 'ASC'),'','display:none;')}"></i>
                                    </a>
                                </th>
                                <th style="width:12%;">
                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortTrips('Status__c','{!orderOrientationTrip}');">
                                        <span style="float:left;">Status</span>
                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldTrip == 'Status__c',orderOrientationTrip == 'DESC'),'','display:none;')}"></i>
                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldTrip == 'Status__c',orderOrientationTrip == 'ASC'),'','display:none;')}"></i>
                                    </a>
                                </th>
                            </tr>
                        </thead>
                        <tbody>
                            <apex:repeat value="{!tripList}" var="trip">
                                <tr onclick="selectRowTrip(this);" vid="{!trip.Id}">
                                    <td>
                                        <a href="javascript:void(0);" onclick="viewTripDetail(event,'{!trip.Id}');">
                                            <apex:outputField value="{!trip.Departure_Date__c}" />
                                        </a>
                                    </td>
                                    <td>
                                        {!trip.Dep_Arr__c}
                                    </td>
                                    <td>
                                        <apex:outputField value="{!trip.Return_Date__c}" />
                                    </td>
                                    <td>
                                        {!trip.RT_Dep_Arr__c}
                                    </td>
                                    <td>
                                        {!trip.Trip_Type__c}
                                    </td>
                                    <td>
                                        <span style="color:red;{!IF(AND(trip.Vendor__c <> null,trip.Vendor__c <> ''),'display:none;','')}">Vendor TBD</span>
                                        <a href="/{!trip.Vendor__c}" target="_blank" style="{!IF(AND(trip.Vendor__c <> null,trip.Vendor__c <> ''),'','display:none;')}">{!trip.Vendor__r.Name}</a>
                                    </td>
                                    <td>
                                        {!trip.PAX__c}
                                    </td>
                                    <td>
                                        {!trip.Baggage__c}
                                    </td>
                                    <td>
                                        <apex:outputField value="{!trip.Decision_Due_Date__c}" />
                                    </td>
                                    <td>
                                        {!trip.Status__c}
                                    </td>
                                </tr>
                            </apex:repeat>
                            <tr style="{!IF(tripList.size > 0,'display:none;','')}">
                            	<td colspan="8" style="text-align:center;color:red">No records found</td>
                            </tr>
                        </tbody>
                    </table>
                    <div id="fileNavigatorTop" style="display: flex; padding: 4px; background-color:#e9ecef; border: 1px solid #dee2e6;">
                        <div style="flex: 1; display: flex; align-items: center;">
                            <button class="btn btn-secondary btn-sm filePaginator btn-nav-modal btn-listtrip-first" type="button" onclick="GotoPageTrip('first');">
                                <i class="fas fa-step-backward"></i>
                            </button>
                            <button class="btn btn-secondary btn-sm filePaginator btn-nav-modal btn-listtrip-previous" type="button" style="padding-right: 3px;" onclick="GotoPageTrip('previous');">
                                <i class="fas fa-caret-left fa-lg"></i>
                            </button>
                            <button class="btn btn-secondary btn-sm filePaginator btn-nav-modal btn-listtrip-next" type="button" style="padding-left: 3px;" onclick="GotoPageTrip('next');">
                                <i class="fas fa-caret-right fa-lg"></i>
                            </button>
                            <button class="btn btn-secondary btn-sm btn-nav-modal btn-listtrip-last" type="button" onclick="GotoPageTrip('last');">
                                <i class="fas fa-step-forward"></i>
                            </button>
                        </div>
                        <div style="display: flex;">
                            <div class="fileNavigatorMessage" style="display: flex; flex: 1; align-self: center;">Page {!IF(OR(offsetTrip == null,offsetTrip <= 0),1,(offsetTrip/limitTrip)+1)} of {!totalPagesTrip}</div>
                        </div>
                    </div>
                </div>
            </div>
        </apex:outputPanel>
    </div>
    
    <!-- TRIP DETAIL -->
    <apex:outputPanel id="tripDetailPanel">
        <div style="{!IF(tripView.Id <> null,'','display:none;')}">
            <apex:inputHidden id="tripid" value="{!tripView.Id}" />
            <apex:inputHidden id="date_today" value="{!dateToday}" />
            <!--<input type="hidden" id="cityHidden" value="{!tripView.Start_City__r.Name}" />-->
            <!--<div class="fieldset">
                <div class="row" style="margin-top: 0 !important;">
                    <div class="col-md-12">
                       <apex:outputText value="{!IF(tripView.Description__c <> null, tripView.Description__c, '&nbsp;')}" escape="false" />
                    </div>
                </div>
                <div class="row">
                    <div class="col-md-9">
                        <span style="font-weight:bold;">Service Type:</span> {!tripView.Service_Type__c} | <span style="font-weight:bold;">Group:</span> {!tripView.Group_Type__c}
                    </div>
                    <div class="col-md-3 text-right">
                        <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="viewDocuments();"><i class="fa fa-book"></i> Documents</button>
                        <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="viewTripJournals();"><i class="fa fa-check-square"></i> Trip Journals</button>
                    </div>
                </div>
            </div>-->
            <div class="row">
                <div class="col-md-3">
                    <div class="accordion" id="accordionOne">
                        <div class="card">
                            <!--<div class="card-header" id="headingOne">
                                <h2 class="mb-0">
                                    Info
                                    <span style="float:right;">
                                        <a href="javascript:void(0);" onclick="checkIcon(this,'collapseOne');">
                                            <i class="fa fa-angle-up btn-show"></i>
                                        </a>
                                    </span>
                                </h2>
                            </div>-->
                            <div id="collapseOne" class="collapse show" aria-labelledby="headingOne" data-parent="#accordionOne">
                                <div class="card-body" style="min-height: 300px;">
                                    <div class="row" style="margin-top:0 !important;">
                                        <div class="col-md-12">
                                            <label style="font-weight:bold;">Production:</label>
                                            <span style="font-weight:bold;">{!opportunity.Name}</span>
                                        </div>
                                    </div>
                                    <div class="row" style="margin-top:15px !important;">
                                        <div class="col-md-12">
                                            <label style="font-weight:bold;">Contact:</label>
                                            <apex:selectList size="1" value="{!clientByProduction.Id}" id="trip_primarycontact" styleClass="form-control form-control-sm" onchange="changeClientTrip(this);">
                                                <apex:selectOptions value="{!clientsByProduction}" />
                                            </apex:selectList>
                                        </div>
                                    </div>
                                    <div class="row" style="margin-top:15px !important;">
                                        <div class="col-md-12">
                                            <label style="font-weight:bold;">Trip Type:</label>
                                            {!tripView.Trip_Type__c}
                                        </div>
                                    </div>
                                    <div class="row" style="margin-top:15px !important;">
                                        <div class="col-md-12">
                                            <label style="font-weight:bold;">Group Type:</label>
                                            {!tripView.Group_Type__c}
                                        </div>
                                    </div>
                                    <div class="row" style="margin-top:15px !important;">
                                        <div class="col-md-12">
                                            <label style="font-weight:bold;">Vendor:</label>
                                            <a href="/{!tripView.Vendor__c}" target="_blank">{!tripView.Vendor__r.Name}</a>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="col-md-3">
                    <div class="accordion" id="accordionTwo">
                        <div class="card">
                            <!--<div class="card-header" id="headingOne">
                                <h2 class="mb-0">
                                    Dates
                                    <span style="float:right;">
                                        <a href="javascript:void(0);" onclick="checkIcon(this,'collapseTwo');">
                                            <i class="fa fa-angle-up btn-show"></i>
                                        </a>
                                    </span>
                                </h2>
                            </div>-->
                            <div id="collapseTwo" class="collapse show" aria-labelledby="headingTwo" data-parent="#accordionTwo">
                                <div class="card-body" style="min-height: 300px;">
                                    <apex:outputPanel id="datesTripViewPanel" layout="block">
                                        <div class="row" style="margin-top:0 !important;">
                                            <div class="col-md-12">
                                                <label style="font-weight:bold;">Start Date:</label><br/>
                                                <apex:outputText value="{0, date, dd'-'MMMM'-'yyyy}" styleClass="simulate-disabled">
                                                    <apex:param value="{!tripView.Departure_Date__c}" />
                                                </apex:outputText>
                                                <span style="display:none;"><apex:inputField id="tripview_startdate" value="{!tripView.Departure_Date__c}" /></span>
                                            </div>
                                        </div>
                                        <div class="row">
                                            <div class="col-md-12">
                                                <label style="font-weight:bold;">End Date:</label><br/>
                                                <apex:outputText value="{0, date, dd'-'MMMM'-'yyyy}" styleClass="simulate-disabled" style="{!IF(tripView.Return_Date__c <> null,'','display:none;')}">
                                                    <apex:param value="{!tripView.Return_Date__c}" />
                                                </apex:outputText>
                                                <span class="simulate-disabled" style="{!IF(tripView.Return_Date__c <> null,'display:none;','')}">&nbsp;</span>
                                                <span style="display:none;"><apex:inputField id="tripview_enddate" value="{!tripView.Return_Date__c}" /></span>
                                            </div>
                                        </div>
                                    </apex:outputPanel>
                                    <div class="row">
                                        <div class="col-md-12">
                                            <label style="font-weight:bold;">Trace Date:</label><br/>
                                            <apex:inputField id="tripview_tracedate" value="{!tripView.Trace_Date__c}" onblur="saveOtherInformation('tripview_tracedate');" />
                                            <span class="error-message"></span>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-12">
                                            <label style="font-weight:bold;">Decision Due Date:</label><br/>
                                            <apex:inputField id="tripview_decisionduedate" value="{!tripView.Decision_Due_Date__c}" onblur="saveOtherInformation('tripview_decisionduedate');" />
                                            <span class="error-message"></span>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-12">
                                            <label style="font-weight:bold;">Deadline Date:</label><br/>
                                            <apex:inputField id="tripview_deadlinedate" value="{!tripView.Deadline_Date__c}" onblur="saveOtherInformation('tripview_deadlinedate');" />
                                            <span class="error-message"></span>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="col-md-3">
                    <div class="accordion" id="accordionThree">
                        <div class="card">
                            <!--<div class="card-header" id="headingThree">
                                <h2 class="mb-0">
                                    Coordinator Info
                                    <span style="float:right;">
                                        <a href="javascript:void(0);" onclick="checkIcon(this,'collapseThree');">
                                            <i class="fa fa-angle-up btn-show"></i>
                                        </a>
                                    </span>
                                </h2>
                            </div>-->
                            <div id="collapseThree" class="collapse show" aria-labelledby="headingThree" data-parent="#accordionThree">
                                <div class="card-body" style="min-height: 300px;">
                                    <div class="row" style="margin-top:0 !important;">
                                        <div class="col-md-12">
                                            <label style="font-weight:bold;">Coordinator</label><br/>
                                            <apex:outputText id="production_coordinator" value="{!IF(AND(coordinatorGTName <> null,coordinatorGTName <> ''),coordinatorGTName,'')}" styleClass="simulate-disabled" style="{!IF(coordinatorGTName <> null,'','display:none;')}" />
                                            <span class="simulate-disabled" style="{!IF(coordinatorGTName <> null,'display:none;','')}">&nbsp;</span>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-12">
                                            <label style="font-weight:bold;">Backend Coordinator:</label><br/>
                                            <apex:selectList size="1" id="trip_backendcoordinator" styleClass="form-control form-control-sm" value="{!tripView.Back_end_Coordinator__c}" onchange="saveBackEndCoordinator(this);">
                                                <apex:selectOptions value="{!teamMembers}" />
                                            </apex:selectList>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-12">
                                            <label style="font-weight:bold;">Status:</label><br/>
                                            <apex:selectList size="1" id="tripview_status" value="{!tripView.Status__c}" styleClass="form-control form-control-sm" onchange="saveStatusTrip(this);">
                                                <apex:selectOptions value="{!statusItineraryPL}" />
                                            </apex:selectList>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="col-md-3">
                    <div class="accordion" id="accordionFour">
                        <div class="card">
                            <!--<div class="card-header" id="headingFour">
                            </div>-->
                            <div id="collapseFour" class="collapse show" aria-labelledby="headingFour" data-parent="#accordionFour">
                                <div class="card-body" style="min-height: 300px;">
                                    <div class="row" style="margin-top:0 !important;">
                                        <div class="col-md-12 text-center">
                                            <div style="margin-top:20px;"><button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="viewTripJournals();">Trip Journals</button> </div>
                                            <div style="margin-top:20px;"><button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="viewDocuments();">Documents</button> </div>
                                            <div style="margin-top:20px;"><button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="javascript:void(0);" style="{!IF(tripView.Status__c == 'In Contracting','','display:none;')}">Bid Details</button> </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="row">
                <div class="col-md-12">
                    <div class="accordion" id="accordionFour">
                        <div class="card">
                            <apex:outputPanel id="tabsByGroundPanel">
                                <div class="card-header" id="headingFour" style="padding: 0 1.25rem;">
                                    <div class="slds-box slds-box_x-small slds-grid"  style="margin: 0; flex-direction: column;padding: 0;border: 0;">
                                        <div class="slds-tabs_default" style="background: none;">
                                            <apex:inputHidden id="tabGroundDefault" value="{!tabGroundDefault}" />
                                            <ul class="slds-tabs_default__nav" role="tablist" style="border: 0;">
                                                <li class="slds-tabs_default__item {!IF(tabGroundDefault == 'trip_bids','slds-is-active','')}" title="Sales" role="presentation">
                                                    <a class="slds-tabs_default__link" href="javascript:void(0);" onclick="loadTabContentGround('trip_bids');" role="tab" tabindex="{!IF(tabGroundDefault == 'trip_bids','0','-1')}" aria-selected="{!IF(tabGroundDefault == 'trip_bids','true','false')}" aria-controls="tab-default-trip-bids" id="tab-default-trip-bids__item">
                                                        Bids
                                                    </a>
                                                </li>
                                                <li class="slds-tabs_default__item {!IF(tabGroundDefault == 'trip_trip_details','slds-is-active','')}" title="Sales" role="presentation" style="{!IF(tripView.Air_Charter__c == true,'','display:none;')}">
                                                    <a class="slds-tabs_default__link" href="javascript:void(0);" onclick="loadTabContentGround('trip_trip_details');" role="tab" tabindex="{!IF(tabGroundDefault == 'trip_trip_details','0','-1')}" aria-selected="{!IF(tabGroundDefault == 'trip_trip_details','true','false')}" aria-controls="tab-default-trip-trip-details" id="tab-default-trip-trip-details__item">
                                                        Trip Details
                                                    </a>
                                                </li>
                                                <li class="slds-tabs_default__item {!IF(tabGroundDefault == 'trip_rate_details','slds-is-active','')}" title="Sales" role="presentation" style="{!IF(tripView.Air_Charter__c == true,'','display:none;')}">
                                                    <a class="slds-tabs_default__link" href="javascript:void(0);" onclick="loadTabContentGround('trip_rate_details');" role="tab" tabindex="{!IF(tabGroundDefault == 'trip_rate_details','0','-1')}" aria-selected="{!IF(tabGroundDefault == 'trip_rate_details','true','false')}" aria-controls="tab-default-trip-rate-details" id="tab-default-trip-rate-details__item">
                                                        Rate Details
                                                    </a>
                                                </li>
                                            </ul>
                                            
                                        </div>
                                    </div>
                                </div>
                                <div id="collapseFour" class="collapse show" aria-labelledby="headingFour" data-parent="#accordionFour">
                                    <div class="card-body">
                                        <div clcass="row" style="margin-top:0 !important;">
                                            <div class="col-md-12"  style="padding: 0;">
                                                <div class="slds-tabs_default__content slds-show" role="tabpanel" style="padding: 0 0;">
                                                    <apex:outputPanel rendered="{!IF(tabGroundDefault == 'trip_bids',true,false)}">
                                                        <div class="row">
                                                            <div class="col-md-12">
                                                                <button type="button" class="btn btn-danger btn-sm" onclick="openSearchVendor('simple');">Search Vendors</button>
                                                            </div>
                                                        </div>
                                                        <apex:outputPanel id="bidsByTripPanel">
                                                            <input type="hidden" id="tripview_option" value="{!tripview_option}" />
                                                            <div class="row">
                                                                <div class="col-md-6">
                                                                    <input type="hidden" id="bidlist_prevshowbid" value="{!prevShowBid}" />
                                                                    <input type="hidden" id="bidlist_nextshowbid" value="{!nextShowBid}" />
                                                                    <!--<button type="button" class="btn btn-sm btn-outline-secondary btn-prev-first-bids" onclick="FirstPageBids();" >&lt;&lt;</button>
                                                                    <button type="button" class="btn btn-sm btn-outline-secondary btn-prev-bids" onclick="previousBids();" >&lt;</button>
                                                                    <button type="button" class="btn btn-sm btn-outline-secondary btn-next-bids" onclick="nextBids();" >&gt;</button>
                                                                    <button type="button" class="btn btn-sm btn-outline-secondary btn-last-next-bids" onclick="LastPageBids();" >&gt;&gt;</button>-->
                                                                </div>
                                                                <div class="col-md-6 text-right" style="padding-top: 10px;font-weight: bold;">
                                                                    <!--<span style="{!IF(totalrecsBids == 0,'display:none;','')}">{!OffsetSizeBids + 1} - {!IF((OffsetSizeBids + LimitSizeBids) < totalrecsBids, (OffsetSizeBids + LimitSizeBids) ,totalrecsBids)} of {!totalrecsBids} items</span>-->
                                                                    <span style="margin-left: 15px;"><a href="javascript:void(0);" onclick="viewTripDetail(event,'{!tripViewId}');" style="color: black !important;"><i class="fas fa-redo"></i></a></span>
                                                                </div>
                                                            </div>
                                                            <div class="row">
                                                                <div class="col-md-12">
                                                                    <table id="trip-bid-list" class="table table-sm table-bordered" style="margin-top:5px;margin-bottom:0;">
                                                                        <thead class="thead-light">
                                                                            <tr>
                                                                                <th width="5%">
                                                                                    <apex:inputHidden id="orderFieldBidsActual" value="{!orderFieldBid}" />
                                                                                </th>
                                                                                <th width="15%">
                                                                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortBids('vendor','{!orderOrientationBid}');">
                                                                                        <span style="float:left;">Vendor</span>
                                                                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldBid == 'vendor',orderOrientationBid == 'DESC'),'','display:none;')}"></i>
                                                                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldBid == 'vendor',orderOrientationBid == 'ASC'),'','display:none;')}"></i>
                                                                                    </a>
                                                                                </th>
                                                                                <th width="10%">
                                                                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortBids('contact','{!orderOrientationBid}');">
                                                                                        <span style="float:left;">Contact</span>
                                                                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldBid == 'contact',orderOrientationBid == 'DESC'),'','display:none;')}"></i>
                                                                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldBid == 'contact',orderOrientationBid == 'ASC'),'','display:none;')}"></i>
                                                                                    </a>
                                                                                </th>
                                                                                <th width="10%">
                                                                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortBids('status','{!orderOrientationBid}');">
                                                                                        <span style="float:left;">Status</span>
                                                                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldBid == 'status',orderOrientationBid == 'DESC'),'','display:none;')}"></i>
                                                                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldBid == 'status',orderOrientationBid == 'ASC'),'','display:none;')}"></i>
                                                                                    </a>
                                                                                </th>
                                                                                <th width="10%">
                                                                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortBids('fare','{!orderOrientationBid}');">
                                                                                        <span style="float:left;">Fare</span>
                                                                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldBid == 'fare',orderOrientationBid == 'DESC'),'','display:none;')}"></i>
                                                                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldBid == 'fare',orderOrientationBid == 'ASC'),'','display:none;')}"></i>
                                                                                    </a>
                                                                                </th>
                                                                                <th width="10%">
                                                                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortBids('pax','{!orderOrientationBid}');">
                                                                                        <span style="float:left;">#PAX</span>
                                                                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldBid == 'pax',orderOrientationBid == 'DESC'),'','display:none;')}"></i>
                                                                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldBid == 'pax',orderOrientationBid == 'ASC'),'','display:none;')}"></i>
                                                                                    </a>
                                                                                </th>
                                                                                <th width="15%">
                                                                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortBids('notes','{!orderOrientationBid}');">
                                                                                        <span style="float:left;">Note</span>
                                                                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldBid == 'notes',orderOrientationBid == 'DESC'),'','display:none;')}"></i>
                                                                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldBid == 'notes',orderOrientationBid == 'ASC'),'','display:none;')}"></i>
                                                                                    </a>
                                                                                </th>
                                                                                <th width="10%">
                                                                                    <a href="javascript:void(0);" style="color: #495057;" onclick="sortBids('options','{!orderOrientationBid}');">
                                                                                        <span style="float:left;">Option</span>
                                                                                        <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldBid == 'options',orderOrientationBid == 'DESC'),'','display:none;')}"></i>
                                                                                        <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldBid == 'options',orderOrientationBid == 'ASC'),'','display:none;')}"></i>
                                                                                    </a>
                                                                                </th>
                                                                                <th width="15%"></th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody>
                                                                            <apex:repeat value="{!bidsByTripShowList}" var="bid">
                                                                                <tr>
                                                                                    <td style="text-align:center;vertical-align:middle;">
                                                                                        <i class="fa fa-check-circle" style="{!IF(bid.status == 'Contracted','','display:none;')}"></i>
                                                                                    </td>
                                                                                    <td>
                                                                                        <a href="/{!bid.b.Vendor__c}" target="_blank">{!bid.vendor}</a> <br/>
                                                                                        <i class="fas fa-map-marker-alt"></i>&nbsp;
                                                                                        <apex:outputText value="{!IF(bid.b.Vendor__r.BillingStreet <> null, bid.b.Vendor__r.BillingStreet + '<br/>','')}" escape="false" />
                                                                                        <apex:outputText value="{!IF(bid.b.Vendor__r.BillingCity <> null, bid.b.Vendor__r.BillingCity,'')}" escape="false" />
                                                                                        <apex:outputText value="{!IF(bid.b.Vendor__r.BillingState <> null, ',' + bid.b.Vendor__r.BillingState,'')}" escape="false" />
                                                                                        <apex:outputText value="{!IF(bid.b.Vendor__r.BillingPostalCode <> null, ',' + bid.b.Vendor__r.BillingPostalCode,'')}" escape="false" />
                                                                                    </td>
                                                                                    <td>
                                                                                        {!bid.contact}
                                                                                    </td>
                                                                                    <td>
                                                                                        <a href="javascript:void(0);" onclick="goToBidsTab({!bid.numberz},{!totalRecsBids});">{!bid.status}</a>
                                                                                        <span style="margin-left:1em;">
                                                                                            <a href="/one/one.app#/alohaRedirect/apex/AirDashboard?OpenBidId={!bid.b.Id}" target="_blank"><i class="fas fa-external-link-alt"></i></a>
                                                                                        </span>
                                                                                    </td>
                                                                                    <td>
                                                                                        {!IF(bid.b.No_Bid_reason__c <> null,bid.b.No_Bid_reason__c,'')}
                                                                                        {!IF(AND(OR(bid.b.No_Bid_reason__c == null,bid.b.No_Bid_reason__c == ''),bid.currency_code <> null),IF(bid.fare <> 0,symbolMap[bid.currency_code],''),'')}
                                                                                        <apex:outputText value="{0,number,###,##0.00}" rendered="{!IF(bid.b.No_Bid_reason__c <> null,false,IF(bid.fare <> 0,true,false))}">
                                                                                        <apex:param value="{!bid.fare}"/>
                                                                                        </apex:outputText>
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:outputText value="{0,number,###,##0}" rendered="{!IF(bid.pax == 0,false,true)}">
                                                                                            <apex:param value="{!bid.pax}"/>
                                                                                        </apex:outputText>
                                                                                    </td>
                                                                                    <td>
                                                                                        <span class="show-data">{!bid.notes}</span>
                                                                                        <span class="data" style="display:none;">
                                                                                            <input value="{!bid.notes}" class="form-control form-control-sm bid-notes" />
                                                                                        </span>
                                                                                    </td>
                                                                                    <td>
                                                                                        <span class="show-data bid-option-span">{!IF(bid.options == 999999,'n/a',bid.options)}</span>
                                                                                        <span class="data" style="display:none;">
                                                                                            <input value="{!IF(bid.options == 999999,null,bid.options)}" class="form-control form-control-sm bid-options" />
                                                                                        </span>
                                                                                    </td>
                                                                                    <td style="text-align:center;">
                                                                                        <input type="hidden" value="{!bid.b.Id}" class="id"  />
                                                                                        <input type="hidden" value="{!bid.b.Locked__c}" class="bid-locked-status" />
                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-save" onclick="saveEditBid(this,'options','ASC');" style="display:none;"><i class="fa fa-check"></i> Save</button>
                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-edit" onclick="editBid(this);"><i class="fa fa-pencil-alt"></i> Edit</button>
                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-cancel" onclick="cancel(this);" style="display:none;"><i class="fa fa-ban"></i> Cancel</button>
                                                                                    </td>
                                                                                </tr>
                                                                                <apex:repeat value="{!bidRevenueMap[bid.b.Id]}" var="revenue" rendered="{!IF(bid.b.No_Bid_reason__c <> null,false,true)}">
                                                                                    <tr>
                                                                                        <td colspan="4" style="border:0px;">
                                                                                        </td>
                                                                                        <td>
                                                                                            {!IF(revenue.Total_Price_Currency__c <> null,symbolMap[revenue.Total_Price_Currency__c],'')}
                                                                                            <apex:outputText value="{0,number,###,##0.00}">
                                                                                                <apex:param value="{!revenue.Total_Price__c}"/>
                                                                                            </apex:outputText>
                                                                                        </td>
                                                                                        <td>
                                                                                            <apex:outputText value="{0,number,###,##0}">
                                                                                                <apex:param value="{!revenue.of_seats__c}"/>
                                                                                            </apex:outputText>
                                                                                        </td>
                                                                                        <td colspan="3" style="border:0px;">
                                                                                        </td>
                                                                                    </tr>
                                                                                </apex:repeat>
                                                                            </apex:repeat>
                                                                        </tbody>
                                                                    </table>
                                                                </div>
                                                            </div>
                                                        </apex:outputPanel>
                                                        <div class="row">
                                                            <div class="col-md-12">
                                                                Additional Notes
                                                            </div>
                                                        </div>
                                                        <div class="row">
                                                            <div class="col-md-12">
                                                                <textarea class="form-control form-control-sm">{!tripView.Itinerary__r[0].Client_Notes__c}</textarea>
                                                            </div>
                                                        </div>
                                                        <div class="row">
                                                            <div class="col-md-12">
                                                                <button type="button" class="btn btn-danger btn-sm" onclick="openSendBidRequest();" >Send Bid Request</button>
                                                                <button type="button" class="btn btn-danger btn-sm" onclick="openPreviewOptions();" >Preview Options</button>
                                                                <button type="button" class="btn btn-danger btn-sm" onclick="openSendOptions();" >Send Options</button>
                                                                <button type="button" class="btn btn-danger btn-sm" onclick="openPreviewCommunityOptions('{!tripViewId}');" >Preview Community Options</button>
                                                                <button type="button" class="btn btn-danger btn-sm" onclick="openReleaseBid();" >Release Bid</button>
                                                                <button type="button" class="btn btn-danger btn-sm" onclick="openDecisionDueDateJs();">Decision Due Date</button>
                                                                <apex:outputPanel id="formDecisionDueDatePanel">
                                                                    {!tripView.Form_Decision_Due_Date__c}
                                                                </apex:outputPanel>
                                                                    
                                                            </div>
                                                        </div>
                                                    </apex:outputPanel>
                                                    <apex:outputPanel rendered="{!IF(tabGroundDefault == 'trip_trip_details',true,false)}">
                                                        <!--<div class="row">
                                                            <div class="col-md-12">
                                                                  <button type="button" class="btn btn-secondary btn-custom btn-add-trip-details" onclick="newSubTrip();"><i class="fa fa-plus"></i> {!IF(subTripList.size > 0, 'Add Additional Trip','Add Trip Details')}</button>
                                                            </div>
                                                        </div>-->
                                                        <div class="accordion" id="accordionBidOne" style="margin-top:10px;">
                                                            <div class="card">
                                                                <div class="card-header" id="headingBidOne">
                                                                    <h2 class="mb-0">
                                                                        <span style="font-size:14px;">Trip Details</span>
                                                                        <span style="float:right;">
                                                                            <a href="javascript:void(0);" onclick="checkIcon(this,'collapseBidOne');">
                                                                                <i class="fa fa-angle-up btn-show"></i>
                                                                            </a>
                                                                        </span>
                                                                    </h2>
                                                                </div>
                                                                <div id="collapseBidOne" class="collapse show" aria-labelledby="headingBidOne" data-parent="#accordionBidOne">
                                                                    <div class="card-body" style="min-height: 235px;">
                                                                        <div class="row">
                                                                            <div class="col-md-3">
                                                                                <span style="float:left;font-weight:bold;">Charter Type:</span>
                                                                                <span style="float:left;margin-left: 10px;"><apex:inputField id="itinerary_chartertype" value="{!tripView.Charter_Type__c}" styleClass="form-control form-control-sm" onchange="saveItineraryTrip();"  /></span>
                                                                            </div>
                                                                            <div class="col-md-3">
                                                                                <span style="float:left;font-weight:bold;">Description:</span> 
                                                                                <span style="float:left;margin-left: 10px;"><apex:inputField id="itinerary_description" value="{!tripView.Description__c}" styleClass="form-control form-control-sm" onblur="saveItineraryTrip();"  /></span>
                                                                            </div>
                                                                            <div class="col-md-2">
                                                                                <span style="font-weight:bold;">Group Type:</span> {!tripView.Group_Type__c}
                                                                            </div>
                                                                            <div class="col-md-2">
                                                                                <span style="float:left;font-weight:bold;">#PAX:</span> 
                                                                                <span style="float:left;margin-left: 10px;"><apex:inputField id="itinerary_pax" value="{!tripView.PAX__c}" styleClass="form-control form-control-sm" onblur="saveItineraryTrip();"  /></span>
                                                                            </div>
                                                                            <div class="col-md-2">
                                                                                <span style="color:red;margin-left:20px;" class="message-itinerary message-success"></span>
                                                                            </div>
                                                                        </div>
                                                                        <div class="row" style="margin-top:20px !important;">
                                                                            <div class="col-md-12">
                                                                                <div style="border-bottom: 1px solid rgba(0,0,0,.125);"><span style="font-size:18px;">Travel Information</span></div>
                                                                            </div>
                                                                        </div>
                                                                        <div class="row">
                                                                            <div class="col-md-12">
                                                                                <button type="button" class="btn btn-sm btn-secondary btn-custom" onclick="newItinerary();"><i class="fa fa-plus"></i> Add New Travel Information</button>
                                                                            </div>
                                                                        </div>
                                                                        <div class="row">
                                                                            <div class="col-md-12">
                                                                                <apex:outputPanel id="itineraryByTripPanel">
                                                                                    <table class="table table-sm" style="margin-top:5px;margin-bottom:0;">
                                                                                        <thead class="thead-light">
                                                                                            <tr>
                                                                                                <th width="5%">Order #</th>
                                                                                                <th width="8%">Dep Date</th>
                                                                                                <th width="8%">Arr Date</th>
                                                                                                <th width="5%">Flight No</th>
                                                                                                <th width="14%">Dep City</th>
                                                                                                <th width="14%">Arr City</th>
                                                                                                <th width="5%">Dep Time</th>
                                                                                                <th width="5%">Arr Time</th>
                                                                                                <th width="9%">Flight Duration</th>
                                                                                                <th width="7%">Equip. Type</th>
                                                                                                <th width="8%">Notes</th>
                                                                                                <th width="12%">Actions</th>
                                                                                            </tr>
                                                                                        </thead>
                                                                                        <tbody>
                                                                                            <tr class="new-itinerary new-record" style="display:none;">
                                                                                                <td>
                                                                                                    <apex:inputField value="{!newItineraryTrip.Order__c}" styleClass="form-control form-control-sm new-data order" />
                                                                                                </td>
                                                                                                <td>
                                                                                                    <span class="data">
                                                                                                        <!--<apex:inputField value="{!newItineraryTrip.Departure_Date__c}" styleClass="form-control form-control-sm new-data depdate" />-->
                                                                                                        <apex:inputField value="{!newItineraryTrip.Departure_Date__c}" styleClass="form-control form-control-sm new-data depdate date-picker" />
                                                                                                        <span class="error-message" style="color:red;"></span>
                                                                                                    </span>
                                                                                                </td>
                                                                                                <td>
                                                                                                    <!--<apex:inputField value="{!newItineraryTrip.Arrival_Date__c}" styleClass="form-control form-control-sm new-data arrdate" />-->
                                                                                                    <apex:inputField value="{!newItineraryTrip.Arrival_Date__c}" styleClass="form-control form-control-sm new-data arrdate date-picker" />
                                                                                                    <span class="error-message" style="color:red;"></span>
                                                                                                </td>
                                                                                                <td>
                                                                                                    <apex:inputField value="{!newItineraryTrip.Flight_No__c}" styleClass="form-control form-control-sm new-data flight" />
                                                                                                </td>
                                                                                                <td>
                                                                                                    <span class="data">
                                                                                                        <apex:inputText styleClass="form-control form-control-sm new-data depcity dep-city-search" onkeyup="setInputDepCityBid();" />
                                                                                                        <input type="hidden" class="new-data depcityid" />
                                                                                                        <span class="error-message" style="color:red;"></span>
                                                                                                    </span>
                                                                                                </td>
                                                                                                <td>
                                                                                                    <span class="data">
                                                                                                        <apex:inputText styleClass="form-control form-control-sm new-data arrcity arr-city-search" onkeyup="setInputArrCityBid();" />
                                                                                                        <input type="hidden" class="new-data arrcityid" />
                                                                                                        <span class="error-message" style="color:red;"></span>
                                                                                                    </span>
                                                                                                </td>
                                                                                                <td>
                                                                                                    <apex:inputField value="{!newItineraryTrip.Dep_Time__c}" styleClass="form-control form-control-sm new-data deptime" type="time" />
                                                                                                </td>
                                                                                                <td>
                                                                                                    <apex:inputField value="{!newItineraryTrip.Arr_Time__c}" styleClass="form-control form-control-sm new-data arrtime" type="time" />
                                                                                                </td>
                                                                                                <td>
                                                                                                    <apex:inputField value="{!newItineraryTrip.Flight_Duration_hrs__c}" styleClass="form-control form-control-sm new-data durationhrs" style="width:50px;" />&nbsp;:&nbsp;
                                                                                                    <apex:inputField value="{!newItineraryTrip.Flight_Duration_Mins__c}" styleClass="form-control form-control-sm new-data durationmins" style="width:50px;" />
                                                                                                </td>
                                                                                                <td>
                                                                                                    <apex:inputField value="{!newItineraryTrip.Equip_Type__c}" styleClass="form-control form-control-sm new-data equiptype" />
                                                                                                </td>
                                                                                                <td>
                                                                                                    <apex:inputField value="{!newItineraryTrip.Segment_Notes__c}" styleClass="form-control form-control-sm new-data notes" />
                                                                                                </td>
                                                                                                <td>
                                                                                                    <input type="hidden" class="id"  />
                                                                                                    <button type="button" style="margin-left:0;" class="btn btn-secondary btn-sm btn-custom" onclick="saveEditItineraryTrip(this);"><i class="fa fa-check"></i> Save</button>
                                                                                                    <button type="button" style="margin-left:0;" class="btn btn-danger btn-sm btn-custom" onclick="cancelItineraryTrip();"><i class="fa fa-ban"></i> Cancel</button>
                                                                                                </td>
                                                                                            </tr>
                                                                                            <apex:repeat value="{!itineraryTripList}" var="itinerarytrip"> 
                                                                                                <tr data-id="{!itinerarytrip.Id}">
                                                                                                    <td>
                                                                                                        <span class="show-data"><apex:outputText value="{!itinerarytrip.Order__c}" /></span>
                                                                                                        <apex:inputField value="{!itinerarytrip.Order__c}" styleClass="form-control form-control-sm data order" style="display:none" />
                                                                                                    </td>
                                                                                                    <td>
                                                                                                        <span class="show-data">
                                                                                                            <apex:outputText value="{0,date,dd-MMMM-yyyy}">
                                                                                                                <apex:param value="{!itinerarytrip.Departure_Date__c}" />
                                                                                                            </apex:outputText>
                                                                                                        </span>
                                                                                                        <span class="data" style="display:none">
                                                                                                            <apex:inputField value="{!itinerarytrip.Departure_Date__c}" styleClass="form-control form-control-sm depdate"/>
                                                                                                            <!--<apex:inputField value="{!itinerarytrip.Departure_Date__c}" styleClass="form-control form-control-sm depdate date-picker" />-->
                                                                                                            <span class="error-message" style="color:red;"></span>
                                                                                                        </span>
                                                                                                    </td>
                                                                                                    <td>
                                                                                                        <span class="show-data">
                                                                                                            <apex:outputText value="{0,date,dd-MMMM-yyyy}">
                                                                                                                <apex:param value="{!itinerarytrip.Arrival_Date__c}" />
                                                                                                            </apex:outputText>
                                                                                                        </span>
                                                                                                        <span class="data" style="display:none">
                                                                                                            <apex:inputField value="{!itinerarytrip.Arrival_Date__c}" styleClass="form-control form-control-sm arrdate"/>
                                                                                                            <span class="error-message" style="color:red;"></span>
                                                                                                        </span>
                                                                                                    </td>
                                                                                                    <td>
                                                                                                        <span class="show-data">{!itinerarytrip.Flight_No__c}</span>
                                                                                                        <apex:inputField value="{!itinerarytrip.Flight_No__c}" styleClass="form-control form-control-sm data flight" style="display:none" />
                                                                                                    </td>
                                                                                                    <td>
                                                                                                        <span class="show-data">{!itinerarytrip.Departure_City__r.Airport_Code__c}</span>
                                                                                                        <span class="data" style="display:none">
                                                                                                            <apex:inputText value="{!itinerarytrip.Departure_City__r.Full_Name__c}" styleClass="form-control form-control-sm depcity dep-city-search" onkeyup="setInputDepCityBid();"  />
                                                                                                            <input type="hidden" value="{!itinerarytrip.Departure_City__c}" class="depcityid"   />
                                                                                                            <span class="error-message" style="color:red;"></span>
                                                                                                        </span>
                                                                                                    </td>
                                                                                                    <td>
                                                                                                        <span class="show-data">{!itinerarytrip.Arrival_City__r.Airport_Code__c}</span>
                                                                                                        <span class="data" style="display:none">
                                                                                                            <apex:inputText value="{!itinerarytrip.Arrival_City__r.Full_Name__c}" styleClass="form-control form-control-sm arrcity arr-city-search" onkeyup="setInputArrCityBid();"  />
                                                                                                            <input type="hidden" value="{!itinerarytrip.Arrival_City__c}" class="arrcityid"   />
                                                                                                            <span class="error-message" style="color:red;"></span>
                                                                                                        </span>
                                                                                                    </td>
                                                                                                    <td>
                                                                                                        <span class="show-data">
                                                                                                            {!itinerarytrip.Dep_Time_Text__c}
                                                                                                        </span>
                                                                                                        <apex:inputField value="{!itinerarytrip.Dep_Time__c}" styleClass="form-control form-control-sm data deptime" type="time" style="display:none" />
                                                                                                    </td>
                                                                                                    <td>
                                                                                                        <span class="show-data">
                                                                                                            {!itinerarytrip.Arr_Time_Text__c}
                                                                                                        </span>
                                                                                                        <apex:inputField value="{!itinerarytrip.Arr_Time__c}" styleClass="form-control form-control-sm data arrtime" type="time" style="display:none" />
                                                                                                    </td>
                                                                                                    <td>
                                                                                                        <span class="show-data">{!IF(itinerarytrip.Flight_Duration_hrs__c != null, TEXT(itinerarytrip.Flight_Duration_hrs__c) + 'HRS','')} {!IF(itinerarytrip.Flight_Duration_Mins__c != null, TEXT(itinerarytrip.Flight_Duration_Mins__c) + 'MINS','')}</span>
                                                                                                        <span class="data" style="display:none">
                                                                                                            <apex:inputField value="{!itinerarytrip.Flight_Duration_hrs__c}" styleClass="form-control form-control-sm durationhrs" style="width:50px;" />&nbsp;:&nbsp;
                                                                                                            <apex:inputField value="{!itinerarytrip.Flight_Duration_Mins__c}" styleClass="form-control form-control-sm durationmins" style="width:50px;margin-left:0px;" />
                                                                                                        </span>
                                                                                                    </td>
                                                                                                    <td>
                                                                                                        <span class="show-data">{!itinerarytrip.Equip_Type__c}</span>
                                                                                                        <apex:inputField value="{!itinerarytrip.Equip_Type__c}" styleClass="form-control form-control-sm data equiptype" style="display:none" />
                                                                                                    </td>
                                                                                                    <td>
                                                                                                        <span class="show-data">{!itinerarytrip.Segment_Notes__c}</span>
                                                                                                        <apex:inputField value="{!itinerarytrip.Segment_Notes__c}" styleClass="form-control form-control-sm data notes" style="display:none" />
                                                                                                    </td>
                                                                                                    <td>
                                                                                                        <input type="hidden" value="{!itinerarytrip.Id}" class="id"  />
                                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-copy" onclick="copyAir(this);"><i class="far fa-clone"></i></button>
                                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-save" onclick="saveEditItineraryTrip(this);" style="display:none;margin-left: 0.5rem;"><i class="fa fa-check"></i> Save</button>
                                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-edit" onclick="edit(this);" style="margin-left: 0px;"><i class="fa fa-pencil-alt"></i> Edit</button>
                                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-cancel" onclick="cancel(this);" style="display:none;margin-left:0;"><i class="fa fa-ban"></i> Cancel</button>
                                                                                                        <button type="button" style="margin-left:0;" class="btn btn-secondary btn-sm btn-custom btn-delete" onclick="deleteItineraryTrip('{!itinerarytrip.Id}');"><i class="fas fa-window-close"></i> Delete</button>
                                                                                                    </td>
                                                                                                </tr>
                                                                                            </apex:repeat>
                                                                                        </tbody>
                                                                                    </table>
                                                                                    <script>
                                                                                    createAutocompleteDepCity = false;
                                                                                    createAutocompleteArrCity = false;
                                                                                    createAutocompleteOperatedBy = false;
                                                                                    </script>
                                                                                </apex:outputPanel>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                        <div class="row" style="margin-top: 35px !important;">
                                                            <div class="col-md-6">
                                                                <span style="font-weight:bold;">Aircrafts Information</span>
                                                            </div>
                                                            <div class="col-md-6 text-right">
                                                                <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="newAircraftTrip();"><i class="fa fa-plus"></i> Add Aircraft</button>
                                                            </div>
                                                        </div>
                                                        <div class="row">
                                                            <div class="col-md-12">
                                                                <apex:outputPanel id="newAircraftTripPanel">
                                                                    <table class="table table-sm" style="margin-top:5px;margin-bottom:0;">
                                                                        <thead class="thead-light">
                                                                            <tr>
                                                                                <th width="15%">Aircraft Type</th>
                                                                                <th width="15%"># economy seats</th>
                                                                                <th width="10%">Cargo Capacity</th>
                                                                                <th width="10%">Seat Pitch</th>
                                                                                <th width="10%">Airline</th>
                                                                                <th width="10%">Position from &amp; time</th>
                                                                                <th width="15%">Air Charter Trip Contents</th>
                                                                                <th width="15%"></th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody>
                                                                            <tr class="new-aircraft-trip" style="display:none;">
                                                                                <td>
                                                                                    <apex:inputField value="{!newAircraftTrip.Aircraft_Type__c}" styleClass="form-control form-control-sm newdata newdata-aircrafttype" />
                                                                                </td>
                                                                                <td>
                                                                                    <apex:inputField value="{!newAircraftTrip.economy_seats__c}" styleClass="form-control form-control-sm newdata newdata-economyseats" />
                                                                                </td>
                                                                                <td>
                                                                                    <apex:inputField value="{!newAircraftTrip.Cargo_capacity__c}" styleClass="form-control form-control-sm newdata newdata-cargocapacity" />
                                                                                </td>
                                                                                <td>
                                                                                    <apex:inputField value="{!newAircraftTrip.Seat_pitch__c}" styleClass="form-control form-control-sm newdata newdata-seatpitch" />
                                                                                </td>
                                                                                <td>
                                                                                    <input type="text" class="form-control form-control-sm newdata airline aircraft-search" onkeyup="setInputAircraftTrip();" />
                                                                                    <input type="hidden" value="{!newAircraftTrip.Airline__c}" class="newdata airlineid" />
                                                                                </td>
                                                                                <td>	
                                                                                    <apex:inputField value="{!newAircraftTrip.Positioning_from_time__c}" styleClass="form-control form-control-sm newdata newdata-positioningfromtime" />
                                                                                </td>
                                                                                <td>
                                                                                    <apex:inputField value="{!newAircraftTrip.Air_Charter_Trip_Contents__c}" styleClass="form-control form-control-sm newdata newdata-tripcontents" />
                                                                                </td>
                                                                                <td class="text-center" width="15%">
                                                                                    <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="saveAircraftTrip(this);"><i class="fa fa-check"></i> Save</button>
                                                                                    <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="cancelAircraftTrip();"><i class="fa fa-ban"></i> Cancel</button>
                                                                                </td>
                                                                            </tr>
                                                                        </tbody>
                                                                    </table>
                                                                    <script>
                                                                    createAutocompleteAircraftTrip = false;
                                                                    </script>
                                                                </apex:outputPanel>
                                                                <apex:outputPanel id="aircraftsTripPanel">
                                                                    <table class="table table-sm">
                                                                        <tbody>
                                                                            <apex:repeat value="{!aircraftsByTripList}" var="aircraftTrip">
                                                                                <tr data-id="{!aircraftTrip.Id}">
                                                                                    <td width="15%">
                                                                                        <input type="hidden" value="{!aircraftTrip.Id}" class="id"  />
                                                                                        <span class="show-data">{!aircraftTrip.Aircraft_Type__c}</span>
                                                                                        <apex:inputField value="{!aircraftTrip.Aircraft_Type__c}" styleClass="form-control form-control-sm data aircrafttype" style="display:none;" />
                                                                                    </td>
                                                                                    <td width="15%">
                                                                                        <span class="show-data">{!aircraftTrip.economy_seats__c}</span>
                                                                                        <apex:inputField value="{!aircraftTrip.economy_seats__c}" styleClass="form-control form-control-sm data economyseats" style="display:none;" />
                                                                                    </td>
                                                                                    <td width="10%">
                                                                                        <span class="show-data">{!aircraftTrip.Cargo_capacity__c}</span>
                                                                                        <apex:inputField value="{!aircraftTrip.Cargo_capacity__c}" styleClass="form-control form-control-sm data cargocapacity" style="display:none;" />
                                                                                    </td>
                                                                                    <td width="10%">
                                                                                        <span class="show-data">{!aircraftTrip.Seat_pitch__c}</span>
                                                                                        <apex:inputField value="{!aircraftTrip.Seat_pitch__c}" styleClass="form-control form-control-sm data seatpitch" style="display:none;" />
                                                                                    </td>
                                                                                    <td width="10%">
                                                                                        <span class="show-data">{!aircraftTrip.Airline__r.Name}</span>
                                                                                        <span class="data" style="display:none;">
                                                                                            <input type="text" value="{!aircraftTrip.Airline__r.Name}" class="form-control form-control-sm airline aircraft-search" onkeyup="setInputAircraftTrip();" />
                                                                                            <input type="hidden" value="{!aircraftTrip.Airline__c}" class="airlineid" />
                                                                                        </span>
                                                                                    </td>
                                                                                    <td width="10%">
                                                                                        <span class="show-data">{!aircraftTrip.Positioning_from_time__c}</span>
                                                                                        <apex:inputField value="{!aircraftTrip.Positioning_from_time__c}" styleClass="form-control form-control-sm data positioningfromtime" style="display:none;" />
                                                                                    </td>
                                                                                    <td wdith="15%">
                                                                                        <span class="show-data">{!aircraftTrip.Air_Charter_Trip_Contents__c}</span>
                                                                                        <apex:inputField value="{!aircraftTrip.Air_Charter_Trip_Contents__c}" styleClass="form-control form-control-sm data tripcontents" style="display:none;" />
                                                                                    </td>
                                                                                    <td class="text-center" width="15%">
                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-save" onclick="saveEditAircraftTrip(this);" style="display:none;"><i class="fa fa-check"></i> Save</button>
                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-edit" onclick="edit(this);"><i class="fa fa-pencil"></i> Edit</button>
                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-cancel" onclick="cancel(this);" style="display:none;"><i class="fa fa-ban"></i> Cancel</button>
                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-delete" onclick="deleteAircraftTrip('{!aircraftTrip.Id}');"><i class="fa fa-times"></i> Delete</button>
                                                                                    </td>
                                                                                </tr>
                                                                            </apex:repeat>
                                                                        </tbody>
                                                                    </table>
                                                                    <script>
                                                                    createAutocompleteAircraftTrip = false;
                                                                    </script>
                                                                </apex:outputPanel>
                                                            </div>
                                                        </div>
                                                    </apex:outputPanel>
                                                    <apex:outputPanel rendered="{!IF(tabGroundDefault == 'trip_rate_details',true,false)}">
                                                        <div class="row">
                                                            <div class="col-md-12 text-right">
                                                                <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="newConcessionTrip();"><i class="fa fa-plus"></i> Add New Item</button>
                                                            </div>
                                                        </div>
                                                        <div class="row">
                                                            <div class="col-md-12">
                                                                <apex:outputPanel id="newConcessionsTripPanel">
                                                                    <table class="table table-sm" style="margin-top:5px;margin-bottom:0;">
                                                                        <thead class="thead-light">
                                                                            <tr>
                                                                                <th width="10%">Create in Bid</th>
                                                                                <th width="75%">Additional Fees</th>
                                                                                <th width="15%"></th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody>
                                                                            <tr class="new-concession-trip" style="display:none;">
                                                                                <td>
                                                                                	<apex:inputField value="{!newConcessionTrip.Create_in_Bid__c}" styleClass="form-control form-control-sm newdata-createinbid" />
                                                                                </td>
                                                                                <td>
                                                                                    <input class="form-control form-control-sm newdata newdata-requested data-concession-search-new" />
                                                                                </td>
                                                                                <td class="text-center" width="15%">
                                                                                    <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="saveConcessionTrip();"><i class="fa fa-check"></i> Save</button>
                                                                                    <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="cancelConcessionTrip();"><i class="fa fa-ban"></i> Cancel</button>
                                                                                </td>
                                                                            </tr>
                                                                        </tbody>
                                                                    </table>
                                                                    <script>
                                                                    $('.data-concession-search-new').inputpicker({
                                                                        data: {!concessionJson},
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
                                                                </apex:outputPanel>
                                                                <apex:outputPanel id="concessionsTripPanel">
                                                                    <table class="table table-sm">
                                                                        <tbody>
                                                                            <apex:repeat value="{!concessionsRequestedTrip}" var="concessionRequested">
                                                                                <tr>
                                                                                    <td width="10%">
                                                                                    	<input type="hidden" value="{!concessionRequested.Id}" class="id"  />
                                                                                        <span class="show-data">{!IF(concessionRequested.Create_in_Bid__c == true,'Yes','No')}</span>
                                                                                        <apex:inputField value="{!concessionRequested.Create_in_Bid__c}" styleClass="form-control form-control-sm data createinbid" style="display:none;" />
                                                                                    </td>
                                                                                    <td width="75%">
                                                                                        <span class="show-data">{!IF(concessionRequested.Concessions_Requested__c != null,concessionRequested.Concessions_Requested__c,'-')}</span>
                                                                                        <input type="hidden" class="data-original-requested" value="{!concessionRequested.Concessions_Requested__c}"  style="display:none;" />
                                                                                        <input class="form-control form-control-sm data requested data-concession-search" style="display:none;" value="{!concessionRequested.Concessions_Requested__c}" />
                                                                                    </td>
                                                                                    <td class="text-center" width="15%">
                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-save" onclick="saveEditConcessionTrip(this);" style="display:none;"><i class="fa fa-check"></i> Save</button>
                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-edit" onclick="editConcessionTrip(this);"><i class="fa fa-pencil"></i> Edit</button>
                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-cancel" onclick="cancel(this);" style="display:none;"><i class="fa fa-ban"></i> Cancel</button>
                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-delete" onclick="deleteConcession('{!concessionRequested.Id}');"><i class="fa fa-times"></i> Delete</button>
                                                                                    </td>
                                                                                </tr>
                                                                            </apex:repeat>
                                                                        </tbody>
                                                                    </table>
                                                                    <script>
                                                                    $('.data-concession-search').inputpicker({
                                                                        data: {!concessionJson},
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
                                                                </apex:outputPanel>
                                                            </div>
                                                        </div>
                                                    </apex:outputPanel>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </apex:outputPanel>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </apex:outputPanel>
    <!-- END TRIP DETAIL -->
    
    <!-- Modal content-->
    <div class="modal fade" id="myModalTripJournal" role="dialog">
        <div class="modal-dialog modal-xl">
            <!-- Modal content-->
            <div class="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title">Trip Journals</h4>
                    <button type="button" class="close" data-dismiss="modal">&times;</button>
                </div>
                <div class="modal-body" style="padding-top: 0 !important;">
                    <div class="row">
                        <div class="col-md-12">
                            <button type="button" class="btn btn-danger btn-sm" onclick="openCreateJournal('','trip_stay');" >Create Journal</button>
                        </div>
                    </div>
                    <div class="form-group row fieldset"> 
                        <table>
                            <tr>
                                <td style="width:23%;">
                                    <label style="padding-top: 5px;">Search Journals :</label>
                                </td>
                                <td style="width:25%;">
                                    <input class="form-control form-control-sm" id="tripjournalsearch" />
                                </td>
                                <td style="width:15%;">
                                    <apex:inputCheckbox label="Issue" styleClass="form-check-input checkIssue" id="checkIssue" title="Issue" style="margin-left: 15px !important;margin-top:0px !important;" />
                                    <label style="margin-left: -5px !important;">Issue</label>
                                </td>
                                <td style="width:15%;">
                                    <apex:inputCheckbox label="Sales" styleClass="form-check-input checkSales" id="checkSales" title="Sales" style="margin-left: 15px !important;margin-top:0px !important;" />
                                    <label style="margin-left: -5px !important;">Sales</label>
                                </td>
                                <td style="width:22%;">
                                    <button type="button" class="btn btn-primary btn-sm btn-custom" onclick="searchTripJournalsByGT();">Search</button>
                                    <button type="button" class="btn btn-primary btn-sm btn-custom" onclick="clearViewTripJournalsByGT();">Clear</button>
                                </td>
                            </tr>
                        </table>
                    </div>
                    <apex:outputPanel id="tripJournalsPanel">
                        <apex:repeat value="{!journalByTripList}" var="journalByTrip">
                            <div class="group-custom" style="margin-top: 2px !important;{!IF(journalByTrip.Bid__c == null,'background-color:#EEE;','')}">
                                <a href="javascript:void(0);" onclick="openCreateJournal('{!journalByTrip.Id}','trip_stay');">{!journalByTrip.Name}</a>
                                &nbsp;-&nbsp;<span>{!journalByTrip.CreatedBy.Name}</span>
                                &nbsp;-&nbsp;
                                <span>
                                    <apex:outputText value="{0,date,[dd-MMMM-yyyy hh:mm a]}">
                                        <apex:param value="{!journalByTrip.CreatedDate - 0.291666666}" />
                                    </apex:outputText>
                                </span>
                                &nbsp;-&nbsp;<a href="javascript:void(0);" onclick="viewReplyJournal('{!journalByTrip.Id}','');">Reply</a>
                                <br/>
                                <apex:outputText value="{!SUBSTITUTE(SUBSTITUTE(JSENCODE(journalByTrip.Journal_Entry__c),'\u003Cbr /\u003E','<br/>'),'
','<br/>')}" escape="false" />
                            </div>
                            <apex:repeat value="{!journalByTripMap[journalByTrip.Id]}" var="journalByTripChild">
                                <div class="group-custom" style="margin-left:20px !important;margin-top: 2px !important;">
                                    <a href="javascript:void(0);" onclick="viewReplyJournal('{!journalByTrip.Id}','{!journalByTripChild.Id}');">{!journalByTripChild.Name}</a>
                                    &nbsp;-&nbsp;<span>{!journalByTrip.CreatedBy.Name}</span>
                                    &nbsp;-&nbsp;
                                    <span>
                                        <apex:outputText value="{0,date,[dd-MMMM-yyyy hh:mm a]}">
                                            <apex:param value="{!journalByTripChild.CreatedDate - 0.291666666}" />
                                        </apex:outputText>
                                    </span>
                                    <br/>
                                    <apex:outputText value="{!SUBSTITUTE(SUBSTITUTE(JSENCODE(journalByTripChild.Journal_Entry__c),'\u003Cbr /\u003E','<br/>'),'
','<br/>')}" escape="false" />
                                </div>
                            </apex:repeat>
                        </apex:repeat>
                    </apex:outputPanel>
                </div>
            </div>
        </div>
    </div>
    <!-- End Modal -->
    <!-- Modal content-->
    <div class="modal fade" id="myModalSearchVendor" role="dialog">
        <div class="modal-dialog modal-xl">
            <div class="modal-content">
                <div class="modal-header" style="border-bottom: 0px;padding: 5px 1rem 0 5px;">
                    <button type="button" class="close" data-dismiss="modal">&times;</button>
                </div>
                <div class="modal-body" style="padding-top: 0 !important;font-size:12px;min-height:600px;">
                    <nav>
                        <div class="nav nav-tabs" id="nav-vendortab" role="tablist">
                            <a class="nav-item nav-link active" id="nav-vendor-search-tab" onclick="showScroll('myModalSearchVendor');" data-toggle="tab" href="#nav-vendor-search" role="tab" aria-controls="nav-vendor-search" aria-selected="true">Vendor Search</a>
                            <a class="nav-item nav-link" id="nav-vendor-detail-tab" onclick="hideScroll('myModalSearchVendor');" data-toggle="tab" href="#nav-vendor-detail" role="tab" aria-controls="nav-vendor-detail" aria-selected="false">Details</a>
                            <!--<a class="nav-item nav-link" id="nav-vendor-google-tab" onclick="hideScroll('myModalSearchVendor');" data-toggle="tab" href="#nav-vendor-google" role="tab" aria-controls="nav-vendor-google" aria-selected="false">Google</a>-->
                        </div>
                    </nav>
                    <div class="tab-content" id="nav-vendortabContent" style="padding: 0;">
                        <div class="tab-pane fade show active" id="nav-vendor-search" role="tabpanel" aria-labelledby="nav-vendor-search-tab">
                            <div class="row" style="margin-top: 0px !important;">
                                <div class="col-md-12">
                                    <table class="table table-sm table-whithout-border" style="margin-top: 7px;margin-bottom: 5px;">
                                        <tr>
                                            <td width="40%">
                                                <input type="hidden" id="searchvendor_type" />
                                                <input type="hidden" id="searchvendor_trips_selected" />
                                                <div class="input-group mb-3" style="margin-bottom: 0px !important;">
                                                    <div class="input-group-prepend">
                                                        <span class="input-group-text" id="basic-addon1"><i class="fas fa-search"></i></span>
                                                    </div>
                                                    <input type="text" id="searchvendor_airline" class="form-control form-control-sm" placeholder="Airline Name OR Airline code (2 letters)" aria-describedby="basic-addon1" />
                                                </div>
                                            </td>
                                            <td width="60%" style="padding-top:5px !important">
                                                <button type="button" class="btn btn-info btn-sm btn-custom" onclick="searchVendor();">Search</button>
                                            </td>
                                        </tr>
                                    </table>
                                </div>
                            </div>     
                            <div class="row">
                                <div class="col-md-12">
                                    <div style="border-bottom:1px solid #dee2e6;"><h4 style="font-size: 20px;">Select Vendor</h4></div>
                                </div>
                            </div>
                            <div class="row">
                                <div class="col-md-6">
                                    <button type="button" class="btn btn-danger btn-sm" onclick="createBidRequest();" >Create Bid Request</button>
                                </div>
                                <div class="col-md-6">
                                    
                                </div>
                            </div>
                            <div class="row" style="margin-bottom:10px;">
                                <div class="col-md-12">
                                    <span style="float:left;margin-top:6px;">View:</span>
                                    <span style="float:left;margin-left:17px;">
                                        <select id="searchvendor_status" class="form-control form-control-sm" style="width: 200px;" onchange="searchVendor();">
                                            <option value="All">All</option>
                                            <option value="Inactive">Inactive</option>
                                            <option value="Active" selected="selected">Active</option>
                                        </select>
                                    </span>
                                </div>
                            </div>
                            <apex:outputPanel id="searchVendorPanel">
                                <input type="hidden" value="{!limitVendor}" id="listtrip_limitVendor" />
                                <input type="hidden" value="{!offsetVendor}" id="listtrip_offsetVendor" />
                                <input type="hidden" value="{!totalPagesVendor}" id="listtrip_totalPagesVendor" />
                                <div style="display: flex; padding: 4px; background-color:#e9ecef; border: 1px solid #dee2e6;">
                                    <div style="flex: 1; display: flex; align-items: center;">
                                        <button class="btn btn-secondary btn-sm filePaginator btn-nav-modal btn-listvendor-first" type="button" onclick="GotoPageVendor('first');">
                                            <i class="fas fa-step-backward"></i>
                                        </button>
                                        <button class="btn btn-secondary btn-sm btn-nav-modal btn-listvendor-previous" type="button" style="padding-right: 3px;" onclick="GotoPageVendor('previous');">
                                            <i class="fas fa-caret-left fa-lg"></i>
                                        </button>
                                        <button class="btn btn-secondary btn-sm btn-nav-modal btn-listvendor-next" type="button" style="padding-left: 3px;" onclick="GotoPageVendor('next');">
                                            <i class="fas fa-caret-right fa-lg"></i>
                                        </button>
                                        <button class="btn btn-secondary btn-sm btn-nav-modal btn-listvendor-last" type="button" onclick="GotoPageVendor('last');">
                                            <i class="fas fa-step-forward"></i>
                                        </button>
                                    </div>
                                    <div style="display: flex;">
                                        <div class="fileNavigatorMessage" style="display: flex; flex: 1; align-self: center;">Page {!IF(OR(offsetVendor == null,offsetVendor <= 0),1,(offsetVendor/limitVendor)+1)} of {!totalPagesVendor}</div>
                                    </div>
                                </div>
                                <table id="dataVendors" class="table table-sm" style="margin-top:0;margin-bottom:0;">
                                    <thead class="thead-light">
                                        <tr>
                                            <th scope="col" width="5%">
                                                <a href="javascript:void(0);" style="color: #495057;" onclick="sortVendor('Flag_icon__c','{!orderOrientationVendor}');">
                                                    <span style="float:left;"><i class="fas fa-info-circle"></i></span>
                                                    <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldVendor == 'Flag_icon__c',orderOrientationVendor == 'DESC'),'','display:none;')}"></i>
                                                    <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldVendor == 'Flag_icon__c',orderOrientationVendor == 'ASC'),'','display:none;')}"></i>
                                                </a>
                                            </th>
                                            <th scope="col" width="10%">
                                                <a href="javascript:void(0);" style="color: #495057;" onclick="sortVendor('Airline_Code__c','{!orderOrientationVendor}');">
                                                    <span style="float:left;">Code</span>
                                                    <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldVendor == 'Airline_Code__c',orderOrientationVendor == 'DESC'),'','display:none;')}"></i>
                                                    <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldVendor == 'Airline_Code__c',orderOrientationVendor == 'ASC'),'','display:none;')}"></i>
                                                </a>
                                            </th>
                                            <th scope="col" width="25%">
                                                <a href="javascript:void(0);" style="color: #495057;" onclick="sortVendor('Name','{!orderOrientationVendor}');">
                                                    <span style="float:left;">Vendor</span>
                                                    <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldVendor == 'Name',orderOrientationVendor == 'DESC'),'','display:none;')}"></i>
                                                    <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldVendor == 'Name',orderOrientationVendor == 'ASC'),'','display:none;')}"></i>
                                                </a>
                                            </th>
                                            <th scope="col" width="20%">
                                                <span style="float:left;">Type</span>
                                                <!--<a href="javascript:void(0);" style="color: #495057;" onclick="sortVendor('Service_Types__c','{!orderOrientationVendor}');">
                                                    <span style="float:left;">Type</span>
                                                    <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldVendor == 'Service_Types__c',orderOrientationVendor == 'DESC'),'','display:none;')}"></i>
                                                    <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldVendor == 'Service_Types__c',orderOrientationVendor == 'ASC'),'','display:none;')}"></i>
                                                </a>-->
                                            </th>
                                            <th scope="col" width="15%">
                                                <a href="javascript:void(0);" style="color: #495057;" onclick="sortVendor('Status__c','{!orderOrientationVendor}');">
                                                    <span style="float:left;">Status</span>
                                                    <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldVendor == 'Status__c',orderOrientationVendor == 'DESC'),'','display:none;')}"></i>
                                                    <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldVendor == 'Status__c',orderOrientationVendor == 'ASC'),'','display:none;')}"></i>
                                                </a>
                                            </th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <apex:repeat value="{!searchVendorList}" var="vendor">
                                            <tr onclick="selectVendorRow(this);" vid="{!vendor.Id}">
                                                <td>
                                                    <apex:outputText value="{!vendor.Flag_icon__c}" escape="false" />
                                                </td>
                                                <td>
                                                    {!vendor.Airline_Code__c}
                                                </td>
                                                <td>
                                                    <a href="javascript:void(0);" onclick="viewVendorDetail(event,'{!vendor.Id}');">{!vendor.Name}</a>
                                                </td>
                                                <td>
                                                   	{!vendor.Service_Types__c}
                                                </td>
                                                <td>
                                                    {!vendor.Status__c}
                                                </td>
                                            </tr>
                                        </apex:repeat>
                                    </tbody>
                                </table>
                                <div style="display: flex; padding: 4px; background-color:#e9ecef; border: 1px solid #dee2e6;">
                                    <div style="flex: 1; display: flex; align-items: center;">
                                        <button class="btn btn-secondary btn-sm filePaginator btn-nav-modal btn-listvendor-first" type="button" onclick="GotoPageVendor('first');">
                                            <i class="fas fa-step-backward"></i>
                                        </button>
                                        <button class="btn btn-secondary btn-sm btn-nav-modal btn-listvendor-previous" type="button" style="padding-right: 3px;" onclick="GotoPageVendor('previous');">
                                            <i class="fas fa-caret-left fa-lg"></i>
                                        </button>
                                        <button class="btn btn-secondary btn-sm btn-nav-modal btn-listvendor-next" type="button" style="padding-left: 3px;" onclick="GotoPageVendor('next');">
                                            <i class="fas fa-caret-right fa-lg"></i>
                                        </button>
                                        <button class="btn btn-secondary btn-sm btn-nav-modal btn-listvendor-last" type="button" onclick="GotoPageVendor('last');">
                                            <i class="fas fa-step-forward"></i>
                                        </button>
                                    </div>
                                    <div style="display: flex;">
                                        <div class="fileNavigatorMessage" style="display: flex; flex: 1; align-self: center;">Page {!IF(OR(offsetVendor == null,offsetVendor <= 0),1,(offsetVendor/limitVendor)+1)} of {!totalPagesVendor}</div>
                                    </div>
                                </div>
                            </apex:outputPanel>
                        </div>
                        <div class="tab-pane fade" id="nav-vendor-detail" role="tabpanel" aria-labelledby="nav-vendor-detail-tab" style="padding-top:10px;">
                            <apex:outputPanel id="detailVendorPanel">
                                <span style="{!IF(detailId == null,'','display:none;')}">Click Vendor name in "Vendor Search" tab to get the details.</span>
                                <apex:iframe src="AccountDetailVFP?detailid={!detailId}" rendered="{!IF(detailId == null, false, true)}" scrolling="true" />
                            </apex:outputPanel>
                        </div>
                        <div class="tab-pane fade" id="nav-vendor-google" role="tabpanel" aria-labelledby="nav-vendor-google-tab">
                            <apex:outputPanel id="vendorGooglePanel">
                                <span style="{!IF(searchVendor_CityGoogle == '','','display:none;')}">Select the city.</span>
                                <!--<apex:iframe src="https://www.google.com/maps/search/?api=1&query={!searchVendor_CityGoogle}" rendered="{!IF(searchVendor_CityGoogle == '', false, true)}" width="100%" scrolling="true" />-->
                                <apex:iframe src="https://www.google.com/maps/embed/v1/place?q={!searchVendor_CityGoogle}&zoom=14&key=AIzaSyBMG4nEYV5KPLW39kztJ_F8M-lSA_gCZmY" rendered="{!IF(searchVendor_CityGoogle == '', false, true)}" width="100%" scrolling="true" />
                            </apex:outputPanel>
                        </div>
                    </div>
                </div>
                <div class="modal-footer text-right" style="display: block;">
                    <button type="button" class="btn btn-sm btn-outline-secondary" data-dismiss="modal">Close</button>
                    <apex:outputPanel id="totalBidsCreatedPanel">
                        <input type="hidden" id="totalbidscreate" value="{!bidsCreated}" />
                    </apex:outputPanel>
                </div>
            </div>
        </div>
    </div>
    <!-- End Modal -->
    <!-- Modal content-->
    <div class="modal fade" id="myModalSendBidRequest" role="dialog" style="padding-right: 18px;">
        <div class="modal-dialog modal-xl">
            <!-- Modal content-->
            <div class="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title">Send Leads to selected Vendor Contacts</h4>
                    <button type="button" class="close" onclick="closeModalSendBidRequestJs($('input[id$=tripid]').val());">&times;</button>
                </div>
                <div class="modal-body" style="font-size:12px;">
                    <apex:outputPanel id="sendBidRequestSelectPanel">
                        <div class="{!IF(sendBidRequestMapSize == 0,'','d-none')} row"><div class="col text-center">There are no bids available to send.</div></div>
                        <div class="row {!IF(sendBidRequestMapSize == 0,'d-none','')}">
                            <div class="col-md-9">
                                <!--<button type="button" class="btn btn-secondary btn-custom" onclick="openAttachProductionDocs();">Attach Production Docs</button>-->
                            </div>
                            <div class="col-md-3" style="text-align: right;padding-right: 25px;">
                                <label>Select All Vendors</label>
                                <input class="form-check-input" type="checkbox" id="sendbidrequest_allvendors" style="margin-left: -5px;margin-top: 0px;" onchange="selectAllVendors(this,'myModalSendBidRequest');" />
                            </div>
                        </div>
                    </apex:outputPanel>
                    <apex:outputPanel id="sendBidRequestPanel">
                        <apex:outputPanel rendered="{!isBidRequestRendered}">
                            <apex:inputHidden id="trip_sendbidfirsttime" value="{!bidSendBidFirstTime}" />
                            <apex:repeat value="{!sendBidRequestMap}" var="bidRequest">
                                <div class="group-vendor" style="margin-bottom:15px;">
                                    <div class="fieldset" style="font-size: 12px;">
                                        <div class="row" style="margin-top: 0px !important;">
                                            <div class="col-md-2">
                                                Vendor Name
                                            </div>
                                            <div class="col-md-4">
                                                <span style="position:absolute;">
                                                    <a href="/{!sendBidRequestMap[bidRequest].Vendor__c}" target="_blank" style="{!IF(sendBidRequestMap[bidRequest].Vendor__c <> null,'','display:none;')}">{!sendBidRequestMap[bidRequest].Vendor__r.Name}</a>
                                                    <a href="/{!sendBidRequestMap[bidRequest].Provider__c}" target="_blank" style="{!IF(AND(sendBidRequestMap[bidRequest].Vendor__c == null, sendBidRequestMap[bidRequest].Provider__c <> null),'','display:none;')}">{!sendBidRequestMap[bidRequest].Provider__r.Name}</a>
                                                </span>
                                            </div>
                                            <div class="col-md-6 col-data" style="text-align: right;" data-id="{!bidRequest}">
                                                <!--<input class="form-check-input select-vendor" data-id="{!bidRequest}" type="checkbox" style="margin-right: 0px;margin-top: 0px;" />-->
                                                <apex:inputCheckbox styleClass="form-check-input select-vendor" style="margin-right: 0px;margin-top: 0px;" value="{!sendBidRequestMapSelected[bidRequest]}" />
                                                <label>Select Vendor</label>
                                            </div>
                                        </div>
                                        <div class="row">
                                            <div class="col-md-2">
                                                Select Primary Contact
                                            </div>
                                            <div class="col-md-4">
                                                <span style="float:left;width:55%;">
                                                    <apex:selectList size="1" styleClass="form-control form-control-sm primary-contact" value="{!sendBidRequestMap[bidRequest].Vendor_Contact__c}" onchange="changeContactVendorBid(this,'{!bidRequest}');" style="{!IF(contactSelectOption_bidRequestSizeMap[bidRequest] > 0,'','display:none;')}">
                                                        <apex:selectOptions value="{!contactSelectOption_bidRequestMap[bidRequest]}" />
                                                    </apex:selectList>
                                                    <span style="color:red;{!IF(contactSelectOption_bidRequestSizeMap[bidRequest] > 0,'display:none;','')}">No contact found</span>
                                                </span>
                                            </div>
                                            <div class="col-md-3" style="padding:0;text-align:right;">
                                                <!--<button type="button" class="btn btn-secondary btn-custom" onclick="javascript:void(0);">Preview Pdf</button>-->
                                                <button type="button" class="btn btn-secondary btn-custom" onclick="openAddContactVendor('{!bidRequest}','{!IF(sendBidRequestMap[bidRequest].Vendor__c <> null,sendBidRequestMap[bidRequest].Vendor__r.Name,sendBidRequestMap[bidRequest].Provider__r.Name)}','');">Add Contact</button>
                                                <!--<button type="button" class="btn btn-secondary btn-custom btn-preview-link" onclick="openPreviewLink(this,'{!sendBidRequestMap[bidRequest].Id}','{!bidRequest}','{!IF(sendBidRequestMap[bidRequest].Vendor__c <> null,sendBidRequestMap[bidRequest].Vendor__r.Name,sendBidRequestMap[bidRequest].Provider__r.Name)}','link');">Preview Link</button>-->
                                                <button type="button" class="btn btn-secondary btn-custom btn-preview-pdf" onclick="if('{!tripView.Air_Charter__c}' == 'false') openPreviewReleaseBid(this,'{!sendBidRequestMap[bidRequest].Id}','{!bidRequest}','{!sendBidRequestMap[bidRequest].Vendor__r.Name}','send_bid_request'); else congaPreviewSendBidRequest(this,'{!itineraryId}','{!tripView.id}','{!tripView.Status__c}','{!sendBidRequestMap[bidRequest].Id}','{!sendBidRequestMap[bidRequest].Status__c}', '{!JSENCODE(sendBidRequest_congaQueriesJson)}', '{!sendBidRequest_congaEmailTemplateId}', '{!JSENCODE(sendBidRequest_congaEmailSubject)}', '{!sendBidRequest_congaTemplateId1}');">Preview</button>
                                            </div>
                                            <div class="col-md-3" style="text-align:right;">
                                                <span style="font-weight:bold;margin-right:20px;">{!sendBidRequestMap[bidRequest].Status__c}</span>
                                                <input type="hidden" class="sendbidrequest-status" value="{!sendBidRequestMap[bidRequest].Status__c}" />
                                            </div>
                                        </div>
                                    </div>
                                    <div class="row" style="padding:0;margin-top: 0px !important;">
                                        <div class="col-md-12">
                                            <table class="table table-sm table-bordered" style="margin-top:5px;margin-bottom:0;">
                                                <thead class="thead-light">
                                                    <tr>
                                                        <th width="7%">Select</th>
                                                        <th width="8%">Order</th>
                                                        <th width="20%">Name</th>
                                                        <th width="15%">Designation/Title</th>
                                                        <th width="20%">Work Phone</th>
                                                        <th width="15%">Email</th>
                                                        <th width="15%">Fax</th>
                                                    </tr>
                                                </thead>
                                                <tbody>
                                                    <apex:repeat value="{!contactsByVendorParent_bidRequestMap[sendBidRequestMap[bidRequest].Vendor__r.ParentId]}" var="contactv" rendered="{!IF(sendBidRequestMap[bidRequest].Vendor__r.ParentId <> null,true,false)}">
                                                        <tr>
                                                            <td email-data="{!contactv.c.Email}" contactid-data="{!contactv.c.Id}">
                                                                <apex:inputCheckbox value="{!contactv.selected}" disabled="{!contactv.disabled}" styleClass="form-check-input check-contact" style="margin-left: 10px;" />
                                                            </td>
                                                            <td>{!contactv.c.Order__c} NR</td>
                                                            <td><a href="javascript:void(0);" onclick="openAddContactVendor('{!contactv.c.AccountId}','{!contactv.c.Account.Name}','{!contactv.c.Id}');">{!contactv.c.Name}</a></td>
                                                            <td>{!contactv.c.Designation_title__c}</td>
                                                            <td><a href="tel:{!contactv.c.Phone}">{!contactv.c.Phone}</a></td>
                                                            <td><a href="mailto:{!contactv.c.Email}">{!contactv.c.Email}</a></td>
                                                            <td>{!contactv.c.Fax}</td>
                                                        </tr>
                                                    </apex:repeat>
                                                    <apex:repeat value="{!contactsByVendor_bidRequestMap[bidRequest]}" var="contactv">
                                                        <tr>
                                                            <td email-data="{!contactv.c.Email}" contactid-data="{!contactv.c.Id}">
                                                                <apex:inputCheckbox value="{!contactv.selected}" disabled="{!contactv.disabled}" styleClass="form-check-input check-contact" style="margin-left: 10px;" />
                                                            </td>
                                                            <td>{!contactv.c.Order__c}</td>
                                                            <td><a href="javascript:void(0);" onclick="openAddContactVendor('{!contactv.c.AccountId}','{!contactv.c.Account.Name}','{!contactv.c.Id}');">{!contactv.c.Name}</a></td>
                                                            <td>{!contactv.c.Designation_title__c}</td>
                                                            <td><a href="tel:{!contactv.c.Phone}">{!contactv.c.Phone}</a></td>
                                                            <td><a href="mailto:{!contactv.c.Email}">{!contactv.c.Email}</a></td>
                                                            <td>{!contactv.c.Fax}</td>
                                                        </tr>
                                                    </apex:repeat>
                                                </tbody>
                                            </table>
                                        </div>
                                    </div>
                                </div>
                                <hr/>
                            </apex:repeat>
                        </apex:outputPanel>
                    </apex:outputPanel>
                </div>
                <div class="modal-footer" style="display: block;">
                    <button type="button" class="btn btn-danger btn-sm btn-send-pdf" onclick="sendBidRequest()" >Send Email</button>
                    <button type="button" class="btn btn-danger btn-sm btn-edit-all-pdf" onclick="openEditPDF('pdf');" >Edit All PDFs</button>
                    <!--<button type="button" class="btn btn-danger btn-sm btn-send-link" onclick="sendBidRequestLink();" >Send Link</button>
                    <button type="button" class="btn btn-danger btn-sm btn-edit-all-link" onclick="openEditPDF('link');" >Edit All Links</button>-->
                </div>
            </div>
        </div>
    </div>
    <!-- End Modal -->
    <!-- Modal content-->
    <div class="modal fade" id="myModalSendOptions" role="dialog">
        <apex:outputPanel id="myModalSendOptions" layout="block" styleClass="modal-dialog modal-xl">
            <div class="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title">Send Options to Contacts</h4>
                    <input type="hidden" id="emailedit_type" />
                    <button type="button" class="close" onclick="closeTripModalJs('myModalSendOptions');">&times;</button>
                </div>
                <div class="modal-body" style="font-size:12px;padding-top: 0px;">
                    <apex:outputPanel id="sendOptionsPanel">
                        <div class="fieldset" style="font-size: 12px;">
                            <div class="row" style="margin-top: 0px !important;">
                                <div class="col-md-2 col-md-offset-6">
                                    Select Primary Contact
                                </div>
                                <div class="col-md-3">
                                    <apex:selectList size="1" styleClass="form-control form-control-sm primary-contact" value="{!sendOptions_primaryContactId}">
                                        <apex:selectOptions value="{!contactsByProduction}" />
                                        <apex:actionSupport event="onchange" action="{!changeContactProduction}" status="loading" reRender="sendOptionsPanel">
                                        </apex:actionSupport>                                    
                                    </apex:selectList>
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-12">
                                <table class="table table-sm table-bordered" style="margin-top:5px;margin-bottom:0;">
                                    <thead class="thead-light">
                                        <tr>
                                            <th width="10%">Select</th>
                                            <th width="20%">Name</th>
                                            <th width="25%">Company</th>
                                            <th width="25%">Designation/Title</th>
                                            <th width="25%">Email</th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <apex:repeat value="{!contactWrapperByProduction}" var="contactprod">
                                            <tr>
                                                <td data-contactid="{!contactprod.c.id}" data-contactemail="{!contactprod.c.Email}">
                                                    <apex:inputCheckbox value="{!contactprod.selected}" disabled="{!contactprod.disabled}" styleClass="form-check-input check-contact" style="margin-left: 10px;" />
                                                </td>
                                                <td>{!contactprod.c.Name__c}</td>
                                                <td>{!contactprod.c.Account_Name__c}</td>
                                                <td>{!contactprod.c.Designation_title__c}</td>
                                                <td><a href="mailto:{!contactprod.c.Email}">{!contactprod.c.Email}</a></td>
                                            </tr>
                                        </apex:repeat>
                                    </tbody>
                                </table>
                                <div class="row" style="margin-top: 0px !important;">
                                    <div class="col-md-12">
                                        <div class="row">
                                            <div class="col-md-12">
                                                <label>Message:</label>
                                                <apex:inputTextarea id="communitynote_body_air" rows="10" styleClass="form-control form-control-sm" />
                                                <script>
                                                CKEDITOR.replace('{!$Component.communitynote_body_air}', {
                                                    language: 'en',
                                                    extraAllowedContent: 'th{color,background,background-color}'
                                                });
                                                </script>
                                            </div>
                                        </div>                                    
                                    </div>
                                </div>
                            </div>
                        </div>
                    </apex:outputPanel>
                </div>
                <div class="modal-footer" style="display: block;">
                    <button type="button" class="btn btn-danger btn-sm" onclick="congaPreviewSendOptions('{!tripView.id}', '{!tripView.Status__c}', '{!tripItineraryId}', '{!JSENCODE(sendOptions_congaQueriesJson)}', '{!sendOptions_congaEmailTemplateId}', '{!JSENCODE(sendOptions_congaEmailSubject)}', '{!sendOptions_congaTemplateId}');" >Preview</button>
                    <button type="button" class="btn btn-danger btn-sm" onclick="congaSendOptions();" >Send Email</button>
                    <button type="button" class="btn btn-danger btn-sm" onclick="sendLink();" >Send Link</button>
                </div>
            </div>
        </apex:outputPanel>
    </div>
    <!-- End Modal -->
    <!-- Modal content-->
    <div class="modal fade" id="myModalReleaseBid" role="dialog" style="padding-right: 18px;">
        <div class="modal-dialog modal-xl">
            <!-- Modal content-->
            <div class="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title">Send Bid Release Notes to Vendor Contacts</h4>
                    <button type="button" class="close" onclick="closeModalReleaseBidJs($('input[id$=tripid]').val());">&times;</button>
                </div>
                <div class="modal-body" style="font-size:12px;">
                    <apex:outputPanel id="releaseBidAllPanel" layout="block">
                        <apex:outputPanel rendered="{!!bidReleaseActive}" style="color:red;font-weight:bold;font-size: 14px;">Please make sure Bid Request is already sent.</apex:outputPanel>
                        <apex:outputPanel rendered="{!bidReleaseActive}" layout="block">
                            <apex:outputPanel id="releaseBidSelectPanel">
                                <div class="{!IF(sendBidRequestMapReleaseSize == 0,'','d-none')} row"><div class="col text-center">There are no bids available to release.</div></div>
                                <div class="row {!IF(sendBidRequestMapReleaseSize == 0,'d-none','')}">
                                    <div class="col-md-9"></div>
                                    <div class="col-md-3" style="text-align: right;padding-right: 25px;">
                                        <label>Select All Vendors</label>
                                        <input class="form-check-input" type="checkbox" id="sendrelease_allvendors" style="margin-left: -5px;margin-top: 0px;" onchange="selectAllVendors(this,'myModalReleaseBid');" />
                                    </div>
                                </div>
                            </apex:outputPanel>
                            <apex:outputPanel id="releaseBidPanel">
                                <apex:outputPanel rendered="{!isBidReleaseRendered}">
                                    <apex:repeat value="{!sendBidRequestMapRelease}" var="bidRequest">
                                        <div class="group-vendor" style="margin-bottom:15px;">
                                            <div class="fieldset" style="font-size: 12px;">
                                                <div class="row" style="margin-top: 0px !important;">
                                                    <div class="col-md-2">
                                                        <span>Vendor Name</span>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <span style="position:absolute;">
                                                            <a href="/{!sendBidRequestMapRelease[bidRequest].Vendor__c}" target="_blank" style="{!IF(sendBidRequestMapRelease[bidRequest].Vendor__c <> null,'','display:none;')}">{!sendBidRequestMapRelease[bidRequest].Vendor__r.Name}</a>
                                                        </span>
                                                    </div>
                                                    <div class="col-md-6 col-data" style="text-align:right;" data-id="{!bidRequest}">
                                                        <!--<input class="form-check-input select-vendor" data-id="{!bidRequest}" type="checkbox" style="margin-right: 0px;margin-top: 0px;" />-->
                                                        <apex:inputCheckbox styleClass="form-check-input select-vendor" style="margin-right: 0px;margin-top: 0px;" value="{!sendBidRequestMapReleaseSelected[bidRequest]}" />
                                                        <label>Select Vendor</label>
                                                    </div>
                                                </div>
                                                <div class="row">
                                                    <div class="col-md-2">
                                                        <label>Select Primary Contact</label>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <span style="float:left;width:55%;">
                                                            <apex:selectList size="1" styleClass="form-control form-control-sm primary-contact" value="{!sendBidRequestMapRelease[bidRequest].Vendor_Contact__c}" onchange="changeContactReleaseBid(this,'{!bidRequest}');" style="{!IF(contactSelectOption_releaseSizeMap[bidRequest] > 0,'','display:none;')}">
                                                                <apex:selectOptions value="{!contactSelectOption_releaseMap[bidRequest]}" />
                                                            </apex:selectList>
                                                            <span style="color:red;{!IF(contactSelectOption_releaseSizeMap[bidRequest] > 0,'display:none;','')}">No contact found</span>
                                                        </span>
                                                    </div>
                                                    <div class="col-md-3" style="padding:0;text-align:right;">
                                                        <button type="button" class="btn btn-secondary btn-custom" onclick="openAddContactVendor('{!bidRequest}','{!IF(sendBidRequestMapRelease[bidRequest].Vendor__c <> null,sendBidRequestMapRelease[bidRequest].Vendor__r.Name,sendBidRequestMapRelease[bidRequest].Provider__r.Name)}','');">Add Contact</button>
                                                        <button type="button" class="btn btn-secondary btn-custom" onclick="openPreviewReleaseBid(this,'{!sendBidRequestMapRelease[bidRequest].Id}','{!bidRequest}','{!sendBidRequestMapRelease[bidRequest].Vendor__r.Name}','release_bid');">Preview</button>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <!--<span style="font-weight:bold;margin-right:20px;">{!sendBidRequestMapRelease[bidRequest].Status__c}</span>
<input type="hidden" class="sendbidrequest-status" value="{!sendBidRequestMapRelease[bidRequest].Status__c}" />-->
                                                    </div>
                                                </div>
                                            </div>
                                            <div class="row" style="padding:0;margin-top: 0px !important;">
                                                <div class="col-md-12">
                                                    <table class="table table-sm table-bordered" style="margin-top:5px;margin-bottom:0;">
                                                        <thead class="thead-light">
                                                            <tr>
                                                                <th width="7%">Select</th>
                                                                <th width="8%">Order</th>
                                                                <th width="20%">Name</th>
                                                                <th width="15%">Designation/Title</th>
                                                                <th width="20%">Work Phone</th>
                                                                <th width="15%">Email</th>
                                                                <th width="15%">Fax</th>
                                                            </tr>
                                                        </thead>
                                                        <tbody>
                                                            <apex:repeat value="{!contactsByVendorParent_releaseMap[sendBidRequestMapRelease[bidRequest].Vendor__r.ParentId]}" var="contact1" rendered="{!IF(sendBidRequestMapRelease[bidRequest].Vendor__r.ParentId <> null,true,false)}">
                                                                <tr>
                                                                    <td email-data="{!contact1.c.Email}" contactid-data="{!contact1.c.Id}">
                                                                        <apex:inputCheckbox value="{!contact1.selected}" disabled="{!contact1.disabled}" styleClass="form-check-input check-contact" style="margin-left: 10px;" />
                                                                    </td>
                                                                    <td>{!contact1.c.Order__c} NR</td>
                                                                    <td><a href="javascript:void(0);" onclick="openAddContactVendor('{!contact1.c.AccountId}','{!contact1.c.Account.Name}','{!contact1.c.Id}');">{!contact1.c.Name}</a></td>
                                                                    <td>{!contact1.c.Designation_title__c}</td>
                                                                    <td><a href="tel:{!contact1.c.Phone}">{!contact1.c.Phone}</a></td>
                                                                    <td><a href="mailto:{!contact1.c.Email}">{!contact1.c.Email}</a></td>
                                                                    <td>{!contact1.c.Fax}</td>
                                                                </tr>
                                                            </apex:repeat>
                                                            <apex:repeat value="{!contactsByVendor_releaseMap[bidRequest]}" var="contact1">
                                                                <tr>
                                                                    <td email-data="{!contact1.c.Email}" contactid-data="{!contact1.c.Id}">
                                                                        <apex:inputCheckbox value="{!contact1.selected}" disabled="{!contact1.disabled}" styleClass="form-check-input check-contact" style="margin-left: 10px;" />
                                                                    </td>
                                                                    <td>{!contact1.c.Order__c}</td>
                                                                    <td><a href="javascript:void(0);" onclick="openAddContactVendor('{!contact1.c.AccountId}','{!contact1.c.Account.Name}','{!contact1.c.Id}');">{!contact1.c.Name}</a></td>
                                                                    <td>{!contact1.c.Designation_title__c}</td>
                                                                    <td><a href="tel:{!contact1.c.Phone}">{!contact1.c.Phone}</a></td>
                                                                    <td><a href="mailto:{!contact1.c.Email}">{!contact1.c.Email}</a></td>
                                                                    <td>{!contact1.c.Fax}</td>
                                                                </tr>
                                                            </apex:repeat>
                                                        </tbody>
                                                    </table>
                                                </div>
                                            </div>
                                        </div>
                                        <hr/>
                                    </apex:repeat>
                                </apex:outputPanel>
                            </apex:outputPanel>
                        </apex:outputPanel>
                    </apex:outputPanel>
                </div>
                <apex:outputPanel id="releaseBidButtonsPanel" layout="block">
                    <apex:outputPanel rendered="{!bidReleaseActive}" layout="block">
                        <div class="modal-footer" style="display: block;">
                            <button type="button" class="btn btn-danger btn-sm" onclick="sendReleaseBid();" >Send Email</button>
                            <button type="button" class="btn btn-danger btn-sm" onclick="openEditReleaseBid();" >Edit All Emails</button>
                        </div>
                    </apex:outputPanel>
                </apex:outputPanel>
            </div>
        </div>
    </div>
    <!-- End Modal -->
    <!-- Modal content-->
    <div class="modal fade" id="myModalDecisionDueDate" role="dialog">
        <div class="modal-dialog modal-xl">
            <!-- Modal content-->
            <apex:outputPanel id="decisionDueDateModal" layout="block" styleClass="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title">Decision Due Reminder</h4>
                    <!--<button type="button" onclick="{!IF(OR(ISBLANK(bidData.Rate_Agreement_Last_Send_Date__c),ISBLANK(bidData.Housing_Contract_Last_Send_Date__c)),'verifyRateOrHousingSentJs();','')}" class="close" data-dismiss="modal">&times;</button>-->
                    <button type="button" class="close" data-dismiss="modal">&times;</button>
                </div>
                <div class="modal-body" style="font-size:12px;padding-top: 0px;">
                    <apex:outputPanel id="decisionDueDateMessagePanel">
                        <div class="row">
                            <div class="col-md-12">
                                <div class="alert alert-danger alert-dismissible alert-email-message" role="alert" style="margin-bottom: 0px !important;{!IF(emailMessage <> '','','display:none;')}">
                                    {!emailMessage}
                                    <button type="button" class="close" data-dismiss="alert" aria-label="Close" style="padding: 9px 15px !important;">
                                        <span aria-hidden="true">&times;</span>
                                    </button>
                                    <input type="hidden" value="{!emailMessage}" class="error-message" />
                                </div>
                            </div>
                        </div>
                    </apex:outputPanel>
                    <apex:outputPanel id="decisionDueDatePanel">
                        <div class="row">
                            <div class="col-md-12">
                                <div class="fieldset" style="margin-top: 0 !important;">
                                    <div class="row" style="margin-top: 0 !important;">
                                        <div class="col-md-2">
                                            Production : 
                                        </div>
                                        <div class="col-md-4">
                                            <a href="/{!opportunity.Id}" target="_blank">{!opportunity.Name}</a>
                                        </div>
                                        <div class="col-md-6" style="text-align:right;">
                                            Doc Id: {!draft.Name}
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-2">
                                            Attention :
                                        </div>
                                        <div class="col-md-4">
                                            <apex:selectList size="1" value="{!draft.Attention__c}" id="decisionduedate_attention" styleClass="form-control form-control-sm" onchange="changeAttention(this);">
                                                <apex:selectOptions value="{!clientsByProduction}" />
                                            </apex:selectList>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-2">
                                            To :
                                        </div>
                                        <div class="col-md-10">
                                            <apex:outputPanel id="decisionDueDateToPanel">
                                                <div class="decisionduedate-to">
                                                    {!decisionDueDateContact.Email}
                                                </div>
                                            </apex:outputPanel>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-2">
                                            CC :
                                        </div>
                                        <div class="col-md-10">
                                            <div class="all-cc-email-decisionduedate"></div>
                                            <input type="text" class="form-control form-control-sm cc-email-decisionduedate" />
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-2">
                                            BCC :
                                        </div>
                                        <div class="col-md-10">
                                            <div class="all-bcc-email-decisionduedate"></div>
                                            <input type="text" class="form-control form-control-sm bcc-email-decisionduedate" />
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-12">
                                Subject <br/>
                                <apex:inputField id="decisionduedate_subject" value="{!draft.Subject__c}" styleClass="form-control form-control-sm subject-decisionduedate" />
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-12">
                                Salutation <br/>
                                <apex:outputPanel id="decisionDueDateSalutationPanel">
                                    <apex:inputField id="decisionduedate_salutation" value="{!draft.Salutation__c}" styleClass="form-control form-control-sm salutation-decisionduedate" />
                                </apex:outputPanel>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-4">
                                Attached: <br/>
                                <apex:selectList size="4" id="decisionduedate_attachs" style="width:100%;" />
                            </div>
                            <div class="col-md-8" style="padding-top: 15px;">      
                                <button type="button" class="btn btn-secondary btn-custom" onclick="removeAttachDocs('decisionduedate_attachs');" style="float: left;margin-right: 5px;">Remove</button>
                                <div class="upload-btn-wrapper" style="display: block;float: left;margin-right: 5px;">
                                    <button class="btn btn-secondary btn-custom" onclick="javascript:void(0);">Attach</button>
                                    <input type="file" id="fileDecisionDueDate" onchange="remoteLocationPostLast(event,'decision_due_date','decisionduedate_attachs','{!tripView.Id}');" />
                                </div>
                                <button type="button" class="btn btn-secondary btn-custom" onclick="openAttachDocs('bid','{!bidDataDecision.Id}','myModalDecisionDueDate','decisionduedate_attachs');">Attach Contracting Docs</button>
                            </div>
                        </div><!--
                        <div class="row">
                            <div class="col-md-12">
                                <label>Body</label>
                                <apex:inputTextarea id="decisionduedate_body2" value="{!draft.Body__c}" rows="5" styleClass="form-control form-control-sm" />
                                <script>
                                CKEDITOR.replace('{!$Component.decisionduedate_body2}', {
                                    language: 'en',
                                    extraAllowedContent: 'th{color,background,background-color}'
                                });
                                </script>
                            </div>
                        </div>
                    -->
                        <div class="row">
                            <div class="col-md-12">
                                Closing <br/>
                                <apex:inputTextarea id="decisionduedate_closing" value="{!draft.Closing__c}" styleClass="form-control form-control-sm" rows="4" />
                            </div>
                        </div>
                        <!--<div class="row">
                            <div class="col-md-12">
                                <label>Urgent:</label> <apex:inputCheckbox value="{!draft.Urgent__c}" id="decisionduedate_urgent" style="margin-left: -5px;margin-top: 3px;" styleClass="form-check-input" />
                            </div>
                        </div>-->
                        <apex:outputPanel id="fcqAuditFields" layout="block" styleClass="row">
                            <div class="col-md-12">
                                <div class="fieldset" style="margin-top: 0 !important;">
                                    <div class="row" style="margin-top: 0 !important;">
                                        <div class="col-md-3">
                                            Created By : <b>{!draft.CreatedBy.Name}</b>
                                        </div>
                                        <div class="col-md-3">
                                            Created On :&nbsp;
                                            <b><apex:outputField value="{!draft.CreatedDate}"/></b>
                                        </div>
                                        <div class="col-md-3">
                                            Sent By : <b><apex:outputField value="{!tripView.Decision_Due_Date_Last_Send_By__c}"/></b>
                                        </div>
                                        <div class="col-md-3">
                                            Sent On :&nbsp;
                                            <b><apex:outputField value="{!tripView.Decision_Due_Date_Last_Send_Date__c}"/></b>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-3">
                                            Modified By : <b>{!draft.LastModifiedBy.Name}</b>
                                        </div>
                                        <div class="col-md-3">
                                            Modified On :&nbsp;
                                            <b><apex:outputField value="{!draft.LastModifiedDate}"/></b>
                                        </div>
                                        <div class="col-md-3">
                                            Sent Via : <!--<span style="font-weight:bold;">{!IF(bidData.Rate_agreement_last_modified_by__c <> null,modifiedByRateAgreement,'')}</span>-->
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </apex:outputPanel>
                    </apex:outputPanel>
                </div>
                <div class="modal-footer" style="display: block;">
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="saveDecisionDueDate();" >Save</button>
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="sendEmailDecisionDueDate();" >Send Email</button>
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="deactivateDecisionDueDate();" >Deactivate</button>
                </div>
            </apex:outputPanel>
        </div>
    </div>
    <!-- End Modal -->
    
    <!-- Victor -->
    <apex:actionFunction action="{!sendLink}" name="sendLinkJs" status="loading" reRender="noneRender" oncomplete="alert('Link has been sent.');closeModal('myModalSendOptions');">
        <apex:param assignTo="{!communityNoteCoordinator}" name="communityNoteCoordinator" value="" />
    </apex:actionFunction>
    
    <!-- Conga Actionfunctions -->
    <apex:actionFunction action="{!openPreviewOptions}" name="openPreviewOptionsJs" status="loading" reRender="noneRender" oncomplete="congaPreviewOptions('{!tripView.Id}', '{!JSENCODE(sendOptions_congaQueriesJson)}', '{!sendOptions_congaEmailTemplateId}', '{!sendOptions_congaTemplateId}')"/>
    <apex:actionFunction action="{!openSendOptions}" name="openSendOptionsJs" status="loading" reRender="myModalSendOptions" oncomplete="openModal('myModalSendOptions');" />
    <apex:actionFunction action="{!congaSendOptions}" name="congaSendOptionsJs" status="loading" reRender="tripDetailPanel" oncomplete="alert('Air Options Sheet has been sent.');closeModal('myModalSendOptions');" />
    <apex:actionFunction name="loadTabContentAirJs" status="loadingSubTab" reRender="tabsByGroundPanel" oncomplete="$('.multiselect').chosen();verifyButtonsListBid();">
        <apex:param assignTo="{!tabAirDefault}" name="tabAirDefault" value="" />
    </apex:actionFunction>
    <!-- End Conga Actionfunctions -->

    <script>
    $(function(){
        verifyButtonsListTrip();
        if('{!tripViewId}' != ''){
            reRenderBidsByTrip('{!orderFieldBid}', '{!orderOrientationBid}');
        }
    });
    function verifyButtonsListTrip(){
        var limit = $('input[id$=listtrip_limitTrip]').val();
        var offset = parseInt($('input[id$=listtrip_offsetTrip]').val()) || 0;
        var totalpages = $('input[id$=listtrip_totalPagesTrip]').val();
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
    function verifyButtonsListVendor(){
        var limit = $('input[id$=listtrip_limitVendor]').val();
        var offset = parseInt($('input[id$=listtrip_offsetVendor]').val()) || 0;
        var totalpages = $('input[id$=listtrip_totalPagesVendor]').val();
        $('.btn-listvendor-first').prop('disabled',false);
        $('.btn-listvendor-previous').prop('disabled',false);
        $('.btn-listvendor-next').prop('disabled',false);
        $('.btn-listvendor-last').prop('disabled',false);
        if(offset == null || offset <= 0){
            $('.btn-listvendor-first').prop('disabled',true);
            $('.btn-listvendor-previous').prop('disabled',true);
        }
        var actual_page = 1;
        if(offset == null || offset <= 0) actual_page = 1; else actual_page = (offset/limit)+1;
        if(totalpages == actual_page){
            $('.btn-listvendor-next').prop('disabled',true);
            $('.btn-listvendor-last').prop('disabled',true);
        }
    }
    function deleteItineraryTrip(val){
        var confirmAction = confirm('Are you sure you want to delete this item?');
        if(confirmAction) deleteItineraryTripJs(val);
    }
    function deleteAircraftTrip(val){
        var confirmAction = confirm('Are you sure you want to delete this item?');
        if(confirmAction) deleteAircraftTripJs(val);
    }
    function editBid(val) {
        $(val).parents('table').find('.btn-edit').show();
        $(val).parents('table').find('.btn-delete').hide();
        $(val).parents('table').find('.show-data').show();
        $(val).parents('table').find('.btn-cancel').hide();
        $(val).parents('table').find('.btn-save').hide();
        $(val).parents('table').find('.data').hide();
        
        $(val).hide();
        $(val).parents('tr').find('.show-data').hide();
        $(val).parents('tr').find('.btn-cancel').show();
        $(val).parents('tr').find('.btn-save').show();
        $(val).parents('tr').find('.data').show();
    }
    function copyAir(val){
        $('.error-message').text('');
        $('.newdata').val('');
        $(val).parents('table').find('.new-record .order').val($(val).parents('tr').find('.order').val());
		$(val).parents('table').find('.new-record .depdate').val($(val).parents('tr').find('.depdate').val());
        $(val).parents('table').find('.new-record .arrdate').val($(val).parents('tr').find('.arrdate').val());
        $(val).parents('table').find('.new-record .flight').val($(val).parents('tr').find('.flight').val());
        $(val).parents('table').find('.new-record .depcity').val($(val).parents('tr').find('.depcity').val());
        $(val).parents('table').find('.new-record .depcityid').val($(val).parents('tr').find('.depcityid').val());
        $(val).parents('table').find('.new-record .arrcity').val($(val).parents('tr').find('.arrcity').val());
        $(val).parents('table').find('.new-record .arrcityid').val($(val).parents('tr').find('.arrcityid').val());
        $(val).parents('table').find('.new-record .deptime').val($(val).parents('tr').find('.deptime').val());
        $(val).parents('table').find('.new-record .arrtime').val($(val).parents('tr').find('.arrtime').val());
        $(val).parents('table').find('.new-record .durationhrs').val($(val).parents('tr').find('.durationhrs').val());
        $(val).parents('table').find('.new-record .durationmins').val($(val).parents('tr').find('.durationmins').val());
        $(val).parents('table').find('.new-record .equiptype').val($(val).parents('tr').find('.equiptype').val());
        $(val).parents('table').find('.new-record .seats').val($(val).parents('tr').find('.seats').val());
        $(val).parents('table').find('.new-record .notes').val($(val).parents('tr').find('.notes').val());
        $(val).parents('table').find('.new-record').show();
    }
    function isEmpty(obj) {
        for(var key in obj) if(obj.hasOwnProperty(key)) return false;
        return true;
    }
    function saveEditItineraryTrip(val){
        var id = $(val).parents('tr').find('.id').val();
        var order = $(val).parents('tr').find('.order').val();
        var depdate = $(val).parents('tr').find('.depdate').val();
        var arrdate = $(val).parents('tr').find('.arrdate').val();
        var flight = $(val).parents('tr').find('.flight').val();
        var depcityid = $(val).parents('tr').find('.depcityid').val();
        var arrcityid = $(val).parents('tr').find('.arrcityid').val();
        var deptime = $(val).parents('tr').find('.deptime').val();
        var arrtime = $(val).parents('tr').find('.arrtime').val();
        var durationhrs = $(val).parents('tr').find('.durationhrs').val();
        var durationmins = $(val).parents('tr').find('.durationmins').val();
        var equiptype = $(val).parents('tr').find('.equiptype').val();
        var notes = $(val).parents('tr').find('.notes').val();
        var saveData = true;
        
        $('.error-message').text('');
        if(depdate == ''){
            $(val).parents('tr').find('.depdate').parents('.data').find('.error-message').text('Date is required');
            saveData = false;
        }
        if(depcityid == ''){
            $(val).parents('tr').find('.depcityid').parents('.data').find('.error-message').text('City required');
            saveData = false;
        }
        if(arrcityid == ''){
            $(val).parents('tr').find('.arrcityid').parents('.data').find('.error-message').text('City required');
            saveData = false;
        }

        if(saveData){
            var datesForValidate = {};
            datesForValidate['depdate'] = 'Date cannot be a past date='+depdate;
            console.log(datesForValidate);
            Visualforce.remoting.Manager.invokeAction(
                '{!$RemoteAction.AirDashboardController.validateDatesForToday}',JSON.stringify(datesForValidate),
                function(result, event){
                    if (event.status) {
                        if(!isEmpty(result)){
                            $(val).parents('tr').find('.depdate').parents('.data').find('.error-message').text('Date cannot be a past date');
                        }else{
                            saveEditItineraryTripJs(id,order,depdate,arrdate,flight,depcityid,arrcityid,deptime,arrtime,durationhrs,durationmins,equiptype,notes);
                        }
                    } else if (event.type === 'exception') {
                        
                    } else {
                        alert('other');
                    }
                }, 
                {escape: true}
            );
        }
    }
    function setInputDepCityBid(){
        if(createAutocompleteDepCity == false){
            createAutocompleteDepCity = true;
            $('.dep-city-search').autocomplete({
                lookup: function (query, done) {
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.AirDashboardController.searchAirport}',query,
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
                    $(this).val(suggestion.value);
                    $(this).parents('.data').find('.depcityid').val(suggestion.data);
                }
            });
        }
    }
    function setInputArrCityBid(){
        if(createAutocompleteArrCity == false){
            createAutocompleteArrCity = true;
            $('.arr-city-search').autocomplete({
                lookup: function (query, done) {
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.AirDashboardController.searchAirport}',query,
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
                    $(this).val(suggestion.value);
                    $(this).parents('.data').find('.arrcityid').val(suggestion.data);
                }
            });
        }
    }
    function cancelItineraryTrip(){
        $('.new-itinerary').hide();
    }
    function newItinerary(){
        $('.new-data').val('');
        $('.new-itinerary').show();
    }
    function showMessageItinerary(){
        $('.message-itinerary').text('Saved Successfully');
        setTimeout(function() { 
            $('.message-itinerary').text('');
        }, 3000);
    }
    function saveItineraryTrip(){
        var charter_type = $('select[id$=itinerary_chartertype]').val();
        var description = $('input[id$=itinerary_description]').val();
        var pax = $('input[id$=itinerary_pax]').val();
        saveItineraryTripJs(charter_type,description,pax);
    }
    function remoteLocationPostLast(event,type,charge,recordId) {
        var input = event.target;
        var reader = new FileReader();
        reader.onload = function(){
            var dataURL = reader.result;
            $('input[id$=outputtrip]').val(dataURL);
        };
        reader.readAsDataURL(input.files[0]);
        setTimeout(function() {
            fileUploadLast(type,charge,recordId);
        }, 2000);
    };
    function fileUploadLast(type,charge,recordId) {
        var fileData;
        switch(type) {
            case 'decision_due_date': fileData = $('input[id$=fileDecisionDueDate]').val(); break;
        }
        $('input[id$=attachment_new_charge]').val(charge);
        var pieces = fileData.split('\');
        var filename = pieces[pieces.length-1];
        //var fileBlob = $('input[id=output]').val();
        //console.log('recordId: ' + recordId);
        passToControllerTrip(filename,recordId);
    }
    function setDataToSelect() {
        var selectid = $('input[id$=attachment_new_charge]').val();
        var attachment_new_id = $('input[id$=attachment_new_id]').val();
        var attachment_new_name = $('input[id$=attachment_new_name]').val();
        $('select[id$='+selectid+']').append('<option value="'+attachment_new_id+'">' + attachment_new_name +'</option>');
    }
    function openAttachDocs(typez,object_id,modal_parent,modal_select) {
        $('input[id$=attachdocument_modal]').val(modal_parent);
        $('input[id$=attachdocument_select_id]').val(modal_select);
        $('#'+modal_parent).css('z-index','1039');
        openAttachDocsJs(object_id);
    }
    function selectAttachDocument() {
        var select_attachs = false;
        var document_ids = [];
        var document_names = [];
        $('input[id$=document-attach-ids]').val('');
        $("#data-attach-documents tr").each(function() {
            if($(this).hasClass("highlighted")) {
                select_attachs = true;
                document_ids.push($(this).attr('vid'));
                document_names.push($(this).attr('vname'));
            }
        });
        if(select_attachs) {
            console.log(document_ids);
            var modalid = $('input[id$=attachdocument_modal]').val();
            var selectid = $('input[id$=attachdocument_select_id]').val();
            $('input[id$=document-attach-ids]').val(document_ids);
            $('input[id$=document-attach-names]').val(document_names);
            for(x=0; x < document_ids.length; x++){
                $('select[id$='+selectid+']').append('<option value="'+document_ids[x]+'">' + document_names[x] +'</option>');
            }
            
            viewModalIndex(modalid);
            closeModal('myModalAttachDocumentsTrip');
        }else{
            alert('Please select a Document.');
        }
    }
    function selectDocumentProdRow(val) {
        var selected = $(val).hasClass("highlighted");
        if(!selected)
            $(val).addClass("highlighted");
        else
            $(val).removeClass("highlighted");
    }
    function sendEmailDecisionDueDate(){
        var emailTo = $('.decisionduedate-to').text();
        if(emailTo != ''){
            var emailCC = '';
            $(".all-cc-email-decisionduedate span.email-ids").each(function() {
                emailCC = emailCC + $(this).html().replace(' <span class="cancel-email">x</span>','') + ',';
            });
            var emailBCC = '';
            $(".all-bcc-email-decisionduedate span.email-ids").each(function() {
                emailBCC = emailBCC + $(this).html().replace(' <span class="cancel-email">x</span>','') + ',';
            });
            var subject = $('input[id$=decisionduedate_subject]').val();
            var salutation = $('input[id$=decisionduedate_salutation]').val();
            var emailBody;
            for ( instance in CKEDITOR.instances ) {
                if(instance.includes('decisionduedate_body')) emailBody = CKEDITOR.instances[instance].getData();
            }
            var closing = $('textarea[id$=decisionduedate_closing]').val().replace(/(
|
|)/gm,'<br/>');
            var attachs = '';
            $("select[id$=decisionduedate_attachs] option").each(function() {
                attachs = attachs + $(this).val() + ',';
            });
            sendEmailDecisionDueDateJs(emailTo,emailCC,emailBCC,subject,salutation,emailBody,closing,attachs);
        }else{
            alert('Selected contact doesn\'t have Email address.');
        }
    }
    function deactivateDecisionDueDate(){
        var confirmAction = confirm('Are you sure you want to deactivate this document?');
        if(confirmAction) deactivateDecisionDueDateJs();
    }
    function saveDecisionDueDate(){
        var emailBody = '';
        for ( instance in CKEDITOR.instances ) {
            if(instance.includes('decisionduedate_body')) emailBody = CKEDITOR.instances[instance].getData();
        }
        saveDecisionDueDateJs(emailBody);
    }
    function checkInputsDecisionDueDate(){
        $('input,select').keypress(function(event) { return event.keyCode != 13; });
        $(".cc-email-decisionduedate").keydown(function (e) {
            $(this).removeClass('error-custom');
            if (e.keyCode == 13 || e.keyCode == 32) {
                var getValue = $(this).val();
                if(validateEmail(getValue)){
                    $('.all-cc-email-decisionduedate').append('<span class="email-ids">'+ getValue +' <span class="cancel-email">x</span></span>');
                    $(this).val('');
                }else{
                    $(this).addClass('error-custom');
                }
            }
        });
        
        $(".bcc-email-decisionduedate").keydown(function (e) {
            $(this).removeClass('error-custom');
            if (e.keyCode == 13 || e.keyCode == 32) {
                var getValue = $(this).val();
                if(validateEmail(getValue)){
                    $('.all-bcc-email-decisionduedate').append('<span class="email-ids">'+ getValue +' <span class="cancel-email">x</span></span>');
                    $(this).val('');
                }else{
                    $(this).addClass('error-custom');
                }
            }
        });
    }
    
    function changeAttention(val){
        var attention = $(val).val();
        changeAttentionJs(attention);
    }
    function openPreviewReleaseBid(val,bidid,accountid,name,type_z){
        $('select[id$=emailbid_attachs]').empty();
        $('#myModalReleaseBid').css('z-index','1039');
        $('#myModalReleaseBidData').css('z-index','1039');
        $('#myModalSendBidRequest').css('z-index','1039');
        if(type_z == 'release_bid'){
            $('#myModalPreviewPdf').find('.modal-title').text('Bid Release Note to '+ name);
        }else{
            $('#myModalPreviewPdf').find('.modal-title').text('Bid Request to '+ name);
        }
        
        $('#myModalPreviewPdf').find('.modal-body .email-attachs').hide();
        $('#myModalPreviewPdf').find('.modal-footer .btn-send').text('Send Email');
        var primary_contact = $(val).parents('.group-vendor').find('.primary-contact').val();
        $('input[id$=emailbid_primarycontactname]').val($(val).parents('.group-vendor').find('.primary-contact').children("option:selected").text());
        $('input[id$=emailbid_primaryaccountname]').val(name);
        $('input[id$=emailbid_type]').val(type_z);
        var productionid = $('input[id$=production]').val();
        var tripid = $('input[id$=tripid]').val();
        $('input[id$=emailbid_bid]').val(bidid);
        $('input[id$=emailbid_subject]').val('');
        Visualforce.remoting.Manager.invokeAction(
            '{!$RemoteAction.AirDashboardController.getDataEmailBid}',productionid,tripid,bidid,primary_contact,type_z,'http://' + window.location.host,
            function(result, event){
                console.log(result);
                console.log(event);
                if (event.status) {
                    $('#myModalPreviewPdf .modal-body').find('.emailbid_to').html(result[0]);
                    $('#myModalPreviewPdf .modal-body').find('input[id$=emailbid_subject]').val(decodeData(result[1]));
                    for ( instance in CKEDITOR.instances ){
                        if(instance.includes('emailBidBody')) CKEDITOR.instances[instance].setData(decodeData(result[2]).replace(/(&lt\;)/g,"<").replace(/(&gt\;)/g,">"));
                    }
                    $('input[id$=cc-email-bid]').val('');
                    $('.all-cc-email-bid').html('');
                    $(val).parents('.group-vendor').find('.check-contact').each(function(){
                        if($(this).is(":checked") && $(this).parents('td').attr('contactid-data') != primary_contact){
                            $('.all-cc-email-bid').append('<span class="email-ids">'+ $(this).parents('td').attr('email-data') + ' <span class="cancel-email">x</span></span>');
                        }
                    });
                    $('input[id$=bcc-email-bid]').val('');
                    $('.all-bcc-email-bid').html('');
                    openModal('myModalPreviewPdf');
                } else if (event.type === 'exception') {
                    
                } else {
                    alert('other');
                }
            }, 
            {escape: true}
        );
    }
    function sendPreviewPdf() {
        var typez = $('input[id$=emailbid_type]').val();
        var emailTo = $('.emailbid_to').html();
        var emailCC = '';
        $(".all-cc-email-bid span.email-ids").each(function() {
            emailCC = emailCC + $(this).html().replace(' <span class="cancel-email">x</span>','') + ',';
        });
        var emailBCC = '';
        $(".all-bcc-email-bid span.email-ids").each(function() {
            emailBCC = emailBCC + $(this).html().replace(' <span class="cancel-email">x</span>','') + ',';
        });
        var subject = $('input[id$=emailbid_subject]').val();
        var emailBody;
        for ( instance in CKEDITOR.instances ) {
            if(instance.includes('emailBidBody')) emailBody = CKEDITOR.instances[instance].getData();
        }
        var attachs = '';
        $("select[id$=emailbid_attachs] option").each(function() {
            attachs = attachs + $(this).val() + ',';
        });
        if(emailTo == '') {
            alert('Enter the recipient email.');
        }else{
            var bid_id = $('input[id$=emailbid_bid]').val();
            var primary_contact_name = $('input[id$=emailbid_primarycontactname]').val();
            sendPreviewPdfJs(emailTo,emailCC,emailBCC,subject,emailBody,primary_contact_name,bid_id,typez,attachs);
        }
    }
    function showMessagePreviewPdf() {
        var account_name = $('input[id$=emailbid_primaryaccountname]').val();
        if($('input[id$=emailbid_type]').val() == 'datechange') {
            alert('Date Change Email has been sent.');
        }else if($('input[id$=emailbid_type]').val() == 'sendoptions') {
            alert('Housing Option Sheet has been sent.');
        }else if($('input[id$=emailbid_type]').val() == 'release_bid') {
            alert('Bid Release Note has been sent to ' + account_name);
        }else{
            alert('Bid Request has been sent to ' + account_name);
        }
    }
    function setInputTripVendor(){
        if(createAutocompleteTripVendor == false){
            createAutocompleteTripVendor = true;
            $('.gttrip-vendor').autocomplete({
                lookup: function (query, done) {
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.AirDashboardController.searchAccount}',query,'Airline Vendor',
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
    function setInputTripCity(){
        if(createAutocompleteTripCity == false){
            createAutocompleteTripCity = true;
            $('.gttrip-city').autocomplete({
                lookup: function (query, done) {
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.AirDashboardController.searchAirport}',query,
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
    function saveStatusTrip(val){
        var status = $(val).val();
        var confirmAction = confirm('Are you sure you want to change the status?');
        if(confirmAction){
            $('select[id$=tripview_status]').data('pre',$('select[id$=tripview_status]').val());
            saveStatusTripJs(status);
        }else{
            var data_pre = $('select[id$=tripview_status]').data('pre');
            $('select[id$=tripview_status]').val(data_pre);
        }
    }
    function saveBackEndCoordinator(val){
        var backend = $(val).val();
        var confirmAction = confirm('Are you sure you want to change the assigned back-end coordinator?');
        if(confirmAction){
            $('select[id$=trip_backendcoordinator]').data('pre',$('select[id$=trip_backendcoordinator]').val());
            saveBackEndCoordinatorJs(backend);
        }else{
            var data_pre = $('select[id$=trip_backendcoordinator]').data('pre');
            $('select[id$=trip_backendcoordinator]').val(data_pre);
        }
    }
    function changeClientTrip(val){
        var primary_contact = $(val).val();
        var confirmAction = confirm('Are you sure you want to change the client?');
        if(confirmAction){
            $('select[id$=trip_primarycontact]').data('pre',$('select[id$=trip_primarycontact]').val());
            changeClientTripJs(primary_contact);
        }else{
            var data_pre = $('select[id$=trip_primarycontact]').data('pre');
            $('select[id$=trip_primarycontact]').val(data_pre);
        }
    }
    function createMultipleBids(){
        var trip_selecteds = false;
        var trips = [];
        $("#dataTrips tr").each(function() {
            if($(this).hasClass("highlighted")) {
                trip_selecteds = true;
                trips.push($(this).attr('vid'));
            }
        });
        if(trip_selecteds) {
            console.log(trips);
            $('input[id$=searchvendor_trips_selected]').val(trips.toString());
            openSearchVendor('multiple');
        }else{
            alert('Please select trip(s).');
        }
    }
    $("#dataTrips tr").removeClass("highlighted");
    function selectRowTrip(val){
        var selected = $(val).hasClass("highlighted");
        if(!selected)
            $(val).addClass("highlighted");
        else
            $(val).removeClass("highlighted");
    }
    function setInputSV5(){
        if(createAutocompleteSV5 == false){
            createAutocompleteSV5 = true;
            $('.searchvendorpanel-venue').autocomplete({
                lookup: function (query, done) {
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.AirDashboardController.searchVenue}',query,
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
    function setInputSV4(){
        if(createAutocompleteSV4 == false){
            createAutocompleteSV4 = true;
            $('.searchvendor-venue').autocomplete({
                lookup: function (query, done) {
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.AirDashboardController.searchVenue}',query,
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
    function saveOtherInformation(inputName) {
        var trace_date = $('input[id$=tripview_tracedate]').val();
        var decision_due_date = $('input[id$=tripview_decisionduedate]').val();
        var deadline_date = $('input[id$=tripview_deadlinedate]').val();
        var saveData;
        var date_today = new Date($('input[id$=date_today]').val());
        var date_actual;
        
        $('input[id$=tripview_tracedate]').parents('.row').find('.error-message').text('');
        $('input[id$=tripview_decisionduedate]').parents('.row').find('.error-message').text('');
        $('input[id$=tripview_deadlinedate]').parents('.row').find('.error-message').text('');
        
        if(inputName == 'tripview_tracedate' && trace_date != null && trace_date != ''){
            saveData = true;
            date_actual = trace_date;
        }
        if(inputName == 'tripview_decisionduedate' && decision_due_date != null && decision_due_date != ''){
            saveData = true;
            date_actual = decision_due_date;
        }
        if(inputName == 'tripview_deadlinedate' && deadline_date != null && deadline_date != ''){
            saveData = true;
            date_actual = deadline_date;
        }
        
        if(saveData){
            var datesForValidate = {};
            if(inputName == 'tripview_tracedate' && trace_date != null && trace_date != '') datesForValidate['tripview_tracedate'] = 'Cannot post-date a trace='+date_actual;
			if(inputName == 'tripview_decisionduedate' && decision_due_date != null && decision_due_date != '') datesForValidate['tripview_decisionduedate'] = 'Cannot post-date a trace='+date_actual;
            if(inputName == 'tripview_deadlinedate' && deadline_date != null && deadline_date != '') datesForValidate['tripview_deadlinedate'] = 'Cannot post-date a trace='+date_actual;
            Visualforce.remoting.Manager.invokeAction(
                '{!$RemoteAction.AirDashboardController.validateDatesForToday}',JSON.stringify(datesForValidate),
                function(result, event){
                    if (event.status) {
                        if(!isEmpty(result)){
                            alert('Cannot post-date a trace.');
                            if(inputName == 'tripview_tracedate' && trace_date != null && trace_date != '') $('input[id$=tripview_tracedate]').val('');
                            if(inputName == 'tripview_decisionduedate' && decision_due_date != null && decision_due_date != '') $('input[id$=tripview_decisionduedate]').val('');
                            if(inputName == 'tripview_deadlinedate' && deadline_date != null && deadline_date != '') $('input[id$=tripview_deadlinedate]').val('');
                        }else{
                            saveOtherInformationJs(inputName,date_actual);
                        }
                    } else if (event.type === 'exception') {
                        
                    } else {
                        alert('other');
                    }
                }, 
                {escape: true}
            );
        }
    }
    function setInputSV3(){
        if(createAutocompleteSV3 == false){
            createAutocompleteSV3 = true;
            $('.searchvendor-airport').autocomplete({
                lookup: function (query, done) {
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.AirDashboardController.searchAirport}',query,
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
    function setInputSV2(){
        if(createAutocompleteSV2 == false){
            createAutocompleteSV2 = true;
            $('.searchvendorpanel-city').autocomplete({
                lookup: function (query, done) {
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.AirDashboardController.searchCity}',query,
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
    function setInputSV1(){
        if(createAutocompleteSV1 == false){
            createAutocompleteSV1 = true;
            $('.searchvendor-city').autocomplete({
                lookup: function (query, done) {
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.AirDashboardController.searchCity}',query,
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
    
    function setInputSV6(){
        if(createAutocompleteSV6 == false){
            createAutocompleteSV6 = true;
            $('.searchvendor-vendor').autocomplete({
                lookup: function (query, done) {
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.AirDashboardController.searchAccount}',query,'Ground Travel Vendor',
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
    
    function setInputAircraftTrip(){
        if(createAutocompleteAircraftTrip == false){
            createAutocompleteAircraftTrip = true;
            $('.aircraft-search').autocomplete({
                lookup: function (query, done) {
                    tripid = $('input[id$=tripid]').val();
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.AirDashboardController.searchAccount}',query,'Airline Vendor',
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
                    $(this).parents('td').find('.airlineid').val(suggestion.data);
                }
            });
        }
    }
    function saveEditTravel(val) {
        var id = $(val).parents('tr').find('.id').val();
        var line = $(val).parents('tr').find('.line').val();
        var vehicle = $(val).parents('tr').find('.vehicle').val();
        var start_date = $(val).parents('tr').find('.startdate').val();
        var end_date = $(val).parents('tr').find('.enddate').val();
        var travel_type = $(val).parents('tr').find('.traveltype').val();
        var group_type = $(val).parents('tr').find('.grouptype').val();
        var location_type = $(val).parents('tr').find('.locationtype').val();
        var location_pickup = $(val).parents('tr').find('.locationpickup').val();
        var location_dropoff = $(val).parents('tr').find('.locationdropoff').val();
        var location_details = $(val).parents('tr').find('.locationdetails').val();
        var airline_notes = $(val).parents('tr').find('.notes').val();
        
        var start_date_trip = new Date($('input[id$=tripview_startdate]').val());
        var end_date_trip = new Date($('input[id$=tripview_enddate]').val());
        var date1 = start_date != '' ? new Date(start_date.split(' ')[0]) : null;
        var date2 = end_date != '' ? new Date(end_date.split(' ')[0]) : null;
        var validateDates = true;
        
        if(date1 < start_date_trip || date1 > end_date_trip || date2 < start_date_trip || date2 > end_date_trip) validateDates = false;

        if(validateDates){
            saveEditTravelJs(id,'',line,vehicle,start_date,end_date,travel_type,group_type,location_type,location_pickup,location_dropoff,location_details,airline_notes,false);
        }else{
            var confirmAction = confirm('You have created a trip outside the master trip date, would you like us to update the master trip date. Click accept to confirm, click cancel to cancel the update.');
            if(confirmAction) saveEditTravelJs(id,'',line,vehicle,start_date,end_date,travel_type,group_type,location_type,location_pickup,location_dropoff,location_details,airline_notes,true);
        }
    }
    function deleteTravel(val){
        deleteTravelJs(val)
    }
    function saveTravelComplete(val){
        var subtripid = $(val).parents('.card-body-trip').find('.subtripid').val();
        var trip_order = $(val).parents('.card-body-trip').find('.triporder').val();
        var line = $(val).parents('.card-body-trip').find('.new-travel .line').val();
        var vehicle = $(val).parents('.card-body-trip').find('.new-travel .vehicle').val();
        var start_date = $(val).parents('.card-body-trip').find('.new-travel .startdate').val();
        var end_date = $(val).parents('.card-body-trip').find('.new-travel .enddate').val();
        var travel_type = $(val).parents('.card-body-trip').find('.new-travel .traveltype').val();
        var group_type = $(val).parents('.card-body-trip').find('.new-travel .grouptype').val();
        var location_type = $(val).parents('.card-body-trip').find('.new-travel .locationtype').val();
        var location_pickup = $(val).parents('.card-body-trip').find('.new-travel .locationpickup').val();
        var location_dropoff = $(val).parents('.card-body-trip').find('.new-travel .locationdropoff').val();
        var location_details = $(val).parents('.card-body-trip').find('.new-travel .locationdetails').val();
        var airline_notes = $(val).parents('.card-body-trip').find('.new-travel .notes').val();
        saveTravelCompleteJs(trip_order,'',subtripid,line,vehicle,start_date,end_date,travel_type,group_type,location_type,location_pickup,location_dropoff,location_details,airline_notes,true);
    }
    function saveTravelAddMore(val){
        var subtripid = $(val).parents('.card-body-trip').find('.subtripid').val();
        var trip_order = $(val).parents('.card-body-trip').find('.triporder').val();
        var line = $(val).parents('.card-body-trip').find('.new-travel .line').val();
        var vehicle = $(val).parents('.card-body-trip').find('.new-travel .vehicle').val();
        var start_date = $(val).parents('.card-body-trip').find('.new-travel .startdate').val();
        var end_date = $(val).parents('.card-body-trip').find('.new-travel .enddate').val();
        var travel_type = $(val).parents('.card-body-trip').find('.new-travel .traveltype').val();
        var group_type = $(val).parents('.card-body-trip').find('.new-travel .grouptype').val();
        var location_type = $(val).parents('.card-body-trip').find('.new-travel .locationtype').val();
        var location_pickup = $(val).parents('.card-body-trip').find('.new-travel .locationpickup').val();
        var location_dropoff = $(val).parents('.card-body-trip').find('.new-travel .locationdropoff').val();
        var location_details = $(val).parents('.card-body-trip').find('.new-travel .locationdetails').val();
        var airline_notes = $(val).parents('.card-body-trip').find('.new-travel .notes').val();
        
        var start_date_trip = new Date($('input[id$=tripview_startdate]').val());
        var end_date_trip = new Date($('input[id$=tripview_enddate]').val());
        var date1 = start_date != '' ? new Date(start_date.split(' ')[0]) : null;
        var date2 = end_date != '' ? new Date(end_date.split(' ')[0]) : null;
        var validateDates = true;
        if(date1 < start_date_trip || date1 > end_date_trip || date2 < start_date_trip || date2 > end_date_trip) validateDates = false;
        
        if(validateDates){
            saveTravelAddMoreJs(trip_order,'',subtripid,line,vehicle,start_date,end_date,travel_type,group_type,location_type,location_pickup,location_dropoff,location_details,airline_notes,false);
        }else{
            var confirmAction = confirm('You have created a trip outside the master trip date, would you like us to update the master trip date. Click accept to confirm, click cancel to cancel the update.');
            if(confirmAction) saveTravelAddMoreJs(trip_order,'',subtripid,line,vehicle,start_date,end_date,travel_type,group_type,location_type,location_pickup,location_dropoff,location_details,airline_notes,true);
        }
    }
    function cancelTravel(val){
        $(val).parents('.card-body-trip').find('.new-travel').hide();
    }
    function addTravelLine(val){
        var start_date = $('input[id$=tripview_startdate]').val();
        $(val).parents('.card-body-trip').find('.new-travel .new-data').val('');
        $(val).parents('.card-body-trip').find('.new-travel .startdate').val(start_date + ' 12:00 PM');
        $(val).parents('.card-body-trip').find('.new-travel .enddate').val(start_date + ' 12:00 PM');
        $(val).parents('.card-body-trip').find('.new-travel').show();
    }
    function addTravelLineByCClass(val){
        var start_date = $('input[id$=tripview_startdate]').val();
        $(val).find('.new-travel .new-data').val('');
        $(val).find('.new-travel .startdate').val(start_date + ' 12:00 PM');
        $(val).find('.new-travel .enddate').val(start_date + ' 12:00 PM');
        $(val).find('.new-travel').show();
    }
    function showFreight(val){
        if($(val).prop('checked')){
            $(val).parents('.card-body-trip').find('.freight-for-trip').show();
        }else{
            $(val).parents('.card-body-trip').find('.freight-for-trip').hide();
        }
    }
    function saveSubTrip(val){
        saveSubTripJs(val);
    }
    function deleteSubTrip(val){
        deleteSubTripJs(val);
    }
    function newSubTrip(){
        $('.btn-add-trip-details').html('<i class="fa fa-plus"></i> Add Additional Trip');
        newSubTripJs();
    }
    function saveEditAircraftTrip(val){
        var id = $(val).parents('tr').attr('data-id');
        var aircraft_type = $(val).parents('tr').find('.aircrafttype').val();
        var economy_seats = $(val).parents('tr').find('.economyseats').val();
        var cargo_capacity = $(val).parents('tr').find('.cargocapacity').val();
        var seat_pitch = $(val).parents('tr').find('.seatpitch').val();
        var airlineid = $(val).parents('tr').find('.airlineid').val();
        var positioning_from_time = $(val).parents('tr').find('.positioningfromtime').val();
        var trip_contents = $(val).parents('tr').find('.tripcontents').val();
        saveEditAircraftTripJs(id,aircraft_type,economy_seats,cargo_capacity,seat_pitch,airlineid,positioning_from_time,trip_contents);
    }
    function saveAircraftTrip(val){
        $('.new-aircraft-trip').hide();
        var airlineid = $(val).parents('tr').find('.airlineid').val();
        saveAircraftTripJs(airlineid);
    }
    function cancelAircraftTrip() {
        $('.newdata').val('');
        $('.new-aircraft-trip').hide();
    }
    function newAircraftTrip(){
        $('.newdata').val('');
        newAircraftTripJs();
    }
    function saveEditConcessionTrip(val) {
        var id = $(val).parents('tr').find('.id').val();
        var createinbid = $(val).parents('tr').find('.createinbid').prop('checked');
        //var concessionRequested = $(val).parents('tr').find('.concessionrequested').val();
        var concessionRequested = $(val).parents('tr').find('.requested.inputpicker-input').val();
        //var notes = $(val).parents('tr').find('.notes').val();
        //saveEditConcessionTripJs(id,concessionRequested,notes);
        saveEditConcessionTripJs(id,concessionRequested,createinbid);
    }
    function editConcessionTrip(val){
        var data_original = $(val).parents('tr').find('.data-original-requested').val();
        $(val).parents('tr').find('.requested.inputpicker-input').val(data_original);
        $(val).hide();
        $(val).parents('tr').find('.btn-delete').hide();
        $(val).parents('tr').find('.btn-copy').hide();
        $(val).parents('tr').find('.btn-cancel').show();
        $(val).parents('tr').find('.btn-save').show();
        $(val).parents('tr').find('.show-data').hide();
        $(val).parents('tr').find('.data').show();
    }
    function deleteConcession(val) {
        var confirmAction = confirm('Are you sure you want to delete this item?');
        if(confirmAction) deleteConcessionJs(val);
    }
    function saveConcessionTrip() {
        $('.new-concession-trip').hide();
        var createinbid = $('.newdata-createinbid').prop('checked');
        var requested = $('.newdata-requested.inputpicker-input').val();
        saveConcessionTripJs(createinbid,requested);
    }
    function cancelConcessionTrip() {
        $('.newdata').val('');
        $('.new-concession-trip').hide();
    }
    function completeNewConcessionTrip() {
        $('.newdata').val('');
        $('.newdata-createinbid').prop('checked',true);
        $('.new-concession-trip').show();
    }
    function newConcessionTrip() {
        newConcessionTripJs();
    }
    function sendEditReleaseBid() {
        var bids = [];
        var enter = false;
        $("#myModalReleaseBid .select-vendor").each(function() {
            if($(this).prop('checked')) {
                enter = true;
                bids.push($(this).parents('.col-data').attr('data-id'));
            }
        });
        if(enter) {
            var subject = $('#myModalEditReleaseBid').find('input[id$=emaileditreleasebid_subject]').val();
            var body = '';
            for ( instance in CKEDITOR.instances ) {
                if(instance.includes('emaileditreleasebid_body')) body = CKEDITOR.instances[instance].getData();
            }
            sendEditReleaseBidJs(bids.toString(),subject,body);
        }else{
            alert('Please select Vendor');
        }
    }
    function saveAndCloseReleaseBid() {
        var subject = $('#myModalEditReleaseBid').find('input[id$=emaileditreleasebid_subject]').val();
        var body = '';
        for ( instance in CKEDITOR.instances ) {
            if(instance.includes('emaileditreleasebid_body')) body = CKEDITOR.instances[instance].getData();
        }
        saveAndCloseReleaseBidJs(subject,body);
    }
    function openEditReleaseBid(){
        $('#myModalReleaseBid').css('z-index','1039');
        var productionid = $('input[id$=production]').val();
        var tripid = $('input[id$=tripid]').val();
        console.log('productionid: ' + productionid);
        Visualforce.remoting.Manager.invokeAction(
            '{!$RemoteAction.AirDashboardController.getDataEmailBid}',productionid,tripid,'','','release_bid2','http://' + window.location.host,
            function(result, event){
                if (event.status) {
                    $('#myModalEditReleaseBid .modal-body').find('input[id$=emaileditreleasebid_subject]').val(result[1]);
                    for ( instance in CKEDITOR.instances ){
                        if(instance.includes('emaileditreleasebid_body')) CKEDITOR.instances[instance].setData(result[2].replace(/(&lt\;)/g,"<").replace(/(&gt\;)/g,">"));
                    }
                    openModal('myModalEditReleaseBid');
                } else if (event.type === 'exception') {
                    
                } else {
                    alert('other');
                }
            }, 
            {escape: true}
        );
    }
    function sendReleaseBid() {
        var bids = [];
        var enter = false;
        $("#myModalReleaseBid .select-vendor").each(function() {
            if($(this).prop('checked')) {
                enter = true;
                bids.push($(this).parents('.col-data').attr('data-id'));
            }
        });
        if(enter) {
            sendReleaseBidJs(bids.toString(),'release_bid');
        }else{
            alert('Please select Vendor');
        }
    }
    function sendBidRequestEdit(){
        var bids = [];
        var enter = false;
        $("#myModalSendBidRequest .select-vendor").each(function() {
            if($(this).prop('checked')) {
                enter = true;
                bids.push($(this).parents('.col-data').attr('data-id'));
            }
        });
        if(enter) {
            var emailBody;
            for ( instance in CKEDITOR.instances ) {
                if(instance.includes('emailEditBidBody')) emailBody = CKEDITOR.instances[instance].getData();
            }
            sendBidRequestEditJs(bids.toString(),'send_bid_request',emailBody);
        }else{
            alert('Please select Vendor');
        }
    }
    function sendBidRequest(){
        var bids = [];
        var enter = false;
        $("#myModalSendBidRequest .select-vendor").each(function() {
            if($(this).prop('checked')) {
                enter = true;
                bids.push($(this).parents('.col-data').attr('data-id'));
            }
        });
        if(enter) {
            sendBidRequestJs(bids.toString(),'send_bid_request');
        }else{
            alert('Please select Vendor');
        }
    }
    function changeContactReleaseBid(val,accountid) {
        changeContactReleaseBidJs($(val).val(),accountid);
    }
    function openReleaseBid() {
        if(reviewCoordinator()) {
            openReleaseBidJs();
        }else{
            alert('Air Coordinator is not for this this tour please add');
        }
    }
    function changeContactVendorBid(val,accountid) {
        changeContactVendorBidJs($(val).val(),accountid);
    }
    function reviewButtonsOnBidRequest(){
        if($('#myModalSendBidRequest input[id$=sendbidrequest_allvendors]').prop('checked')){
            $("#myModalSendBidRequest .sendbidrequest-status").each(function() {
                if($(this).val() == 'Unsent') $(this).parents('.fieldset').find('.select-vendor').prop('checked',true);
            });
        }
    }
    function reviewButtonsBidRequest() {
        var recordtype = $('input[id$=housing_recordtype]').val();
        $('#myModalSendBidRequest').find('.btn-send-pdf').text('Send Email');
        $('#myModalSendBidRequest').find('.btn-edit-all-pdf').text('Edit All Emails');
        $('#myModalSendBidRequest').find('.btn-send-link').removeAttr('disabled');
        $('#myModalSendBidRequest').find('.btn-edit-all-link').removeAttr('disabled');
        $('#myModalSendBidRequest').find('.btn-send-link').show();
        $('#myModalSendBidRequest').find('.btn-edit-all-link').show();
        $('#myModalSendBidRequest').find('.btn-preview-pdf').show();
        $('#myModalSendBidRequest').find('.btn-preview-link').show();
        $('#myModalSendBidRequest').find('.btn-preview-pdf').text('Preview');
        var first_time = $('input[id$=trip_sendbidfirsttime]').val();
        if(first_time == 'true') {
            $('#myModalSendBidRequest input[id$=sendbidrequest_allvendors]').prop('checked',true);
            $('#myModalSendBidRequest').find('.select-vendor').prop('checked',true);
        }else{
            $('#myModalSendBidRequest input[id$=sendbidrequest_allvendors]').prop('checked',false);
            $('#myModalSendBidRequest').find('.select-vendor').prop('checked',false);
            $("#myModalSendBidRequest .sendbidrequest-status").each(function() {
                if($(this).val() == 'Unsent') $(this).parents('.fieldset').find('.select-vendor').prop('checked',true);
            });
        }
        openModal('myModalSendBidRequest');
    }
    function openSendBidRequest(){
        //$("#dataProductionDocuments tr").removeClass("highlighted");
        if(reviewCoordinator()) {
            openSendBidRequestJs();
        }else{
            alert('Air Coordinator is not for this this tour please add');
        }
    }
    function createBidRequest() {
        var createBids = false;
        var vendors = [];
        $("#dataVendors tr").each(function() {
            if($(this).hasClass("highlighted")) {
                createBids = true;
                vendors.push($(this).attr('vid'));
            }
        });
        if(createBids) {
            $('input[id$=totalbidscreate]').val(vendors.length);
            var trips_selected = $('input[id$=searchvendor_trips_selected]').val();
            createBidRequestJs(vendors.toString(),trips_selected);
        }else{
            alert('Please select a Vendor.');
        }
    }
    function openFilterSearchVendor(){
        if($('.filters-search-vendor').hasClass('show-panel')){
            $('.filters-search-vendor').removeClass('show-panel');
            $('.filters-search-vendor').hide();
        }else{
            $('.filters-search-vendor').addClass('show-panel');
            $('.filters-search-vendor').show();
        }
    }
    
    function sortVendor(sortOrder,sortOrientation) {
        var actual = $('input[id$=orderFieldVendorActual]').val();
        var change = false;
        if(actual != sortOrder) change = true;
        searchVendorSortJs(sortOrder,sortOrientation,true,change);
    }
    function searchVendor(){
        var search_vendor_word = $('input[id$=searchvendor_airline]').val();
        var typez = $('input[id$=searchvendor_type').val();
        var status = $('select[id$=searchvendor_status').val();
        searchVendorJs(typez,search_vendor_word,status,'Name','ASC');
    }
    function openSearchVendor(typez) {
        $('input[id$=searchvendor_type]').val(typez);
        if(typez != 'multiple'){
            $('input[id$=searchvendor_trips_selected]').val($('input[id$=tripid]').val());
        }
        searchVendorJs(typez,'','All','Name','ASC');
    }
    
    function viewVendorDetail(event,val) {
        event.stopPropagation();
        viewVendorDetailJs(val);
    }
    
    function changeTabVendor() {
        $('#nav-vendortab').find('#nav-vendor-search-tab').removeClass('active');
        $('#nav-vendortab').find('#nav-vendor-search-tab').removeClass('show');
        $('#nav-vendortabContent').find('#nav-vendor-search').removeClass('active');
        $('#nav-vendortabContent').find('#nav-vendor-search').removeClass('show');
        
        $('#nav-vendortab').find('#nav-vendor-detail-tab').addClass('active');
        $('#nav-vendortab').find('#nav-vendor-detail-tab').addClass('show');
        $('#nav-vendortabContent').find('#nav-vendor-detail').addClass('active');
        $('#nav-vendortabContent').find('#nav-vendor-detail').addClass('show');
        $('#myModalSearchVendor').find('.modal-body').addClass('overflow');
    }
    
    function clearSearchVendor(){
    }
    
    function saveEditBid(val,orderField,orientation) {        
        var enterSave = true;    
        var message = '';
        var arrData = [];
        var numberMajor = 0;
        var numberAux;
        $("span[id$=bidsByTripPanel] tr").each(function() {
            if($(this).find('span.bid-option-span').text() != "n/a"){
                arrData.push($(this).find('span.bid-option-span').text());
                numberAux = parseInt($(this).find('span.bid-option-span').text()) || 0;
                if(numberMajor < numberAux) numberMajor = numberAux;
            }
        });
        
        if($(val).parents('tr').find('.bid-options').val() != ''
           && (($(val).parents('tr').find('span.bid-option-span').text() == "n/a" && $('input[id$=tripview_option]').val() != $(val).parents('tr').find('.bid-options').val() && !arrData.includes($(val).parents('tr').find('.bid-options').val())
               && parseInt($(val).parents('tr').find('.bid-options').val()) > numberMajor) ||    
               ($(val).parents('tr').find('span.bid-option-span').text() != "n/a" && !arrData.includes($(val).parents('tr').find('.bid-options').val()))
              )){
            enterSave = false;
            message = 'Order number should be unique and in sequence. Please enter a different order number.';
        }
        
        /*var enterSaveDuplicate = true;
        $("span[id$=bidsByTripPanel] tr").each(function() {
            if($(this).find('span.bid-option-span').text() != "n/a" && $(this).find('.id').val() != $(val).parents('tr').find('.id').val() && $(val).parents('tr').find('.bid-options').val() != ''){
                if($(val).parents('tr').find('.bid-options').val() == $(this).find('span.bid-option-span').text()){
                    enterSaveDuplicate = false;
                }
            }
        });
        
        if(!enterSaveDuplicate){
            if($(val).parents('tr').find('span.bid-option-span').text() == "n/a"){
                message = 'You have already used the same option number on another record.';
                enterSave = false;
            }
        }*/
        //enterSave = true;
        if(enterSave){
            var id = $(val).parents('tr').find('.id').val();
            var notes = $(val).parents('tr').find('.bid-notes').val();
            var option = $(val).parents('tr').find('.bid-options').val();
            saveEditBidJs(id,notes,option,orderField,orientation);
        }else{
            alert(message);
        }
    }
    function verifyButtonsListBid(){
        var prevbid = $('input[id$=bidlist_prevshowbid]').val();
        var nextbid = $('input[id$=bidlist_nextshowbid]').val();
        if(prevbid == 'true'){
            $('.btn-prev-first-bids').attr('disabled',true);
            $('.btn-prev-bids').attr('disabled',true);
        }else{
            $('.btn-prev-first-bids').removeAttr('disabled');
            $('.btn-prev-bids').removeAttr('disabled');
        }
        if(nextbid == 'true'){
            $('.btn-last-next-bids').attr('disabled',true);
            $('.btn-next-bids').attr('disabled',true);
        }else{
            $('.btn-last-next-bids').removeAttr('disabled');
            $('.btn-next-bids').removeAttr('disabled');
        }
        $('select[id$=searchvendorpanel_amenities]').selectpicker();
        $('select[id$=searchvendorpanel_servicetype]').selectpicker();
        
        var locked_status;
        $("#trip-bid-list .bid-locked-status").each(function() {
            locked_status = $(this).val();
            if(locked_status == 'true') 
                $(this).parents('td').find('.btn-edit').attr('disabled',true);
            else
                $(this).parents('td').find('.btn-edit').attr('disabled',false);
        });
        $('select[id$=trip_backendcoordinator]').data('pre',$('select[id$=trip_backendcoordinator]').val());
        $('select[id$=tripview_status]').data('pre',$('select[id$=tripview_status]').val());
        $('select[id$=trip_primarycontact]').data('pre',$('select[id$=trip_primarycontact]').val());
    }
    function sortBids(sortOrder,sortOrientation) {
        var actual = $('input[id$=orderFieldBidsActual]').val();
        var change = false;
        if(actual != sortOrder) change = true;
        getBidsByTripSortJs(sortOrder,sortOrientation,true,change);
    }
    function FirstPageBids(){
        FirstPageBidsJs();
    }
    function previousBids(){
        previousBidsJs();
    }
    function LastPageBids(){
        LastPageBidsJs();
    }
    function nextBids(){
        nextBidsJs();
    }
    function loadTabContentGround(tabName) {
        var tabGroundDefault = $('input[id$=tabGroundDefault]').val();
        if(tabGroundDefault != tabName) loadTabContentGroundJs(tabName);
    }
    function checkIcon(val,collapse){
        if($(val).find('i').hasClass('btn-show')){
            $(val).find('i').addClass('btn-hide');
            $(val).find('i').removeClass('btn-show');
            $(val).html('<i class="fa fa-angle-down btn-hide"></i>');
        }else{
            $(val).find('i').addClass('btn-show');
            $(val).find('i').removeClass('btn-hide');
            $(val).html('<i class="fa fa-angle-up btn-show"></i>');
        }
        $('#'+collapse).toggle('slow');
    }
    function createJournal() {
        var newJournalChildEntry = $('textarea[id$=newJournalChildEntry]').val();
        createJournalJs(newJournalChildEntry);
        $('textarea[id$=newJournalChildEntry]').val('');
    }
    function viewReplyJournal(journalId,journalChildId) {
        $('#myModalTripJournal').css('z-index','1039');
        viewReplyJournalJs(journalId,journalChildId);
    }
    function searchTripJournalsByGT() {
        var wordjournalsearch = $('#myModalTripJournal input[id$=tripjournalsearch]').val();
        var checkIssue = $("#myModalTripJournal input[id$=checkIssue]").prop("checked");
        var checkSales = $("#myModalTripJournal input[id$=checkSales]").prop("checked");
        searchTripJournalsByGTJs(wordjournalsearch,checkIssue,checkSales);
    }
    function viewTripJournals(){
        viewTripJournalsJs();
    }
    function clearViewTripJournalsByGT(){
        $('#myModalTripJournal input[id$=tripjournalsearch]').val('');
        $('#myModalTripJournal input[id$=checkIssue]').prop('checked',false);
        $('#myModalTripJournal input[id$=checkSales]').prop('checked',false);
        searchTripJournalsByGTJs('',false,false);
    }
    function viewTripDetail(event,val){
        event.stopPropagation();
        viewTripDetailJs(val);
    }
    function sortTrips(sortOrder,sortOrientation){
        var actual = $('input[id$=orderFieldTripActual]').val();
        var change = false;
        if(actual != sortOrder) change = true;
        sortTripsJs(sortOrder,sortOrientation,true,change);
    }
    function searchTrip(){
        var trip_start = $('input[id$=tripstart]').val();
        var trip_end = $('input[id$=tripend]').val();
        var trip_city = $('input[id$=tripcity]').val();
        var trip_vendor = $('input[id$=tripvendor]').val();
        //var trip_city = $('input[id$=tripcity_lkid]').val() != '000000000000000' ? $('input[id$=tripcity_lkid]').val() : '';
        //var trip_vendor = $('input[id$=tripvendor_lkid]').val() != '000000000000000' ? $('input[id$=tripvendor_lkid]').val() : '';
        var trip_status = $('select[id$=tripstatus]').val();
        var trip_showprior = $("input[id$=trip_showprior]").prop("checked");
        var trip_showcontracted = $("input[id$=trip_showcontracted]").prop("checked");
        var trip_showcancelled = $("input[id$=trip_showcancelled]").prop("checked");
        searchTripJs(trip_start,trip_end,trip_city,trip_vendor,trip_status,trip_showprior,trip_showcontracted,trip_showcancelled);
    }
    function clearTripFields(){
        $('input[id$=tripstart]').val('');
        $('input[id$=tripend]').val('');
        $('input[id$=tripcity]').val('');
        //$('input[id$=tripcity_lkid]').val('');
        $('input[id$=tripvendor]').val('');
        //$('input[id$=tripvendor_lkid]').val('');
        $("input[id$=trip_showprior]").prop("checked", false);
        $("input[id$=trip_showcontracted]").prop("checked", false);
        $("input[id$=trip_showcancelled]").prop("checked", false);
        $('select[id$=tripstatus]').val('');
    }
    function reviewCoordinator() {
        var coordinator = $('span[id$=production_coordinator]').text();
        console.log(coordinator);
        if(coordinator.trim() != '&nbsp;' && coordinator.trim() != '') return true;
        return false;
    }
    function openPreviewOptions() {
        var openPreviewOptions = false;
        $("span[id$=bidsByTripPanel] tr span.bid-option-span").each(function() {
            if($(this).text() != "n/a") openPreviewOptions = true;
        });
        if(openPreviewOptions) openPreviewOptionsJs();
   		else alert('Please include at least a bid in options.');
    }
    function openSendOptions() {
        if(reviewCoordinator()) {
            var openSendOptions = false;
            $("span[id$=bidsByTripPanel] tr span.bid-option-span").each(function() {
                if($(this).text() != "n/a") openSendOptions = true;
            });
            if(openSendOptions) openSendOptionsJs();
            else alert('Please select your options to send options to client');
        }else{
            alert('Air Coordinator is not for this this tour please add');
        }
    }
    function goToBidsTab(numberz,totalrecords) {
        goToBidsTabJs(numberz, totalrecords, 'gt-bids');
    }

    function sendLink() {
      var communityNoteBody;
      for ( instance in CKEDITOR.instances ) {
          if(instance.includes('communitynote_body_air')) communityNoteBody = CKEDITOR.instances[instance].getData();
      }
      console.log('communityNoteBody : ' + communityNoteBody);    var enter = false;
      $("#myModalSendOptions .check-contact").each(function() {
          if($(this).prop('checked')) {
              enter = true;
          }
      });
      if(enter) {
          sendLinkJs(communityNoteBody);  
      }else{
          alert('Please select Vendor');
      }
    }
    /*---@Conga: Update for Conga---*/
    function congaPreviewSendBidRequest(btn, itineraryId, tripId, tripStatus, bidId, bidStatus, congaQueriesJson, congaEmailTemplateId, congaEmailSubject, congaTemplateId1){ 
        var primary_contact = $(btn).parents('.group-vendor').find('.primary-contact').val();
        var emails = '';
        if(primary_contact != null && primary_contact.trim() != ''){
            $(btn).parents('.group-vendor').find('.check-contact').each(function(){
                if($(this).is(":checked") && $(this).parents('td').attr('contactid-data') != primary_contact) emails = emails.trim() != "" ? emails + ', ' + $(this).parents('td').attr('email-data') : $(this).parents('td').attr('email-data');
            });
            var i = 0;
            var updates = '&UF0=1';
            if(bidId != '' && bidStatus == 'Unsent'){
                updates += '&MFTSId' + i + '=' + bidId + '&MFTS' + i + '=Status__c&MFTSValue' + i + '=Lead Sent';
                i++;
                updates += '&MFTSId' + i + '=' + bidId + '&MFTS' + i + '=Lead_Sent__c&MFTSValue' + i + '=true';
                i++;
            }
            if(tripId != '' && tripStatus != 'Contracted'){
                /*updates += '&MFTSId' + i + '=' + tripId + '&MFTS' + i + '=Status_Ground__c&MFTSValue' + i + '=Bid Request Stage';
                i++;*/
            }
            //if(itineraryId != '') updates += '&MFTSId' + i + '=' + itineraryId + '&MFTS' + i + '=Status__c&MFTSValue' + i + '=Bid Request Stage';
            var congaQueriesMap = JSON.parse(congaQueriesJson);
            window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('Air - AirCharterBidById') ? '&QueryId=[Bid]' + congaQueriesMap['Air - AirCharterBidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Air - BidItinerarySegmentsByBidId') ? ',[BidItinerarySegments]' + congaQueriesMap['Air - BidItinerarySegmentsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('Air - ProductionAssociationsByOppId') ? ',[ProductionAssoc]' + congaQueriesMap['Air - ProductionAssociationsByOppId'].Id + '?pv0={!opportunityId}' : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + '&EmailToId=' + primary_contact + '&EmailCC=' + emails + '&TemplateId=' + congaTemplateId1 + updates + '&OFN=Air+Charter+Bid+Request' + '&DS7=2&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
        }
        else alert('No contacts found. Please make sure Vendor has Contacts.');
    }
    function congaPreviewOptions(tripId, congaQueriesJson, congaEmailTemplateId, congaTemplateId){ 
        var openSendOptions = false;
        $("span[id$=bidsByTripPanel] tr span.bid-option-span").each(function() {
            if($(this).text() != "n/a") openSendOptions = true;
        });
        if(openSendOptions){
            var congaQueriesMap = JSON.parse(congaQueriesJson);
            window.open('/apex/APXTConga4__Conga_Composer?id=' + tripId + (congaQueriesMap.hasOwnProperty('Air - BidsWithOptionsByAirTrip') ? '&QueryId=[Bids]' + congaQueriesMap['Air - BidsWithOptionsByAirTrip'].Id + '?pv0=' + tripId : '') + '&TemplateId=' + congaTemplateId + '&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
        } 
   		else alert('Please include at least a bid in options.');
    }
    function congaPreviewSendOptions(tripId, tripStatus, tripItineraryId, congaQueriesJson, congaEmailTemplateId, congaEmailSubject, congaTemplateId){ 
        var primary_contact = $('#myModalSendOptions .primary-contact').val();
        var emails = '';
        if(primary_contact != null && primary_contact.trim() != ''){
            $('#myModalSendOptions').find('.check-contact').each(function(){
                if($(this).is(":checked") && $(this).parents("td").data('contactid') != primary_contact) emails = emails.trim() != "" ? emails + ', ' + $(this).parents("td").data('contactemail') : $(this).parents("td").data('contactemail');
            });
            var congaQueriesMap = JSON.parse(congaQueriesJson);
            var updates = '';
            if(tripStatus != 'Contracted') updates = '&UF0=1&MFTSId0=' + tripId + '&MFTS0=Status__c&MFTSValue0=Pending Client Choice' + '&MFTSId1=' + tripItineraryId + '&MFTS1=Status__c&MFTSValue1=Pending Client Choice';
            window.open('/apex/APXTConga4__Conga_Composer?id=' + tripId + (congaQueriesMap.hasOwnProperty('Air - BidsWithOptionsByAirTrip') ? '&QueryId=[Bids]' + congaQueriesMap['Air - BidsWithOptionsByAirTrip'].Id + '?pv0=' + tripId : '') + (congaQueriesMap.hasOwnProperty('Air - ContactById') ? ',[Contact]' + congaQueriesMap['Air - ContactById'].Id + '?pv0=' + primary_contact : '')  + (congaQueriesMap.hasOwnProperty('Air - ProductionAssociationsByOppId') ? ',[ProductionAssoc]' + congaQueriesMap['Air - ProductionAssociationsByOppId'].Id + '?pv0={!opportunityId}' : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + '&EmailToId=' + primary_contact + '&EmailCC=' + emails + '&TemplateId=' + congaTemplateId + updates + '&OFN=Air+Options&DS7=2&DefaultPDF=1&SC0=1&SC1=SalesforceFile', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
        }
        else alert('Please select a Primary Contact.');
    }
    function congaSendOptions() {
        var primary_contact = $('#myModalSendOptions .primary-contact').val();
        if(primary_contact != null && primary_contact.trim() != '') congaSendOptionsJs();
        else alert('Please select a Primary Contact.');
    }
    function openPreviewCommunityOptions(tripId) {
      // Base64 encode the compDefinition JS object
      window.open('/apex/VoyajerPreviewApp?airId=' + tripId, '_blank');
    }
    /*---@/Conga---*/
    </script>
</apex:component>
```


# Last Modified


# Usage
