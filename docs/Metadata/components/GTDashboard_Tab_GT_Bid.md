---
layout: default
title: GTDashboard_Tab_GT_Bid
parent: components
grand_parent: Metadata
---
# Metadata Type
components


# Filename 
GTDashboard_Tab_GT_Bid


# Raw XML
```
<apex:component layout="block" controller="GTDashboard_Tab_GT_Bid_Controller" allowDML="true">
    <apex:attribute type="DashboardConfigurationWrapper" name="variables" assignTo="{!vfpConfiguration}" description="The variables of the VFP" required="true" />
    <apex:attribute name="vopportunityid" type="String" description="opportunity id" assignTo="{!opportunityId}" />
    <apex:attribute name="vtripBidNumber" type="Integer" description="tripBidNumber" assignTo="{!tripBidNumber}" />
    <apex:attribute name="vGTDashboard" type="GTDashboard" description="gtDashboard variables" assignTo="{!gtDashboard}" />
    <apex:attribute name="vtotalRecsBids" type="Integer" description="totalRecsBids" assignTo="{!totalRecsBids}" />
    <style>
        /*---myModalBidAgreement---*/
        .myModalBidAgreement table>thead{
            background-color:rgba(0,0,0,.05);
        }
        .myModalBidAgreement table th{
            padding:5px;
        }
        .myModalBidAgreement table td{
            padding:5px;
        }
        .myModalBidAgreement tbody tr:nth-of-type(even) {
            background-color: rgba(0,0,0,.02);
        }
        /*----Messages--------*/
        .saveMessage{
            color:red;
            font-weight:bold;
        }
    </style>
    <apex:outputPanel id="bidBody" layout="block">
        <apex:outputPanel rendered="{!OR(tripBidNumber == null,tripBidNumber == 0)}">Click Bid or "Bid Search" to get the details</apex:outputPanel>
        <div style="{!IF(OR(tripBidNumber == null,tripBidNumber == 0),'display:none;','')}">
            <apex:inputHidden id="isPageLoadedInput" value="{!isPageLoaded}" />
            <apex:inputHidden id="bidid" value="{!bidData.Id}" />
            <apex:inputHidden id="gtbid_tripid" value="{!bidData.GT__c}" />
            <apex:inputHidden id="production_coordinator_bid" value="{!coordinatorGT}" />
            <apex:inputHidden id="trip_have_contracted" value="{!tripHaveContracted}" />
            <apex:inputHidden id="production_office_location" value="{!bidData.Production__r.Office_Location__c}" />
            <apex:inputHidden id="resendBidAgreement_emailFromUserId" value="{!resendBidAgreement_emailFromUserId}"/>
            <apex:inputHidden id="resendBidAgreement_congaEmailFromId" value="{!resendBidAgreement_congaEmailFromId}"/>
            <div class="row">
                <div class="col-md-12">
                    <div class="fieldset" style="margin-top: 0 !important;">
                        <apex:outputPanel id="bidCoordinator">
                        </apex:outputPanel>
                        <apex:outputPanel id="datesTripViewPanel">
                            <span style="display:none;">
                                <apex:inputField id="tripview_startdate" value="{!bidData.GT__r.Start_Date__c}"  />
                                <apex:inputField id="tripview_enddate" value="{!bidData.GT__r.End_Date__c}" />
                            </span>
                        </apex:outputPanel>
                        <table class="table table-sm no-border" style="margin-bottom: 0 !important;">
                            <tbody>
                                <tr>
                                    <td style="width:50%;">
                                        <span>Production ID: </span><span style="font-weight:bold;">{!bidData.Production__r.Production_ID__c}</span>
                                        <span style="margin-left: 15px;">Trip ID: </span><span style="font-weight:bold;">{!bidData.GT__r.Name}</span>
                                        <span style="margin-left: 15px;">Bid ID: </span><span style="font-weight:bold;">{!bidData.Name}</span>
                                        <input type="hidden" id="bidpanel_total" value="{!totalRecsBids}" />
                                    </td>
                                    <td>
                                        <span>Bid {!tripBidNumber} of {!totalRecsBids}</span>
                                        <span>
                                            <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="changeBid({!tripBidNumber - 1});"><i class="fa fa-angle-double-left"></i></button>
                                            <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="changeBid({!tripBidNumber + 1});"><i class="fa fa-angle-double-right"></i></button>
                                        </span>
                                        <span style="margin-left:20px;">
                                            <span>Locked</span>
                                            <span>
                                                <apex:inputCheckbox id="lockedInput" value="{!bidData.Locked__c}" styleClass="toggle toogle-bid toogle-data-bid" html-data-size="mini" html-data-style="ios" onchange="editBidDataLocked(this,'{!bidData.Id}');" />
                                            </span>
                                        </span>
                                    </td>
                                    <td style="text-align:right;">
                                        <a href="javascript:void(0);" onclick="getBidInformation('{!tripBidNumber}');" style="color: black !important;"><i class="fa fa-refresh"></i></a>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <div>
                                            <span>Production:</span>
                                            <span style="{!IF(bidData.Vendor__c == null,'margin-left:45px;','margin-left:40px;')}">
                                                <a href="/{!bidData.Production__c}" target="_blank">{!bidData.Production__r.Name}</a>
                                            </span>
                                        </div>
                                        <div style="margin-top: 10px;">
                                            <span>{!IF(bidData.Vendor__c == NULL,'Provider:','Vendor:')}</span>
                                            <span style="margin-left:60px;{!IF(bidData.Vendor__c == null,'display:none;','')}">
                                                <a href="/{!bidData.Vendor__c}" target="_blank">{!bidData.Vendor__r.Name}</a> - {!bidData.Vendor__r.City__r.Name}
                                            </span>
                                        </div>
                                    </td>
                                    <td colspan="2" style="padding-top: 10px;">
                                        <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="openBidHistory('{!bidData.Vendor__r.Name}');">Bid History</button>
                                        <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="openBidJournalsJs();">Bid Journals</button>
                                        <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="viewBidDocumentsJs(true);">Documents</button>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <span style="float:left;">Vendor Contact:</span>
                                        <span style="margin-left:20px;float:left;width: 85%;">
                                            <apex:outputPanel id="contactBidPanel">
                                                <apex:selectList size="1" id="biddata_primarycontact" styleClass="form-control form-control-sm" value="{!bidData.Vendor_Contact__c}">
                                                    <apex:selectOptions value="{!contactsBidsByVendor}" />
                                                    <apex:actionSupport event="onchange" action="{!changeContactPrimaryBid}" status="loading" reRender="contactInfoBidPanel"/>
                                                </apex:selectList>
                                            </apex:outputPanel>
                                            <apex:outputPanel id="contactInfoBidPanel">
                                                <span><i class="fa fa-envelope-o"></i>&nbsp;<a href="/{!bidPrimaryContact.Id}" target="_blank"><apex:outputText value="{!bidPrimaryContact.Email}" escape="false" /></a></span>
                                                <span style="margin-left:15px;"><i class="fa fa-phone" style="{!if(!isNull(bidPrimaryContact.Phone), '', 'display:none;')}"></i>&nbsp;{!bidPrimaryContact.Phone}</span>
                                            </apex:outputPanel>
                                        </span>
                                    </td>
                                    <td colspan="2">
                                        <button type="button" class="btn btn-danger btn-sm btn-custom" onclick="openAssociateVendor('{!tripBidNumber}')" style="{!IF(bidData.Vendor__c == NULL,'','display:none;')}">Associate Vendor</button>
                                        <button type="button" class="btn btn-success btn-sm btn-custom" onclick="contract('{!tripBidNumber}')" style="{!IF(bidData.Status__c == 'Contracted','display:none;',IF(bidData.Vendor__c <> NULL,'','display:none;'))}">Contract</button>
                                        <button type="button" class="btn btn-danger btn-sm btn-custom" onclick="viewContractingDetailByBidJs('{!bidData.Id}','{!bidData.GT__c}');" style="{!IF(bidData.Status__c == 'Contracted','','display:none;')}">G. Contracting</button>
                                        <button type="button" class="btn btn-danger btn-sm btn-custom" onclick="uncontract('{!tripBidNumber}');" style="{!IF(bidData.Status__c == 'Contracted','','display:none;')}">Uncontract</button>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <span style="float:left;">Venue:</span>
                                        <span style="margin-left:70px;">
                                            {!bidData.DX_to_Venue__c} from <a href="/{!bidData.Venue__c}">{!bidData.Venue__r.Name}</a>
                                        </span>
                                        <span style="margin-left: 34%;">Status:</span>
                                        <span style="font-weight:bold;" class="bid-tab-status">{!bidData.Status__c}</span>
                                    </td>
                                    <td colspan="2"></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
            <div class="row">
                <div class="col-md-12">
                    <button type="button" class="btn btn-secondary btn-custom btn-add-trip-details-bid" onclick="newSubTripBid();"><i class="fa fa-plus"></i> {!IF(bidSubTrips.size > 0, 'Add Additional Trip','Add Trip Details')}</button>
                </div>
            </div>
            <div class="accordion" id="accordionSeven" style="margin-top:10px;">
                <div class="card">
                    <div class="card-header" id="headingSeven">
                        <h2 class="mb-0">
                            Trip Details
                            <span style="float:right;">
                                <a href="javascript:void(0);" onclick="checkIcon(this,'collapseSeven');">
                                    <i class="fa fa-angle-up btn-show"></i>
                                </a>
                            </span>
                        </h2>
                    </div>
                    <div id="collapseSeven" class="collapse show" aria-labelledby="headingSeven" data-parent="#accordionSeven">
                        <div class="card-body" style="min-height: 235px;">
                            <apex:outputPanel id="subTripsByBidPanel">
                                <apex:repeat value="{!bidSubTrips}" var="bidSubTrip">
                                    <div class="row">
                                        <div class="col-md-12">
                                            <div class="accordion" id="accordionFive">
                                                <div class="card">
                                                    <div class="card-header" id="headingFive">
                                                        <h2 class="mb-0">
                                                            Trip {!bidSubTrip.Trip_Order__c}
                                                            <span style="float:right;">
                                                                <apex:inputField value="{!bidSubTrip.Trip_Order__c}" styleClass="form-control form-control-sm" style="width:40px !important;margin-right:20px;"  />
                                                                <a href="javascript:void(0);" onclick="checkIcon(this,'collapseFive-{!bidSubTrip.Trip_Order__c}');">
                                                                    <i class="fa fa-angle-up btn-show"></i>
                                                                </a>
                                                            </span>
                                                        </h2>
                                                    </div>
                                                    <div id="collapseFive-{!bidSubTrip.Trip_Order__c}" class="collapse show" aria-labelledby="headingFive" data-parent="#accordionFive">
                                                        <div class="card-body card-body-trip card-body-{!bidSubTrip.Trip_Order__c}" style="min-height: 235px;">
                                                            <div class="row" style="margin-top:0 !important;">
                                                                <div class="col-md-2">
                                                                    <label style="font-weight:bold;">Trip Type</label><br/>
                                                                    <apex:inputField value="{!bidSubTrip.Sub_Trip_Type__c}" styleClass="form-control form-control-sm"  />
                                                                </div>
                                                                <div class="col-md-4">
                                                                    <label style="font-weight:bold;">Description</label><br/>
                                                                    <apex:inputField value="{!bidSubTrip.Description__c}" styleClass="form-control form-control-sm"  />
                                                                </div>
                                                                <div class="col-md-3">
                                                                </div>
                                                                <div class="col-md-3 text-right">
                                                                    <button type="button" class="btn btn-success btn-sm btn-custom" onclick="saveSubTripBid('{!bidSubTrip.Id}');"><i class="fas fa-download"></i> Save</button>
                                                                    <button type="button" class="btn btn-danger btn-sm btn-custom" onclick="deleteSubTripBid('{!bidSubTrip.Id}');"><i class="fa fa-times"></i> Delete</button>
                                                                </div>
                                                            </div>
                                                            <div class="row">
                                                                <div class="col-md-6">
                                                                    <span style="font-weight:bold;">Travel Information</span>
                                                                </div>
                                                                <div class="col-md-6 text-right">
                                                                    <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="addTravelLineBid(this);"><i class="fa fa-plus"></i> Add Travel</button>
                                                                </div>
                                                            </div>
                                                            <div class="row">
                                                                <div class="col-md-12">
                                                                    <input type="hidden" value="{!bidSubTrip.Id}" class="new-data subtripid" />
                                                                    <apex:outputPanel id="travelsByTripPanel">
                                                                        <table class="table table-sm" style="margin-top:5px;margin-bottom:0;">
                                                                            <thead class="thead-light">
                                                                                <tr>
                                                                                <!-- Changes as per 176568992 -->
                                                                                    <!--th width="5%">Line #</th-->
                                                                                    <th width="8%">Vehicle</th>
                                                                                    <th width="6%">Start Date</th>
                                                                                    <th width="5%">Spot Time</th>
                                                                                    <th width="6%">End Date</th>
                                                                                    <th width="5%">Departure Time</th>
                                                                                    <th width="7%">Group</th>
                                                                                    <th width="12%">Location Pick Up Type</th>
                                                                                    <th width="8%">Location Pick Up Details</th>
                                                                                    <th width="8%">Location Drop Off Type</th>
                                                                                    <th width="8%">Location Drop Off Details</th>
                                                                                    <th width="8%">Airline Info/Special Notes</th>
                                                                                    <th width="7%">Actions</th>
                                                                                </tr>
                                                                            </thead>
                                                                            <tbody>
                                                                                <tr class="new-travel line-travel-{!bidSubTrip.Id}" style="display:none;">
                                                                                    <!-- Changes as per 176568992 -->
                                                                                    <!--td>
                                                                                        <apex:inputField value="{!newTravel.Line__c}" styleClass="form-control form-control-sm new-data line" />
                                                                                    </td-->
                                                                                    <td>
                                                                                        <apex:inputField value="{!newTravel.Vehicle_Ref__c}" styleClass="form-control form-control-sm new-data vehicle vehicle-travel-search" onkeyup="setInputVehicleBid();" />
                                                                                        <input type="hidden" class="vehicleid" />
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:inputField value="{!newTravel.Start_Date__c}" styleClass="form-control form-control-sm new-data startdate" />
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:inputField value="{!newTravel.Start_Date_Time__c}" styleClass="form-control form-control-sm new-data starttime" type="time" />
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:inputField value="{!newTravel.End_Date__c}" styleClass="form-control form-control-sm new-data enddate" />
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:inputField value="{!newTravel.End_Date_Time__c}" styleClass="form-control form-control-sm new-data endtime" type="time" />
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:inputField value="{!newTravel.Travel_Type__c}" styleClass="form-control form-control-sm new-data traveltype" />
                                                                                    </td>
                                                                                    <td>
                                                                                        <!--<apex:inputField value="{!newTravel.Group_Type__c}" styleClass="form-control form-control-sm new-data grouptype" />-->
                                                                                        <input value="{!newTravel.Group_Type__c}" class="form-control form-control-sm new-data grouptype" />
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:inputField value="{!newTravel.Location_Type__c}" styleClass="form-control form-control-sm new-data locationtype" style="width:70%;float:left;" />
                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="openSelectLocationType(this,'{!bidSubTrip.Id}','pickup');" style="float:left;"><i class="fas fa-search"></i></button>
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:inputField value="{!newTravel.Location_Details__c}" styleClass="form-control form-control-sm new-data locationdetails" />
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:inputField value="{!newTravel.Location_Drop_Off_Type__c}" styleClass="form-control form-control-sm new-data locationdropofftype" style="width:70%;float:left;" />
                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="openSelectLocationType(this,'{!bidSubTrip.Id}','dropoff');" style="float:left;"><i class="fas fa-search"></i></button>
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:inputField value="{!newTravel.Location_Details_Drop_Off__c}" styleClass="form-control form-control-sm new-data locationdetailsdropoff" />
                                                                                    </td>
                                                                                    <td>
                                                                                        <input value="{!newTravel.Airline_Info_Special_Notes__c}" class="form-control form-control-sm new-data notes airline-info" />
                                                                                    </td>
                                                                                    <td>
                                                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="saveTravelAddMoreBid(this);" title="Save & Add More Travel"><i class="fas fa-save"></i></button>
                                                                                        <button type="button" style="margin-left:0;" class="btn btn-secondary btn-sm btn-custom" onclick="saveTravelCompleteBid(this);" title="Save & Complete Trip"><i class="fas fa-business-time"></i></button>
                                                                                        <button type="button" style="margin-left:0;" class="btn btn-danger btn-sm btn-custom" onclick="cancelTravelBid(this);"><i class="fas fa-window-close"></i></button>
                                                                                    </td>
                                                                                </tr>
                                                                                <apex:repeat value="{!bidSubTripTravelsMap[bidSubTrip.id]}" var="bidTravel">
                                                                                    <tr class="line-travel-{!bidTravel.Id}">
                                                                                        <!-- Changes as per 176568992 -->
                                                                                        <!--td>
                                                                                            <span class="show-data"><apex:outputText value="{!bidTravel.Line__c}" /></span>
                                                                                            <apex:inputField value="{!bidTravel.Line__c}" styleClass="form-control form-control-sm data line" style="display:none" />
                                                                                        </td-->
                                                                                        <td>
                                                                                            <span class="show-data"><apex:outputText value="{!bidTravel.Vehicle_Ref__c}" /></span>
                                                                                            <apex:inputField value="{!bidTravel.Vehicle_Ref__c}" styleClass="form-control form-control-sm data vehicle vehicle-travel-search" style="display:none" onkeyup="setInputVehicleBid();" />
                                                                                            <input type="hidden" class="vehicleid" value="{!bidTravel.Vehicle_Lookup__c}" />
                                                                                        </td>
                                                                                        <td>
                                                                                            <span class="show-data">
                                                                                                <apex:outputText value="{0,date,dd-MMMM-yyyy}">
                                                                                                    <apex:param value="{!bidTravel.Start_Date__c}" />
                                                                                                </apex:outputText>
                                                                                            </span>
                                                                                            <span class="data" style="display:none">
                                                                                                <apex:inputField value="{!bidTravel.Start_Date__c}" styleClass="form-control form-control-sm startdate" />
                                                                                            </span>
                                                                                        </td>
                                                                                        <td>
                                                                                            <span class="show-data">
                                                                                                {!bidTravel.Start_Date_Time_Text__c}
                                                                                            </span>
                                                                                            <apex:inputField value="{!bidTravel.Start_Date_Time__c}" styleClass="form-control form-control-sm data starttime" type="time" style="display:none" />
                                                                                        </td>
                                                                                        <td>
                                                                                            <span class="show-data">
                                                                                                <apex:outputText value="{0,date,dd-MMMM-yyyy}">
                                                                                                    <apex:param value="{!bidTravel.End_Date__c}" />
                                                                                                </apex:outputText>
                                                                                            </span>
                                                                                            <span class="data" style="display:none">
                                                                                                <apex:inputField value="{!bidTravel.End_Date__c}" styleClass="form-control form-control-sm enddate" />
                                                                                            </span>
                                                                                        </td>
                                                                                        <td>
                                                                                            <span class="show-data">
                                                                                                {!bidTravel.End_Date_Time_Text__c}
                                                                                            </span>
                                                                                            <apex:inputField value="{!bidTravel.End_Date_Time__c}" styleClass="form-control form-control-sm data endtime" type="time" style="display:none" />
                                                                                        </td>
                                                                                        <td>
                                                                                            <input type="hidden" class="data-original-grouptype" value="{!bidTravel.Group_Type__c}"  style="display:none;" />
                                                                                            <span class="show-data"><apex:outputText value="{!bidTravel.Group_Type__c}" /></span>
                                                                                            <input value="{!bidTravel.Group_Type__c}" class="form-control form-control-sm data grouptype" style="display:none" />
                                                                                        </td>
                                                                                        <td>
                                                                                            <span class="show-data"><apex:outputText value="{!bidTravel.Location_Type__c}" /></span>
                                                                                            <span class="data" style="display:none;">
                                                                                                <apex:inputField value="{!bidTravel.Location_Type__c}" styleClass="form-control form-control-sm locationtype"  style="width:70%;float:left;" />
                                                                                                <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="openSelectLocationType(this,'{!bidTravel.Id}','pickup');" style="float:left;"><i class="fas fa-search"></i></button>
                                                                                            </span>
                                                                                        </td>
                                                                                        <td>
                                                                                            <span class="show-data"><apex:outputText value="{!bidTravel.Location_Details__c}" /></span>
                                                                                            <apex:inputField value="{!bidTravel.Location_Details__c}" styleClass="form-control form-control-sm data locationdetails" style="display:none" />
                                                                                        </td>
                                                                                        <td>
                                                                                            <span class="show-data"><apex:outputText value="{!bidTravel.Location_Drop_Off_Type__c}" /></span>
                                                                                            <span class="data" style="display:none;">
                                                                                                <apex:inputField value="{!bidTravel.Location_Drop_Off_Type__c}" styleClass="form-control form-control-sm data locationdropofftype" style="width:70%;float:left;" />
                                                                                                <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="openSelectLocationType(this,'{!bidTravel.Id}','dropoff');" style="float:left;"><i class="fas fa-search"></i></button>
                                                                                            </span>
                                                                                        </td>
                                                                                        <td>
                                                                                            <span class="show-data"><apex:outputText value="{!bidTravel.Location_Details_Drop_Off__c}" /></span>
                                                                                            <apex:inputField value="{!bidTravel.Location_Details_Drop_Off__c}" styleClass="form-control form-control-sm data locationdetailsdropoff" style="display:none" />
                                                                                        </td>
                                                                                        <td>
                                                                                            <input type="hidden" class="data-original-airlineinfo" value="{!bidTravel.Airline_Info_Special_Notes__c}"  style="display:none;" />
                                                                                            <span class="show-data"><apex:outputText value="{!bidTravel.Airline_Info_Special_Notes__c}" /></span>
                                                                                            <input value="{!bidTravel.Airline_Info_Special_Notes__c}" class="form-control form-control-sm data notes airline-info" style="display:none" />
                                                                                        </td>
                                                                                        <td>
                                                                                            <input type="hidden" value="{!bidTravel.Id}" class="id"  />
                                                                                            <button type="button" class="btn btn-success btn-sm btn-custom btn-save" onclick="saveEditTravelBid(this);" style="display:none;margin-left: 0.5rem;"><i class="fa fa-check"></i></button>
                                                                                            <button type="button" class="btn btn-secondary btn-sm btn-custom btn-edit" onclick="editTravelBid(this);"><i class="fa fa-pencil-alt"></i></button>
                                                                                            <button type="button" class="btn btn-secondary btn-sm btn-custom btn-cancel" onclick="cancel(this);" style="display:none;margin-left:0;"><i class="fa fa-ban"></i></button>
                                                                                            <button type="button" style="margin-left:0;" class="btn btn-danger btn-sm btn-custom btn-delete" onclick="deleteTravelBid('{!bidTravel.Id}');"><i class="fas fa-window-close"></i></button>
                                                                                        </td>
                                                                                    </tr>
                                                                                </apex:repeat>
                                                                            </tbody>
                                                                        </table>
                                                                    </apex:outputPanel>
                                                                </div>
                                                            </div>
                                                            <div class="row">
                                                                <div class="col-md-12">
                                                                    <label style="font-weight:bold;">Trip Notes</label>
                                                                    <apex:inputField value="{!bidSubTrip.Sub_Trip_Notes__c}" styleClass="form-control form-control-sm" />
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </apex:repeat>
                                <script>
                                createAutocompleteVehicleBid = false;
                                $('.airline-info').inputpicker({
                                    data: {!airlineInfoJson},
                                    fields:[
                                        {name:'dataname',text:'Name'}
                                    ],
                                    fieldText: 'dataname',
                                    fieldValue: 'dataid',
                                    headShow: false,
                                    filterOpen: true,
                                    autoOpen: false
                                });
                                $('.grouptype').inputpicker({
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
                            </apex:outputPanel>
                            
                            <div class="row" style="margin-top: 35px !important;">
                                <div class="col-md-6">
                                    <span style="font-weight:bold;">Vehicle Information</span>
                                </div>
                                <div class="col-md-6 text-right">
                                    <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="newVehicleBid();"><i class="fa fa-plus"></i> Add Vehicle</button>
                                </div>
                            </div>
                            <div class="row">
                                <div class="col-md-12">
                                    <apex:outputPanel id="newVehicleTripPanel">
                                        <table class="table table-sm" style="margin-top:5px;margin-bottom:0;">
                                            <thead class="thead-light">
                                                <tr>
                                                    <th width="11%">Vehicle</th>
                                                    <th width="10%">Vehicle Type</th>
                                                    <th width="7%">Capacity</th>
                                                    <th width="7%">Make</th>
                                                    <th width="7%">Model</th>
                                                    <th width="7%">Year</th>
                                                    <th width="12%">Gear / Luggage Space Needed</th>
                                                    <th>Amenities</th>
                                                    <th width="9%" class="other-amenities-data-header" style="display:none;">Other Amenities</th>
                                                    <th width="15%"></th>
                                                </tr>
                                            </thead>
                                            <tbody>
                                                <tr class="new-vehicle-bid" style="display:none;">
                                                    <td>
                                                        <apex:inputField value="{!newVehicleBid.Vehicle_Ref__c}" styleClass="form-control form-control-sm newdata newdata-vehicleref" />
                                                    </td>
                                                    <td>
                                                        <apex:inputField value="{!newVehicleBid.Vehicle_Type__c}" styleClass="form-control form-control-sm newdata newdata-vehicletype" />
                                                    </td>
                                                    <td>
                                                        <apex:inputField value="{!newVehicleBid.Capacity__c}" styleClass="form-control form-control-sm newdata newdata-capacity" />
                                                    </td>
                                                    <td>
                                                        <!--<apex:inputField value="{!newVehicleBid.Make__c}" styleClass="form-control form-control-sm newdata newdata-make" /-->
                                                        <input class="form-control form-control-sm newdata newdata-make" value="{!newVehicleBid.Make__c}" />
                                                    </td>
                                                    <td>
                                                        <!--<apex:inputField value="{!newVehicleBid.Model__c}" styleClass="form-control form-control-sm newdata  newdata-model" />-->
                                                        <input class="form-control form-control-sm newdata newdata-model" value="{!newVehicleBid.Model__c}" />
                                                    </td>
                                                    <td>    
                                                        <apex:inputField value="{!newVehicleBid.Year__c}" styleClass="form-control form-control-sm newdata newdata-year" />
                                                    </td>
                                                    <td>    
                                                        <apex:inputField value="{!newVehicleBid.Gear_Luggage_Space__c}" styleClass="form-control form-control-sm newdata newdata-luggage" />
                                                    </td>
                                                    <td>
                                                        <apex:selectList id="newvehiclebid_amenities" value="{!newVehicleBid.Amenities__c}" html-data-placeholder="Choose any amenity.." html-multiple="multiple" size="1" styleClass="form-control form-control-sm multiselect multiselect-bid newdata-multiselect-bid">
                                                            <apex:selectOptions value="{!ground_amenitiesPL}" />
                                                        </apex:selectList>
                                                    </td>
                                                    <td>    
                                                        <apex:inputField value="{!newVehicleBid.Other_Amenities__c}" styleClass="form-control form-control-sm newdata newdata-otheramenities" />
                                                    </td>
                                                    <td class="text-center" width="15%">
                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="saveVehicleBid();"><i class="fa fa-check"></i> Save</button>
                                                        <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="cancelVehicleBid();"><i class="fa fa-ban"></i> Cancel</button>
                                                    </td>
                                                </tr>
                                            </tbody>
                                        </table>
                                        <script>
                                        $('.newdata-make').inputpicker({
                                            data: {!makeJson},
                                            fields:[
                                                {name:'dataname',text:'Name'}
                                            ],
                                            fieldText: 'dataname',
                                            fieldValue: 'dataid',
                                            headShow: false,
                                            filterOpen: true,
                                            autoOpen: false
                                        });
                                        $('.newdata-model').inputpicker({
                                            data: {!modelJson},
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
                                    <apex:outputPanel id="vehiclesBidPanel">
                                        <table class="table table-sm">
                                            <tbody>
                                                <apex:repeat value="{!vehiclesByBidList}" var="vehicleBid">
                                                    <tr data-id="{!vehicleBid.Id}">
                                                        <td width="11%">
                                                            <input type="hidden" value="{!vehicleBid.Id}" class="id"  />
                                                            <span class="show-data">{!vehicleBid.Vehicle_Ref__c}</span>
                                                            <apex:inputField value="{!vehicleBid.Vehicle_Ref__c}" styleClass="form-control form-control-sm data vehicleref" style="display:none;" />
                                                        </td>
                                                        <td width="10%">
                                                            <span class="show-data">{!vehicleBid.Vehicle_Type__c}</span>
                                                            <apex:inputField value="{!vehicleBid.Vehicle_Type__c}" styleClass="form-control form-control-sm data vehicletype" style="display:none;" />
                                                        </td>
                                                        <td width="7%">
                                                            <span class="show-data">{!vehicleBid.Capacity__c}</span>
                                                            <apex:inputField value="{!vehicleBid.Capacity__c}" styleClass="form-control form-control-sm data capacity" style="display:none;" />
                                                        </td>
                                                        <td width="7%">
                                                            <span class="show-data">{!vehicleBid.Make__c}</span>
                                                            <!--<apex:inputField value="{!vehicleBid.Make__c}" styleClass="form-control form-control-sm data make" style="display:none;" />-->
                                                            <input type="hidden" class="data-original-make" value="{!vehicleBid.Make__c}"  style="display:none;" />
                                                            <input class="form-control form-control-sm data make make-search" value="{!vehicleBid.Make__c}" style="display:none;" />
                                                        </td>
                                                        <td width="7%">
                                                            <span class="show-data">{!vehicleBid.Model__c}</span>
                                                            <!--<apex:inputField value="{!vehicleBid.Model__c}" styleClass="form-control form-control-sm data model" style="display:none;" />-->
                                                            <input type="hidden" class="data-original-model" value="{!vehicleBid.Model__c}"  style="display:none;" />
                                                            <input class="form-control form-control-sm data model model-search" value="{!vehicleBid.Model__c}" style="display:none;" />
                                                        </td>
                                                        <td width="7%">
                                                            <span class="show-data">{!vehicleBid.Year__c}</span>
                                                            <apex:inputField value="{!vehicleBid.Year__c}" styleClass="form-control form-control-sm data year" style="display:none;" />
                                                        </td>
                                                        <td width="12%">
                                                            <span class="show-data">{!vehicleBid.Gear_Luggage_Space__c}</span>
                                                            <apex:inputField value="{!vehicleBid.Gear_Luggage_Space__c}" styleClass="form-control form-control-sm data luggage" style="display:none;" />
                                                        </td>
                                                        <td>
                                                            <span class="show-data-without-other-amenities" style="display:none;">{!vehicleBid.Amenities__c}</span>
                                                            <span class="show-data-with-other-amenities">{!vehicleBid.Amenities__c + if(vehicleBid.Other_Amenities__c != null,',' + vehicleBid.Other_Amenities__c,'')}</span>
                                                            <span class="data" style="display:none;">
                                                                <apex:selectList html-data-placeholder="Choose any amenity.." html-multiple="multiple" size="1" styleClass="form-control form-control-sm multiselect multiselect-bid amenities">
                                                                    <apex:selectOptions value="{!ground_amenitiesPL}" />
                                                                </apex:selectList>
                                                            </span>
                                                        </td>
                                                        <td width="9%" class="other-amenities-data" style="display:none;">
                                                            <span class="show-data">{!vehicleBid.Other_Amenities__c}</span>
                                                            <apex:inputField value="{!vehicleBid.Other_Amenities__c}" styleClass="form-control form-control-sm data otheramenities" style="display:none;" />
                                                        </td>
                                                        <td class="text-center" width="15%">
                                                            <button type="button" class="btn btn-secondary btn-sm btn-custom btn-save" onclick="saveEditVehicleBid(this);" style="display:none;"><i class="fa fa-check"></i> Save</button>
                                                            <button type="button" class="btn btn-secondary btn-sm btn-custom btn-edit" onclick="editVehicleBid(this);"><i class="fa fa-pencil"></i> Edit</button>
                                                            <button type="button" class="btn btn-secondary btn-sm btn-custom btn-cancel" onclick="cancelEditVehicleBid(this);" style="display:none;"><i class="fa fa-ban"></i> Cancel</button>
                                                            <button type="button" class="btn btn-secondary btn-sm btn-custom btn-delete" onclick="deleteVehicleBid('{!vehicleBid.Id}');"><i class="fa fa-times"></i> Delete</button>
                                                        </td>
                                                    </tr>
                                                </apex:repeat>
                                            </tbody>
                                        </table>
                                        <script>
                                        $('.make-search').inputpicker({
                                            data: {!makeJson},
                                            fields:[
                                                {name:'dataname',text:'Name'}
                                            ],
                                            fieldText: 'dataname',
                                            fieldValue: 'dataid',
                                            headShow: false,
                                            filterOpen: true,
                                            autoOpen: false
                                        });
                                        $('.model-search').inputpicker({
                                            data: {!modelJson},
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
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="row">
                <div class="col-md-12">
                    <div class="accordion" id="accordionSix">
                        <div class="card">
                            <div class="card-header" id="headingSix">
                                <h2 class="mb-0">
                                    Rate Details
                                    <span style="float:right;">
                                        <a href="javascript:void(0);" onclick="checkIcon(this,'collapseSix');">
                                            <i class="fa fa-angle-up btn-show"></i>
                                        </a>
                                    </span>
                                </h2>
                            </div>
                            <div id="collapseSix" class="collapse show" aria-labelledby="headingSix" data-parent="#accordionSix">
                                <div class="card-body" style="min-height: 235px;">
                                    <div class="row" style="margin-top:0 !important;">
                                        <div class="col-md-6">
                                            <div class="row">
                                                <div class="col-md-12">
                                                    <strong>Rate Details</strong>
                                                </div>
                                            </div>
                                            <apex:outputPanel id="rateDetailsPanel" layout="block" styleClass="row">
                                                <div class="col-md-12">
                                                    <div class="card">
                                                        <div class="card-body">
                                                            <div class="row">
                                                                <div class="col-md-12">
                                                                    <div class="form-group">
                                                                        <apex:outputLabel value="Base Cost :" for="bidRevenue_baseCostInput" style="font-weight:bold;"/>{!symbolMap[bidRevenue.CurrencyIsoCode]}
                                                                        <apex:inputField id="bidRevenue_baseCostInput" value="{!bidRevenue.Base_Cost__c}" styleClass="form-control" onfocus="saveDataPreview('bidRevenue_baseCostInput',this);" onblur="calculateRevenue();" />
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="row">
                                                                <div class="col-md-6">
                                                                    <div class="form-group">
                                                                        <apex:outputLabel value="Commission :" for="bidRevenue_CommissionInput" style="font-weight:bold;"/>{!symbolMap[bidRevenue.CurrencyIsoCode]}
                                                                        <apex:inputField id="bidRevenue_CommissionInput" value="{!bidRevenue.Commission__c}" styleClass="form-control" onfocus="saveDataPreview('bidRevenue_CommissionInput',this);" onblur="calculateRevenueByCommission();" />
                                                                    </div>
                                                                </div>
                                                                <div class="col-md-6">
                                                                    <div class="form-group">
                                                                        <apex:outputLabel value="Rate : % " for="bidRevenue_rateInput" style="font-weight:bold;"/>
                                                                        <apex:inputField id="bidRevenue_rateInput" value="{!bidRevenue.Rate__c}" styleClass="form-control" onfocus="saveDataPreview('bidRevenue_rateInput',this);" onblur="calculateRevenueByRate();" />
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="row" style="{!IF(bidData.GT__r.GT_Preferences__c == 'RRE','','display:none;')}">
                                                                <div class="col-md-6">
                                                                    <div class="form-group">
                                                                        <apex:outputLabel value="Vat : %" for="bidRevenue_varInput" style="font-weight:bold;"/>
                                                                        <apex:inputField id="bidRevenue_varInput" value="{!bidRevenue.VAT_Rate__c}" styleClass="form-control"/>
                                                                    </div>
                                                                </div>
                                                                <div class="col-md-6">
                                                                    <div class="form-group" style="padding-top: 2em;">
                                                                        <apex:inputField value="{!bidRevenue.VAT_Included_in_Total__c}" label="Included in Total Price" styleClass="form-control"/>
                                                                        <label>Included in Total Price</label>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="row">
                                                                <div class="col-md-12">
                                                                    <div class="form-group">
                                                                        <apex:outputLabel value="Gratuity :" for="bidRevenue_gratuityInput" style="font-weight:bold;"/>{!symbolMap[bidRevenue.CurrencyIsoCode]}
                                                                        <apex:inputField id="bidRevenue_gratuityInput" value="{!bidRevenue.Gratuity__c}" styleClass="form-control" onfocus="saveDataPreview('bidRevenue_gratuityInput',this);" onblur="calculateTotalPrice();" />
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="row">
                                                                <div class="col-md-6">
                                                                    <div class="form-group">
                                                                        <apex:outputLabel value="Total Price :" for="bidRevenue_totalPriceInput" style="font-weight:bold;"/>{!symbolMap[bidRevenue.CurrencyIsoCode]}
                                                                        <apex:inputField id="bidRevenue_totalPriceInput" value="{!bidRevenue.Total_Price__c}" styleClass="form-control"/>
                                                                    </div>
                                                                </div>
                                                                <div class="col-md-6">
                                                                    <div class="form-group">
                                                                        <apex:outputLabel value="Currency :" for="bidRevenue_currencyIsoCodeInput" style="font-weight:bold;"/>
                                                                        <apex:selectList id="bidRevenue_currencyIsoCodeInput" value="{!bidRevenue.CurrencyIsoCode}" size="1" styleClass="form-control" onchange="changeSymbolJs(this);">
                                                                            <apex:selectOptions value="{!CurrencyValues}"/>
                                                                        </apex:selectList>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </apex:outputPanel>
                                        </div>
                                        <div class="col-md-6">
                                            <div class="row">
                                                <div class="col-md-12">
                                                    <span style="font-weight:bold;">Additional Fees</span>
                                                </div>
                                            </div>
                                            <div class="row">
                                                <div class="col-md-12 text-right">
                                                    <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="newConcessionTrip();"><i class="fa fa-plus"></i> Add New Item</button>
                                                </div>
                                            </div>
                                            <div class="row">
                                                <div class="col-md-12">
                                                    <table class="table table-sm" style="margin-top:5px;margin-bottom:0;">
                                                        <thead class="thead-light">
                                                            <tr>
                                                                <th width="7%"></th>
                                                                <th width="12%"></th>
                                                                <th width="18%">Additional Fees &amp; Details</th>
                                                                <th width="43%">Notes</th>
                                                                <th width="7%">Rate</th>
                                                                <th width="13%"></th>
                                                            </tr>
                                                        </thead>
                                                        <tbody>
                                                            <tr class="new-concession-bid" style="display:none;">
                                                                <td>
                                                                    <input class="form-control form-control-sm newdata newdata-order" />
                                                                </td>
                                                                <td>
                                                                    <select class="form-control form-control-sm newdata newdata-included">
                                                                        <option value="">--Select--</option>
                                                                        <option value="Included">Included</option>
                                                                        <option value="Excluded">Excluded</option>
                                                                    </select>
                                                                </td>
                                                                <td>
                                                                    <input class="form-control form-control-sm newdata newdata-requested data-concession-search-new" />
                                                                </td>
                                                                <td>
                                                                    <input class="form-control form-control-sm newdata newdata-notes" />
                                                                </td>
                                                                <td>
                                                                    <input class="form-control form-control-sm newdata newdata-rate" />
                                                                </td>
                                                                <td class="text-center" width="15%">
                                                                    <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="saveConcessionBid();"><i class="fa fa-check"></i></button>
                                                                    <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="cancelConcessionBid();"><i class="fa fa-ban"></i></button>
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
                                                    <apex:outputPanel id="concessionsBidPanel">
                                                        <table class="table table-sm">
                                                            <tbody>
                                                                <apex:repeat value="{!concessionsRequestedBid}" var="concessionRequested">
                                                                    <tr>
                                                                        <td width="7%">
                                                                            <span class="show-data">{!concessionRequested.Order__c}</span>
                                                                            <input class="form-control form-control-sm data order" style="display:none;" value="{!concessionRequested.Order__c}" />
                                                                        </td>
                                                                        <td width="12%">
                                                                            <span class="show-data">{!concessionRequested.Included_Excluded__c}</span>
                                                                            <select class="form-control form-control-sm data included" style="display:none;" data-value="{!concessionRequested.Included_Excluded__c}">
                                                                                <option value="">--Select--</option>
                                                                                <option value="Included">Included</option>
                                                                                <option value="Excluded">Excluded</option>
                                                                            </select>
                                                                        </td>
                                                                        <td width="18%">
                                                                            <input type="hidden" value="{!concessionRequested.Id}" class="id"  />
                                                                            <span class="show-data">{!IF(concessionRequested.Concessions_Requested__c != null,concessionRequested.Concessions_Requested__c,'-')}</span>
                                                                            <input type="hidden" class="data-original-requested" value="{!concessionRequested.Concessions_Requested__c}"  style="display:none;" />
                                                                            <input class="form-control form-control-sm data requested data-concession-search" style="display:none;" value="{!concessionRequested.Concessions_Requested__c}" />
                                                                        </td>
                                                                        <td width="43%">
                                                                            <span class="show-data">{!concessionRequested.Notes__c}</span>
                                                                            <input class="form-control form-control-sm data notes" style="display:none;" value="{!concessionRequested.Notes__c}" />
                                                                        </td>
                                                                        <td width="7%">
                                                                            <span class="show-data">{!concessionRequested.Rate__c}</span>
                                                                            <input class="form-control form-control-sm data rate money" style="display:none;" value="{!concessionRequested.Rate__c}" />
                                                                        </td>
                                                                        <td class="text-center" width="13%">
                                                                            <button type="button" class="btn btn-secondary btn-sm btn-custom btn-save" onclick="saveEditConcessionBid(this);" style="display:none;"><i class="fas fa-save"></i></button>
                                                                            <button type="button" class="btn btn-secondary btn-sm btn-custom btn-edit" onclick="editConcessionBid(this);"><i class="fas fa-edit"></i></button>
                                                                            <button type="button" class="btn btn-secondary btn-sm btn-custom btn-cancel" onclick="cancel(this);" style="display:none;"><i class="fa fa-times"></i></button>
                                                                            <button type="button" class="btn btn-secondary btn-sm btn-custom btn-delete" onclick="deleteConcessionBid('{!concessionRequested.Id}');"><i class="fa fa-times"></i></button>
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
                                        </div>
                                        <div class="col-md-6">
                                            <div class="row">
                                                <div class="col-md-12">
                                                    <strong>Options</strong>
                                                </div>
                                            </div>
                                            <div class="row">
                                                <div class="col-md-12">
                                                    <div class="card">
                                                        <div class="card-body">
                                                            <div class="row">
                                                                <div class="col-md-3">
                                                                    <strong>Option Number #:</strong>
                                                                </div>
                                                                <div class="col-md-9">
                                                                    <div class="form-group row">
                                                                        <div class="col-sm-2">
                                                                            <apex:inputField id="bidRevenue_optionsInput" value="{!bidData.Options__c}" styleClass="form-control"/>
                                                                        </div>
                                                                        <div class="col-sm-10">
                                                                            <button type="button" class="btn btn-danger btn-sm" onclick="congaPreviewOptions('{!bidData.id}', '{!bidData.Status__c}', '{!bidData.GT__c}', '{!JSENCODE(previewBidOptions_congaQueriesJson)}', '{!previewBidOptions_congaTemplateId}')">Preview Options</button>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="row">
                                                                <div class="col-md-3">
                                                                    <button type="button" class="btn btn-danger btn-sm" onclick="soldOutBidStatus()" >Sold Out</button>
                                                                </div>
                                                                <div class="col-md-9">
                                                                    <div class="form-group">
                                                                        <apex:outputLabel value="No Bid Reason:" for="bidRevenue_noBidReasonInput" style="font-weight:bold;"/>
                                                                        <apex:inputField id="bidRevenue_noBidReasonInput" value="{!bidData.No_Bid_reason__c}" styleClass="form-control"/>
                                                                    </div>
                                                                </div>
                                                                <div class="col-md-12">
                                                                    <div class="form-group">
                                                                        <apex:outputLabel value="Internal Notes" for="bidRevenue_internalNotesInput" style="font-weight:bold;"/>
                                                                        <apex:inputField id="bidRevenue_internalNotesInput" value="{!bidData.Internal_notes__c}" styleClass="form-control"/>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
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
                    <button type="button" class="btn btn-danger btn-sm" onclick="deactivateBid();" style="{!IF(bidData.Status__c <> 'Contracted','','display:none;')}">Deactivate Bid</button>
                    <button type="button" class="btn btn-danger btn-sm" onclick="save();">Save</button>
                    <button type="button" class="btn btn-danger btn-sm" onclick="congaPreviewBid('{!bidData.id}', '{!bidData.Name}', '{!bidData.Status__c}', '{!bidData.GT__c}', '{!JSENCODE(resendBidAgreement_congaQueriesJson)}', '{!resendBidAgreement_congaTemplateId}')">Preview Bid</button>
                    <button type="button" class="btn btn-danger btn-sm" onclick="openBidAgreementJs('Trip Details Update');" style="{!IF(bidData.Status__c == 'Contracted','','display:none;')}">Trip Details Update</button>
                    <button type="button" class="btn btn-danger btn-sm" onclick="openBidAgreementJs('Rate Agreement');" style="{!IF(bidData.Status__c == 'Contracted','','display:none;')}">Rate Agreement</button>
                    <button type="button" class="btn btn-danger btn-sm" onclick="openBidAgreementJs('Transportation Contract');" style="{!IF(bidData.Status__c == 'Contracted','','display:none;')}">Transportation Contract</button>
                    <button type="button" class="btn btn-danger btn-sm" onclick="openResendBidJs();">Resend Bid</button>
                    <button type="button" class="btn btn-danger btn-sm" onclick="openReleaseByBid();" style="{!If(bidData.Status__c != 'Contracted' && bidData.Status__c != 'Cancelled' && bidData.Status__c != 'Contracted On Own' && bidData.Status__c != 'Bid Released', 'display:none;', '')}">Release Bid</button>
                    <span id="saveMessage" class="saveMessage" style="display:none;">Saved Successfully</span>
                </div>
            </div>
        </div>
    </apex:outputPanel>
    
    <!-- Modal content-->
    <div class="modal fade myModalBidAgreement" id="myModalBidAgreement" role="dialog">
        <apex:outputPanel id="myModalBidAgreement" layout="block" styleClass="modal-dialog modal-xl">
            <!-- Modal content-->
            <apex:outputPanel layout="block" rendered="{!isBidAgreementRendered}" styleClass="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title">{!bidAgreement_type}</h4>
                    <apex:inputHidden id="bidJournal_recordtype" value="{!journal_bidjournalRT}"/>
                    <apex:inputHidden id="bidAgreement_congaEmailFromId" value="{!bidAgreement_congaEmailFromId}"/>
                    <button type="button" class="close" data-dismiss="modal">&times;</button>
                </div>
                <div class="modal-body" style="font-size:12px;padding-top: 0px;">
                    <apex:outputPanel id="BidAgreementPanel">
                        <apex:outputPanel layout="block" rendered="{!bidAgreement_type != 'Trip Details Update'}" styleClass="row">
                            <div class="col-md-12">
                                <div class="fieldset" style="margin-top: 0 !important;">
                                    <div class="row" style="margin-top: 0 !important;">
                                        <div class="col-md-6">
                                            Trip ID : <strong>{!bidData.GT__r.Name}</strong>&nbsp;&nbsp;&nbsp;Production ID : <strong>{!bidData.Production__r.Production_ID__c}</strong>
                                        </div>
                                        <div class="col-md-6 text-right">
                                            Bid ID : <strong>{!bidData.Name}</strong>&nbsp;&nbsp;&nbsp;Vendor ID: <strong>{!bidData.Vendor__r.Vendor_ID__c}</strong>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </apex:outputPanel>
                        <apex:outputPanel layout="block" rendered="{!bidAgreement_type == 'Trip Details Update'}" styleClass="row">
                            <div class="col-md-12">
                                <div class="fieldset" style="margin-top: 0 !important;">
                                    <div class="row" style="margin-top: 0 !important;">
                                        <div class="col-md-3">
                                            <div class="row">
                                                <div class="col-md-12">
                                                    <apex:outputLabel value="Vendor :" for="bidAgreementAttentionVendorLink"/>
                                                </div>
                                                <div class="col-md-12">
                                                    <apex:outputLink id="bidAgreementAttentionVendorLink" value="/{!bidData.Vendor__c}">{!bidData.Vendor__r.Name}</apex:outputLink>
                                                </div>
                                            </div>
                                        </div>
                                        <div class="col-md-3">
                                            <apex:outputLabel value="Attention: " for="bidAgreementAttentionContactSelect" style="font-weight:bold;"/>
                                            <apex:selectList size="1" id="bidAgreementAttentionContactSelect" styleClass="form-control form-control-sm" value="{!draft.Attention__c}">
                                                <apex:selectOptions value="{!contactsBidsByVendor}"/>
                                                <apex:actionSupport event="onchange" action="{!changeBidAgreementAttentionContact}" status="loading" reRender="bidAgreementAttentionContactTitleLink,bidAgreementAttentionContactEmailLink,bidAgreementToPanel,bidAgreement_salutation"/>
                                            </apex:selectList>
                                        </div>
                                        <div class="col-md-3">
                                            <div class="row">
                                                <div class="col-md-12">
                                                    <apex:outputLabel value="Title :" for="bidAgreementAttentionContactTitleLink"/>
                                                </div>
                                                <div class="col-md-12">
                                                    <apex:outputLink id="bidAgreementAttentionContactTitleLink" value="/{!bidAgreementAttentionContact.id}" target="_blank">{!bidAgreementAttentionContact.Title}</apex:outputLink>
                                                </div>
                                            </div>
                                        </div>
                                        <div class="col-md-3">
                                            <div class="row">
                                                <div class="col-md-12">
                                                    <apex:outputLabel value="Email :" for="bidAgreementAttentionContactEmailLink"/>
                                                </div>
                                                <div class="col-md-12">
                                                    <apex:outputLink id="bidAgreementAttentionContactEmailLink" value="mailto:{!bidAgreementAttentionContact.Email}">{!bidAgreementAttentionContact.Email}</apex:outputLink>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </apex:outputPanel>
                        <apex:outputPanel layout="block" rendered="{!bidAgreement_type != 'Trip Details Update'}" styleClass="row">
                            <div class="col-md-6">
                                <div class="fieldset" style="height: 200px;margin-top: 0 !important;">
                                    <div class="row" style="margin-top: 0 !important;">
                                        <div class="col-md-3">
                                            Vendor :
                                        </div>
                                        <div class="col-md-9">
                                            <a href="/{!bidData.Vendor__c}" target="_blank">{!bidData.Vendor__r.Name}</a>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-3">
                                            Address : 
                                        </div>
                                        <div class="col-md-9">
                                            <span style="font-weight:bold;"><apex:outputText value="{!SUBSTITUTE(bidData.Vendor_Address__c,'<br>',', ')}" escape="true" /></span>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-3">
                                            Contact :
                                        </div>
                                        <div class="col-md-9">
                                            <apex:selectList size="1" id="bidAgreementContactSelect" styleClass="form-control form-control-sm" value="{!draft.Primary_Contact_Id__c}">
                                                <apex:selectOptions value="{!contactsBidsByVendor}"/>
                                                <apex:actionSupport event="onchange" action="{!changeBidAgreementContactPrimary}" status="loading" reRender="bidAgreementContactPanel,bidAgreementToPanel,bidAgreement_salutation"/>
                                            </apex:selectList>
                                        </div>
                                    </div>
                                    <apex:outputPanel id="bidAgreementContactPanel">
                                        <div class="row">
                                            <div class="col-md-3">
                                                Phone : 
                                            </div>
                                            <div class="col-md-9">
                                                <a href="{!bidAgreementPrimaryContact.Phone}">{!bidAgreementPrimaryContact.Phone}</a>
                                            </div>
                                        </div>
                                        <div class="row">
                                            <div class="col-md-3">
                                                Email : 
                                            </div>
                                            <div class="col-md-9">
                                                <a href="mailto:{!bidAgreementPrimaryContact.Email}">{!bidAgreementPrimaryContact.Email}</a>
                                            </div>
                                        </div>
                                    </apex:outputPanel>
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="fieldset" style="height: 200px;margin-top: 0 !important;">
                                    <div class="row" style="margin-top: 0 !important;">
                                        <div class="col-md-3">
                                            Production :
                                        </div>
                                        <div class="col-md-9">
                                            <input type="text" value="{!bidData.Production__r.Name}" class="form-control form-control-sm" />
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-3">
                                            Company : 
                                        </div>
                                        <div class="col-md-9">
                                            {!bidData.Production__r.Account.Name}
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-3">
                                            Address : 
                                        </div>
                                        <div class="col-md-9">
                                            <span style="font-weight:bold;">
                                                <apex:outputText value="{!SUBSTITUTE(bidData.Production__r.Account.Physical_Address__c,'<br>',', ')}" escape="true" />
                                            </span>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-3">
                                            Contact : 
                                        </div>
                                        <div class="col-md-9">
                                            <apex:selectList size="1" id="bidAgreementProductionAssociationContactsSelect" styleClass="form-control form-control-sm" value="{!draft.Production_Assoc_Contact_Id__c}">
                                                <apex:selectOptions value="{!BidAgreementProductionAssociationContacts}" />
                                            </apex:selectList>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </apex:outputPanel>
                        <div class="row">
                            <div class="col-md-12">
                                <div class="fieldset" style="margin-top: 0 !important;">
                                    <table style="width:100%" cellspacing="0" cellpadding="0">
                                        <tr>
                                            <td style="width:10%;padding: 5px 0 5px 0;">To :</td>
                                            <td style="width:90%;padding: 5px 0 5px 0;">
                                                <apex:outputPanel id="bidAgreementToPanel">
                                                    <div id="bidAgreement_primarycontactemail" class="bidAgreement-to">
                                                        <apex:outputText value="{!bidAgreementPrimaryContact.Email}" rendered="{!bidAgreement_type != 'Trip Details Update'}"/>
                                                        <apex:outputText value="{!bidAgreementAttentionContact.Email}" rendered="{!bidAgreement_type == 'Trip Details Update'}"/>
                                                    </div>
                                                </apex:outputPanel>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td style="vertical-align:top;padding: 5px 0 5px 0;"> CC :</td>
                                            <td style="padding: 5px 0 5px 0;">
                                                <div class="all-cc-email-bidAgreement"></div>
                                                <input type="text" class="form-control form-control-sm cc-email-bidAgreement" />
                                            </td>
                                        </tr>
                                        <tr>
                                            <td style="vertical-align:top;padding: 5px 0 5px 0;">BCC :</td>
                                            <td style="padding: 5px 0 5px 0;">
                                                <div class="all-bcc-email-bidAgreement"></div>
                                                <input type="text" class="form-control form-control-sm bcc-email-bidAgreement" />
                                            </td>
                                        </tr>
                                        <tr>
                                            <td style="vertical-align:top;padding: 5px 0 5px 0;">Subject :</td>
                                            <td style="padding: 5px 0 5px 0;">
                                                <apex:inputField id="bidAgreement_subject" value="{!draft.Subject__c}" styleClass="form-control form-control-sm subject-bidAgreement" /> 
                                            </td>
                                        </tr>
                                    </table>
                                    <table style="width:100%" cellspacing="0" cellpadding="0">
                                        <tr>
                                            <td style="width:30%;padding: 5px 0 5px 0;">
                                                Attached: <br/>
                                                <apex:selectList size="4" id="bidAgreement_attachs" style="width:100%;" />
                                            </td>
                                            <td style="padding: 5px;vertical-align: top;padding-top: 25px;">
                                                <button type="button" class="btn btn-secondary btn-custom" onclick="removeAttachDocs('bidAgreement_attachs');" style="float: left;margin-right: 5px;">Remove</button>
                                                <div class="upload-btn-wrapper" style="display: block;float: left;margin-right: 5px;">
                                                    <button class="btn btn-secondary btn-custom" onclick="javascript:void(0);">Attach</button>
                                                    <input type="file" id="fileBidAgreement" onchange="remoteLocationPostLast(event,'Rate Agreement','bidAgreement_attachs', '{!bidData.Id}');" />
                                                </div>
                                                <button type="button" class="btn btn-secondary btn-custom" onclick="openAttachDocs('bid','{!bidData.Id}','myModalBidAgreement','bidAgreement_attachs');">Attach Contracting Docs</button>
                                                <apex:inputHidden value="{!body}" id="output"/>
                                                <input type="hidden" id="attachment_new_charge"/>
                                                <apex:outputPanel id="newAttachmentPanel">
                                                    <input type="hidden" id="attachment_new_id" value="{!newattachment_id}" />
                                                    <input type="hidden" id="attachment_new_name" value="{!newattachment_name}" />
                                                </apex:outputPanel>
                                            </td>
                                        </tr>
                                    </table>
                                    <table style="width:100%" cellspacing="0" cellpadding="0">
                                        <tr>
                                            <td style="width:10%;vertical-align:top;padding: 5px 0 5px 0;">Salutation :</td>
                                            <td style="width:90%;padding: 5px 0 5px 0;">
                                                <apex:inputField id="bidAgreement_salutation" value="{!draft.Salutation__c}" styleClass="form-control form-control-sm"/>
                                            </td>
                                        </tr>
                                    </table>
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-12">
                                <label>Message Body</label>
                                <apex:inputTextarea id="bidAgreement_message" value="{!bidAgreement_message}" rows="5" styleClass="form-control form-control-sm" />
                                <script>
                                CKEDITOR.replace('{!$Component.bidAgreement_message}', {
                                    language: 'en',
                                    extraAllowedContent: 'th{color,background,background-color}'
                                });
                                </script>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-12">
                                <h2>
                                    <strong>Trip Details</strong>
                                </h2>
                            </div>
                        </div>
                        <apex:repeat value="{!bidAgreementSubTrips}" var="bidSubTrip">
                            <div class="row">
                                <div class="col-md-12">
                                    <div class="accordion" id="accordionFive">
                                        <div class="card">
                                            <div class="card-header" id="headingFive">
                                                <h2 class="mb-0">
                                                    Trip {!bidSubTrip.Trip_Order__c}
                                                    <span style="float:right;">
                                                        <a href="javascript:void(0);" onclick="checkIcon(this,'collapseBidSubTrips-{!bidSubTrip.Trip_Order__c}');">
                                                            <i class="fa fa-angle-up btn-show"></i>
                                                        </a>
                                                    </span>
                                                </h2>
                                            </div>
                                            <div id="collapseBidSubTrips-{!bidSubTrip.Trip_Order__c}" class="collapse show" aria-labelledby="headingFive" data-parent="#accordionFive">
                                                <div class="card-body card-body-trip card-body-{!bidSubTrip.Trip_Order__c}" style="min-height: 235px;">
                                                    <div class="row" style="margin-top:0 !important;">
                                                        <div class="col-md-2">
                                                            <label style="font-weight:bold;">Trip Type</label><br/>
                                                            <apex:outputField value="{!bidSubTrip.Sub_Trip_Type__c}" styleClass="form-control form-control-sm"  />
                                                        </div>
                                                        <div class="col-md-4">
                                                            <label style="font-weight:bold;">Description</label><br/>
                                                            <apex:outputField value="{!bidSubTrip.Description__c}" styleClass="form-control form-control-sm"  />
                                                        </div>
                                                        <div class="col-md-6">
                                                        </div>
                                                    </div>
                                                    <div class="row">
                                                        <div class="col-md-12">
                                                            <span style="font-weight:bold;">Travel Information</span>
                                                        </div>
                                                    </div>
                                                    <div class="row">
                                                        <div class="col-md-12">
                                                            <apex:outputPanel id="travelsByTripPanel">
                                                                <table class="table" style="padding: 5px;margin-bottom:0;">
                                                                    <thead>
                                                                        <tr>
                                                                            <th width="10%">Vehicle</th>
                                                                            <th width="8%">Start Date</th>
                                                                            <th width="7%">Time</th>
                                                                            <th width="8%">End Date</th>
                                                                            <th width="7%">Time</th>
                                                                            <th width="7%">Type</th>
                                                                            <th width="7%">Group</th>
                                                                            <th width="7%">Location Pick Up Type</th>
                                                                            <th width="7%">Location Pick Up Details</th>
                                                                            <th width="7%">Location Drop Off Type</th>
                                                                            <th width="7%">Location Drop Off Details</th>
                                                                            <th width="18%">Airline Info/Special Notes</th>
                                                                        </tr>
                                                                    </thead>
                                                                    <tbody>
                                                                        <apex:repeat value="{!bidSubTrip.GTTravels__r}" var="bidTravel">
                                                                            <tr>
                                                                                <td>
                                                                                    <apex:outputField value="{!bidTravel.Vehicle_Ref__c}" styleClass="form-control form-control-sm"/>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputField value="{!bidTravel.Start_Date__c}" styleClass="form-control form-control-sm"/>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputField value="{!bidTravel.Start_Date_Time__c}" styleClass="form-control form-control-sm"/>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputField value="{!bidTravel.End_Date__c}" styleClass="form-control form-control-sm"/>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputField value="{!bidTravel.End_Date_Time__c}" styleClass="form-control form-control-sm"/>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputField value="{!bidTravel.Travel_Type__c}" styleClass="form-control form-control-sm"/>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputField value="{!bidTravel.Group_Type__c}" styleClass="form-control form-control-sm"/>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputField value="{!bidTravel.Location_Type__c}" styleClass="form-control form-control-sm"/>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputField value="{!bidTravel.Location_Details__c}" styleClass="form-control form-control-sm"/>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputField value="{!bidTravel.Location_Drop_Off_Type__c}" styleClass="form-control form-control-sm"/>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputField value="{!bidTravel.Location_Details_Drop_Off__c}" styleClass="form-control form-control-sm"/>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputField value="{!bidTravel.Airline_Info_Special_Notes__c}" styleClass="form-control form-control-sm"/>
                                                                                </td>
                                                                            </tr>
                                                                        </apex:repeat>
                                                                    </tbody>
                                                                </table>
                                                            </apex:outputPanel>
                                                        </div>
                                                    </div>
                                                    <div class="row">
                                                        <div class="col-md-12">
                                                            <label style="font-weight:bold;">Trip Notes</label>
                                                            <apex:outputField value="{!bidSubTrip.Sub_Trip_Notes__c}" styleClass="form-control form-control-sm" />
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </apex:repeat>
                        <div class="row">
                            <div class="col-md-12">
                                <h2>
                                    <strong>Vehicle Information</strong>
                                </h2>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-12">
                                <div class="card">
                                    <div class="card-body">
                                        <div class="row">
                                            <div class="col-md-12">
                                                <table class="table" style="padding: 5px;margin-bottom:0;">
                                                    <thead>
                                                        <tr>
                                                            <th width="15%">Vehicle</th>
                                                            <th width="15%">Vehicle Type</th>
                                                            <th width="10%">Capacity</th>
                                                            <th width="10%">Make</th>
                                                            <th width="10%">Model</th>
                                                            <th width="10%">Year</th>
                                                            <th width="15%">Amenities</th>
                                                        </tr>
                                                    </thead>
                                                    <tbody>
                                                        <apex:repeat value="{!bidAgreementVehicles}" var="bidVehicle">
                                                            <tr>
                                                                <td>
                                                                    <apex:outputField value="{!bidVehicle.Vehicle_Ref__c}"/>
                                                                </td>
                                                                <td>
                                                                    <apex:outputField value="{!bidVehicle.Vehicle_Type__c}"/>
                                                                </td>
                                                                <td>
                                                                    <apex:outputField value="{!bidVehicle.Capacity__c}"/>
                                                                </td>
                                                                <td>
                                                                    <apex:outputField value="{!bidVehicle.Make__c}"/>
                                                                </td>
                                                                <td>
                                                                    <apex:outputField value="{!bidVehicle.Model__c}"/>
                                                                </td>
                                                                <td>
                                                                    <apex:outputField value="{!bidVehicle.Year__c}"/>
                                                                </td>
                                                                <td>
                                                                    <apex:outputField value="{!bidVehicle.Amenities__c}"/>{!IF(!ISNULL(bidVehicle.Other_Amenities__c), ',' + bidVehicle.Other_Amenities__c, '')}
                                                                </td>
                                                            </tr>
                                                        </apex:repeat>
                                                    </tbody>
                                                </table>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-12">
                                <h2>
                                    <strong>Payment info:</strong>
                                </h2>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-12">
                                <div class="card">
                                    <div class="card-body">
                                        <div class="row">
                                            <div class="col-md-4">
                                                <div class="form-group">
                                                    <apex:outputLabel value="Total Trip Price:" for="bidAgreementRevenue_totalPriceInput" style="font-weight:bold;"/>
                                                    <apex:outputField id="bidAgreementRevenue_totalPriceInput" value="{!bidAgreementRevenue.Total_Price__c}" styleClass="form-control"/>
                                                </div>
                                                <div class="form-group">
                                                    <apex:outputLabel value="Gratuity:" for="bidAgreementRevenue_gratuityInput" style="font-weight:bold;"/>
                                                    <apex:outputField id="bidAgreementRevenue_gratuityInput" value="{!bidAgreementRevenue.Gratuity__c}" styleClass="form-control"/>
                                                </div>
                                                <div class="form-group">
                                                    <apex:outputLabel value="Additional Fees:" style="font-weight:bold;"/>
                                                    <apex:repeat value="{!bidAgreementConcessions}" var="bidConcession"><p>{!bidConcession.Included_Excluded__c + ' - ' + bidConcession.Concessions_Requested__c + ' - ' + bidConcession.Rate__c}</p></apex:repeat>
                                                </div>
                                                <apex:outputPanel layout="block" rendered="{!bidAgreement_type == 'Transportation Contract'}" styleClass="form-group">
                                                    <apex:outputLabel value="Credit Card Information:" style="font-weight:bold;"/>
                                                    <apex:selectList size="1" id="bidAgreementCreditCardsSelect" styleClass="form-control form-control-sm" value="{!draft.Credit_Card_Id__c}">
                                                        <apex:selectOptions value="{!BidAgreementCreditCards}"/>
                                                    </apex:selectList>
                                                </apex:outputPanel>
                                            </div>
                                            <div class="col-md-4">
                                                <div class="form-group">
                                                    <apex:outputLabel value="Payment Policy:" for="bidAgreementRevenue_paymentPolicyInput" style="font-weight:bold;"/>
                                                    <apex:inputTextarea id="bidAgreementRevenue_paymentPolicyInput" value="{!draft.Payment_Policy__c}" styleClass="form-control"/>
                                                </div>
                                            </div>
                                            <div class="col-md-4">
                                                <div class="form-group">
                                                    <apex:outputLabel value="Cancellation Policy:" for="bidAgreementRevenue_cancellationPolicyInput" style="font-weight:bold;"/>
                                                    <apex:inputTextarea id="bidAgreementRevenue_cancellationPolicyInput" value="{!draft.Cancellation_Policy__c}" styleClass="form-control"/>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <apex:outputPanel layout="block" rendered="{!bidAgreement_type != 'Trip Details Update'}" styleClass="row">
                            <div class="col-md-12">
                                <label style="font-weight:bold;">Terms</label>
                                <apex:inputTextarea id="bidAgreement_terms" value="{!bidAgreement_terms}" rows="5" styleClass="form-control form-control-sm" />
                                <script>
                                CKEDITOR.replace('{!$Component.bidAgreement_terms}', {
                                    language: 'en',
                                    extraAllowedContent: 'th{color,background,background-color}'
                                });
                                </script>
                            </div>
                        </apex:outputPanel>
                        <apex:outputPanel id="bidAgreementAuditFields" layout="block" styleClass="row" style="margin-top: 1rem !important;">
                            <div class="col">
                                <div class="row" style="margin-top: 0 !important;">
                                    <div class="col-md-5" style="text-align: right;">Created By :</div>
                                    <div class="col" style="padding: 0;">
                                        <strong>{!draft.CreatedBy.Name}</strong>
                                    </div>
                                </div>
                                <div class="row" style="margin-top: 0 !important;">
                                    <div class="col-md-5" style="text-align: right;">Modified By :</div>
                                    <div class="col" style="padding: 0;">
                                        <strong>{!draft.LastModifiedBy.Name}</strong>
                                    </div>
                                </div>
                            </div>
                            <div class="col">
                                <div class="row" style="margin-top: 0 !important;">
                                    <div class="col-md-5" style="text-align: right;">Created On :</div>
                                    <div class="col" style="padding: 0;">
                                        <b>
                                            <apex:outputField value="{!draft.CreatedDate}"/>
                                        </b>
                                    </div>
                                </div>
                                <div class="row" style="margin-top: 0 !important;">
                                    <div class="col-md-5" style="text-align: right;">Modified On :</div>
                                    <div class="col" style="padding: 0;">
                                        <b>
                                            <apex:outputField value="{!draft.LastModifiedDate}"/>
                                        </b>
                                    </div>
                                </div>
                            </div>
                            <div class="col">
                                <div class="row" style="margin-top: 0 !important;">
                                    <div class="col-md-5" style="text-align: right;">Sent By :</div>
                                    <div class="col" style="padding: 0;">
                                        <b>
                                            <apex:outputField value="{!bidData.Rate_Agreement_Last_Send_By__c}" rendered="{!bidAgreement_type = 'Rate Agreement'}"/>
                                            <apex:outputField value="{!bidData.Trip_Details_Update_Last_Send_By__c}" rendered="{!bidAgreement_type = 'Trip Details Update'}"/>
                                            <apex:outputField value="{!bidData.Transportation_Contract_Last_Send_By__c}" rendered="{!bidAgreement_type = 'Transportation Contract'}"/>
                                        </b>
                                    </div>
                                </div>
                            </div>
                            <div class="col">
                                <div class="row" style="margin-top: 0 !important;">
                                    <div class="col-md-5" style="text-align: right;">Sent On :</div>
                                    <div class="col" style="padding: 0;">
                                        <b>
                                            <apex:outputField value="{!bidData.Rate_Agreement_Last_Send_Date__c}" rendered="{!bidAgreement_type = 'Rate Agreement'}"/>
                                            <apex:outputField value="{!bidData.Trip_Details_Update_Last_Send_Date__c}" rendered="{!bidAgreement_type = 'Trip Details Update'}"/>
                                            <apex:outputField value="{!bidData.Transportation_Contract_Last_Send_Date__c}" rendered="{!bidAgreement_type = 'Transportation Contract'}"/>
                                        </b>
                                    </div>
                                </div>
                            </div>
                        </apex:outputPanel>
                    </apex:outputPanel>
                </div>
                <div class="modal-footer" style="display: block;">
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="deactivateBidAgreement();" >Deactivate</button>
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="saveBidAgreement();" >Save</button>
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="congaSendBidAgreementHandler();" >Send Email</button>
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="congaPreviewBidAgreementHandler();" >Preview</button>
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="congaSignBidAgreementHandler();" >Send Signer</button>
                    <span id="saveBidAgreementMessage" class="saveMessage" style="display:none;">Saved Successfully</span>
                </div>
            </apex:outputPanel>
        </apex:outputPanel>
    </div>
    <!-- End Modal -->
    <!-- Modal content-->
    <div class="modal fade" id="myModalResendBid" role="dialog" style="padding-right: 18px;">
        <apex:outputPanel id="myModalResendBid" layout="block" styleClass="modal-dialog modal-xl">
            <!-- Modal content-->
            <apex:outputPanel layout="block" rendered="{!isResendBidRendered}" styleClass="modal-content group-vendor">
                <div class="modal-header">
                    <h4 class="modal-title">Resend Bid to Vendor Contacts</h4>
                    <button type="button" class="close" onclick="closeBidModalJs('myModalResendBid');">&times;</button>
                </div>
                <apex:outputPanel id="resendBidPanel">
                    <div class="modal-body" style="font-size:12px;">
                        <div class="fieldset" style="font-size: 12px;">
                            <div class="row" style="margin-top: 5px !important;">
                                <div class="col-md-4">
                                    <a href="/{!bidData.Vendor__c}" target="_blank">{!bidData.Vendor__r.Name}</a>
                                </div>
                                <div class="col-md-2">
                                    Select Primary Contact
                                </div>
                                <div class="col-md-3">
                                    <apex:selectList size="1" id="resendbid_contactprimary" value="{!resendBidAgreement_contactPrimary}" onchange="changeContactVendorResendBid(this,'{!bidData.Vendor__c}');" styleClass="form-control form-control-sm primary-contact">
                                        <apex:selectOptions value="{!contactSelectOptionBidMap[bidData.Vendor__c]}" />
                                    </apex:selectList>
                                    <script>
                                    if('{!bidData.Vendor_Contact__c}' != ''){
                                        $("select[id$=resendbid_contactprimary] option").each(function(){
                                            if($(this).val() == '{!bidData.Vendor_Contact__c}'){        
                                                $(this).attr('selected',true);
                                            }
                                        });
                                    }
                                    </script>
                                </div>
                                <div class="col-md-3">
                                    <button type="button" class="btn btn-danger btn-sm" onclick="congaPreviewResendBid('{!itineraryId}', '{!bidData.GT__c}', '{!bidData.GT__r.Status_Ground__c}', '{!bidData.Id}', '{!bidData.Name}', '{!bidData.Status__c}', '{!JSENCODE(resendBidAgreement_congaQueriesJson)}', '{!JSENCODE(resendBidAgreement_congaEmailSubject)}', '{!resendBidAgreement_congaEmailTemplateId}', '{!resendBidAgreement_congaTemplateId}')">Preview</button>
                                    <button type="button" class="btn btn-danger btn-sm" onclick="openContactVendor('{!bidData.Vendor__c}','{!bidData.Vendor__r.Name}','');">Add Contact</button>
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
                                        <apex:repeat value="{!contactsByVendorParentBidMap[bidData.Vendor__r.ParentId]}" var="contact1" rendered="{!IF(bidData.Vendor__r.ParentId <> null,true,false)}">
                                            <tr>
                                                <td data-contactid="{!contact1.c.Id}" data-contactemail="{!contact1.c.email}">
                                                    <apex:inputCheckbox value="{!contact1.selected}" disabled="{!contact1.disabled}" styleClass="form-check-input check-contact" style="margin-left: 10px;" />
                                                </td>
                                                <td>{!contact1.c.Order__c} NR</td>
                                                <td><a href="javascript:void(0);" onclick="openContactVendor('{!contact1.c.AccountId}','{!contact1.c.Account.Name}','{!contact1.c.Id}');">{!contact1.c.Name}</a></td>
                                                <td>{!contact1.c.Designation_title__c}</td>
                                                <td><a href="tel:{!contact1.c.Phone}">{!contact1.c.Phone}</a></td>
                                                <td><a href="mailto:{!contact1.c.Email}">{!contact1.c.Email}</a></td>
                                                <td>{!contact1.c.Fax}</td>
                                            </tr>
                                        </apex:repeat>
                                        <apex:repeat value="{!contactsByVendorBidMap[bidData.Vendor__c]}" var="contact1" rendered="{!IF(bidData.Vendor__c <> null, true, false)}">
                                            <tr>
                                                <td data-contactid="{!contact1.c.Id}" data-contactemail="{!contact1.c.email}">
                                                    <apex:inputCheckbox value="{!contact1.selected}" disabled="{!contact1.disabled}" styleClass="form-check-input check-contact" style="margin-left: 10px;" />
                                                </td>
                                                <td>{!contact1.c.Order__c}</td>
                                                <td><a href="javascript:void(0);" onclick="openContactVendor('{!contact1.c.AccountId}','{!contact1.c.Account.Name}','{!contact1.c.Id}');">{!contact1.c.Name}</a></td>
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
                    <div class="modal-footer" style="display: block;">
                        <button type="button" class="btn btn-danger btn-sm" onclick="congaResendBid()" >Send PDF</button>
                        <button type="button" class="btn btn-danger btn-sm" onclick="sendResendBid();" >Send Link</button>
                        <button type="button" class="btn btn-danger btn-sm" onclick="openPreviewResendLink(this,'{!bidData.Id}','{!bidData.Vendor__c}','{!bidData.Vendor__r.Name}','link');">Preview Link</button>
                        
                    </div>
                </apex:outputPanel>
            </apex:outputPanel>
        </apex:outputPanel>
    </div>
    <!-- End Modal -->
    <!-- Modal content-->
    <div class="modal fade" id="myModalAddContactVendor" role="dialog">
        <div class="modal-dialog modal-lg">
            <!-- Modal content-->
            <div class="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title">Add New Contact for</h4>
                    <button type="button" class="close" onclick="viewModalIndex('myModalResendBid');viewModalIndex('myModalReleaseByBid');closeModal('myModalAddContactVendor');">&times;</button>
                </div>
                <div class="modal-body" style="font-size:12px;padding-top: 0px;">
                    <div class="row">
                        <div class="col-md-12">
                            <button type="button" class="btn btn-danger btn-sm" onclick="saveAddContactVendorBid();" >Save</button>
                            <input type="hidden" id="addcontact_accountid" />
                            <input type="hidden" id="addcontact_contactid" />
                        </div>
                    </div>
                    <apex:outputPanel id="addContactVendorMessagePanel">
                        <div class="row message-create-contact-vendor" style="{!IF(messageCreateContact <> '','','display:none;')}">
                            <div class="col-md-12">
                                <div class="alert alert-danger" role="alert">
                                    {!messageCreateContact}
                                    <input type="hidden" id="addcontactvendor_message" value="{!messageCreateContact}" />
                                </div>
                            </div>
                        </div>
                    </apex:outputPanel>
                    <div class="row">
                        <div class="col-md-6">
                            <label>First Name</label>
                            <input type="text" id="addcontact_firstname" class="form-control form-control-sm" />
                        </div>
                        <div class="col-md-6">
                            <label>Last Name</label>
                            <input type="text" id="addcontact_lastname" class="form-control form-control-sm" />
                        </div>
                    </div>
                    <div class="row">
                        <div class="col-md-6">
                            <label>Designation/Title</label>
                            <apex:selectList id="addcontact_designation" size="1" styleClass="form-control form-control-sm newdata">
                                <apex:selectOptions value="{!contact_DesignationTitle}" />
                            </apex:selectList>
                        </div>
                        <div class="col-md-6"></div>
                    </div>
                    <div class="row">
                        <div class="col-md-6">
                            <label>Work Phone</label>
                            <input type="text" id="addcontact_phone" class="form-control form-control-sm" />
                        </div>
                        <div class="col-md-6">
                            <label>Work Phone Extension</label>
                            <input type="text" id="addcontact_extension" class="form-control form-control-sm" />
                        </div>
                    </div>
                    <div class="row">
                        <div class="col-md-6">
                            <label>Mobile</label>
                            <input type="text" id="addcontact_mobile" class="form-control form-control-sm" />
                        </div>
                        <div class="col-md-6">
                            <label>Fax</label>
                            <input type="text" id="addcontact_fax" class="form-control form-control-sm" />
                        </div>
                    </div>
                    <div class="row">
                        <div class="col-md-6">
                            <label>Email</label>
                            <input type="text" id="addcontact_email" class="form-control form-control-sm" />
                        </div>
                        <div class="col-md-6">
                            <label>Alternate Email</label>
                            <input type="text" id="addcontact_alternateemail" class="form-control form-control-sm" />
                        </div>
                    </div>
                    <div class="row">
                        <div class="col-md-6">
                            <label>Internal Notes</label>
                            <textarea id="addcontact_internalnotes" class="form-control form-control-sm" rows="3" />
                        </div>
                        <div class="col-md-6"></div>
                    </div>
                    <div class="row">
                        <div class="col-md-6">
                            <label>Home Address Line 1</label>
                            <input type="text" id="addcontact_address1" class="form-control form-control-sm" />
                        </div>
                        <div class="col-md-6">
                            <label>Home Address Line 2</label>
                            <input type="text" id="addcontact_address2" class="form-control form-control-sm" />
                        </div>
                    </div>
                    <div class="row">
                        <div class="col-md-6">
                            <label>City</label>
                            <input type="text" id="addcontact_city" class="form-control form-control-sm addContactCitySearch"/>
                            <input type="hidden" id="addcontact_cityid" />
                        </div>
                        <div class="col-md-6">
                            <label>Postal Code</label>
                            <input type="text" id="addcontact_postalcode" class="form-control form-control-sm" />
                        </div>
                    </div>
                    <div class="row">
                        <div class="col-md-12">
                            <button type="button" class="btn btn-danger btn-sm" onclick="saveAddContactVendorBid();" >Save</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- End Modal -->
    <!-- Modal content-->
    <div class="modal fade" id="myModalAttachDocuments" role="dialog">
        <div class="modal-dialog modal-lg">
            <apex:outputPanel layout="block" rendered="{!tripBidNumber != null}" styleClass="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title">Documents</h4>
                    <input type="hidden" id="attachdocument_modal" />
                    <input type="hidden" id="attachdocument_select_id" />
                    <button type="button" class="close" onclick="viewModalIndex('myModalBidAgreement');viewModalIndex('myModalPreviewPdf');closeModal('myModalAttachDocuments');">&times;</button>
                </div>
                <div class="modal-body" style="font-size:12px;">
                    <input type="hidden" id="document-attach-ids" />
                    <input type="hidden" id="document-attach-names" />
                    <apex:outputPanel id="attachDocumentsPanel">
                        <table id="data-attach-documents" class="table table-sm" style="margin-top:10px;margin-bottom:0;">
                            <thead class="thead-light">
                                <tr>
                                    <th scope="col" width="80%">File name</th>
                                    <th scope="col" width="20%">Date uploaded</th>
                                </tr>
                            </thead>
                            <tbody>
                                <apex:repeat value="{!attachDocumentList}" var="attachDocument">
                                    <tr onclick="selectDocumentProdRow(this);" vid="{!attachDocument.Id}" vname="{!attachDocument.Title}">
                                        <td>
                                            {!attachDocument.Title} <!--.{!attachDocument.FileExtension}-->
                                        </td>
                                        <td>
                                            <apex:outputText value="{0,date,dd-MMMM-yyyy hh:mm a}">
                                                <apex:param value="{!attachDocument.CreatedDate - 0.291666666}" />
                                            </apex:outputText>
                                        </td>
                                    </tr>
                                </apex:repeat>
                            </tbody>
                        </table>
                    </apex:outputPanel>
                </div>
                <div class="modal-footer" style="display: block;">
                    <button type="button" class="btn btn-secondary btn-custom" onclick="selectAttachDocument();">Attach</button>
                </div>
            </apex:outputPanel>
        </div>
    </div>
    <!-- End Modal -->
    <!-- Modal content-->
    <div class="modal fade" id="myModalBidHistory" role="dialog">
        <div class="modal-dialog modal-xl">
            <!-- Modal content-->
            <div class="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title">Bid History of</h4>
                    <button type="button" class="close" data-dismiss="modal">&times;</button>
                </div>
                <div class="modal-body" style="font-size:12px;padding-top: 0px;">
                    <div class="fieldset" style="font-size: 12px;">
                        <div class="row" style="margin-top: 0px !important;">
                            <div class="col-md-2">
                                <label>Market</label>
                                <apex:selectList size="1" id="bidhistory_market" styleClass="form-control form-control-sm">
                                    <apex:selectOptions value="{!production_markettypes}" />
                                </apex:selectList>
                            </div>
                            <div class="col-md-2">
                                <label>From</label><br/>
                                <apex:inputField id="bidhistory_from" value="{!groundFilter.Start_Date__c}" styleClass="form-control form-control-sm" />
                            </div>
                            <div class="col-md-2">
                                <label>To</label><br/>
                                <apex:inputField id="bidhistory_to" value="{!groundFilter.End_Date__c}" styleClass="form-control form-control-sm" />
                            </div>
                            <div class="col-md-6" style="padding-top:20px">
                                <button type="button" class="btn btn-primary btn-sm btn-custom" onclick="searchBidHistory();">Search</button>
                                <button type="button" class="btn btn-primary btn-sm btn-custom" onclick="clearBidHistory();">Clear</button>
                                <!--<button type="button" class="btn btn-danger btn-sm btn-custom" onclick="javascript:void(0);">Details</button>
                                <span>
                                    <apex:inputCheckbox label="Issue" styleClass="form-check-input" id="bidhistory_onlyirstays" title="Issue" style="margin-left: 15px !important;margin-top:0px !important;" />
                                    <label style="margin-left: -5px !important;">Only IR Stays</label>
                                </span>
                                <span>
                                    <apex:inputCheckbox label="Issue" styleClass="form-check-input" id="bidhistory_showall" title="Issue" style="margin-left: 0px !important;margin-top:0px !important;" />
                                    <label style="margin-left: -5px !important;">Show All</label>
                                </span>-->
                            </div>
                        </div>
                    </div>
                    <apex:outputPanel id="bidHistoryPanel">
                        <div class="row">
                            <div class="col-md-12">
                                <apex:inputHidden id="orderFieldBidHistoryActual" value="{!orderBidHistory}" />
                                <table class="table table-sm table-bordered">
                                    <thead class="thead-light">
                                        <tr>
                                            <th>
                                                <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidHistory('name','{!orderBidHistoryOrientation}');">
                                                    <span style="float:left;">Bid ID</span>
                                                    <i class="fa fa-sort-desc" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderBidHistory == 'name',orderBidHistoryOrientation == 'DESC'),'','display:none;')}"></i>
                                                    <i class="fa fa-sort-asc" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderBidHistory == 'name',orderBidHistoryOrientation == 'ASC'),'','display:none;')}"></i>
                                                </a>
                                            </th>
                                            <th>
                                                <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidHistory('production','{!orderBidHistoryOrientation}');">
                                                    <span style="float:left;">Production</span>
                                                    <i class="fa fa-sort-desc" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderBidHistory == 'production',orderBidHistoryOrientation == 'DESC'),'','display:none;')}"></i>
                                                    <i class="fa fa-sort-asc" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderBidHistory == 'production',orderBidHistoryOrientation == 'ASC'),'','display:none;')}"></i>
                                                </a>
                                            </th>
                                            <th>
                                                <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidHistory('date_in','{!orderBidHistoryOrientation}');">
                                                    <span style="float:left;">Date In</span>
                                                    <i class="fa fa-sort-desc" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderBidHistory == 'date_in',orderBidHistoryOrientation == 'DESC'),'','display:none;')}"></i>
                                                    <i class="fa fa-sort-asc" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderBidHistory == 'date_in',orderBidHistoryOrientation == 'ASC'),'','display:none;')}"></i>
                                                </a>
                                            </th>
                                            <th>
                                                <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidHistory('date_out','{!orderBidHistoryOrientation}');">
                                                    <span style="float:left;">Date Out</span>
                                                    <i class="fa fa-sort-desc" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderBidHistory == 'date_out',orderBidHistoryOrientation == 'DESC'),'','display:none;')}"></i>
                                                    <i class="fa fa-sort-asc" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderBidHistory == 'date_out',orderBidHistoryOrientation == 'ASC'),'','display:none;')}"></i>
                                                </a>
                                            </th>
                                            <th>
                                                <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidHistory('description','{!orderBidHistoryOrientation}');">
                                                    <span style="float:left;">Description</span>
                                                    <i class="fa fa-sort-desc" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderBidHistory == 'unit',orderBidHistoryOrientation == 'DESC'),'','display:none;')}"></i>
                                                    <i class="fa fa-sort-asc" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderBidHistory == 'unit',orderBidHistoryOrientation == 'ASC'),'','display:none;')}"></i>
                                                </a>
                                            </th>
                                            <th>
                                                <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidHistory('rate','{!orderBidHistoryOrientation}');">
                                                    <span style="float:left;">Rate</span>
                                                    <i class="fa fa-sort-desc" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderBidHistory == 'rate',orderBidHistoryOrientation == 'DESC'),'','display:none;')}"></i>
                                                    <i class="fa fa-sort-asc" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderBidHistory == 'rate',orderBidHistoryOrientation == 'ASC'),'','display:none;')}"></i>
                                                </a>
                                            </th>
                                            <th>
                                                <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidHistory('status','{!orderBidHistoryOrientation}');">
                                                    <span style="float:left;">Status</span>
                                                    <i class="fa fa-sort-desc" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderBidHistory == 'status',orderBidHistoryOrientation == 'DESC'),'','display:none;')}"></i>
                                                    <i class="fa fa-sort-asc" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderBidHistory == 'status',orderBidHistoryOrientation == 'ASC'),'','display:none;')}"></i>
                                                </a>
                                            </th>
                                            <th>
                                                <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidHistory('no_bid_reason','{!orderBidHistoryOrientation}');">
                                                    <span style="float:left;">No Bid Reason</span>
                                                    <i class="fa fa-sort-desc" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderBidHistory == 'no_bid_reason',orderBidHistoryOrientation == 'DESC'),'','display:none;')}"></i>
                                                    <i class="fa fa-sort-asc" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderBidHistory == 'no_bid_reason',orderBidHistoryOrientation == 'ASC'),'','display:none;')}"></i>
                                                </a>
                                            </th>
                                            <th>
                                                <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidHistory('venue','{!orderBidHistoryOrientation}');">
                                                    <span style="float:left;">Venue</span>
                                                    <i class="fa fa-sort-desc" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderBidHistory == 'venue',orderBidHistoryOrientation == 'DESC'),'','display:none;')}"></i>
                                                    <i class="fa fa-sort-asc" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderBidHistory == 'venue',orderBidHistoryOrientation == 'ASC'),'','display:none;')}"></i>
                                                </a>
                                            </th>
                                            <th>
                                                <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidHistory('provider','{!orderBidHistoryOrientation}');">
                                                    <span style="float:left;">Provider</span>
                                                    <i class="fa fa-sort-desc" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderBidHistory == 'provider',orderBidHistoryOrientation == 'DESC'),'','display:none;')}"></i>
                                                    <i class="fa fa-sort-asc" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderBidHistory == 'provider',orderBidHistoryOrientation == 'ASC'),'','display:none;')}"></i>
                                                </a>
                                            </th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <apex:repeat value="{!bidRelatedVendorList}" var="bidRelatedVendor">
                                            <tr>
                                                <th><a href="/{!bidRelatedVendor.b.Id}" target="_blank">{!bidRelatedVendor.name}</a></th>
                                                <th><a href="/{!bidRelatedVendor.b.Production__c}" target="_blank">{!bidRelatedVendor.production}</a></th>
                                                <th>
                                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                        <apex:param value="{!bidRelatedVendor.datein}" />
                                                    </apex:outputText>
                                                </th>
                                                <th>
                                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                        <apex:param value="{!bidRelatedVendor.dateout}" />
                                                    </apex:outputText>
                                                </th>
                                                <th>{!bidRelatedVendor.description}</th>
                                                <th>{!bidRelatedVendor.rate}</th>
                                                <th>{!bidRelatedVendor.status}</th>
                                                <th>{!bidRelatedVendor.nobidreason}</th>
                                                <th>{!bidRelatedVendor.venue}</th>
                                                <th>{!bidRelatedVendor.vendorparent}</th>
                                            </tr>
                                        </apex:repeat>
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </apex:outputPanel>
                </div>
            </div>
        </div>
    </div>
    <!-- End Modal -->
    <!-- Modal content-->
    <div class="modal fade" id="myModalReleaseByBid" role="dialog" style="padding-right: 18px;">
        <apex:outputPanel id="myModalReleaseByBid" layout="block" styleClass="modal-dialog modal-lg">
            <!-- Modal content-->
            <apex:outputPanel layout="block" rendered="{!isReleaseBidRendered}" styleClass="modal-content group-vendor">
                <div class="modal-header">
                    <h4 class="modal-title">Send Bid Release Notes to Vendor Contacts</h4>
                    <button type="button" class="close" onclick="closeBidModalJs('myModalReleaseByBid');">&times;</button>
                </div>
                <apex:outputPanel id="releaseBidDataPanel">
                    <div class="modal-body" style="font-size:12px;">
                        <div class="row" style="margin-top: 0 !important;">
                            <div class="col-md-12">
                                <button type="button" class="btn btn-secondary btn-custom" onclick="openContactVendor('{!bidData.Vendor__c}','{!bidData.Vendor__r.Name}','');">Add Contact</button>
                            </div>
                        </div>
                        <div class="fieldset" style="font-size: 12px;">
                            <div class="row" style="margin-top: 0px !important;">
                                <div class="col-md-2">
                                    Vendor Name
                                </div>
                                <div class="col-md-8">
                                    <a href="/{!bidData.Vendor__c}" target="_blank">{!bidData.Vendor__r.Name}</a>
                                </div>
                            </div>
                            <div class="row" style="margin-top: 5px !important;">
                                <div class="col-md-2">
                                    Select Primary Contact
                                </div>
                                <div class="col-md-8">
                                    <apex:selectList size="1" id="releasebybid_contactprimary" styleClass="form-control form-control-sm primary-contact" onchange="changeContactVendorReleaseByBid(this,'{!bidData.Vendor__c}');">
                                        <apex:selectOptions value="{!contactSelectOption_releaseMap[bidData.Vendor__c]}" />
                                    </apex:selectList>
                                    <script>
                                    if('{!bidData.Vendor_Contact__c}' != ''){
                                        $("select[id$=releasebybid_contactprimary] option").each(function(){
                                            if($(this).val() == '{!bidData.Vendor_Contact__c}'){        
                                                $(this).attr('selected',true);
                                            }
                                        });
                                    }
                                    </script>
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
                                        <apex:repeat value="{!contactsByVendorParent_releaseMap[bidData.Vendor__r.ParentId]}" var="contact1" rendered="{!IF(bidData.Vendor__r.ParentId <> null,true,false)}">
                                            <tr>
                                                <td data-contactid="{!contact1.c.Id}" data-contactemail="{!contact1.c.email}">
                                                    <apex:inputCheckbox value="{!contact1.selected}" disabled="{!contact1.disabled}" styleClass="form-check-input check-contact" style="margin-left: 10px;" />
                                                </td>
                                                <td>{!contact1.c.Order__c} NR</td>
                                                <td><a href="javascript:void(0);" onclick="openContactVendor('{!contact1.c.AccountId}','{!contact1.c.Account.Name}','{!contact1.c.Id}');">{!contact1.c.Name}</a></td>
                                                <td>{!contact1.c.Designation_title__c}</td>
                                                <td><a href="tel:{!contact1.c.Phone}">{!contact1.c.Phone}</a></td>
                                                <td><a href="mailto:{!contact1.c.Email}">{!contact1.c.Email}</a></td>
                                                <td>{!contact1.c.Fax}</td>
                                            </tr>
                                        </apex:repeat>
                                        <apex:repeat value="{!contactsByVendor_releaseMap[bidData.Vendor__c]}" var="contact1">
                                            <tr>
                                                <td data-contactid="{!contact1.c.Id}" data-contactemail="{!contact1.c.email}">
                                                    <apex:inputCheckbox value="{!contact1.selected}" disabled="{!contact1.disabled}" styleClass="form-check-input check-contact" style="margin-left: 10px;" />
                                                </td>
                                                <td>{!contact1.c.Order__c}</td>
                                                <td><a href="javascript:void(0);" onclick="openContactVendor('{!contact1.c.AccountId}','{!contact1.c.Account.Name}','{!contact1.c.Id}');">{!contact1.c.Name}</a></td>
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
                    <div class="modal-footer" style="display: block;">
                        <button type="button" class="btn btn-danger btn-sm" onclick="openPreviewReleaseBid(this,'{!opportunityId}','{!bidData.GT__c}','{!bidData.Id}','{!bidData.Vendor__r.Name}');">Preview</button>
                        <button type="button" class="btn btn-danger btn-sm" onclick="sendReleaseByBid();">Send Email</button>
                    </div>
                </apex:outputPanel>
            </apex:outputPanel>
        </apex:outputPanel>
    </div>
    <!-- End Modal -->
    
    <div class="modal fade" id="myModalJournalsAvailable" role="dialog" style="padding-right: 18px;">
        <apex:outputPanel id="myModalJournalsAvailable" layout="block" styleClass="modal-dialog modal-xl">
            <div class="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title">Bid Journals</h4>
                    <button type="button" class="close" onclick="closeBidJournalsJs();">&times;</button>
                </div>
                <apex:outputPanel id="bidJournals" layout="block" styleClass="modal-body" rendered="{!isBidJournalsRendered}">
                    <c:Dashboard_Journals recordId="{!bidData.Id}" SOBjectName="Bid" scope="Bid" productionId="{!vfpConfiguration.productionId}" pCompanies="{!vfpConfiguration.companies}" pContacts="{!vfpConfiguration.contacts}" pCompanyContacts="{!vfpConfiguration.companyContacts}" pTeamMembers="{!vfpConfiguration.teamMembers}" />
                </apex:outputPanel>
            </div>
        </apex:outputPanel>
    </div>
    
    <div class="modal fade" id="myModalBidDocuments" role="dialog" style="padding-right: 18px;">
        <div class="modal-dialog" style="min-width: 75em;">
            <div class="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title">Ground Travel Documents</h4>
                    <button type="button" class="close" onclick="closeBidDocumentsPanel();">&times;</button>
                </div>
                <apex:outputPanel id="bidDocumentsPanel" layout="block" styleClass="modal-body">
                    <c:Dashboard_Dialog_Documents rendered="{!loadDocuments}" recordId="{!vfpConfiguration.bidId}" parentSObject="{!vfpConfiguration.parentSObject}" contract="false" />
                </apex:outputPanel>
            </div>
        </div>
    </div>
    
    <!-- Actionfunctions -->
    <apex:actionFunction action="{!getBidInformation}" name="getBidInformationJs" status="loading" reRender="bidBody,bidJournals" oncomplete="createToggleBidData();" focus="lockedInput"/>
    <apex:actionFunction action="{!save}" name="saveJs" status="loading" reRender="bidBody,bidJournals" oncomplete="saveMessage();">
    </apex:actionFunction>
    <apex:actionFunction action="{!openBidAgreement}" name="openBidAgreementJs" status="loading" reRender="myModalBidAgreement" oncomplete="setupBidAgreement();openModal('myModalBidAgreement');">
        <apex:param assignTo="{!bidAgreement_type}" name="bidAgreement_type" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!saveBidAgreement}" name="saveBidAgreementJs" status="loading" reRender="bidAgreementAuditFields" oncomplete="saveBidAgreementMessage();">
        <apex:param assignTo="{!bidAgreement_message}" name="bidAgreement_message" value="" />
        <apex:param assignTo="{!bidAgreement_terms}" name="bidAgreement_terms" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!saveBidAgreement}" name="congaPreviewBidAgreementJs" status="loading" reRender="bidAgreementAuditFields" oncomplete="saveBidAgreementMessage();congaPreviewBidAgreement('{!bidData.id}', '{!bidData.Name}', '{!bidData.GT__c}', '{!bidData.GT__r.Name}', '{!JSENCODE(congaQueriesJson)}', '{!bidAgreement_congaTemplateId}');">
        <apex:param assignTo="{!bidAgreement_message}" name="bidAgreement_message" value="" />
        <apex:param assignTo="{!bidAgreement_terms}" name="bidAgreement_terms" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!saveBidAgreement}" name="congaSendBidAgreementJs" status="loading" reRender="bidAgreementAuditFields" oncomplete="saveBidAgreementMessage();congaSendBidAgreement('{!bidData.id}', '{!bidData.Name}', '{!bidData.GT__c}', '{!bidData.GT__r.Name}', '{!JSENCODE(congaQueriesJson)}', '{!bidAgreement_congaEmailTemplateId}', '{!bidAgreement_congaTemplateId}');">
        <apex:param assignTo="{!bidAgreement_message}" name="bidAgreement_message" value="" />
        <apex:param assignTo="{!bidAgreement_terms}" name="bidAgreement_terms" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!saveBidAgreement}" name="congaSignBidAgreementJs" status="loading" reRender="bidAgreementAuditFields" oncomplete="saveBidAgreementMessage();congaSignBidAgreement('{!bidData.id}', '{!bidData.Name}', '{!bidData.GT__c}', '{!bidData.GT__r.Name}', '{!JSENCODE(congaQueriesJson)}', '{!bidAgreement_congaSignTemplateId}', '{!JSENCODE(emailResult)}');">
        <apex:param assignTo="{!bidAgreement_to}" name="bidAgreement_to" value="" />
        <apex:param assignTo="{!bidAgreement_cc}" name="bidAgreement_cc" value="" />
        <apex:param assignTo="{!bidAgreement_bcc}" name="bidAgreement_bcc" value="" />
        <apex:param assignTo="{!bidAgreement_message}" name="bidAgreement_message" value="" />
        <apex:param assignTo="{!bidAgreement_terms}" name="bidAgreement_terms" value="" />
        <apex:param assignTo="{!isCongaSignSent}" name="isCongaSignSent" value="false"/>
    </apex:actionFunction>
    <apex:actionFunction action="{!deactivateBidAgreement}" name="deactivateBidAgreementJs" status="loading" reRender="myModalBidAgreement" oncomplete="closeModal('myModalBidAgreement');" />
    <apex:actionFunction action="{!soldOutBidStatus}" name="soldOutBidStatusJs" status="loading" reRender="bidBody,bidJournals"/>
    <apex:actionFunction action="{!openResendBid}" name="openResendBidJs" status="loading" reRender="myModalResendBid" oncomplete="openModal('myModalResendBid');" />
    <apex:actionFunction action="{!openReleaseByBid}" name="openReleaseByBidJs" status="loading" reRender="myModalReleaseByBid,releaseBidDataPanel" oncomplete="openModal('myModalReleaseByBid');" />
    <apex:actionFunction action="{!sendReleaseByBid}" name="sendReleaseByBidJs" status="loading" reRender="noneRender" oncomplete="alert('Bid Release Note has been sent.');" >
        <apex:param assignTo="{!releaseVendorcontact_actual_id}" name="contactPrimarySelected" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!changeContactVendorReleaseByBid}" name="changeContactVendorReleaseByBidJs" status="loading" reRender="releaseBidDataPanel">
        <apex:param assignTo="{!releaseVendorcontact_actual_id}" name="releaseVendorcontact_actual_id" value="" />
        <apex:param assignTo="{!vendoraccount_actual_id}" name="vendoraccount_actual_id" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!deactivateBid}" name="deactivateBidJs" status="loading" reRender="bidBody,bidJournals" oncomplete="loadTabContentJs('gt-trip')" />
    <apex:actionFunction action="{!congaResendBid}" name="congaResendBidJs" status="loading" reRender="bidBody" oncomplete="alert('Ground Travel Bid Request has been sent.');closeModal('myModalResendBid');" />
    <apex:actionFunction action="{!getBidInformation}" name="closeBidModalJs" status="loading" reRender="bidBody,bidJournals" oncomplete="createToggleBidData();closeModal('{!modal}');">
        <apex:param assignTo="{!modal}" name="modal" value=""/>
    </apex:actionFunction>
    <apex:actionFunction action="{!openAttachDocs}" name="openAttachDocsJs" status="loading" reRender="attachDocumentsPanel" oncomplete="openModal('myModalAttachDocuments');">
        <apex:param assignTo="{!attachdocument_objectid}" name="attachdocument_objectid" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!changeContactVendorResendBid}" name="changeContactVendorResendBidJs" status="loading" reRender="resendBidPanel">
        <apex:param assignTo="{!vendorcontact_actual_id}" name="vendorcontact_actual_id" value="" />
        <apex:param assignTo="{!vendoraccount_actual_id}" name="vendoraccount_actual_id" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!saveAddContactVendor}" name="saveAddContactVendorBidJs" status="loading" reRender="resendBidPanel,releaseBidDataPanel,addContactVendorMessagePanel" oncomplete="validateResultAddContactBid();">
        <apex:param assignTo="{!vendorContact.AccountId}" name="accountid" value="" />
        <apex:param assignTo="{!vendorContact_id}" name="contactid" value="" />
        <apex:param assignTo="{!vendorContact.FirstName}" name="firstname" value="" />
        <apex:param assignTo="{!vendorContact.LastName}" name="lastname" value="" />
        <apex:param assignTo="{!vendorContact.Designation_title__c}" name="designation" value="" />
        <apex:param assignTo="{!vendorContact.Phone}" name="phone" value="" />
        <apex:param assignTo="{!vendorContact.Work_Phone_Extension__c}" name="extension" value="" />
        <apex:param assignTo="{!vendorContact.MobilePhone}" name="mobile" value="" />
        <apex:param assignTo="{!vendorContact.Fax}" name="fax" value="" />
        <apex:param assignTo="{!vendorContact.Email}" name="email" value="" />
        <apex:param assignTo="{!vendorContact.Alternate_Email__c}" name="alternateemail" value="" />
        <apex:param assignTo="{!vendorContact.Description}" name="internalnotes" value="" />
        <apex:param assignTo="{!vendorContact.MailingStreet}" name="address1" value="" />
        <apex:param assignTo="{!vendorContact.OtherStreet}" name="address2" value="" />
        <apex:param assignTo="{!vendorContact.City__c}" name="cityid" value="" />
        <apex:param assignTo="{!vendorContact.MailingPostalCode}" name="postalcode" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!doAttachmentLast}" name="passToControllerLast" status="loading" reRender="newAttachmentPanel,documentsHousingPanel,documentsBidContracted,documentsBidPanel" oncomplete="setDataToSelect()">
        <apex:param assignTo="{!filename}" name="filename" value="" />
        <apex:param assignTo="{!documentRelationId}" name="documentRelationId" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!openBidHistory}" name="openBidHistoryJs" status="loading" reRender="bidHistoryPanel" oncomplete="openModal('myModalBidHistory');" />
    <apex:actionFunction action="{!searchBidHistory}" name="sortBidHistoryJs" status="loading" reRender="bidHistoryPanel">
        <apex:param assignTo="{!orderBidHistory}" name="orderBidHistory" value="" />
        <apex:param assignTo="{!orderBidHistoryOrientation}" name="orderBidHistoryOrientation" value="" />
        <apex:param assignTo="{!orderCheckBidHistory}" name="orderCheckBidHistory" value="" />
        <apex:param assignTo="{!orderChangeBidHistory}" name="orderChangeBidHistory" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!searchBidHistory}" name="searchBidHistoryJs" status="loading" reRender="bidHistoryPanel">
        <apex:param assignTo="{!bidhistorysearch_market}" name="bidhistorysearch_market" value="" />
        <apex:param assignTo="{!bidhistorysearch_from}" name="bidhistorysearch_from" value="" />
        <apex:param assignTo="{!bidhistorysearch_to}" name="bidhistorysearch_to" value="" />
        <apex:param assignTo="{!orderCheckBidHistory}" name="orderCheckBidHistory" value="" />
        <apex:param assignTo="{!orderBidHistory}" name="orderBidHistory" value="" />
        <apex:param assignTo="{!orderBidHistoryOrientation}" name="orderBidHistoryOrientation" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!addConcessionBid}" name="saveConcessionBidJs" status="loading" reRender="concessionsBidPanel">
        <apex:param assignTo="{!concessionRequestedActual}" name="concessionRequestedActual" value="" />
        <apex:param assignTo="{!concessionNoteActual}" name="concessionNoteActual" value="" />
        <apex:param assignTo="{!concessionIncludedActual}" name="concessionIncludedActual" value="" />
        <apex:param assignTo="{!concessionRateActual}" name="concessionRateActual" value="" />
        <apex:param assignTo="{!concessionOrderActual}" name="concessionOrderActual" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!deleteConcessionBid}" name="deleteConcessionBidJs" status="loading" reRender="concessionsBidPanel">
        <apex:param assignTo="{!concessionActual}" name="concessionActual" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!saveEditConcessionBid}" name="saveEditConcessionBidJs" status="loading" reRender="concessionsBidPanel">
        <apex:param assignTo="{!concessionActual}" name="concessionActual" value="" />
        <apex:param assignTo="{!concessionRequestedActual}" name="concessionRequestedActual" value="" />
        <apex:param assignTo="{!concessionNoteActual}" name="concessionNoteActual" value="" />
        <apex:param assignTo="{!concessionIncludedActual}" name="concessionIncludedActual" value="" />
        <apex:param assignTo="{!concessionRateActual}" name="concessionRateActual" value="" />
        <apex:param assignTo="{!concessionOrderActual}" name="concessionOrderActual" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!newSubTripBid}" name="newSubTripBidJs" status="loading" reRender="subTripsByBidPanel" />
    <apex:actionFunction action="{!deleteSubTripBid}" name="deleteSubTripBidJs" status="loading" reRender="subTripsByBidPanel">
        <apex:param assignTo="{!subtripIdActual}" name="subtripIdActual" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!saveSubTripBid}" name="saveSubTripBidJs" status="loading" reRender="subTripsByBidPanel">
        <apex:param assignTo="{!subtripIdActual}" name="subtripIdActual" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!deleteTravelBid}" name="deleteTravelBidJs" status="loading" reRender="subTripsByBidPanel">
        <apex:param assignTo="{!travelActualId}" name="travelActualId" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!saveTravelBid}" name="saveEditTravelBidJs" status="loading" reRender="subTripsByBidPanel, datesTripViewPanel">
        <apex:param assignTo="{!travelActualId}" name="travelActualId" value="" />
        <apex:param assignTo="{!newtravel_subtripid}" name="newtravel_subtripid" value="" />
        <apex:param assignTo="{!newtravel_line}" name="newtravel_line" value="" />
        <apex:param assignTo="{!newtravel_vehicle}" name="newtravel_vehicle" value="" />
        <apex:param assignTo="{!newtravel_vehicleid}" name="newtravel_vehicleid" value="" />
        <apex:param assignTo="{!newtravel_startdate}" name="newtravel_startdate" value="" />
        <apex:param assignTo="{!newtravel_starttime}" name="newtravel_starttime" value="" />
        <apex:param assignTo="{!newtravel_enddate}" name="newtravel_enddate" value="" />
        <apex:param assignTo="{!newtravel_endtime}" name="newtravel_endtime" value="" />
        <apex:param assignTo="{!newtravel_traveltype}" name="newtravel_traveltype" value="" />
        <apex:param assignTo="{!newtravel_grouptype}" name="newtravel_grouptype" value="" />
        <apex:param assignTo="{!newtravel_locationpickuptype}" name="newtravel_locationpickuptype" value="" />
        <apex:param assignTo="{!newtravel_locationpickupdetails}" name="newtravel_locationpickupdetails" value="" />
        <apex:param assignTo="{!newtravel_locationdropofftype}" name="newtravel_locationdropofftype" value="" />
        <apex:param assignTo="{!newtravel_locationdropoffdetails}" name="newtravel_locationdropoffdetails" value="" />
        <apex:param assignTo="{!newtravel_notes}" name="newtravel_notes" value="" />
        <apex:param assignTo="{!newtravel_updatemaster}" name="newtravel_updatemaster" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!saveTravelBid}" name="saveTravelAddMoreBidJs" status="loading" reRender="subTripsByBidPanel, datesTripViewPanel" oncomplete="addTravelLineByCClass('.card-body-' + $('input[id$=trip_last_save]').val());">
        <apex:param assignTo="{!travelActualOrder}" name="travelActualOrder" value="" />
        <apex:param assignTo="{!travelActualId}" name="travelActualId" value="" />
        <apex:param assignTo="{!newtravel_subtripid}" name="newtravel_subtripid" value="" />
        <apex:param assignTo="{!newtravel_line}" name="newtravel_line" value="" />
        <apex:param assignTo="{!newtravel_vehicle}" name="newtravel_vehicle" value="" />
        <apex:param assignTo="{!newtravel_vehicleid}" name="newtravel_vehicleid" value="" />
        <apex:param assignTo="{!newtravel_startdate}" name="newtravel_startdate" value="" />
        <apex:param assignTo="{!newtravel_starttime}" name="newtravel_starttime" value="" />
        <apex:param assignTo="{!newtravel_enddate}" name="newtravel_enddate" value="" />
        <apex:param assignTo="{!newtravel_endtime}" name="newtravel_endtime" value="" />
        <apex:param assignTo="{!newtravel_traveltype}" name="newtravel_traveltype" value="" />
        <apex:param assignTo="{!newtravel_grouptype}" name="newtravel_grouptype" value="" />
        <apex:param assignTo="{!newtravel_locationpickuptype}" name="newtravel_locationpickuptype" value="" />
        <apex:param assignTo="{!newtravel_locationpickupdetails}" name="newtravel_locationpickupdetails" value="" />
        <apex:param assignTo="{!newtravel_locationdropofftype}" name="newtravel_locationdropofftype" value="" />
        <apex:param assignTo="{!newtravel_locationdropoffdetails}" name="newtravel_locationdropoffdetails" value="" />
        <apex:param assignTo="{!newtravel_notes}" name="newtravel_notes" value="" />
        <apex:param assignTo="{!newtravel_updatemaster}" name="newtravel_updatemaster" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!saveTravelBid}" name="saveTravelCompleteBidJs" status="loading" reRender="subTripsByBidPanel, datesTripViewPanel">
        <apex:param assignTo="{!travelActualOrder}" name="travelActualOrder" value="" />
        <apex:param assignTo="{!travelActualId}" name="travelActualId" value="" />
        <apex:param assignTo="{!newtravel_subtripid}" name="newtravel_subtripid" value="" />
        <apex:param assignTo="{!newtravel_line}" name="newtravel_line" value="" />
        <apex:param assignTo="{!newtravel_vehicle}" name="newtravel_vehicle" value="" />
        <apex:param assignTo="{!newtravel_vehicleid}" name="newtravel_vehicleid" value="" />
        <apex:param assignTo="{!newtravel_startdate}" name="newtravel_startdate" value="" />
        <apex:param assignTo="{!newtravel_starttime}" name="newtravel_starttime" value="" />
        <apex:param assignTo="{!newtravel_enddate}" name="newtravel_enddate" value="" />
        <apex:param assignTo="{!newtravel_endtime}" name="newtravel_endtime" value="" />
        <apex:param assignTo="{!newtravel_traveltype}" name="newtravel_traveltype" value="" />
        <apex:param assignTo="{!newtravel_grouptype}" name="newtravel_grouptype" value="" />
        <apex:param assignTo="{!newtravel_locationpickuptype}" name="newtravel_locationpickuptype" value="" />
        <apex:param assignTo="{!newtravel_locationpickupdetails}" name="newtravel_locationpickupdetails" value="" />
        <apex:param assignTo="{!newtravel_locationdropofftype}" name="newtravel_locationdropofftype" value="" />
        <apex:param assignTo="{!newtravel_locationdropoffdetails}" name="newtravel_locationdropoffdetails" value="" />
        <apex:param assignTo="{!newtravel_notes}" name="newtravel_notes" value="" />
        <apex:param assignTo="{!newtravel_updatemaster}" name="newtravel_updatemaster" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!deleteVehicleBid}" name="deleteVehicleBidJs" status="loading" reRender="vehiclesBidPanel" oncomplete="$('.multiselect').chosen();">
        <apex:param assignTo="{!vehicleIdActual}" name="vehicleIdActual" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!newVehicleBid}" name="newVehicleBidJs" status="loading" reRender="noneRender" oncomplete="$('.multiselect-bid').chosen();$('.newdata-multiselect-bid').val('').trigger('chosen:updated');$('.new-vehicle-bid').show();" />
    <apex:actionFunction action="{!addVehicleBid}" name="saveVehicleBidJs" status="loading" reRender="vehiclesBidPanel" oncomplete="$('.multiselect').chosen();$('.other-amenities-data-header').hide();$('.show-data-with-other-amenities').show();$('.show-data-without-other-amenities').hide();$('.other-amenities-data').hide();">
        <apex:param assignTo="{!vehicle_amenities}" name="vehicle_amenities" value="" />
        <apex:param assignTo="{!vehicle_make}" name="vehicle_make" value="" />
        <apex:param assignTo="{!vehicle_model}" name="vehicle_model" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!saveEditVehicleBid}" name="saveEditVehicleBidJs" status="loading" reRender="vehiclesBidPanel" oncomplete="$('.multiselect').chosen();$('.other-amenities-data-header').hide();$('.show-data-with-other-amenities').show();$('.show-data-without-other-amenities').hide();$('.other-amenities-data').hide();">
        <apex:param assignTo="{!vehicleIdActual}" name="vehicleIdActual" value="" />
        <apex:param assignTo="{!vehicle_vehicleref}" name="vehicle_vehicleref" value="" />
        <apex:param assignTo="{!vehicle_vehicletype}" name="vehicle_vehicletype" value="" />
        <apex:param assignTo="{!vehicle_capacity}" name="vehicle_capacity" value="" />
        <apex:param assignTo="{!vehicle_make}" name="vehicle_make" value="" />
        <apex:param assignTo="{!vehicle_model}" name="vehicle_model" value="" />
        <apex:param assignTo="{!vehicle_year}" name="vehicle_year" value="" />
        <apex:param assignTo="{!vehicle_amenities}" name="vehicle_amenities" value="" />
        <apex:param assignTo="{!vehicle_otheramenities}" name="vehicle_otheramenities" value="" />
        <apex:param assignTo="{!vehicle_luggage}" name="vehicle_luggage" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!sendResendBid}" name="sendResendBidJs" status="loading" reRender="bidBody" oncomplete="alert('Bid Request has been sent.');closeModal('myModalResendBid');" >
        <apex:param assignTo="{!contactPrimarySelected}" name="contactPrimarySelected" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!editBidDataLocked}" name="editBidDataLockedJs" status="loading" reRender="noneRender">
        <apex:param assignTo="{!bidid_locked}" name="bidid_locked" value="" />
        <apex:param assignTo="{!bidstatus_locked}" name="bidstatus_locked" value="" />
    </apex:actionFunction>
    <apex:actionFunction name="openBidJournalsJs" status="loading" reRender="myModalJournalsAvailable" oncomplete="openModal('myModalJournalsAvailable');">
        <apex:param assignTo="{!isBidJournalsRendered}" name="isBidJournalsRendered" value="true"/>
    </apex:actionFunction>
    <apex:actionFunction name="closeBidJournalsJs" status="loading" reRender="myModalJournalsAvailable" oncomplete="closeModal('myModalJournalsAvailable');">
        <apex:param assignTo="{!isBidJournalsRendered}" name="isBidJournalsRendered" value="false"/>
    </apex:actionFunction>
    <apex:actionFunction action="{!contractBid}" name="contractJs" status="loading" reRender="bidBody" oncomplete="createToggleBidData();">
        <apex:param assignTo="{!tripBidNumber}" name="tripBidNumber" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!contractBid}" name="contractAnotherJs" status="loading" reRender="productionInformation" oncomplete="goToTripTabJs(null,0,'gt-trip');">
        <apex:param assignTo="{!tripBidNumber}" name="tripBidNumber" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!uncontractBid}" name="uncontractJs" status="loading" reRender="bidBody" oncomplete="createToggleBidData();">
        <apex:param assignTo="{!tripBidNumber}" name="tripBidNumber" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!viewContractingDetailByBid}" name="viewContractingDetailByBidJs" status="loading" reRender="noneRender" oncomplete="loadTabContent('gt-contracting');">
        <apex:param assignTo="{!contractingBidId}" name="contractingBidId" value="" />
        <apex:param assignTo="{!contractingParentId}" name="contractingParentId" value="" />
    </apex:actionFunction>
    <apex:actionFunction name="viewBidDocumentsJs" status="loading" reRender="bidDocumentsPanel" oncomplete="openModal('myModalBidDocuments');">
        <apex:param assignTo="{!loadDocuments}" name="loadDocuments" value="" />
    </apex:actionFunction>
    <apex:actionFunction name="closeBidDocumentsPanel" status="loading" reRender="bidDocumentsPanel" oncomplete="closeModal('myModalBidDocuments');">
        <apex:param assignTo="{!loadDocuments}" name="loadDocuments" value="false" />
    </apex:actionFunction>
    <apex:actionFunction name="changeSymbolJs" status="loading" reRender="rateDetailsPanel" />
    
    <apex:actionFunction name="calculateTotalPriceJs" action="{!calculateTotalPrice}" status="loading" reRender="rateDetailsPanel" />
    <apex:actionFunction name="calculateRevenueJs" action="{!calculateRevenue}" status="loading" reRender="rateDetailsPanel" />
    <apex:actionFunction name="calculateRevenueByCommissionJs" action="{!calculateRevenueByCommission}" status="loading" reRender="rateDetailsPanel" />
    <apex:actionFunction name="calculateRevenueByRateJs" action="{!calculateRevenueByRate}" status="loading" reRender="rateDetailsPanel" />
    <!-- End Actionfunctions -->
    
    <script>
    $(function(){
        if('{!tripBidNumber}' != ''){
            if($('input[id$=isPageLoadedInput]').val() == 'true'){
                getBidInformationJs();
                //emailInputKeyEvents();
                $('input[id$=isPageLoadedInput]').val(false);
            } 
            else $('input[id$=isPageLoadedInput]').val(true);
        }
    });
    function createToggleBidData() {
        $('.toogle-data-bid').bootstrapToggle({
            on: "",
            off: "",
            onstyle: "danger",
            offstyle: "success",
            height: "10px",
            width: "50px"
        });
    }
    function editTravelBid(val){
        $(val).hide();
        $(val).parents('tr').find('.btn-delete').hide();
        $(val).parents('tr').find('.btn-copy').hide();
        $(val).parents('tr').find('.btn-cancel').show();
        $(val).parents('tr').find('.btn-save').show();
        $(val).parents('tr').find('.show-data').hide();
        var data_original_grouptype = $(val).parents('tr').find('.data-original-grouptype').val();
        $(val).parents('tr').find('.grouptype.inputpicker-input').val(data_original_grouptype);
        var data_original = $(val).parents('tr').find('.data-original-airlineinfo').val();
        $(val).parents('tr').find('.notes.inputpicker-input').val(data_original);
        $(val).parents('tr').find('.data').show();
    }
    function calculateTotalPrice(){
        if($('input[id$=production_office_location]').val() != 'RRE' && $('input[id$=bidRevenue_gratuityInput]').attr('pre') != $('input[id$=bidRevenue_gratuityInput]').val()){
            calculateTotalPriceJs();
        }
    }
    function calculateRevenue(){
        if($('input[id$=production_office_location]').val() != 'RRE' && $('input[id$=bidRevenue_baseCostInput]').attr('pre') != $('input[id$=bidRevenue_baseCostInput]').val()){
            calculateRevenueJs();
        }
    }
    function calculateRevenueByCommission(){
        if($('input[id$=production_office_location]').val() != 'RRE' && $('input[id$=bidRevenue_CommissionInput]').attr('pre') != $('input[id$=bidRevenue_CommissionInput]').val()){
            calculateRevenueByCommissionJs();
        }
    }
    function calculateRevenueByRate(){
        if($('input[id$=production_office_location]').val() != 'RRE' && $('input[id$=bidRevenue_rateInput]').attr('pre') != $('input[id$=bidRevenue_rateInput]').val()){
            calculateRevenueByRateJs();
        }
    }
    function saveDataPreview(input,val){
        if(input == 'bidRevenue_baseCostInput') $('input[id$=bidRevenue_baseCostInput]').attr('pre',$(val).val());
        if(input == 'bidRevenue_CommissionInput') $('input[id$=bidRevenue_CommissionInput]').attr('pre',$(val).val());
        if(input == 'bidRevenue_rateInput') $('input[id$=bidRevenue_rateInput]').attr('pre',$(val).val());
        if(input == 'bidRevenue_gratuityInput') $('input[id$=bidRevenue_gratuityInput]').attr('pre',$(val).val());
    }
    function showMessagePreviewPdf() {
        var account_name = $('input[id$=emailbid_primaryaccountname]').val();
        alert('Bid Release Note has been sent to ' + account_name);
    }
    function contract(bidnumber) {
        var trip_have_contracted = $('input[id$=trip_have_contracted]').val();
        if(trip_have_contracted == 'true'){
            var confirmAction = confirm('Another bid is already contracted for this trip. Do you want to create a duplicate trip?');
            if(confirmAction) contractAnotherJs(bidnumber);
        }else{
            contractJs(bidnumber);
        }
    }
    function uncontract(bidnumber) {
        uncontractJs(bidnumber);
    }
    function editBidDataLocked(val,bid_id) {
        var checking = $(val).prop('checked');        
        editBidDataLockedJs(bid_id,checking);
    }
    function openPreviewResendLink(val,bidid,accountid,name,type_z){
        $('select[id$=emailbid_attachs]').empty();
        $('#myModalSendBidRequest').css('z-index','1039');
        $('#myModalResendBid').css('z-index','1039');
        $('#myModalPreviewPdf').find('.modal-title').text('Bid Request Link and Vendor Link email');
        $('#myModalPreviewPdf').find('.modal-body .email-attachs').show();
        $('#myModalPreviewPdf').find('.modal-footer .btn-send').text('Send Link');
        var primary_contact = $(val).parents('.group-vendor').find('.primary-contact').val();
        $('input[id$=emailbid_primarycontactname]').val($(val).parents('.group-vendor').find('.primary-contact').children("option:selected").text());
        $('input[id$=emailbid_primaryaccountname]').val(name);
        $('input[id$=emailbid_type]').val(type_z);
        var productionid = $('input[id$=production]').val();
        var tripid = $('input[id$=gtbid_tripid]').val();
        $('input[id$=emailbid_bid]').val(bidid);
        $('input[id$=emailbid_subject]').val('');
        console.log('prod:' + productionid);
        console.log('tripid:' + tripid);
        console.log('bidid:' + bidid);
        console.log('primary_contact:' + primary_contact);
        Visualforce.remoting.Manager.invokeAction(
            '{!$RemoteAction.GTDashboard_Tab_GT_Bid_Controller.getDataPreviewResendBid}',productionid,tripid,bidid,primary_contact,'http://' + window.location.host,
            function(result, event){
                console.log(result);
                console.log(event);
                if (event.status) {
                    $('#myModalPreviewPdf .modal-body').find('.emailbid_to').html(result[0]);
                    $('#myModalPreviewPdf .modal-body').find('input[id$=emailbid_subject]').val(result[1]);
                    for ( instance in CKEDITOR.instances ){
                        if(instance.includes('emailBidBody')) CKEDITOR.instances[instance].setData(result[2].replace(/(&lt\;)/g,"<").replace(/(&gt\;)/g,">"));
                    }
                    $('input[id$=cc-email-bid]').val('');
                    $('.all-cc-email-bid').html('');
                    $(val).parents('.group-vendor').find('.check-contact').each(function(){
                        if($(this).is(":checked") && $(this).parents('td').data('contactid') != primary_contact){
                            $('.all-cc-email-bid').append('<span class="email-ids">'+ $(this).parents('td').data('contactemail') + ' <span class="cancel-email">x</span></span>');
                        }
                    });
                    $('input[id$=bcc-email-bid]').val('');
                    $('.all-bcc-email-bid').html('');
                    openModal('myModalPreviewPdf');
                } else if (event.type === 'exception') {
                    alert('exception');
                } else {
                    alert('other');
                }
            }, 
            {escape: true}
        );
    }
    function sendResendBid() {
        //sendResendBidJs(typez);
        var primary_contact = $('select[id$=resendbid_contactprimary]').val();
        if(primary_contact != null && primary_contact != '') {
            sendResendBidJs(primary_contact);
        }else{
            alert('No contacts found. Please make sure Vendor has Contacts.');
        }
    }
    function cancelEditVehicleBid(val){
        $(val).parents('tr').find('.btn-save').hide();
        $(val).parents('tr').find('.btn-cancel').hide();
        $(val).parents('tr').find('.btn-delete').show();
        $(val).parents('tr').find('.btn-edit').show();
        $(val).parents('tr').find('.btn-copy').show();
        $(val).parents('tr').find('.show-data').show();
        $(val).parents('tr').find('.data').hide();
        
        $('.new-vehicle-trip').hide();
        $('.other-amenities-data-header').hide();
        $('.show-data-with-other-amenities').show();
        $('.show-data-without-other-amenities').hide();
        $('.other-amenities-data').hide();
    }
    function saveEditVehicleBid(val){
        var id = $(val).parents('tr').attr('data-id');
        var vehicle_ref = $(val).parents('tr').find('.vehicleref').val();
        var vehicle_type = $(val).parents('tr').find('.vehicletype').val();
        var capacity = $(val).parents('tr').find('.capacity').val();
        var make = $(val).parents('tr').find('.make.inputpicker-input').val();
        var model = $(val).parents('tr').find('.model.inputpicker-input').val();
        var year = $(val).parents('tr').find('.year').val();
        var luggage = $(val).parents('tr').find('.luggage').val();
        var amenities = $(val).parents('tr').find('.amenities').val().toString();
        var other_amenities = $(val).parents('tr').find('.otheramenities').val();
        saveEditVehicleBidJs(id,vehicle_ref,vehicle_type,capacity,make,model,year,amenities,other_amenities,luggage);
    }
    function saveVehicleBid(){
        $('.new-vehicle-bid').hide();
        var amenities = $('select[id$=newvehiclebid_amenities]').val().toString();
        var make = $('.newdata-make.inputpicker-input').val();
        var model = $('.newdata-model.inputpicker-input').val();
        saveVehicleBidJs(amenities,make,model);
    }
    function cancelVehicleBid() {
        $('.newdata').val('');
        $('.new-vehicle-bid').hide();
        $('.other-amenities-data-header').hide();
        $('.show-data-with-other-amenities').show();
        $('.show-data-without-other-amenities').hide();
        $('.other-amenities-data').hide();
    }
    function newVehicleBid(){
        $('.newdata').val('');
        $('.other-amenities-data-header').show();
        $('.show-data-without-other-amenities').show();
        $('.show-data-with-other-amenities').hide();
        $('.other-amenities-data').show();
        newVehicleBidJs();
    }
    function editVehicleBid(val){
        vehicle_id = $(val).parents('tr').attr('data-id');
        Visualforce.remoting.Manager.invokeAction(
            '{!$RemoteAction.GTDashboard_Tab_GT_Bid_Controller.getGroundAmenities}',
            vehicle_id,
            function(result, event){
                if (event.status) {
                    console.log(result);
                    $(val).parents('tr').find('.multiselect-bid').chosen();
                    $(val).parents('tr').find('.multiselect-bid').val(result).trigger('chosen:updated');
                    $(val).hide();
                    $(val).parents('tr').find('.btn-delete').hide();
                    $(val).parents('tr').find('.btn-cancel').show();
                    $(val).parents('tr').find('.btn-save').show();
                    $(val).parents('tr').find('.show-data').hide();
                    var data_original_make = $(val).parents('tr').find('.data-original-make').val();
                    $(val).parents('tr').find('.make.inputpicker-input').val(data_original_make);
                    var data_original_model = $(val).parents('tr').find('.data-original-model').val();
                    $(val).parents('tr').find('.model.inputpicker-input').val(data_original_model);
                    $('.other-amenities-data-header').show();
                    $('.show-data-without-other-amenities').show();
                    $('.show-data-with-other-amenities').hide();
                    $('.other-amenities-data').show();
                    $(val).parents('tr').find('.other-amenities-data').show();
                    $(val).parents('tr').find('.show-data-without-other-amenities').hide();
                    $(val).parents('tr').find('.show-data-with-other-amenities').hide();
                    $(val).parents('tr').find('.data').show();
                } else if (event.type === 'exception') {
                    alert('exception');
                } else {
                    alert('other');
                }
            }, 
            {escape: true}
        );
    }
    function deleteVehicleBid(val){
        var confirmAction = confirm('Are you sure you want to delete this item?');
        if(confirmAction) deleteVehicleBidJs(val);
    }
    function setInputVehicleBid(){
        if(createAutocompleteVehicleBid == false){
            createAutocompleteVehicleBid = true;
            $('.vehicle-travel-search').autocomplete({
                lookup: function (query, done) {
                    bidid = $('input[id$=bidid]').val();
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.GTDashboard_Tab_GT_Bid_Controller.searchVehicleTrip}',query,bidid,
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
                                alert('exception');
                            } else {
                                alert('other');
                            }
                        }, 
                        {escape: true}
                    );
                },
                onSelect: function (suggestion) {
                    $(this).val(suggestion.value);
                    $(this).parents('td').find('.vehicleid').val(suggestion.data);
                }
            });
        }
    }
    function saveTravelCompleteBid(val){
        var subtripid = $(val).parents('.card-body-trip').find('.subtripid').val();
        var trip_order = $(val).parents('.card-body-trip').find('.triporder').val();
        var line = $(val).parents('.card-body-trip').find('.new-travel .line').val();
        var vehicle = $(val).parents('.card-body-trip').find('.new-travel .vehicle').val();
        var vehicleid = $(val).parents('.card-body-trip').find('.new-travel .vehicleid').val();
        var start_date = $(val).parents('.card-body-trip').find('.new-travel .startdate').val();
        var start_date_time = $(val).parents('.card-body-trip').find('.new-travel .starttime').val();
        var end_date = $(val).parents('.card-body-trip').find('.new-travel .enddate').val();
        var end_date_time = $(val).parents('.card-body-trip').find('.new-travel .endtime').val();
        var travel_type = $(val).parents('.card-body-trip').find('.new-travel .traveltype').val();
        var group_type = $(val).parents('.card-body-trip').find('.new-travel .grouptype.inputpicker-input').val();       
        var location_pickup_type = $(val).parents('.card-body-trip').find('.new-travel .locationtype').val();
        var location_pickup_details = $(val).parents('.card-body-trip').find('.new-travel .locationdetails').val();
        var location_dropoff_type = $(val).parents('.card-body-trip').find('.new-travel .locationdropofftype').val();
        var location_dropoff_details = $(val).parents('.card-body-trip').find('.new-travel .locationdetailsdropoff').val();
        var airline_notes = $(val).parents('.card-body-trip').find('.new-travel .notes.inputpicker-input').val();
        var validateDates = true;
        var bid_status = $('.bid-tab-status').text();
         
        if(bid_status == 'Contracted') validateDates = false;
        
        saveTravelCompleteBidJs(trip_order,'',subtripid,line,vehicle,vehicleid,start_date,start_date_time,end_date,end_date_time,travel_type,group_type,location_pickup_type,location_pickup_details,location_dropoff_type,location_dropoff_details,airline_notes,validateDates);
    }
    function addTravelLineByCClass(val){
        var start_date = $('input[id$=tripview_startdate]').val();
        $(val).find('.new-travel .new-data').val('');
        $(val).find('.new-travel .startdate').val(start_date + ' 12:00 PM');
        $(val).find('.new-travel .enddate').val(start_date + ' 12:00 PM');
        $(val).find('.new-travel').show();
    }
    function saveTravelAddMoreBid(val){
        var subtripid = $(val).parents('.card-body-trip').find('.subtripid').val();
        var trip_order = $(val).parents('.card-body-trip').find('.triporder').val();
        var line = $(val).parents('.card-body-trip').find('.new-travel .line').val();
        var vehicle = $(val).parents('.card-body-trip').find('.new-travel .vehicle').val();
        var vehicleid = $(val).parents('.card-body-trip').find('.new-travel .vehicleid').val();
        var start_date = $(val).parents('.card-body-trip').find('.new-travel .startdate').val();
        var start_date_time = $(val).parents('.card-body-trip').find('.new-travel .starttime').val();
        var end_date = $(val).parents('.card-body-trip').find('.new-travel .enddate').val();
        var end_date_time = $(val).parents('.card-body-trip').find('.new-travel .endtime').val();
        var travel_type = $(val).parents('.card-body-trip').find('.new-travel .traveltype').val();
        var group_type = $(val).parents('.card-body-trip').find('.new-travel .grouptype.inputpicker-input').val();
        var location_pickup_type = $(val).parents('.card-body-trip').find('.new-travel .locationtype').val();
        var location_pickup_details = $(val).parents('.card-body-trip').find('.new-travel .locationdetails').val();
        var location_dropoff_type = $(val).parents('.card-body-trip').find('.new-travel .locationdropofftype').val();
        var location_dropoff_details = $(val).parents('.card-body-trip').find('.new-travel .locationdetailsdropoff').val();
        var airline_notes = $(val).parents('.card-body-trip').find('.new-travel .notes.inputpicker-input').val();
        
        var start_date_trip = new Date($('input[id$=tripview_startdate]').val());
        var end_date_trip = new Date($('input[id$=tripview_enddate]').val());
        var date1 = start_date != '' ? new Date(start_date.split(' ')[0]) : null;
        var date2 = end_date != '' ? new Date(end_date.split(' ')[0]) : null;
        var validateDates = true;
        var bid_status = $('.bid-tab-status').text();
         
        if(bid_status != 'Contracted' && (date1 < start_date_trip || date1 > end_date_trip || date2 < start_date_trip || date2 > end_date_trip)) validateDates = false;
        
        if(validateDates){
            saveTravelAddMoreBidJs(trip_order,'',subtripid,line,vehicle,vehicleid,start_date,start_date_time,end_date,end_date_time,travel_type,group_type,location_pickup_type,location_pickup_details,location_dropoff_type,location_dropoff_details,airline_notes,false);
        }else{
            var confirmAction = confirm('You have created a trip outside the master trip date, would you like us to update the master trip date. Click accept to confirm, click cancel to cancel the update.');
            if(confirmAction) saveTravelAddMoreBidJs(trip_order,'',subtripid,line,vehicle,vehicleid,start_date,start_date_time,end_date,end_date_time,travel_type,group_type,location_pickup_type,location_pickup_details,location_dropoff_type,location_dropoff_details,airline_notes,true);
        }
    }
    function cancelTravelBid(val){
        $(val).parents('.card-body-trip').find('.new-travel').hide();
    }
    function addTravelLineBid(val){
        var start_date = $('input[id$=tripview_startdate]').val();
        $(val).parents('.card-body-trip').find('.new-travel .new-data').val('');
        $(val).parents('.card-body-trip').find('.new-travel .startdate').val(start_date);
        $(val).parents('.card-body-trip').find('.new-travel .enddate').val(start_date);
        $(val).parents('.card-body-trip').find('.new-travel').show();
    }
    function saveEditTravelBid(val) {
        var id = $(val).parents('tr').find('.id').val();
        var line = $(val).parents('tr').find('.line').val();
        var vehicle = $(val).parents('tr').find('.vehicle').val();
        var vehicleid = $(val).parents('tr').find('.vehicleid').val();
        var start_date = $(val).parents('tr').find('.startdate').val();
        var start_date_time = $(val).parents('tr').find('.starttime').val();
        var end_date = $(val).parents('tr').find('.enddate').val();
        var end_date_time = $(val).parents('tr').find('.endtime').val();
        var travel_type = $(val).parents('tr').find('.traveltype').val();
        var group_type = $(val).parents('tr').find('.grouptype.inputpicker-input').val();
        var location_pickup_type = $(val).parents('tr').find('.locationtype').val();
        var location_pickup_details = $(val).parents('tr').find('.locationdetails').val();
        var location_dropoff_type = $(val).parents('tr').find('.locationdropofftype').val();
        var location_dropoff_details = $(val).parents('tr').find('.locationdetailsdropoff').val();
        var airline_notes = $(val).parents('tr').find('.notes.inputpicker-input').val();
        
        var start_date_trip = new Date($('input[id$=tripview_startdate]').val());
        var end_date_trip = new Date($('input[id$=tripview_enddate]').val());
        var date1 = start_date != '' ? new Date(start_date.split(' ')[0]) : null;
        var date2 = end_date != '' ? new Date(end_date.split(' ')[0]) : null;
        var validateDates = true;
        var bid_status = $('.bid-tab-status').text();
         
        if(bid_status != 'Contracted' && (date1 < start_date_trip || date1 > end_date_trip || date2 < start_date_trip || date2 > end_date_trip)) validateDates = false;
        
        if(validateDates){
            saveEditTravelBidJs(id,'',line,vehicle,vehicleid,start_date,start_date_time,end_date,end_date_time,travel_type,group_type,location_pickup_type,location_pickup_details,location_dropoff_type,location_dropoff_details,airline_notes,false);
        }else{
            var confirmAction = confirm('You have created a trip outside the master trip date, would you like us to update the master trip date. Click accept to confirm, click cancel to cancel the update.');
            if(confirmAction) saveEditTravelBidJs(id,'',line,vehicle,vehicleid,start_date,start_date_time,end_date,end_date_time,travel_type,group_type,location_pickup_type,location_pickup_details,location_dropoff_type,location_dropoff_details,airline_notes,true);
        }
    }
    function deleteTravelBid(val){
        var confirmAction = confirm('Are you sure you want to delete this item?');
        if(confirmAction) deleteTravelBidJs(val)
    }
    function saveSubTripBid(val){
        saveSubTripBidJs(val);
    }
    function deleteSubTripBid(val){
        deleteSubTripBidJs(val);
    }
    function newSubTripBid(){
        $('.btn-add-trip-details-bid').html('<i class="fa fa-plus"></i> Add Additional Trip');
        newSubTripBidJs();
    }
    function saveEditConcessionBid(val) {
        var id = $(val).parents('tr').find('.id').val();
        var concessionRequested = $(val).parents('tr').find('.requested.inputpicker-input').val();
        var notes = $(val).parents('tr').find('.notes').val();
        var included = $(val).parents('tr').find('.included').val();
        var rate = $(val).parents('tr').find('.rate').val();
        var order = $(val).parents('tr').find('.order').val();
        $(val).parents('tr').find('.rate').removeClass('error-custom');
        if(included == 'Excluded'){
            //if(rate.trim() == ''){
            //    $(val).parents('tr').find('.rate').addClass('error-custom');
            //}else{
                saveEditConcessionBidJs(id,concessionRequested,notes,included,rate,order);
            //}
        }else{
            if(included == '--Select--') included = '';
            saveEditConcessionBidJs(id,concessionRequested,notes,included,rate,order);
        }
    }
    function deleteConcessionBid(val) {
        var confirmAction = confirm('Are you sure you want to delete this item?');
        if(confirmAction) deleteConcessionBidJs(val);
    }
    function editConcessionBid(val){
        var data_original = $(val).parents('tr').find('.data-original-requested').val();
        $(val).parents('tr').find('.requested.inputpicker-input').val(data_original);
        $(val).parents('tr').find('.included').val($(val).parents('tr').find('.included').attr('data-value'));
        $(val).hide();
        $(val).parents('tr').find('.btn-delete').hide();
        $(val).parents('tr').find('.btn-copy').hide();
        $(val).parents('tr').find('.btn-cancel').show();
        $(val).parents('tr').find('.btn-save').show();
        $(val).parents('tr').find('.show-data').hide();
        $(val).parents('tr').find('.data').show();
    }
    function cancelConcessionBid() {
        $('.newdata').val('');
        $('.new-concession-bid').hide();
    }
    function saveConcessionBid() {
        var requested = $('.newdata-requested.inputpicker-input').val();
        var notes = $('.newdata-notes').val();
        var included = $('.newdata-included').val();
        var rate = $('.newdata-rate').val();
        var order = $('.newdata-order').val();
        $('.newdata-rate').removeClass('error-custom');
        if(included == 'Excluded'){
            //if(rate.trim() == ''){
            //    $('.newdata-rate').addClass('error-custom');
            //}else{
                $('.new-concession-bid').hide();
                saveConcessionBidJs(requested,notes,included,rate,order);
            //}
        }else{
            if(included == '--Select--') included = '';
            $('.new-concession-bid').hide();
            saveConcessionBidJs(requested,notes,included,rate,order);
        }
    }
    function newConcessionTrip() {
        $('.newdata').val('');
        $('.new-concession-bid').show();
    }
    function clearBidHistory() {
        $('select[id$=bidhistory_market]').val('');
        $('input[id$=bidhistory_from]').val('');
        $('input[id$=bidhistory_to]').val('');
        //$("input[id$=bidhistory_onlyirstays]").prop("checked", false);
        //$("input[id$=bidhistory_showall]").prop("checked", false);
        searchBidHistoryJs('','','',false,'created_date','DESC');
    }
    function searchBidHistory() {
        var market = $('select[id$=bidhistory_market]').val();
        var from = $('input[id$=bidhistory_from]').val();
        var to = $('input[id$=bidhistory_to]').val();
        //var onlyirstays = $("input[id$=bidhistory_onlyirstays]").prop("checked");
        //var showall = $("input[id$=bidhistory_showall]").prop("checked");
        searchBidHistoryJs(market,from,to,false,'created_date','DESC');
    }
    function sortBidHistory(sortOrder,sortOrientation) {
        var actual = $('input[id$=orderFieldBidHistoryActual]').val();
        var change = false;
        if(actual != sortOrder) change = true;
        sortBidHistoryJs(sortOrder,sortOrientation,true,change);
    }

    function openBidHistory(vendor) {
        $('#myModalBidHistory').find('.modal-title').text('Bid History of '+vendor);
        openBidHistoryJs();
    }
    function save(){
        saveJs();
    }
    function saveMessage(){
        $("span#saveMessage").show();
        setTimeout(function(){$('span#saveMessage').fadeOut('slow');}, 2000);
    }
    function soldOutBidStatus() {
        $('input[id$=bidRevenue_noBidReasonInput]').val('SOLD OUT');
        soldOutBidStatusJs();
    }
    //Email Inputs
    function emailInputKeyEvents(){
        $('div[id$=myModalBidAgreement]').off('keydown','.cc-email-bidAgreement');
        $('div[id$=myModalBidAgreement]').on('keydown','.cc-email-bidAgreement', function(e) {
            $(this).removeClass('error-custom');
            if (e.keyCode == 13 || e.keyCode == 32) {
                var getValue = $(this).val();
                if(validateEmail(getValue)) {
                    $('.all-cc-email-bidAgreement').append('<span class="email-ids">'+ getValue +' <span class="cancel-email" onclick="cancelEmail(this)">x</span></span>');
                    $(this).val('');
                }else{
                    $(this).addClass('error-custom');
                }
            }
        });
        $('div[id$=myModalBidAgreement]').off('keydown','.bcc-email-bidAgreement');
        $('div[id$=myModalBidAgreement]').on('keydown','.bcc-email-bidAgreement', function(e) {
            $(this).removeClass('error-custom');
            if (e.keyCode == 13 || e.keyCode == 32) {
                var getValue = $(this).val();
                if(validateEmail(getValue)) {
                    $('.all-bcc-email-bidAgreement').append('<span class="email-ids">'+ getValue +' <span class="cancel-email" onclick="cancelEmail(this)">x</span></span>');
                    $(this).val('');
                }else{
                    $(this).addClass('error-custom');
                }
            }
        });
    }
    function validateEmail(email) {
        var re = /^(([^<>()\[\]\.,;:\s@"]+(\.[^<>()\[\]\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
        return re.test(String(email).toLowerCase());
    }
    function cancelEmail(span){
        $(span).parents('.email-ids').remove();
    }
    //End Email Inputs
    //BidAgreement
    function saveBidAgreement() {
        var message = '';
        for(instance in CKEDITOR.instances) if(instance.includes('bidAgreement_message')) message = CKEDITOR.instances[instance].getData();
        var terms = '';
        for (instance in CKEDITOR.instances) if(instance.includes('bidAgreement_terms')) terms = CKEDITOR.instances[instance].getData();
        saveBidAgreementJs(message, terms);
    }
    function saveBidAgreementMessage(){
        $("span#saveBidAgreementMessage").show();
        setTimeout(function(){$('span#saveBidAgreementMessage').fadeOut('slow');}, 2000);
    }
    function deactivateBidAgreement() {
        if(confirm("Are you sure you want to deactivate this contract?")) deactivateBidAgreementJs();
    }
    function setupBidAgreement(){
        $('#myModalBidAgreement input.cc-email-bidAgreement').autocomplete({
            lookup: function (query, done){
                Visualforce.remoting.Manager.invokeAction(
                    '{!$RemoteAction.GTDashboard_Tab_GT_Bid_Controller.searchContactEmail}',query,
                    function(result, event){
                        if (event.status) {
                            var t1 = result;
                            var results = t1.replace(/(&quot\;)/g,"\"").replace(/&#39;/g,"'").replace(/(&amp\;)/g,"&").replace(/(&lt\;)/g,"<").replace(/(&gt\;)/g,">");
                            var resultAuto = {
                                suggestions: JSON.parse(results)
                            };
                            done(resultAuto);
                        } else if (event.type === 'exception') {
                            alert('exception');
                        } else {
                            alert('other');
                        }
                    }, 
                    {escape: true}
                );
            },
            onSelect: function (suggestion) {
                $(this).prev().append('<span class="email-ids" data-contactid="' + suggestion.data + '">'+ suggestion.extra1 +' <span class="cancel-email" onclick="cancelEmail(this)">x</span></span>');
                $(this).val('');
            }
        });
        $('#myModalBidAgreement input.bcc-email-bidAgreement').autocomplete({
            lookup: function (query, done){
                Visualforce.remoting.Manager.invokeAction(
                    '{!$RemoteAction.GTDashboard_Tab_GT_Bid_Controller.searchContactEmail}',query,
                    function(result, event){
                        if (event.status) {
                            var t1 = result;
                            var results = t1.replace(/(&quot\;)/g,"\"").replace(/&#39;/g,"'").replace(/(&amp\;)/g,"&").replace(/(&lt\;)/g,"<").replace(/(&gt\;)/g,">");
                            var resultAuto = {
                                suggestions: JSON.parse(results)
                            };
                            done(resultAuto);
                        } else if (event.type === 'exception') {
                            alert('exception');
                        } else {
                            alert('other');
                        }
                    }, 
                    {escape: true}
                );
            },
            onSelect: function (suggestion) {
                $(this).prev().append('<span class="email-ids" data-contactid="' + suggestion.data + '">'+ suggestion.extra1 +' <span class="cancel-email" onclick="cancelEmail(this)">x</span></span>');
                $(this).val('');
            }
        });
    }
    //End BidAgreement
    //ResendBid
    function changeContactVendorResendBid(val,accountid) {
        changeContactVendorResendBidJs($(val).val(),accountid);
    }
    function validateResultAddContactBid() {
        var message_contact = $('input[id$=addcontactvendor_message]').val();
        console.log(message_contact);
        if(message_contact.trim() == '') {
            viewModalIndex('myModalResendBid');
            viewModalIndex('myModalReleaseByBid');
            closeModal('myModalAddContactVendor');
            $('.message-create-contact-vendor').hide();
        }
    }
    //End ResendBid
    //ReleaseBid
    function openReleaseByBid() {
        if(reviewCoordinator()) openReleaseByBidJs();
        else alert('Freight Coordinator is not for this this tour please add');
    }
    function reviewCoordinator() {
        var coordinator = $('input[id$=production_coordinator_bid]').val();
        console.log('coordinator:'+coordinator);
        if(coordinator.trim() != '') return true;
        return false;
    }
    function sendReleaseByBid() {
        var primary_contact = $('select[id$=releasebybid_contactprimary]').val();
        if(primary_contact != null && primary_contact != '') {
            sendReleaseByBidJs(primary_contact);
        }else{
            alert('No contacts found. Please make sure Vendor has Contacts.');
        }
    }
    function changeContactVendorReleaseByBid(val,accountid) {
        changeContactVendorReleaseByBidJs($(val).val(),accountid);
    }
    
    //End ResendBid
    //DeactivateBid
    function deactivateBid() {
        if(confirm("Are you sure you want to deactivate this bid?")) deactivateBidJs();
    }
    //End DeactivateBid
    //AddContacts
    function openContactVendor(id,name,contactid){
        $('input[id$=addcontact_lastname]').removeClass('error-custom');
        $('input[id$=addcontact_lastname]').val('');
        $('input[id$=addcontact_firstname]').val('');
        $('select[id$=addcontact_designation]').val('');
        $('input[id$=addcontact_phone]').val('');
        $('input[id$=addcontact_extension]').val('');
        $('input[id$=addcontact_mobile]').val('');
        $('input[id$=addcontact_fax]').val('');
        $('input[id$=addcontact_email]').val('');
        $('input[id$=addcontact_alternateemail]').val('');
        $('textarea[id$=addcontact_internalnotes]').val('');
        $('input[id$=addcontact_address1]').val('');
        $('input[id$=addcontact_address2]').val('');
        $('input[id$=addcontact_city]').val('');
        $('input[id$=addcontact_cityid]').val('');
        $('input[id$=addcontact_postalcode]').val('');
        $('input[id$=addcontact_accountid]').val(id);
        $('input[id$=addcontact_contactid]').val(contactid);
        $('#myModalBidAgreement').css('z-index','1039');
        $('#myModalResendBid').css('z-index','1039');
        $('#myModalReleaseByBid').css('z-index','1039');
        $('.message-create-contact-vendor').hide();
        if(contactid.trim() != ''){
            $('#myModalAddContactVendor').find('.modal-title').text('Edit This Contact of "' + name + '"');
            Visualforce.remoting.Manager.invokeAction(
                '{!$RemoteAction.GTDashboard_Tab_GT_Bid_Controller.getDataContact}',
                contactid,
                function(result, event){
                    if (event.status) {
                        console.log(result);
                        $('input[id$=addcontact_firstname]').val(result.FirstName);
                        $('input[id$=addcontact_lastname]').val(result.LastName);
                        $('select[id$=addcontact_designation]').val(result.Designation_title__c);
                        $('input[id$=addcontact_phone]').val(result.Phone);
                        $('input[id$=addcontact_extension]').val(result.Work_Phone_Extension__c);
                        $('input[id$=addcontact_mobile]').val(result.MobilePhone);
                        $('input[id$=addcontact_fax]').val(result.Fax);
                        $('input[id$=addcontact_email]').val(result.Email);
                        $('input[id$=addcontact_alternateemail]').val(result.Alternate_Email__c);
                        $('textarea[id$=addcontact_internalnotes]').val(result.Description);
                        $('input[id$=addcontact_address1]').val(result.MailingStreet);
                        $('input[id$=addcontact_address2]').val(result.OtherStreet);
                        $('input[id$=addcontact_cityid]').val(result.City__c);
                        if(result.City__c != null && result.City__c != '') $('input[id$=addcontact_city]').val(result.City__r.Name);
                        $('input[id$=addcontact_postalcode]').val(result.MailingPostalCode);
                        openModal('myModalAddContactVendor');
                    } else if (event.type === 'exception') {
                        alert('exception');
                    } else {
                        alert('other');
                    }
                }, 
                {escape: true}
            );
        }else{
            $('#myModalAddContactVendor').find('.modal-title').text('Add New Contact for "' + name + '"');
            openModal('myModalAddContactVendor');
        }
    }
    function saveAddContactVendorBid() {
        var lastname = $('input[id$=addcontact_lastname]').val();
        var email = $('input[id$=addcontact_email]').val();
        $('input[id$=addcontact_lastname]').removeClass('error-custom');
        $('input[id$=addcontact_email]').removeClass('error-custom');
        if(lastname.trim() != '' && email.trim() != '') {
            var accountid = $('input[id$=addcontact_accountid]').val();
            var contactid = $('input[id$=addcontact_contactid]').val();
            var firstname = $('input[id$=addcontact_firstname]').val();
            var designation = $('select[id$=addcontact_designation]').val();
            var phone = $('input[id$=addcontact_phone]').val();
            var extension = $('input[id$=addcontact_extension]').val();
            var mobile = $('input[id$=addcontact_mobile]').val();
            var fax = $('input[id$=addcontact_fax]').val();
            
            var alternateemail = $('input[id$=addcontact_alternateemail]').val();
            var internalnotes = $('textarea[id$=addcontact_internalnotes]').val();
            var address1 = $('input[id$=addcontact_address1]').val();
            var address2 = $('input[id$=addcontact_address2]').val();
            var cityid = $('input[id$=addcontact_cityid]').val();
            var postalcode = $('input[id$=addcontact_postalcode]').val();
            saveAddContactVendorBidJs(accountid,contactid,firstname,lastname,designation,phone,extension,mobile,fax,email,alternateemail,internalnotes,address1,address2,cityid,postalcode);
        }else{
            if(lastname.trim() == '') $('input[id$=addcontact_lastname]').addClass('error-custom');
            if(email.trim() == '') $('input[id$=addcontact_email]').addClass('error-custom');
        }
    }
    //End AddContacts
    //Attachs
    function remoteLocationPostLast(event,type,charge,recordId) {
        var input = event.target;
        var reader = new FileReader();
        reader.onload = function(){
            var dataURL = reader.result;
            $('input[id$=output]').val(dataURL);
        };
        reader.readAsDataURL(input.files[0]);
        setTimeout(function() {
            fileUploadLast(type,charge,recordId);
        }, 2000);
    };
    function fileUploadLast(type,charge,recordId) {
        var fileData;
        switch(type) {
            case 'Rate Agreement': fileData = $('input[id$=fileBidAgreement]').val(); break;
        }
        $('input[id$=attachment_new_charge]').val(charge);
        var pieces = fileData.split('\');
        var filename = pieces[pieces.length-1];
        var fileBlob = $('input[id=output]').val();
        console.log('recordId: ' + recordId);
        passToControllerLast(filename,recordId);
    }
    function openAttachDocs(typez,object_id,modal_parent,modal_select) {
        $('input[id$=attachdocument_modal]').val(modal_parent);
        $('input[id$=attachdocument_select_id]').val(modal_select);
        console.log('modal_select: ' + modal_select);
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
            console.log('selectid: ' + selectid);
            $('input[id$=document-attach-ids]').val(document_ids);
            $('input[id$=document-attach-names]').val(document_names);
            for(x=0; x < document_ids.length; x++){
                $('select[id$='+selectid+']').append('<option value="'+document_ids[x]+'">' + document_names[x] +'</option>');
            }
            
            viewModalIndex(modalid);
            closeModal('myModalAttachDocuments');
        }else{
            alert('Please select a Production Document.');
        }
    }
    function removeAttachDocs(modal_select) {
        var selected = $('select[id$='+modal_select+']').val();
        $('select[id$='+modal_select+']').find('option[value="'+ selected +'"]').remove();
    }
    function setDataToSelect() {
        var selectid = $('input[id$=attachment_new_charge]').val();
        var attachment_new_id = $('input[id$=attachment_new_id]').val();
        var attachment_new_name = $('input[id$=attachment_new_name]').val();
        $('select[id$='+selectid+']').append('<option value="'+attachment_new_id+'">' + attachment_new_name +'</option>');
    }
    function selectDocumentProdRow(val) {
        var selected = $(val).hasClass("highlighted");
        if(!selected)
            $(val).addClass("highlighted");
        else
            $(val).removeClass("highlighted");
    }
    //End Attachs
    /*---@Conga: Update for Conga---*/
    function congaPreviewOptions(bidId, bidStatus, tripId, congaQueriesJson, congaTemplateId){ 
        var congaQueriesMap = JSON.parse(congaQueriesJson);
        window.open('/apex/APXTConga4__Conga_Composer?id=' + tripId + (congaQueriesMap.hasOwnProperty('GT - BidsWithOptionsByBidId') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidsWithOptionsByBidId'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') : '') + '&OFN=GT+Options&TemplateId=' + congaTemplateId + '&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=800, resizable=yes, toolbar=no, location=no, status=yes');
    }
    function congaPreviewBid(bidId, bidName, bidStatus, tripId, congaQueriesJson, congaTemplateId){ 
        var primary_contact = $('select[id$=biddata_primarycontact]').val();
        var congaQueriesMap = JSON.parse(congaQueriesJson);
        window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('GT - UserById') ? ',[EmailFromUser]' + congaQueriesMap['GT - UserById'].Id + '?pv0=' + $('input[id$=resendBidAgreement_emailFromUserId]').val() : '') : '') + '&TemplateId=' + congaTemplateId + '&OFN=GT+Bid-' + bidName + '&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=800, resizable=yes, toolbar=no, location=no, status=yes');
    }
    function congaPreviewBidAgreementHandler(){
        var message = '';
        for(instance in CKEDITOR.instances) if(instance.includes('bidAgreement_message')) message = CKEDITOR.instances[instance].getData();
        var terms = '';
        for (instance in CKEDITOR.instances) if(instance.includes('bidAgreement_terms')) terms = CKEDITOR.instances[instance].getData();
        congaPreviewBidAgreementJs(message, terms);
    }
    function congaPreviewBidAgreement(bidId, bidName, tripId, tripName, congaQueriesJson, congaTemplateId) {
        var primary_contact = $('#myModalBidAgreement .modal-title').text() == 'Rate Agreement' ? $('select[id$=bidAgreementContactSelect]').val() : $('#myModalBidAgreement .modal-title').text() == 'Trip Details Update' ? $('select[id$=bidAgreementAttentionContactSelect]').val() : $('#myModalBidAgreement .modal-title').text() == 'Transportation Contract' ? $('select[id$=bidAgreementContactSelect]').val() : '';
        var client_contact = $('select[id$=bidAgreementProductionAssociationContactsSelect]').val();
        var congaQueriesMap = JSON.parse(congaQueriesJson);
        if($('#myModalBidAgreement .modal-title').text() == 'Rate Agreement') window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('GT - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['GT - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&OFN=GT+Rate+Agreement-' + tripName + '&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=800, resizable=yes, toolbar=no, location=no, status=yes');
        else if($('#myModalBidAgreement .modal-title').text() == 'Trip Details Update') window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&OFN=GT+Trip+Details+Update-' + tripName + '&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=800, resizable=yes, toolbar=no, location=no, status=yes');
        else if($('#myModalBidAgreement .modal-title').text() == 'Transportation Contract') window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('GT - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['GT - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&OFN=GT+Transportation+Contract-' + tripName + '&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=800, resizable=yes, toolbar=no, location=no, status=yes');
    }
    function congaSendBidAgreementHandler() {
        var message = '';
        for(instance in CKEDITOR.instances) if(instance.includes('bidAgreement_message')) message = CKEDITOR.instances[instance].getData();
        var terms = '';
        for (instance in CKEDITOR.instances) if(instance.includes('bidAgreement_terms')) terms = CKEDITOR.instances[instance].getData();
        congaSendBidAgreementJs(message, terms);
    }
    function congaSendBidAgreement(bidId, bidName, tripId, tripName, congaQueriesJson, congaEmailTemplateId, congaTemplateId){
        var primary_contact = $('#myModalBidAgreement .modal-title').text() == 'Rate Agreement' ? $('select[id$=bidAgreementContactSelect]').val() : $('#myModalBidAgreement .modal-title').text() == 'Trip Details Update' ? $('select[id$=bidAgreementAttentionContactSelect]').val() : $('#myModalBidAgreement .modal-title').text() == 'Transportation Contract' ? $('select[id$=bidAgreementContactSelect]').val() : '';
        var primary_contactName = $('#myModalBidAgreement .modal-title').text() == 'Rate Agreement' ? $('select[id$=bidAgreementContactSelect]').children("option:selected").text() : $('#myModalBidAgreement .modal-title').text() == 'Trip Details Update' ? $('select[id$=bidAgreementAttentionContactSelect]').children("option:selected").text() : $('#myModalBidAgreement .modal-title').text() == 'Transportation Contract' ? $('select[id$=bidAgreementContactSelect]').children("option:selected").text() : '';
        var primary_contactEmail = $('#bidAgreement_primarycontactemail').text();
        var client_contact = $('select[id$=bidAgreementProductionAssociationContactsSelect]').val();
        var congaEmailSubject = $('input[id$=bidAgreement_subject]').val();
        var cc_emails = '';
        $("#myModalBidAgreement .all-cc-email-bidAgreement span.email-ids").each(function(){
            cc_emails = cc_emails.trim() != "" ? cc_emails + ',' + $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','') : $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','');
        });
        var bcc_emails = '';
        $("#myModalBidAgreement .all-bcc-email-bidAgreement span.email-ids").each(function(){
            bcc_emails = bcc_emails.trim() != "" ? bcc_emails + ',' + $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','') : $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','');
        });
        var attachments = '';
        $("select[id$=bidAgreement_attachs] option").each(function(){
            attachments = attachments.trim() != "" ? attachments + ',' + $(this).val() : $(this).val();
        });
        if($('#myModalBidAgreement .modal-title').text() == 'Rate Agreement'){
            var updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Rate_Agreement_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Rate Agreement email was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
            var congaQueriesMap = JSON.parse(congaQueriesJson);
            window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('GT - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['GT - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=GT+Rate+Agreement-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
        }
        else if($('#myModalBidAgreement .modal-title').text() == 'Trip Details Update'){
            var updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Trip_Details_Update_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Trip Details Update was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
            var congaQueriesMap = JSON.parse(congaQueriesJson);
            window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=GT+Trip+Details+Update-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
        }
        else if($('#myModalBidAgreement .modal-title').text() == 'Transportation Contract'){
            var updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Transportation_Contract_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Transportation Contract was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
            var congaQueriesMap = JSON.parse(congaQueriesJson);
            window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('GT - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['GT - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=GT+Transportation+Contract-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
        }
    }
    function congaSignBidAgreementHandler() {
        var primary_contactEmail = $('#bidAgreement_primarycontactemail').text();
        var cc_emails = '';
        $("#myModalBidAgreement .all-cc-email-bidAgreement span.email-ids").each(function(){
            cc_emails = cc_emails.trim() != "" ? cc_emails + ',' + $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','') : $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','');
        });
        var bcc_emails = '';
        $("#myModalBidAgreement .all-bcc-email-bidAgreement span.email-ids").each(function(){
            bcc_emails = bcc_emails.trim() != "" ? bcc_emails + ',' + $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','') : $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','');
        });
        var message = '';
        for(instance in CKEDITOR.instances) if(instance.includes('bidAgreement_message')) message = CKEDITOR.instances[instance].getData();
        var terms = '';
        for(instance in CKEDITOR.instances) if(instance.includes('bidAgreement_terms')) terms = CKEDITOR.instances[instance].getData();
        if($('#myModalBidAgreement .modal-title').text() == 'Rate Agreement'){
            if(confirm('An email will be sent before initiating the Conga Sign Process')){
                if(primary_contactEmail.trim() != "") congaSignBidAgreementJs(primary_contactEmail, cc_emails, bcc_emails, message, terms, true);
                else alert("Please you must select a vendor contact.");
            }
        }
        else if($('#myModalBidAgreement .modal-title').text() == 'Trip Details Update'){
            if(primary_contactEmail.trim() != "") congaSignBidAgreementJs(primary_contactEmail, cc_emails, bcc_emails, message, terms, false);
            else alert("Please you must select a vendor contact.");
        }
        else if($('#myModalBidAgreement .modal-title').text() == 'Transportation Contract'){
            if(confirm('An email will be sent before initiating the Conga Sign Process')){
                if(primary_contactEmail.trim() != "") congaSignBidAgreementJs(primary_contactEmail, cc_emails, bcc_emails, message, terms, true);
                else alert("Please you must select a vendor contact.");
            }
        }
    }
    function congaSignBidAgreement(bidId, bidName, tripId, tripName, congaQueriesJson, congaTemplateId, emailResult) {
        var primary_contact = $('#myModalBidAgreement .modal-title').text() == 'Rate Agreement' ? $('select[id$=bidAgreementContactSelect]').val() : $('#myModalBidAgreement .modal-title').text() == 'Trip Details Update' ? $('select[id$=bidAgreementAttentionContactSelect]').val() : $('#myModalBidAgreement .modal-title').text() == 'Transportation Contract' ? $('select[id$=bidAgreementContactSelect]').val() : '';
        var client_contact = $('select[id$=bidAgreementProductionAssociationContactsSelect]').val();
        var csCCRecipients = '';
        var i;
        if($("#myModalBidAgreement .all-bcc-email-bidAgreement span.email-ids").length != 0) alert('BCC emails will not be transferred over to conga sign.');
        if($('#myModalBidAgreement .modal-title').text() == 'Rate Agreement'){
            if(emailResult.trim() == ""){
                i = 2;
                $("#myModalBidAgreement .all-cc-email-bidAgreement span.email-ids").each(function(){
                    csCCRecipients = csCCRecipients.trim() != "" ? csCCRecipients + '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC' : '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC';
                    i++;
                });
                var congaQueriesMap = JSON.parse(congaQueriesJson);
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('GT - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['GT - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&CSRecipient1=' + primary_contact + csCCRecipients + '&csvisible=1&CSRoutingType=SERIAL&csRequestReminder=2&OFN=GT+Rate+Agreement-' + tripName + '&DS7=1141&DefaultPDF=1&contentShareType=V&contentVisibility=AllUsers', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=900, resizable=yes, toolbar=no, location=no, status=yes');            
            }
            else alert(emailResult);
        } 
        else if($('#myModalBidAgreement .modal-title').text() == 'Trip Details Update'){
            i = 2;
            $("#myModalBidAgreement .all-cc-email-bidAgreement span.email-ids").each(function(){
                csCCRecipients = csCCRecipients.trim() != "" ? csCCRecipients + '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC' : '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC';
                i++;
            });
            var congaQueriesMap = JSON.parse(congaQueriesJson);
            window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&CSRecipient1=' + primary_contact + csCCRecipients + '&csvisible=1&CSRoutingType=SERIAL&csRequestReminder=2&OFN=GT+Trip+Details+Update-' + tripName + '&DS7=1141&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=900, resizable=yes, toolbar=no, location=no, status=yes');            
        } 
        else if($('#myModalBidAgreement .modal-title').text() == 'Transportation Contract'){
            if(emailResult.trim() == ""){
                i = 3;
                $("#myModalBidAgreement .all-cc-email-bidAgreement span.email-ids").each(function(){
                    csCCRecipients = csCCRecipients.trim() != "" ? csCCRecipients + '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC' : '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC';
                    i++;
                });
                var congaQueriesMap = JSON.parse(congaQueriesJson);
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('GT - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['GT - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&CSRecipient1=' + primary_contact + csCCRecipients + '&csvisible=1&CSRoutingType=SERIAL&csRequestReminder=2&OFN=GT+Transportation+Contract-' + tripName + '&DS7=1141&DefaultPDF=1&contentShareType=V&contentVisibility=AllUsers', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=900, resizable=yes, toolbar=no, location=no, status=yes');            
            }
            else alert(emailResult);
        } 
    }
    function congaPreviewResendBid(itineraryId, tripId, tripStatus, bidId, bidName, bidStatus, congaQueriesJson, congaEmailSubject, congaEmailTemplateId, congaTemplateId){ 
        var primary_contact = $('select[id$=resendbid_contactprimary]').val();
        var primary_contactName = $('select[id$=resendbid_contactprimary]').children("option:selected").text();
        var primary_contactEmail = '';
        var emails = '';
        if(primary_contact != null && primary_contact != ''){
            $('#myModalResendBid').find('.check-contact').each(function(){
                if($(this).is(":checked") && $(this).parents("td").data('contactid') != primary_contact) emails = emails.trim() != "" ? emails + ', ' + $(this).parents("td").data('contactemail') : $(this).parents("td").data('contactemail');
                else primary_contactEmail = $(this).parents("td").data('contactemail');
            });
            //var updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=New_Journal_RecordType__c&MFTSValue0=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_Entry__c&MFTSValue1=' + 'Resend Bid email was sent to ' + primary_contactName + ' ' + primary_contactEmail + (emails != '' ? ', cc: ' + emails : '');
            var i = 0;
            var updates = '&UF0=1';
            if(bidId != '' && bidStatus != 'Contracted'){
                updates += '&MFTSId' + i + '=' + bidId + '&MFTS' + i + '=Status__c&MFTSValue' + i + '=Sent';
                i++;
            }
            if(tripId != '' && tripStatus != 'Contracted'){
                updates += '&MFTSId' + i + '=' + tripId + '&MFTS' + i + '=Status_Ground__c&MFTSValue' + i + '=Bid Request Stage';
                i++;
                if(itineraryId != '') updates += '&MFTSId' + i + '=' + itineraryId + '&MFTS' + i + '=Status__c&MFTSValue' + i + '=Bid Request Stage';
            }
            var congaQueriesMap = JSON.parse(congaQueriesJson);
            window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('GT - UserById') ? ',[EmailFromUser]' + congaQueriesMap['GT - UserById'].Id + '?pv0=' + $('input[id$=resendBidAgreement_emailFromUserId]').val() : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=resendBidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=resendBidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + emails + '&TemplateId=' + congaTemplateId + updates + '&OFN=GT+Bid-' + bidName + '&DS7=2&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
        }
        else alert('No contacts found. Please make sure Vendor has Contacts.');
    }
    function congaResendBid() {
        var primary_contact = $('select[id$=resendbid_contactprimary]').val();
        if(primary_contact != null && primary_contact != '') congaResendBidJs();
        else alert('No contacts found. Please make sure Vendor has Contacts.');
    }
    /*---@/Conga---*/
    </script>
</apex:component>
```


# Last Modified


# Usage
