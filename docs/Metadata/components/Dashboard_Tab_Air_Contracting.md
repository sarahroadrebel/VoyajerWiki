---
layout: default
title: Dashboard_Tab_Air_Contracting
parent: components
grand_parent: Metadata
---
# Metadata Type
components


# Filename 
Dashboard_Tab_Air_Contracting


# Raw XML
```
<apex:component layout="block" controller="Dashboard_Tab_Contracting" allowDML="true">
    <!-- COMPONENT VARIABLES -->
    <apex:attribute type="DashboardConfigurationWrapper" name="variables" assignTo="{!vfpConfiguration}" description="The variables of the VFP" required="true" />
    <style>
        .input-search { padding-right: 1.8rem !important; }
        .input-search-wrapper { display: inline-block; position: relative; }
        .input-search-wrapper:after { font-family: 'Font Awesome\ 5 Free'; font-weight: 900; content: '002'; position: absolute; right: 0.5rem; top: 0.25rem; font-size: 1rem; color: #495057; }
        .tableResult td, .tableResult th { padding-left: 0.5em !important; border-left: 1px solid rgba(0,0,0,.125); border-right: 1px solid rgba(0,0,0,.125); }
        .tableResult .theadResult th { color: #495057; background-color: #e9ecef; border-color: #dee2e6; }
        .darkCard { background-color: #efefef; }
        .input-group-text { background-color: #ffffff; }
        /** LOADING SUB TAB **/
        /* Absolute Center Spinner */
        /*.loadingSubTab { position: absolute; z-index: 1051; height: 1em; width: 1em; margin: auto; top: 0; left: 0; bottom: 0; right: 0; }*/
        
        /* Transparent Overlay */
        .loadingSubTab:before { content: ''; display: block; z-index: 1051; position: absolute; top: 0; left: 0; width: 100%; height: 100%; background-color: rgba(0,0,0,0.3); }
        
        /* :not(:required) hides these rules from IE9 and below */
        .loadingSubTabSpinner:not(:required) { /* hide "loading..." text */ font: 0/0 a; width: 1em; height: 1em; margin: auto; color: transparent; text-shadow: none; background-color: transparent; border: 0; }
        .loadingSubTabSpinner:not(:required):after { content: ''; display: block; font-size: 10px; width: 1em; height: 1em; margin-top: -0.5em; -webkit-animation: spinner 1500ms infinite linear; -moz-animation: spinner 1500ms infinite linear; -ms-animation: spinner 1500ms infinite linear; -o-animation: spinner 1500ms infinite linear; animation: spinner 1500ms infinite linear; border-radius: 0.5em; -webkit-box-shadow: rgba(0, 0, 0, 0.75) 1.5em 0 0 0, rgba(0, 0, 0, 0.75) 1.1em 1.1em 0 0, rgba(0, 0, 0, 0.75) 0 1.5em 0 0, rgba(0, 0, 0, 0.75) -1.1em 1.1em 0 0, rgba(0, 0, 0, 0.5) -1.5em 0 0 0, rgba(0, 0, 0, 0.5) -1.1em -1.1em 0 0, rgba(0, 0, 0, 0.75) 0 -1.5em 0 0, rgba(0, 0, 0, 0.75) 1.1em -1.1em 0 0; box-shadow: rgba(0, 0, 0, 0.75) 1.5em 0 0 0, rgba(0, 0, 0, 0.75) 1.1em 1.1em 0 0, rgba(0, 0, 0, 0.75) 0 1.5em 0 0, rgba(0, 0, 0, 0.75) -1.1em 1.1em 0 0, rgba(0, 0, 0, 0.75) -1.5em 0 0 0, rgba(0, 0, 0, 0.75) -1.1em -1.1em 0 0, rgba(0, 0, 0, 0.75) 0 -1.5em 0 0, rgba(0, 0, 0, 0.75) 1.1em -1.1em 0 0; }
        /** END LOADING **/
    </style>
    <div class="row">
        <div class="col-md-12 text-right" style="margin-bottom:10px;">
            <button type="button" class="btn btn-danger btn-sm btn-custom" onclick="loadTabContent('gt-itinerary');" >All Events</button>
            <!--<apex:outputPanel id="tripInformationHeaderPanel">
                <span style="font-size:15px;margin-left:15px;">Production ID: </span><span style="font-weight:bold;font-size:15px;">{!opportunity.Production_ID__c}</span> | 
                <span style="font-size:15px;margin-left:5px;">Trip ID: </span><span style="font-weight:bold;font-size:15px;">{!tripView.Name}</span>
            </apex:outputPanel>-->
        </div>
    </div>
    <div class="expand" style="margin-bottom: 0.5em;">
        <div class="card" style="padding-bottom: 1em;margin-bottom:10px;">
            <div class="row" style="align-items: flex-end; padding: 0 1em 1em;">
                <div class="col-md-2">
                    <label for="contractSearchBoxStartDate">From Date</label><br/>
                    <apex:inputField id="contractSearchBoxStartDate" value="{!groundFilter.Start_Date__c}" styleClass="form-control form-control-sm" />
                </div>
                <div class="col-md-2">
                    <label for="contractSearchBoxEndDate">To Date</label><br/>
                    <apex:inputField id="contractSearchBoxEndDate" value="{!groundFilter.End_Date__c}" styleClass="form-control form-control-sm" />
                </div>
                <div class="col-md-2">
                    <span style="margin-top: 25px;display: block;">
                        <label for="contractSearchBoxIsPriorTrip">Show Prior Trips</label><apex:inputCheckbox value="{!searchBoxWrapper.isPriorTrip}" id="contractSearchBoxIsPriorTrip" />
                    </span>
                </div>
            </div>
            <div class="row" style="align-items: flex-end; padding: 0 1em 1em;">
                <div class="col-md-2">
                    <label>City</label>
                    <input id="contractCity" class="form-control form-control-sm gtcontract-city" value="{!searchBoxWrapper.city}" onkeyup="setInputContractCity();" />
                    <script>
                    createAutocompleteContractCity = false;
                    </script>
                </div>
                <div class="col-md-2">
                    <label>Vendor</label>
                    <input id="contractVendor" class="form-control form-control-sm gtcontract-vendor" value="{!searchBoxWrapper.vendor}" onkeyup="setInputContractVendor();" />
                    <script>
                    createAutocompleteContractVendor = false;
                    </script>
                </div>
                <!--<div class="col-md-3">
                    <label>Status</label>
                    <apex:selectList size="1" id="contractSearchBoxStatusValue" styleClass="form-control form-control-sm">
                        <apex:selectOptions value="{!bidContractStatusOptions}" />
                    </apex:selectList>
                </div>-->
                <div class="col-md-2">
                    <span style="margin-top: 25px;display: block;">
                        <label for="contractSearchBoxIsCancelled">Show Cancelled</label><apex:inputCheckbox value="{!searchBoxWrapper.isCancelled}" id="contractSearchBoxIsCancelled" />
                    </span>
                </div>
            </div>
            <div class="row" style="align-items: center;">
                <div class="col-md-3">
                    <button type="button" class="btn btn-sm btn-info btn-custom" onclick="searchBidContracting();">Search</button>
                    <button type="button" class="btn btn-sm btn-outline-dark" onclick="clearBidContracting();">Clear</button>
                </div>
            </div>
        </div>
        <apex:outputPanel id="bidContractList" layout="block">
            <apex:inputHidden id="isPageLoadedInput" value="{!isPageLoaded}" />
            <apex:inputHidden id="orderFieldBidContractActual" value="{!orderFieldBidContract}" />
            <input type="hidden" value="{!limitContract}" id="listtrip_limitContract" />
            <input type="hidden" value="{!offsetContract}" id="listtrip_offsetContract" />
            <input type="hidden" value="{!totalPagesContract}" id="listtrip_totalPagesContract" />
            <div style="display: flex; padding: 4px; background-color:#e9ecef; border: 1px solid #dee2e6;">
                <div style="flex: 1; display: flex; align-items: center;">
                    <button class="btn btn-secondary btn-sm filePaginator btn-nav-modal btn-listcontract-first" type="button" onclick="GotoPageContract('first');">
                        <i class="fas fa-step-backward"></i>
                    </button>
                    <button class="btn btn-secondary btn-sm btn-nav-modal btn-listcontract-previous" type="button" style="padding-right: 3px;" onclick="GotoPageContract('previous');">
                        <i class="fas fa-caret-left fa-lg"></i>
                    </button>
                    <button class="btn btn-secondary btn-sm btn-nav-modal btn-listcontract-next" type="button" style="padding-left: 3px;" onclick="GotoPageContract('next');">
                        <i class="fas fa-caret-right fa-lg"></i>
                    </button>
                    <button class="btn btn-secondary btn-sm btn-nav-modal btn-listcontract-last" type="button" onclick="GotoPageContract('last');">
                        <i class="fas fa-step-forward"></i>
                    </button>
                </div>
                <div style="display: flex;">
                    <div class="fileNavigatorMessage" style="display: flex; flex: 1; align-self: center;">Page {!IF(OR(offsetContract == null,offsetContract <= 0),1,(offsetContract/limitContract)+1)} of {!totalPagesContract}</div>
                </div>
            </div>
            <table class="table tableResult table-sm" style="margin-top:0; margin-bottom:0; border-bottom: 1px solid #dee2e6;">
                <thead class="theadResult">
                    <tr>
                        <th scope="col" width="10%">
                            <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidContracts('Air__r.Departure_Date__c','{!orderOrientationBidContract}');">
                                <span style="float:left;">Departure Date</span>
                                <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldBidContract == 'Air__r.Departure_Date__c',orderOrientationBidContract == 'DESC'),'','display:none;')}"></i>
                                <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldBidContract == 'Air__r.Departure_Date__c',orderOrientationBidContract == 'ASC'),'','display:none;')}"></i>
                            </a>
                        </th>
                        <th scope="col" width="10%">
                            <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidContracts('Air__r.Dep_Arr__c','{!orderOrientationBidContract}');">
                                <span style="float:left;">Dep/Arr</span>
                                <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldBidContract == 'Air__r.Dep_Arr__c',orderOrientationBidContract == 'DESC'),'','display:none;')}"></i>
                                <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldBidContract == 'Air__r.Dep_Arr__c',orderOrientationBidContract == 'ASC'),'','display:none;')}"></i>
                            </a>
                        </th>
                        <th scope="col" width="10%">
                            <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidContracts('Air__r.Return_Date__c','{!orderOrientationBidContract}');">
                                <span style="float:left;">RT Date</span>
                                <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldBidContract == 'Air__r.Return_Date__c',orderOrientationBidContract == 'DESC'),'','display:none;')}"></i>
                                <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldBidContract == 'Air__r.Return_Date__c',orderOrientationBidContract == 'ASC'),'','display:none;')}"></i>
                            </a>
                        </th>
                        <th scope="col" width="10%">
                            <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidContracts('Air__r.RT_Dep_Arr__c','{!orderOrientationBidContract}');">
                                <span style="float:left;">RT Dep/Arr</span>
                                <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldBidContract == 'Air__r.RT_Dep_Arr__c',orderOrientationBidContract == 'DESC'),'','display:none;')}"></i>
                                <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldBidContract == 'Air__r.RT_Dep_Arr__c',orderOrientationBidContract == 'ASC'),'','display:none;')}"></i>
                            </a>
                        </th>
                        <th scope="col" width="10%">
                            <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidContracts('Air__r.Trip_Type__c','{!orderOrientationBidContract}');">
                                <span style="float:left;">Trip Type</span>
                                <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldBidContract == 'Air__r.Trip_Type__c',orderOrientationBidContract == 'DESC'),'','display:none;')}"></i>
                                <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldBidContract == 'Air__r.Trip_Type__c',orderOrientationBidContract == 'ASC'),'','display:none;')}"></i>
                            </a>
                        </th>
                        <th scope="col" width="20%">
                            <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidContracts('Vendor__r.Name','{!orderOrientationBidContract}');">
                                <span style="float:left;">Vendor</span>
                                <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldBidContract == 'Vendor__r.Name',orderOrientationBidContract == 'DESC'),'','display:none;')}"></i>
                                <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldBidContract == 'Vendor__r.Name',orderOrientationBidContract == 'ASC'),'','display:none;')}"></i>
                            </a>
                        </th>
                        <th scope="col" width="15%">
                            <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidContracts('Air__r.PAX__c','{!orderOrientationBidContract}');">
                                <span style="float:left;">#PAX</span>
                                <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldBidContract == 'Air__r.PAX__c',orderOrientationBidContract == 'DESC'),'','display:none;')}"></i>
                                <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldBidContract == 'Air__r.PAX__c',orderOrientationBidContract == 'ASC'),'','display:none;')}"></i>
                            </a>
                        </th>
                        <th scope="col" width="15%">
                            <a href="javascript:void(0);" style="color: #495057;" onclick="sortBidContracts('Status__c','{!orderOrientationBidContract}');">
                                <span style="float:left;">Status</span>
                                <i class="fas fa-sort-down" style="float:left;margin-top:2px;margin-left:5px;{!IF(AND(orderFieldBidContract == 'Status__c',orderOrientationBidContract == 'DESC'),'','display:none;')}"></i>
                                <i class="fas fa-sort-up" style="float:left;margin-top:7px;margin-left:5px;{!IF(AND(orderFieldBidContract == 'Status__c',orderOrientationBidContract == 'ASC'),'','display:none;')}"></i>
                            </a>
                        </th>
                    </tr>
                </thead>
                <tbody>
                    <apex:repeat value="{!bidContractsList}" var="bid">
                        <tr>
                            <td>
                                <span class="show-data">
                                    <a href="javascript:void(0);" onclick="viewBidContracted('{!bid.bidId}','{!bid.bidName}','{!bid.parentId}')">
                                        <apex:outputField value="{!bid.airTrip.Departure_Date__c}"/>
                                    </a>
                                </span>
                            </td>
                            <td>
                                <span class="show-data">{!bid.dep_arr}</span>
                            </td>
                            <td>
                                <span class="show-data">
                                    <apex:outputField value="{!bid.airTrip.Return_Date__c}"/>
                                </span>
                            </td>
                            <td>
                                <span class="show-data">{!bid.rt_dep_arr}</span>
                            </td>
                            <td>
                                <span class="show-data">{!bid.trip_type}</span>
                            </td>
                            <td>
                                <span class="show-data">
                                    <apex:outputLink value="{!'/'+bid.vendorId}" target="_blank">
                                        {!bid.vendor}
                                    </apex:outputLink>
                                </span>
                            </td>
                            <td>
                                <span class="show-data">{!bid.pax}</span>
                            </td>
                            <td>
                                <span class="show-data">{!bid.status}</span>
                            </td>
                        </tr>
                    </apex:repeat>
                </tbody>
            </table>
            <div style="display: flex; padding: 4px; background-color:#e9ecef; border: 1px solid #dee2e6;">
                <div style="flex: 1; display: flex; align-items: center;">
                    <button class="btn btn-secondary btn-sm filePaginator btn-nav-modal btn-listcontract-first" type="button" onclick="GotoPageContract('first');">
                        <i class="fas fa-step-backward"></i>
                    </button>
                    <button class="btn btn-secondary btn-sm btn-nav-modal btn-listcontract-previous" type="button" style="padding-right: 3px;" onclick="GotoPageContract('previous');">
                        <i class="fas fa-caret-left fa-lg"></i>
                    </button>
                    <button class="btn btn-secondary btn-sm btn-nav-modal btn-listcontract-next" type="button" style="padding-left: 3px;" onclick="GotoPageContract('next');">
                        <i class="fas fa-caret-right fa-lg"></i>
                    </button>
                    <button class="btn btn-secondary btn-sm btn-nav-modal btn-listcontract-last" type="button" onclick="GotoPageContract('last');">
                        <i class="fas fa-step-forward"></i>
                    </button>
                </div>
                <div style="display: flex;">
                    <div class="fileNavigatorMessage" style="display: flex; flex: 1; align-self: center;">Page {!IF(OR(offsetContract == null,offsetContract <= 0),1,(offsetContract/limitContract)+1)} of {!totalPagesContract}</div>
                </div>
            </div>
        </apex:outputPanel>
    </div>

    <apex:outputPanel id="bidContractInformation" layout="block">
        <apex:outputPanel layout="block" rendered="{!vfpConfiguration.bidId != ''}">
            <apex:inputHidden id="bidcontractid" value="{!vfpConfiguration.bidId}" />
            <div class="card darkCard" style="font-size: 0.7rem; margin-bottom: 0.5em;">
                <div class="row" style="margin: 0; margin-bottom: 0.5em;">
                    <div class="col" style="padding: 0 0.5em;">
                        <div class="card darkCard" style="padding: 0.5em; height: 100%;">
                            <div class="row">
                                <div class="col-md-4">Description:</div>
                                <div class="col">{!bidSelected.Air__r.Description__c}</div>
                            </div>
                            <div class="row">
                                <div class="col-md-4">Client:</div>
                                <div class="col">
                                    <apex:selectList size="1" id="contracting_client" styleClass="form-control form-control-sm" value="{!contactClientValue}" onchange="changeClientContract(this);">
                                        <apex:selectOptions value="{!vfpConfiguration.clients}" />
                                    </apex:selectList>
                                </div>
                            </div>
                            <div class="row">
                                <div class="col-md-4">Start Date:</div>
                                <div class="col"><apex:outputText value="{0, date, dd'-'MMM'-'yyyy}"><apex:param value="{!bidSelected.Air__r.Departure_Date__c}" /></apex:outputText><span style="font-weight:bold;"><apex:outputText value="{0, date, ' 'EEEE}"> <apex:param value="{!bidSelected.Air__r.Departure_Date__c}" /> </apex:outputText></span></div>
                            </div>
                            <div class="row">
                                <div class="col-md-4">End Date:</div>
                                <div class="col"><apex:outputText value="{0, date, dd'-'MMM'-'yyyy}"><apex:param value="{!bidSelected.Air__r.Return_Date__c}" /></apex:outputText><span style="font-weight:bold;"><apex:outputText value="{0, date, ' 'EEEE}"> <apex:param value="{!bidSelected.Air__r.Return_Date__c}" /> </apex:outputText></span></div>
                            </div>
                            <div class="row">
                                <div class="col-md-4">Decision Due Date:</div>
                                <div class="col"><apex:inputField id="bidselected_decisionduedate" styleClass="form-control form-control-sm" value="{!bidSelected.Air__r.Decision_Due_Date__c}" onblur="saveDecisionDue();" /></div>
                            </div>
                        </div>
                    </div>
                    <div class="col" style="padding: 0 0.5em;">
                        <div class="card darkCard" style="padding: 0.5em; height: 100%;">
                            <div class="row">
                                <div class="col-md-4">Vendor:</div>
                                <div class="col">
                                    <apex:outputLink rendered="{!NOT(ISNULL(bidSelected.Vendor__c))}" value="{!'/'+bidSelected.Vendor__c}" target="_blank">
                                        {!bidSelected.Vendor__r.Name}
                                    </apex:outputLink>
                                </div>
                            </div>
                            <div class="row">
                                <div class="col-md-4">Contact:</div>
                                <div class="col">
                                    <apex:selectList size="1" id="contracting_contact" styleClass="form-control form-control-sm" value="{!bidSelected.Vendor_Contact__c}" onchange="changeContactContract(this);">
                                        <apex:selectOptions value="{!vendorContactOptions}" />
                                    </apex:selectList>
                                </div>
                            </div>
                            <div class="row">
                                <div class="col-md-4">Air Coordinator:</div>
                                <div class="col">
                                    <apex:outputLink rendered="{!NOT(ISNULL(associations[USER_GTCOORDINATOR]))}" value="{!'/'+associations[USER_GTCOORDINATOR].relativeId}" target="_blank">
                                        {!associations[USER_GTCOORDINATOR].name}
                                    </apex:outputLink>
                                    <apex:outputPanel rendered="{!ISNULL(associations[USER_GTCOORDINATOR])}" style="color: red; font-weight: bold;">Not Selected</apex:outputPanel>
                                </div>
                            </div>
                            <div class="row">
                                <div class="col-md-4">Air Backend Coordinator:</div>
                                <div class="col">
                                    <apex:outputLink rendered="{!NOT(ISNULL(associations[USER_GTBACKENDCOORDINATOR]))}" value="{!'/'+associations[USER_GTBACKENDCOORDINATOR].relativeId}" target="_blank">
                                        {!associations[USER_GTBACKENDCOORDINATOR].name}
                                    </apex:outputLink>
                                    <apex:outputPanel rendered="{!ISNULL(associations[USER_GTBACKENDCOORDINATOR])}" style="color: red; font-weight: bold;">Not Selected</apex:outputPanel>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="col" style="padding: 0 0.5em;">
                        <div class="card darkCard" style="padding: 0.5em; height: 100%;">
                            <div class="row">
                                <div class="col-md-4">Contracting Coordinator:</div>
                                <div class="col">
                                    <apex:outputLink rendered="{!NOT(ISNULL(associations[USER_CONTRACTINGCOORDINATOR]))}" value="{!'/'+associations[USER_CONTRACTINGCOORDINATOR].relativeId}" target="_blank">
                                        {!associations[USER_CONTRACTINGCOORDINATOR].name}
                                    </apex:outputLink>
                                    <apex:outputPanel rendered="{!ISNULL(associations[USER_CONTRACTINGCOORDINATOR])}" style="color: red; font-weight: bold;">Not Selected</apex:outputPanel>
                                </div>
                            </div>
                            <div class="row">
                                <div class="col-md-4">Contracting Backend Coordinator:</div>
                                <div class="col">
                                    <apex:selectList size="1" id="contracting_backendcoordinator" styleClass="form-control form-control-sm" value="{!associations[USER_CONTRACTINGBACKENDCOORDINATOR].relativeId}" onchange="saveContractingBackEndCoordinator(this);">
                                        <apex:selectOptions value="{!teamMembers}" />
                                    </apex:selectList>
                                </div>
                            </div>
                            <div class="row">
                                <div class="col" style="font-size: 0.85rem; display: flex;">
                                    <div style="flex: 1;"></div>
                                    <button class="btn btn-secondary btn-sm btn-custom" onclick="loadContractingDocumentsPanel();" type="button"><i class="fas fa-book"></i> Documents</button>
                                    <button class="btn btn-secondary btn-sm btn-custom" onclick="searchBid('{!bidSelected.Name}');" type="button" style="margin-left: 1em;"><i class="far fa-check-square"></i> Bid Details</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <apex:outputPanel id="bidContractTabs" layout="block">
                <div class="slds-tabs_scoped">
                    <ul class="slds-tabs_scoped__nav" role="tablist">
                        <li class="slds-tabs_scoped__item {!IF(tabContractDefault == 'status','slds-is-active','')}" title="Status" role="presentation">
                            <a class="slds-tabs_scoped__link" href="#contract-status" onclick="loadTabContractContent('status');" role="tab" tabindex="{!IF(tabContractDefault == 'status','0','-1')}" aria-selected="{!IF(tabContractDefault == 'status','true','false')}" aria-controls="contract-status" id="contract-status__item">
                                <span><i class="far fa-hourglass"></i> Status</span>
                            </a>
                        </li>
                        <li class="slds-tabs_scoped__item {!IF(tabContractDefault == 'forms','slds-is-active','')}" title="Forms" role="presentation">
                            <a class="slds-tabs_scoped__link" href="#contract-forms" onclick="loadTabContractContent('forms');" role="tab" tabindex="{!IF(tabContractDefault == 'forms','0','-1')}" aria-selected="{!IF(tabContractDefault == 'forms','true','false')}" aria-controls="contract-forms" id="contract-forms__item">
                                <span><i class="fas fa-save"></i> Forms</span>
                            </a>
                        </li>
                        <li class="slds-tabs_scoped__item {!IF(tabContractDefault == 'journals','slds-is-active','')}" title="Journals" role="presentation">
                            <a class="slds-tabs_scoped__link" href="#contract-journals" onclick="loadTabContractContent('journals');" role="tab" tabindex="{!IF(tabContractDefault == 'journals','0','-1')}" aria-selected="{!IF(tabContractDefault == 'journals','true','false')}" aria-controls="contract-journals" id="contract-journals__item">
                                <span><i class="fas fa-align-justify"></i> Journals</span>
                            </a>
                        </li>
                        <li class="slds-tabs_scoped__item {!IF(tabContractDefault == 'gcq','slds-is-active','')}" title="GCQ" role="presentation">
                            <a class="slds-tabs_scoped__link" href="#contract-gcq" onclick="loadTabContractContent('gcq');" role="tab" tabindex="{!IF(tabContractDefault == 'gcq','0','-1')}" aria-selected="{!IF(tabContractDefault == 'gcq','true','false')}" aria-controls="contract-gcq" id="contract-gcq__item">
                                <span><i class="fas fa-map-signs"></i> GCQ</span>
                            </a>
                        </li>
                    </ul>
                    <div class="slds-tabs_scoped__content slds-show" role="tabpanel">
                        <div id="subTabSelected" style="position: relative; margin: -1em;">
                            <div id="contentLoadingSubTab" class="loadingSubTab" style="display: none;">
                                <div style="position: absolute; margin: auto; width: 1em; height: 1em; top: 0; right: 0; bottom: 0; left: 0; z-index: 1000;">
                                    <div class="loadingSubTabSpinner"></div>
                                </div>
                            </div>
                            <div style="padding: 1em;">
                                <c:Dashboard_Tab_Contract_Status rendered="{!IF(tabContractDefault == 'status',true,false)}" traceBidId="{!vfpConfiguration.bidId}" traceParentSObject="{!vfpConfiguration.parentSObject}" productionId="{!vfpConfiguration.productionId}" />
                                <c:Dashboard_Tab_Contract_Forms rendered="{!IF(tabContractDefault == 'forms',true,false)}" formBidId="{!vfpConfiguration.bidId}" formBidParentSObject="{!vfpConfiguration.parentSObject}" formClients="{!vfpConfiguration.clients}" />
                                <c:Dashboard_Journals rendered="{!IF(tabContractDefault == 'journals',true,false)}" recordId="{!vfpConfiguration.bidId}" SOBjectName="Bid" scope="Contracting" productionId="{!vfpConfiguration.productionId}" pCompanies="{!vfpConfiguration.companies}" pContacts="{!vfpConfiguration.contacts}" pCompanyContacts="{!vfpConfiguration.companyContacts}" pTeamMembers="{!vfpConfiguration.teamMembers}" />
                            	<c:Dashboard_Tab_Contract_Air_GCQ rendered="{!IF(tabContractDefault == 'gcq',true,false)}" variables="{!vfpConfiguration}" clientId="{!contactClientValue}"/>
                            </div>
                        </div>
                    </div>
                </div>
            </apex:outputPanel>
            <div class="modal fade" id="myModalContractingDocuments" role="dialog" style="padding-right: 18px;">
                <div class="modal-dialog" style="min-width: 75em;">
                    <div class="modal-content">
                        <div class="modal-header">
                            <h4 class="modal-title">Air Contracting Documents</h4>
                            <button type="button" class="close" onclick="closeContractingDocumentsPanel();">&times;</button>
                        </div>
                        <apex:outputPanel id="contractingDocuments" layout="block" styleClass="modal-body">
                            <c:Dashboard_Dialog_Documents rendered="{!loadDocuments}" recordId="{!vfpConfiguration.bidId}" parentSObject="{!vfpConfiguration.parentSObject}" parentId="{!vfpConfiguration.parentId}" contract="true" />
                        </apex:outputPanel>
                    </div>
                </div>
            </div>
        </apex:outputPanel>
    </apex:outputPanel>
    <apex:actionFunction name="loadBidContractsJs" action="{!loadBidContracts}" status="loading" reRender="bidContractList,bidContractInformation" oncomplete="verifyButtonsListContract();" />
    <apex:actionFunction name="viewBidContractedJs" action="{!viewBidContracted}" status="loading" reRender="bidContractInformation" oncomplete="setDataPre();">
        <apex:param assignTo="{!bidId}" name="bidContractId" value="" />
        <apex:param assignTo="{!bidName}" name="bidNameContractId" value="" />
        <apex:param assignTo="{!parentId}" name="bidParentId" value="" />
    </apex:actionFunction>
    <apex:actionFunction name="loadContractingDocumentsPanel" status="loading" reRender="contractingDocuments" oncomplete="openModal('myModalContractingDocuments');">
        <apex:param assignTo="{!loadDocuments}" name="loadDocuments" value="true" />
    </apex:actionFunction>
    <apex:actionFunction name="closeContractingDocumentsPanel" status="loading" reRender="contractingDocuments,bidContractTabs" oncomplete="closeModal('myModalContractingDocuments');">
        <apex:param assignTo="{!loadDocuments}" name="loadDocuments" value="false" />
    </apex:actionFunction>
    <apex:actionFunction name="loadContractTabContentJs" status="loadingSubTab" reRender="bidContractTabs">
        <apex:param assignTo="{!tabContractDefault}" name="tabDefault" value="" />
    </apex:actionFunction>
    <apex:actionStatus id="loadingSubTab" onstart="loadingSubTab(true);" onstop="loadingSubTab(false);" />
    <apex:actionFunction action="{!searchBidContracts}" name="searchBidContractingJs" status="loading" reRender="bidContractList" oncomplete="verifyButtonsListContract();">
        <apex:param assignTo="{!search_startdate}" name="startDate" value="" />
        <apex:param assignTo="{!search_enddate}" name="endDate" value="" />
        <apex:param assignTo="{!search_vendor}" name="vendor" value="" />
        <apex:param assignTo="{!search_city}" name="city" value="" />
        <apex:param assignTo="{!search_isprior}" name="isPriorTrip" value="" />
        <apex:param assignTo="{!search_iscontracted}" name="isContractedOnOwn" value="" />
        <apex:param assignTo="{!search_iscancelled}" name="isCancelled" value="" />
        <apex:param assignTo="{!offsetContract}" name="offsetContract" value="" />
        <apex:param assignTo="{!orderFieldBidContract}" name="orderFieldBidContract" value="Air__r.Departure_Date__c" />
        <apex:param assignTo="{!orderOrientationBidContract}" name="orderOrientationBidContract" value="ASC" />
    </apex:actionFunction>
    <apex:actionFunction action="{!searchBidContracts}" name="sortBidContractsJs" status="loading" reRender="bidContractList" oncomplete="verifyButtonsListContract();">
        <apex:param assignTo="{!orderFieldBidContract}" name="orderFieldBidContract" value="" />
        <apex:param assignTo="{!orderOrientationBidContract}" name="orderOrientationBidContract" value="" />
        <apex:param assignTo="{!isColumnSelected}" name="isColumnSelected" value="" />
        <apex:param assignTo="{!isSortUpdated}" name="isSortUpdated" value="" />
        <apex:param assignTo="{!offsetContract}" name="offsetContract" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!saveContractingBackEndCoordinator}" name="saveContractingBackEndCoordinatorJs" status="loading" reRender="noneRender" >
        <apex:param assignTo="{!contractingbackendcoordinatorGT}" name="contractingbackendcoordinatorGT" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!changeClientContract}" name="changeClientContractJs" status="loading" reRender="noneRender" >
        <apex:param assignTo="{!contactClientValue}" name="contactClientValue" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!changeContactContract}" name="changeContactContractJs" status="loading" reRender="noneRender" >
        <apex:param assignTo="{!contactContracting}" name="contactContracting" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!changeFinalStatus}" name="changeFinalStatusJs" status="loading" reRender="noneRender" oncomplete="loadTracesJs();">
        <apex:param assignTo="{!contractFinalStatus}" name="contractFinalStatus" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!saveDecisionDue}" name="saveDecisionDueJs" status="loading" reRender="noneRender">
        <apex:param assignTo="{!trip_decisionduedate}" name="trip_decisionduedate" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!searchBidContracts}" name="GotoPageContract" status="loading" reRender="bidContractList" oncomplete="verifyButtonsListContract();">
        <apex:param assignTo="{!searchTypeContract}" name="searchTypeContract" value="" />
    </apex:actionFunction>
    <script>
    var count = 0;
    $(document).ready(function() {
        var loadTable = "{!loadTable}";
        if(loadTable) {
            loadBidContractsJs();
            count++;
            console.log('the page is ready -> '+count);
            console.log("{!loadTable}");
        }
    });
    
    function verifyButtonsListContract(){
        var limit = $('input[id$=listtrip_limitContract]').val();
        var offset = parseInt($('input[id$=listtrip_offsetContract]').val()) || 0;
        var totalpages = $('input[id$=listtrip_totalPagesContract]').val();
        $('.btn-listcontract-first').prop('disabled',false);
        $('.btn-listcontract-previous').prop('disabled',false);
        $('.btn-listcontract-next').prop('disabled',false);
        $('.btn-listcontract-last').prop('disabled',false);
        if(offset == null || offset <= 0){
            $('.btn-listcontract-first').prop('disabled',true);
            $('.btn-listcontract-previous').prop('disabled',true);
        }
        var actual_page = 1;
        if(offset == null || offset <= 0) actual_page = 1; else actual_page = (offset/limit)+1;
        if(totalpages == '' || totalpages == actual_page){
            $('.btn-listcontract-next').prop('disabled',true);
            $('.btn-listcontract-last').prop('disabled',true);
        }
    }
    
    function loadingSubTab(val) {
        if(val) $("#contentLoadingSubTab").css("display","block");
        else $("#contentLoadingSubTab").css("display","none");
    }
    
    function viewBidContracted(bidContractId,bidContractName,bidParentId) {
        console.log(bidContractId);
        viewBidContractedJs(bidContractId,bidContractName,bidParentId);
    }
    
    function loadTabContractContent(tabName) {
        loadContractTabContentJs(tabName);
    }

    function searchBid(searchValue) {
        searchBidJs('searchByBid', searchValue, 'gt-bids');
    }
    
    function setInputContractVendor(){
        if(createAutocompleteContractVendor == false){
            createAutocompleteContractVendor = true;
            $('.gtcontract-vendor').autocomplete({
                lookup: function (query, done) {
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.Dashboard_Tab_Contracting.searchAccount}',query,'Air Vendor',
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
    function setInputContractCity(){
        if(createAutocompleteContractCity == false){
            createAutocompleteContractCity = true;
            $('.gtcontract-city').autocomplete({
                lookup: function (query, done) {
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.Dashboard_Tab_Contracting.searchAirport}',query,
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
    
    function clearBidContracting() {
        $('input[id$=contractSearchBoxStartDate]').val('');
        $('input[id$=contractSearchBoxEndDate]').val('');
        $('input[id$=contractVendor]').val('');
        $('input[id$=contractCity]').val('');
        $('select[id$=contractSearchBoxStatusValue]').val('');
        $("input[id$=contractSearchBoxIsPriorTrip]").prop("checked", false);
        $("input[id$=contractSearchBoxIsContractedOnOwn]").prop("checked", false);
        $("input[id$=contractSearchBoxIsCancelled]").prop("checked", false);
    }
    
    function searchBidContracting(){
        var start_date = $('input[id$=contractSearchBoxStartDate]').val();
        var end_date = $('input[id$=contractSearchBoxEndDate]').val();
        var vendor = $('input[id$=contractVendor]').val();
        var city = $('input[id$=contractCity]').val();
        var show_prior = $("input[id$=contractSearchBoxIsPriorTrip]").prop("checked");
        var contracted_on_own = $("input[id$=housingContractsShowContractedOnOwn]").prop("checked");
        var cancelled = $("input[id$=housingContractsShowCancelled]").prop("checked");
        searchBidContractingJs(start_date,end_date,vendor,city,show_prior,contracted_on_own,cancelled);
    }
    
    function sortBidContracts(sortOrder,sortOrientation){
        var actual = $('input[id$=orderFieldBidContractActual]').val();
        var change = false;
        if(actual != sortOrder) change = true;
        sortBidContractsJs(sortOrder,sortOrientation,true,change);
    }
    
    function saveContractingBackEndCoordinator(val){
        var backend = $(val).val();
        var confirmAction = confirm('Are you sure you want to change the assigned contracting back-end coordinator?');
        if(confirmAction){
            $('select[id$=contracting_backendcoordinator]').data('pre',$('select[id$=contracting_backendcoordinator]').val());
            saveContractingBackEndCoordinatorJs(backend);
        }else{
            var data_pre = $('select[id$=contracting_backendcoordinator]').data('pre');
            $('select[id$=contracting_backendcoordinator]').val(data_pre);
        }
    }
    
    function setDataPre(){
        $('select[id$=contracting_backendcoordinator]').data('pre',$('select[id$=contracting_backendcoordinator]').val());
        $('select[id$=contracting_client]').data('pre',$('select[id$=contracting_client]').val());
        $('select[id$=contracting_contact]').data('pre',$('select[id$=contracting_contact]').val());
        $('select[id$=contracting_finalstatus]').data('pre',$('select[id$=contracting_finalstatus]').val());
    }
    
    function changeClientContract(val){
        var client = $(val).val();
        var confirmAction = confirm('Are you sure you want to change the client?');
        if(confirmAction){
            $('select[id$=contracting_client]').data('pre',$('select[id$=contracting_client]').val());
            changeClientContractJs(client);
        }else{
            var data_pre = $('select[id$=contracting_client]').data('pre');
            $('select[id$=contracting_client]').val(data_pre);
        }
    }
    
    function changeContactContract(val){
        var client = $(val).val();
        var confirmAction = confirm('Are you sure you want to change the contact?');
        if(confirmAction){
            $('select[id$=contracting_contact]').data('pre',$('select[id$=contracting_contact]').val());
            changeContactContractJs(client);
        }else{
            var data_pre = $('select[id$=contracting_contact]').data('pre');
            $('select[id$=contracting_contact]').val(data_pre);
        }
    }
    
    function changeFinalStatus(val){
        var final_status = $(val).val();
        var confirmAction = confirm('Are you sure you want to change the final status?');
        if(confirmAction){
            $('select[id$=contracting_finalstatus]').data('pre',$('select[id$=contracting_finalstatus]').val());
            changeFinalStatusJs(final_status);
        }else{
            var data_pre = $('select[id$=contracting_finalstatus]').data('pre');
            $('select[id$=contracting_finalstatus]').val(data_pre);
        }
    }
    
    function saveDecisionDue() {
        var decision_due_date = $('input[id$=bidselected_decisionduedate]').val();
        saveDecisionDueJs(decision_due_date);
    }
    </script>
</apex:component>
```


# Last Modified


# Usage
