---
layout: default
title: PDF_TraceDashboardBeta
parent: components
grand_parent: Metadata
---
# Metadata Type
components


# Filename 
PDF_TraceDashboardBeta


# Raw XML
```
<apex:component controller="TraceDashboardControllerBeta">
    <div class="content">
        
        <table width="100%" valign="top" cellspacing="0" cellpadding="0" border="0" style="border-bottom:1px solid rgb(143, 161, 152)">
            <thead>
                <tr>
                    <th width="10%" align="left" style="">
                        <apex:image url="{!$Resource.Logo}" style="width: 120px" />
                    </th>
                </tr>
            </thead>
        </table>
        <!--START:HOUSING-->
        <apex:outputPanel layout="block" rendered="{!IF(theJournals.lsJournals_Housing.size > 0 || taskWrappers.lsGroupsTWNoContract_Housing.size > 0 || taskWrappers.lsGroupsTW_Housing_AllOther.size > 0 || taskWrappers.lsGroupsTWContract_Housing.size > 0, true, false)}">
            <h2 style="text-align:center">Housing Traces</h2>
            
            <!-- Start Trace Type is DEADLINE DATE -->
            <apex:outputPanel layout="block" rendered="{!IF(taskWrappers.lsTraceDeadlineDate_Housing.size > 0 && searchInputs.searchTraceType=='DeadLine Date',true,false)}"
                              styleClass="card mb-3">
                <h3>DeadLine Dates</h3>
                <div class="collapse show" id="lsTraceDeadlineDate_Housing">
                    <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                            <thead class="thead-light font-weight-bold">
                                <tr>
                                    <th scope="col">
                                        <span class="font-weight-bold" style="float: left">Status</span>
                                    </th>
                                    <th scope="col">
                                        <span class="font-weight-bold" style="float: left">Production</span>
                                    </th>
                                    <th scope="col">
                                        <span class="font-weight-bold" style="float: left">Stay City</span>
                                    </th>
                                    <th scope="col">
                                        <span class="font-weight-bold" style="float: left">Company</span>
                                    </th>
                                    <th scope="col" width="8%">
                                        <span class="font-weight-bold" style="float: left">Deadline Date</span>
                                    </th>
                                    <th scope="col" width="8%">
                                        <span class="font-weight-bold" style="float: left">Trace Date</span>
                                    </th>
                                    <th scope="col" width="10%">
                                        <span class="font-weight-bold" style="float: left">Trace Owner</span>
                                    </th>
                                </tr>
                            </thead>
                            <tbody>
                                <apex:repeat value="{!taskWrappers.lsTraceDeadlineDate_Housing}" var="t">
                                    <tr>
                                        <td>
                                            {!housingMapDeadlines[t.taskId].Status_CC__c}
                                        </td>
                                        <td>
                                            {!housingMapDeadlines[t.taskId].Production_CC__r.Name}
                                        </td>
                                        <td>{!housingMapDeadlines[t.taskId].City__r.Name}</td>
                                        <td>
                                            {!housingMapDeadlines[t.taskId].Production_CC__r.Account.Name}
                                        </td>
                                        <td>
                                            <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                <apex:param value="{!t.deadlineDate}" />
                                            </apex:outputText>
                                        </td>
                                        <td>
                                            <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                <apex:param value="{!t.deadLineDate}" />
                                            </apex:outputText>
                                        </td>
                                        <td>
                                            <span class="show-data">{!t.coordinator}</span>
                                        </td>
                                    </tr>
                                </apex:repeat>
                            </tbody>
                        </table>
                </div>
            </apex:outputPanel>
            <!-- End  Trace Type is DEADLINE DATE -->
            
            
            <!-- START Trace Type is Trace Date -->
            <apex:outputPanel rendered="{!searchInputs.searchTraceType=='Trace Date'}">
                
                <!-- START Journals -->
                <apex:outputPanel layout="block" rendered="{!theJournals.lsJournals_Housing.size > 0}" styleClass="card mb-3">
                    <h3>Journals</h3>
                    <div class="collapse show" id="lsJournals_Housing">
                        <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                                <thead class="thead-light font-weight-bold">
                                    <tr>
                                        <th scope="col" width="10%">
                                            <span class="font-weight-bold">Follow Up / Trace Date</span>
                                        </th>
                                        <th scope="col">
                                            <span class="font-weight-bold">Journal Entry</span>
                                        </th>
                                        <th scope="col" width="15%">
                                            <span class="font-weight-bold">Categories</span>
                                        </th>
                                        <th scope="col" width="10%">
                                            <span class="font-weight-bold">Created By</span>
                                        </th>
                                        <th scope="col" width="8%">
                                            <span class="font-weight-bold">Created On</span>
                                        </th>
                                        <th scope="col" width="10%">
                                            <span class="font-weight-bold">Coordinator</span>
                                        </th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <apex:repeat value="{!theJournals.lsJournals_Housing}" var="j">
                                        <tr>
                                            <td>
                                                <apex:outputLink value="{!'/'+j.id}" target="_blank">
                                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                        <apex:param value="{!j.Trace_Date__c}" />
                                                    </apex:outputText>
                                                </apex:outputLink>
                                            </td>
                                            <td>{!j.Journal_Entry__c}</td>
                                            <td>
                                                <apex:outputText rendered="{!IF(j.Production__r.Name == null, false, true)}">
                                                    <span class="font-weight-bold">Production: </span>
                                                    <a href="#">{!j.Production__r.Name}</a>
                                                    <br />
                                                </apex:outputText>
                                                <apex:repeat value="{!j.Related_Companies__r}" var="rcom">
                                                    <span class="font-weight-bold">Company: </span>
                                                    <a href="#">{!rcom.Company__r.Name}</a>
                                                    <br />
                                                </apex:repeat>
                                                <apex:repeat value="{!j.Related_Contact__r}" var="rcon">
                                                    <span class="font-weight-bold">Contact: </span>
                                                    <a href="#">{!rcon.Contact__r.Name}</a>
                                                    <br />
                                                </apex:repeat>
                                                <apex:outputText rendered="{!IF(j.Bid__r.Contract_ID__c == null, false, true)}">
                                                    <span class="font-weight-bold">Contract: </span>
                                                    <a href="#">{!j.Bid__r.Contract_ID__c}</a>
                                                    <br />
                                                </apex:outputText>
                                                <!-- id ? -->
                                                <apex:outputText rendered="{!IF(j.Bid__r.Name == null, false, true)}">
                                                    <span class="font-weight-bold">Bid: </span>
                                                    <a href="#">{!j.Bid__r.Name}</a>
                                                    <br />
                                                </apex:outputText>
                                                <apex:outputText rendered="{!IF(j.Bid__r.Stay_ID__c == null, false, true)}">
                                                    <span class="font-weight-bold">Stay: </span>
                                                    <a href="#">{!j.Bid__r.Stay_ID__c}</a>
                                                    <br />
                                                </apex:outputText>
                                            </td>
                                            <td>{!j.CreatedBy.Name}</td>
                                            <td>
                                                <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                    <apex:param value="{!j.CreatedDate}" />
                                                </apex:outputText>
                                            </td>
                                            <td>{!j.Trace_Coordinator__r.Name}</td>
                                        </tr>
                                    </apex:repeat>
                                </tbody>
                            </table>
                    </div>
                </apex:outputPanel>
                <!-- END   Journals -->
                
                <!-- START Group Traces NO Contract List Housing -->
                <apex:outputPanel layout="block" rendered="{!taskWrappers.lsGroupsTWNoContract_Housing.size > 0}">
                    <apex:variable var="item_number" value="0" />
                    <!-- Init -->
                    <h3>Housing Traces</h3>
                    <apex:repeat value="{!taskWrappers.lsGroupsTWNoContract_Housing}" var="gls">
                        <apex:variable var="item_number" value="{!VALUE(item_number) + 1}" />
                        <div class="card mb-3">
                            <div class="card-body card-header p-1">
                                <h2>{!gls.groupTitle} ({!gls.totalTasks})</h2>
                            </div>
                            <div class="collapse show" id="lsGroupsTWNoContract_Housing_{!item_number}">
                                <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                                        <thead class="thead-light font-weight-bold">
                                            <tr>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Trace Date</span>
                                                </th>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Check In Date</span>
                                                </th>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Check Out Date</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">City</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Production</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Company</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Status</span>
                                                </th>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Deadline Date</span>
                                                    <!-- option Date -->
                                                </th>
                                                <th scope="col" width="10%">
                                                    <span class="font-weight-bold">Coordinator</span>
                                                </th>
                                            </tr>
                                        </thead>
                                        <tbody>
                                            <apex:repeat value="{!gls.lsTasks}" var="tw">
                                                <tr>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                            <apex:param value="{!tw.followUpDate}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                            <apex:param value="{!tw.checkInDate}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                            <apex:param value="{!tw.checkOutDate}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>{!tw.city}</td>
                                                    <td>
                                                        {!tw.production}
                                                    </td>
                                                    <td>
                                                        {!tw.companies}
                                                    </td>
                                                    <td>{!tw.status}</td>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                            <apex:param value="{!tw.deadlineDate}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>{!tw.coordinator}</td>
                                                </tr>
                                            </apex:repeat>
                                        </tbody>
                                    </table>
                            </div>
                        </div>
                    </apex:repeat>
                </apex:outputPanel>
                <!-- END   Group Traces NO Contract List Housing -->
                
                <!-- START Group Traces Contract List Housing -->
                <apex:outputPanel layout="block" rendered="{!taskWrappers.lsGroupsTWContract_Housing.size > 0}">
                    <apex:variable var="item_number" value="0" />
                    <!-- Init -->
                    <h3>All Contract Traces</h3>
                    <apex:repeat value="{!taskWrappers.lsGroupsTWContract_Housing}" var="gls">
                        <apex:variable var="item_number" value="{!VALUE(item_number) + 1}" />
                        <div class="card mb-3">
                            <div class="card-body card-header p-1">
                                <h2>{!gls.groupTitle} ({!gls.totalTasks})</h2>
                            </div>
                            <div class="collapse show" id="gls_{!item_number}">
                                <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                                        <thead class="thead-light font-weight-bold">
                                            <tr>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Follow Up Date</span>
                                                </th>
                                                <th scope="col" width="10%">
                                                    <span class="font-weight-bold">Check In Date</span>
                                                </th>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Check Out Date</span>
                                                </th>
                                                <th scope="col" width="13%">
                                                    <span class="font-weight-bold">City</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Production</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Company</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Vendor</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Status</span>
                                                </th>
                                                <th scope="col" width="10%">
                                                    <span class="font-weight-bold">Coordinator</span>
                                                </th>
                                            </tr>
                                        </thead>
                                        <tbody>
                                            <apex:repeat value="{!gls.lsTasks}" var="tw">
                                                <tr>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}" styleClass="text-danger">
                                                            <apex:param value="{!tw.followUpDate}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                            <apex:param value="{!tw.checkInDate}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                            <apex:param value="{!tw.checkOutDate}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>{!tw.city}</td>
                                                    <td>
                                                        {!tw.production}
                                                    </td>
                                                    <td>
                                                        {!tw.companies}
                                                    </td>
                                                    <td>
                                                        {!tw.vendor}
                                                    </td>
                                                    <td>{!tw.status}</td>
                                                    <td>{!tw.coordinator}</td>
                                                </tr>
                                            </apex:repeat>
                                        </tbody>
                                    </table>
                            </div>
                        </div>
                    </apex:repeat>
                </apex:outputPanel>
                <!-- END   Group Traces Contract List Housing -->
                
            </apex:outputPanel>
            <!-- END Trace Type is Trace Date -->
            
        </apex:outputPanel>
        <!--END:HOUSING-->
        
        <!--START:GT-->
        <apex:outputPanel layout="block" rendered="{!IF(theJournals.lsJournals_GT.size > 0 || (taskWrappers.lsGroupsTWNoContract_GT.size > 0 || taskWrappers.lsGroupsTW_GT_AllOther.size > 0 && searchInputs.searchTraceType=='Trace Date'), true, false)}">
            <h2 style="text-align:center">Ground Trace</h2>
            <apex:outputPanel layout="block" rendered="{!IF(taskWrappers.lsTraceDeadlineDate_GT.size > 0 && searchInputs.searchTraceType=='DeadLine Date',true,false)}"
                              styleClass="card mb-3">
                    <h3>DeadLine Dates</h3>
                <div class="collapse show" id="lsTraceDeadlineDate_GT">
                    <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                            <thead class="thead-light font-weight-bold">
                                <tr>
                                    <th scope="col">
                                        <span class="font-weight-bold" style="float: left">Status</span>
                                    </th>
                                    <th scope="col">
                                        <span class="font-weight-bold" style="float: left">Production</span>
                                    </th>
                                    <th scope="col">
                                        <span class="font-weight-bold" style="float: left">Stay City</span>
                                    </th>
                                    <th scope="col">
                                        <span class="font-weight-bold" style="float: left">Company</span>
                                    </th>
                                    <th scope="col" width="8%">
                                        <span class="font-weight-bold" style="float: left">Deadline Date</span>
                                    </th>
                                    <th scope="col" width="8%">
                                        <span class="font-weight-bold" style="float: left">Trace Date</span>
                                    </th>
                                    <th scope="col" width="10%">
                                        <span class="font-weight-bold" style="float: left">Trace Owner</span>
                                    </th>
                                </tr>
                            </thead>
                            <tbody>
                                <apex:repeat value="{!taskWrappers.lsTraceDeadlineDate_GT}" var="t">
                                    <tr>
                                        <td>
                                            {!gtMapDeadlines[t.taskId].Status__c}
                                        </td>
                                        <td>
                                            {!gtMapDeadlines[t.taskId].Production_Ground__r.Name}
                                        </td>
                                        <td>City Field</td>
                                        <td>
                                            {!gtMapDeadlines[t.taskId].Production_Ground__r.Account.Name}
                                        </td>
                                        <td>
                                            <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                <apex:param value="{!t.deadlineDate}" />
                                            </apex:outputText>
                                        </td>
                                        <td>
                                            <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                <apex:param value="{!t.deadLineDate}" />
                                            </apex:outputText>
                                        </td>
                                        <td>
                                            <span class="show-data">{!t.coordinator}</span>
                                        </td>
                                    </tr>
                                </apex:repeat>
                            </tbody>
                        </table>
                </div>
            </apex:outputPanel>
            <!-- End DEADLINE DATE -->
            <apex:outputPanel rendered="{!searchInputs.searchTraceType=='Trace Date'}">
                <!-- START - Journals -->
                <apex:outputPanel layout="block" rendered="{!theJournals.lsJournals_GT.size > 0}" styleClass="card mb-3">
                        <h3>Journals</h3>
                    <div class="collapse show" id="lsJournals_GT">
                            <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                                <thead class="thead-light font-weight-bold">
                                    <tr>
                                        <th scope="col" width="10%">
                                            <span class="font-weight-bold">Follow Up / Trace Date</span>
                                        </th>
                                        <th scope="col">
                                            <span class="font-weight-bold">Journal Entry</span>
                                        </th>
                                        <th scope="col" width="15%">
                                            <span class="font-weight-bold">Categories</span>
                                        </th>
                                        <th scope="col" width="10%">
                                            <span class="font-weight-bold">Created By</span>
                                        </th>
                                        <th scope="col" width="8%">
                                            <span class="font-weight-bold">Created On</span>
                                        </th>
                                        <th scope="col" width="10%">
                                            <span class="font-weight-bold">Coordinator</span>
                                        </th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <apex:repeat value="{!theJournals.lsJournals_GT}" var="j">
                                        <tr>
                                            <td>
                                                <apex:outputLink value="{!'/'+j.id}" target="_blank">
                                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                        <apex:param value="{!j.Trace_Date__c}" />
                                                    </apex:outputText>
                                                </apex:outputLink>
                                            </td>
                                            <td>{!j.Journal_Entry__c}</td>
                                            <td>
                                                <apex:outputText rendered="{!IF(j.Production__r.Name == null, false, true)}">
                                                    <span class="font-weight-bold">Production: </span>
                                                    {!j.Production__r.Name}
                                                    <br />
                                                </apex:outputText>
                                                <apex:repeat value="{!j.Related_Companies__r}" var="rcom">
                                                    <span class="font-weight-bold">Company: </span>
                                                    {!rcom.Company__r.Name}
                                                    <br />
                                                </apex:repeat>
                                                <apex:repeat value="{!j.Related_Contact__r}" var="rcon">
                                                    <span class="font-weight-bold">Contact: </span>
                                                    {!rcon.Contact__r.Name}
                                                    <br />
                                                </apex:repeat>
                                                <apex:outputText rendered="{!IF(j.Bid__r.Contract_ID__c == null, false, true)}">
                                                    <span class="font-weight-bold">Contract: </span>
                                                    {!j.Bid__r.Contract_ID__c}
                                                    <br />
                                                </apex:outputText>
                                                <!-- id ? -->
                                                <apex:outputText rendered="{!IF(j.Bid__r.Name == null, false, true)}">
                                                    <span class="font-weight-bold">Bid: </span>
                                                    {!j.Bid__r.Name}
                                                    <br />
                                                </apex:outputText>
                                                <apex:outputText rendered="{!IF(j.Bid__r.Stay_ID__c == null, false, true)}">
                                                    <span class="font-weight-bold">Stay: </span>
                                                    {!j.Bid__r.Stay_ID__c}
                                                    <br />
                                                </apex:outputText>
                                            </td>
                                            <td>{!j.CreatedBy.Name}</td>
                                            <td>
                                                <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                    <apex:param value="{!j.CreatedDate}" />
                                                </apex:outputText>
                                            </td>
                                            <td>{!j.Trace_Coordinator__r.Name}</td>
                                        </tr>
                                    </apex:repeat>
                                </tbody>
                            </table>
                    </div>
                </apex:outputPanel>
                <!-- END -->
                <!-- START - Group Traces 1 GT -->
                <apex:outputPanel layout="block" rendered="{!taskWrappers.lsGroupsTWNoContract_GT.size > 0}">
                    <apex:variable var="item_number" value="0" />
                    <!-- Init -->
                    <h3>Traces</h3>
                    <apex:repeat value="{!taskWrappers.lsGroupsTWNoContract_GT}" var="gls">
                        <apex:variable var="item_number" value="{!VALUE(item_number) + 1}" />
                        <div class="card mb-3">
                            <h2>{!gls.groupTitle} ({!gls.totalTasks})</h2>
                            <div class="collapse show" id="lsGroupsTWNoContract_GT_{!item_number}">
                                    <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                                        <thead class="thead-light font-weight-bold">
                                            <tr>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Trace Date</span>
                                                </th>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Trip Start Date</span>
                                                </th>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Trip End Date</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Description</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">City</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Service Type</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Production</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Company</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Status</span>
                                                </th>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Deadline Date</span>
                                                </th>
                                                <th scope="col" width="10%">
                                                    <span class="font-weight-bold">Coordinator</span>
                                                </th>
                                            </tr>
                                        </thead>
                                        <tbody>
                                            <apex:repeat value="{!gls.lsTasks}" var="tw">
                                                <tr>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                            <apex:param value="{!tw.followUpDate}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                            <apex:param value="{!tw.tripStartDate_gtfr}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                            <apex:param value="{!tw.tripEndDate_gtfr}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>{!tw.tripDescription_gtfr}</td>
                                                    <td>{!tw.city}</td>
                                                    <td>{!tw.tripServiceType_gtfr}</td>
                                                    <td>
                                                        {!tw.production}
                                                    </td>
                                                    <td>
                                                        {!tw.companies}
                                                    </td>
                                                    <td>{!tw.status}</td>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                            <apex:param value="{!tw.deadlineDate}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>{!tw.coordinator}</td>
                                                </tr>
                                            </apex:repeat>
                                        </tbody>
                                    </table>
                            </div>
                        </div>
                    </apex:repeat>
                </apex:outputPanel>
                <!-- END -->
                
                <!-- START - Group Traces Contract List GT -->
                <apex:outputPanel layout="block" rendered="{!taskWrappers.lsGroupsTW_GT_AllOther.size > 0}">
                    <apex:variable var="item_number" value="0" />
                    <!-- Init -->
                    <h3>All Contract Traces</h3>
                    <apex:repeat value="{!taskWrappers.lsGroupsTW_GT_AllOther}" var="gls">
                        <apex:variable var="item_number" value="{!VALUE(item_number) + 1}" />
                        <div class="card mb-3">
                            <div class="card-body card-header p-1">
                                <span class="font-weight-bold">{!gls.groupTitle} ({!gls.totalTasks})</span>
                            </div>
                            <div class="collapse show" id="gls_gt_{!item_number}">
                                    <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                                        <thead class="thead-light font-weight-bold">
                                            <tr>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Follow Up Date</span>
                                                </th>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Trip Start Date</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Description</span>
                                                </th>
                                                <th scope="col" width="15%">
                                                    <span class="font-weight-bold">City</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Service Type</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Production</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Company</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Vendor</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Status</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Coordinator</span>
                                                </th>
                                            </tr>
                                        </thead>
                                        <tbody>
                                            <apex:repeat value="{!gls.lsTasks}" var="tw">
                                                <tr>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}" styleClass="text-danger">
                                                            <apex:param value="{!tw.followUpDate}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                            <apex:param value="{!tw.tripStartDate_gtfr}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>{!tw.tripDescription_gtfr}</td>
                                                    <td>{!tw.city}</td>
                                                    <td>{!tw.tripServiceType_gtfr}</td>
                                                    <td>
                                                        {!tw.production}
                                                    </td>
                                                    <td>
                                                        {!tw.companies}
                                                    </td>
                                                    <td>
                                                        {!tw.vendor}
                                                    </td>
                                                    <td>{!tw.status}</td>
                                                    <td>{!tw.coordinator}</td>
                                                </tr>
                                            </apex:repeat>
                                        </tbody>
                                    </table>
                            </div>
                        </div>
                    </apex:repeat>
                </apex:outputPanel>
            </apex:outputPanel>
            <!-- END -->
        </apex:outputPanel>
        <!--END:GT-->
        
        <!-- START:FREIGHT-->
        <apex:outputPanel id="traceListContentFreight" layout="block" rendered="{!IF(theJournals.lsJournals_Freight.size > 0 || (taskWrappers.lsGroupsTWNoContract_Freight.size > 0 && searchInputs.searchTraceType=='Trace Date') || (taskWrappers.lsGroupsTW_Freight_AllOther.size > 0 && searchInputs.searchTraceType=='Trace Date'), true, false)}">
            <h2 style="text-align:center">Freight Trace</h2>
            <!-- Start DEADLINE DATE -->
            <apex:outputPanel layout="block" rendered="{!IF(taskWrappers.lsTraceDeadlineDate_Freight.size > 0 && searchInputs.searchTraceType=='DeadLine Date',true,false)}"
                              styleClass="card mb-3">
                <h3>DeadLine Dates</h3>
                <div class="collapse show" id="lsTraceDeadlineDate_Freight">
                        <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                            <thead class="thead-light font-weight-bold">
                                <tr>
                                    <th scope="col">
                                        <span class="font-weight-bold" style="float: left">Status</span>
                                    </th>
                                    <th scope="col">
                                        <span class="font-weight-bold" style="float: left">Production</span>
                                    </th>
                                    <th scope="col">
                                        <span class="font-weight-bold" style="float: left">Stay City</span>
                                    </th>
                                    <th scope="col">
                                        <span class="font-weight-bold" style="float: left">Company</span>
                                    </th>
                                    <th scope="col" width="8%">
                                        <span class="font-weight-bold" style="float: left">Deadline Date</span>
                                    </th>
                                    <th scope="col" width="8%">
                                        <span class="font-weight-bold" style="float: left">Trace Date</span>
                                    </th>
                                    <th scope="col" width="10%">
                                        <span class="font-weight-bold" style="float: left">Trace Owner</span>
                                    </th>
                                </tr>
                            </thead>
                            <tbody>
                                <apex:repeat value="{!taskWrappers.lsTraceDeadlineDate_Freight}" var="t">
                                    <tr>
                                        <td>
                                            {!freightMapDeadlines[t.taskId].Status__c}
                                        </td>
                                        <td>
                                            {!freightMapDeadlines[t.taskId].Production__r.Name}
                                        </td>
                                        <td>{!freightMapDeadlines[t.taskId].Start_City__r.Name}</td>
                                        <td>
                                            {!freightMapDeadlines[t.taskId].Production__r.Account.Name}
                                        </td>
                                        <td>
                                            <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                <apex:param value="{!t.deadlineDate}" />
                                            </apex:outputText>
                                        </td>
                                        <td>
                                            <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                <apex:param value="{!t.deadLineDate}" />
                                            </apex:outputText>
                                        </td>
                                        <td>
                                            <span class="show-data">{!t.coordinator}</span>
                                        </td>
                                    </tr>
                                </apex:repeat>
                            </tbody>
                        </table>
                </div>
            </apex:outputPanel>
            <!-- End DEADLINE DATE -->
            
            <apex:outputPanel rendered="{!searchInputs.searchTraceType=='Trace Date'}">
                <!-- START - Journals -->
                <apex:outputPanel layout="block" rendered="{!theJournals.lsJournals_Freight.size > 0}" styleClass="card mb-3">
                    <h3>Journals</h3>
                    <div class="collapse show" id="lsJournals_Freight">
                            <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                                <thead class="thead-light font-weight-bold">
                                    <tr>
                                        <th scope="col" width="10%">
                                            <span class="font-weight-bold">Follow Up / Trace Date</span>
                                        </th>
                                        <th scope="col">
                                            <span class="font-weight-bold">Journal Entry</span>
                                        </th>
                                        <th scope="col" width="15%">
                                            <span class="font-weight-bold">Categories</span>
                                        </th>
                                        <th scope="col" width="10%">
                                            <span class="font-weight-bold">Created By</span>
                                        </th>
                                        <th scope="col" width="8%">
                                            <span class="font-weight-bold">Created On</span>
                                        </th>
                                        <th scope="col" width="10%">
                                            <span class="font-weight-bold">Coordinator</span>
                                        </th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <apex:repeat value="{!theJournals.lsJournals_Freight}" var="j">
                                        <tr>
                                            <td>
                                                <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                    <apex:param value="{!j.Trace_Date__c}" />
                                                </apex:outputText>
                                            </td>
                                            <td>{!j.Journal_Entry__c}</td>
                                            <td>
                                                <apex:outputText rendered="{!IF(j.Production__r.Name == null, false, true)}">
                                                    <span class="font-weight-bold">Production: </span>
                                                    {!j.Production__r.Name}
                                                    <br />
                                                </apex:outputText>
                                                <apex:repeat value="{!j.Related_Companies__r}" var="rcom">
                                                    <span class="font-weight-bold">Company: </span>
                                                    {!rcom.Company__r.Name}
                                                    <br />
                                                </apex:repeat>
                                                <apex:repeat value="{!j.Related_Contact__r}" var="rcon">
                                                    <span class="font-weight-bold">Contact: </span>
                                                    {!rcon.Contact__r.Name}
                                                    <br />
                                                </apex:repeat>
                                                <apex:outputText rendered="{!IF(j.Bid__r.Contract_ID__c == null, false, true)}">
                                                    <span class="font-weight-bold">Contract: </span>
                                                    {!j.Bid__r.Contract_ID__c}
                                                    <br />
                                                </apex:outputText>
                                                <!-- id ? -->
                                                <apex:outputText rendered="{!IF(j.Bid__r.Name == null, false, true)}">
                                                    <span class="font-weight-bold">Bid: </span>
                                                    {!j.Bid__r.Name}
                                                    <br />
                                                </apex:outputText>
                                                <apex:outputText rendered="{!IF(j.Bid__r.Stay_ID__c == null, false, true)}">
                                                    <span class="font-weight-bold">Stay: </span>
                                                    {!j.Bid__r.Stay_ID__c}
                                                    <br />
                                                </apex:outputText>
                                            </td>
                                            <td>{!j.CreatedBy.Name}</td>
                                            <td>
                                                <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                    <apex:param value="{!j.CreatedDate}" />
                                                </apex:outputText>
                                            </td>
                                            <td>{!j.Trace_Coordinator__r.Name}</td>
                                        </tr>
                                    </apex:repeat>
                                </tbody>
                            </table>
                    </div>
                </apex:outputPanel>
                <!-- END -->
                
                <!-- START - Group Traces 1 Freight -->
                <apex:outputPanel layout="block" rendered="{!taskWrappers.lsGroupsTWNoContract_Freight.size > 0}">
                    <apex:variable var="item_number" value="0" />
                    <!-- Init -->
                    <h3>Traces</h3>
                    <apex:repeat value="{!taskWrappers.lsGroupsTWNoContract_Freight}" var="gls">
                        <apex:variable var="item_number" value="{!VALUE(item_number) + 1}" />
                        <div class="card mb-3">
                            <div class="card-body card-header p-1">
                                <h2>{!gls.groupTitle} ({!gls.totalTasks})</h2>
                            </div>
                            <div class="collapse show" id="lsGroupsTWNoContract_Freight_{!item_number}">
                                    <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                                        <thead class="thead-light font-weight-bold">
                                            <tr>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Trace Date</span>
                                                </th>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Trip Start Date</span>
                                                </th>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Trip End Date</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Description</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">City</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Service Type</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Production</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Company</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Status</span>
                                                </th>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Deadline Date</span>
                                                </th>
                                                <th scope="col" width="10%">
                                                    <span class="font-weight-bold">Coordinator</span>
                                                </th>
                                            </tr>
                                        </thead>
                                        <tbody>
                                            <apex:repeat value="{!gls.lsTasks}" var="tw">
                                                <tr>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                            <apex:param value="{!tw.followUpDate}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                            <apex:param value="{!tw.tripStartDate_gtfr}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                            <apex:param value="{!tw.tripEndDate_gtfr}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>{!tw.tripDescription_gtfr}</td>
                                                    <td>{!tw.city}</td>
                                                    <td>{!tw.tripServiceType_gtfr}</td>
                                                    <td>
                                                        {!tw.production}
                                                    </td>
                                                    <td>
                                                        {!tw.companies}
                                                    </td>
                                                    <td>{!tw.status}</td>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                            <apex:param value="{!tw.deadlineDate}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>{!tw.coordinator}</td>
                                                </tr>
                                            </apex:repeat>
                                        </tbody>
                                    </table>
                            </div>
                        </div>
                    </apex:repeat>
                </apex:outputPanel>
                <!-- END -->
                
                <!-- START - Group Traces Contract List Freight -->
                <apex:outputPanel layout="block" rendered="{!taskWrappers.lsGroupsTWContract_Freight.size > 0}">
                    <apex:variable var="item_number" value="0" />
                    <!-- Init -->
                    <h3>All Contract Traces</h3>
                    <apex:repeat value="{!taskWrappers.lsGroupsTWContract_Freight}" var="gls">
                        <apex:variable var="item_number" value="{!VALUE(item_number) + 1}" />
                        <div class="card mb-3">
                            <div class="card-body card-header p-1">
                                <h2>{!gls.groupTitle} ({!gls.totalTasks})</h2>
                            </div>
                            <div class="collapse show" id="gls_freight_{!item_number}">
                                    <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                                        <thead class="thead-light font-weight-bold">
                                            <tr>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Follow Up Date</span>
                                                </th>
                                                <th scope="col" width="8%">
                                                    <span class="font-weight-bold">Trip Start Date</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Description</span>
                                                </th>
                                                <th scope="col" width="15%">
                                                    <span class="font-weight-bold">City</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Service Type</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Production</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Company</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Vendor</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Status</span>
                                                </th>
                                                <th scope="col">
                                                    <span class="font-weight-bold">Coordinator</span>
                                                </th>
                                            </tr>
                                        </thead>
                                        <tbody>
                                            <apex:repeat value="{!gls.lsTasks}" var="tw">
                                                <tr>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}" styleClass="text-danger">
                                                            <apex:param value="{!tw.followUpDate}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>
                                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                            <apex:param value="{!tw.tripStartDate_gtfr}" />
                                                        </apex:outputText>
                                                    </td>
                                                    <td>{!tw.tripDescription_gtfr}</td>
                                                    <td>{!tw.city}</td>
                                                    <td>{!tw.tripServiceType_gtfr}</td>
                                                    <td>
                                                        {!tw.production}
                                                    </td>
                                                    <td>
                                                        {!tw.companies}
                                                    </td>
                                                    <td>
                                                        {!tw.vendor}
                                                    </td>
                                                    <td>{!tw.status}</td>
                                                    <td>{!tw.coordinator}</td>
                                                </tr>
                                            </apex:repeat>
                                        </tbody>
                                    </table>
                            </div>
                        </div>
                    </apex:repeat>
                </apex:outputPanel>
            </apex:outputPanel>
            <!-- END -->
        </apex:outputPanel>
        <!-- END:FREIGHT-->
        
        <!-- START:AIR-->
        <apex:outputPanel layout="block" rendered="{!IF(theJournals.lsJournals_Air.size > 0 || (taskWrappers.lsGroupsTWNoContract_Air.size > 0 || taskWrappers.lsGroupsTW_Air_AllOther.size > 0 && searchInputs.searchTraceType=='Trace Date'), true, false)}">
                <h2>Air Trace</h2>
                <!-- Start DEADLINE DATE -->
                <apex:outputPanel layout="block" rendered="{!IF(taskWrappers.lsTraceDeadlineDate_Air.size > 0 && searchInputs.searchTraceType=='DeadLine Date',true,false)}"
                  styleClass="card mb-3">
                  <h3>DeadLine Dates</h3>
                  <div class="collapse show" id="lsTraceDeadlineDate_Air">
                      <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                        <thead class="thead-light font-weight-bold">
                          <tr>
                            <th scope="col">
                              <a href="javascript:void(0);" style="color: #495057">
                                <span class="font-weight-bold" style="float: left">Status</span>
                              </a>
                            </th>
                            <th scope="col">
                              <span class="font-weight-bold" style="float: left">Production</span>
                            </th>
                            <th scope="col">
                              <span class="font-weight-bold" style="float: left">Stay City</span>
                            </th>
                            <th scope="col">
                              <span class="font-weight-bold" style="float: left">Company</span>
                            </th>
                            <th scope="col" width="8%">
                              <span class="font-weight-bold" style="float: left">Deadline Date</span>
                            </th>
                            <th scope="col" width="8%">
                              <span class="font-weight-bold" style="float: left">Trace Date</span>
                            </th>
                            <th scope="col" width="10%">
                              <span class="font-weight-bold" style="float: left">Trace Owner</span>
                            </th>
                          </tr>
                        </thead>
                        <tbody>
                          <apex:repeat value="{!taskWrappers.lsTraceDeadlineDate_Air}" var="t">
                            <tr>
                              <td>
                                {!airMapDeadlines[t.taskId].Status__c}
                              </td>
                              <td>
                                {!airMapDeadlines[t.taskId].Production__r.Name}
                              </td>
                              <td>City Field</td>
                              <td>
                                {!airMapDeadlines[t.taskId].Production__r.Account.Name}
                              </td>
                              <td>
                                <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                  <apex:param value="{!t.deadlineDate}" />
                                </apex:outputText>
                              </td>
                              <td>
                                <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                  <apex:param value="{!t.deadLineDate}" />
                                </apex:outputText>
                              </td>
                              <td>
                                <span class="show-data">{!t.coordinator}</span>
                              </td>
                            </tr>
                          </apex:repeat>
                        </tbody>
                      </table>
                  </div>
                </apex:outputPanel>
                <!-- End DEADLINE DATE -->

                <apex:outputPanel rendered="{!searchInputs.searchTraceType=='Trace Date'}">
                  <!-- START - Journals -->
                  <apex:outputPanel layout="block" rendered="{!theJournals.lsJournals_Air.size > 0}" styleClass="card mb-3">
                    <h3>Journals</h3>
                    <div class="collapse show" id="lsJournals_Air">
                        <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                          <thead class="thead-light font-weight-bold">
                            <tr>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Follow Up / Trace Date</span>
                              </th>
                              <th scope="col">
                                <span class="font-weight-bold">Journal Entry</span>
                              </th>
                              <th scope="col" width="15%">
                                <span class="font-weight-bold">Categories</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Created By</span>
                              </th>
                              <th scope="col" width="8%">
                                <span class="font-weight-bold">Created On</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Coordinator</span>
                              </th>
                            </tr>
                          </thead>
                          <tbody>
                            <apex:repeat value="{!theJournals.lsJournals_Air}" var="j">
                              <tr>
                                <td>
                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                      <apex:param value="{!j.Trace_Date__c}" />
                                    </apex:outputText>
                                </td>
                                <td>{!j.Journal_Entry__c}</td>
                                <td>
                                  <apex:outputText rendered="{!IF(j.Production__r.Name == null, false, true)}">
                                    <span class="font-weight-bold">Production: </span>
                                    {!j.Production__r.Name}
                                    <br />
                                  </apex:outputText>
                                  <apex:repeat value="{!j.Related_Companies__r}" var="rcom">
                                    <span class="font-weight-bold">Company: </span>
                                    {!rcom.Company__r.Name}
                                    <br />
                                  </apex:repeat>
                                  <apex:repeat value="{!j.Related_Contact__r}" var="rcon">
                                    <span class="font-weight-bold">Contact: </span>
                                    {!rcon.Contact__r.Name}
                                    <br />
                                  </apex:repeat>
                                  <apex:outputText rendered="{!IF(j.Bid__r.Contract_ID__c == null, false, true)}">
                                    <span class="font-weight-bold">Contract: </span>
                                    {!j.Bid__r.Contract_ID__c}
                                    <br />
                                  </apex:outputText>
                                  <!-- id ? -->
                                  <apex:outputText rendered="{!IF(j.Bid__r.Name == null, false, true)}">
                                    <span class="font-weight-bold">Bid: </span>
                                    {!j.Bid__r.Name}
                                    <br />
                                  </apex:outputText>
                                  <apex:outputText rendered="{!IF(j.Bid__r.Stay_ID__c == null, false, true)}">
                                    <span class="font-weight-bold">Stay: </span>
                                    {!j.Bid__r.Stay_ID__c}
                                    <br />
                                  </apex:outputText>
                                </td>
                                <td>{!j.CreatedBy.Name}</td>
                                <td>
                                  <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                    <apex:param value="{!j.CreatedDate}" />
                                  </apex:outputText>
                                </td>
                                <td>{!j.Trace_Coordinator__r.Name}</td>
                              </tr>
                            </apex:repeat>
                          </tbody>
                        </table>
                    </div>
                  </apex:outputPanel>
                  <!-- END -->
                  <!-- START - Group Traces 1 Air -->
                  <apex:outputPanel layout="block" rendered="{!taskWrappers.lsGroupsTWNoContract_Air.size > 0}">
                    <apex:variable var="item_number" value="0" />
                    <!-- Init -->
                    <h2>Traces</h2>
                    <apex:repeat value="{!taskWrappers.lsGroupsTWNoContract_Air}" var="gls">
                      <apex:variable var="item_number" value="{!VALUE(item_number) + 1}" />
                      <div class="card mb-3">
                        <div class="card-body card-header p-1">
                          <h3>{!gls.groupTitle} ({!gls.totalTasks})</h3>
                        </div>
                        <div class="collapse show" id="lsGroupsTWNoContract_Air_{!item_number}">
                            <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                              <thead class="thead-light font-weight-bold">
                                <tr>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trace Date</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trip Start Date</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trip End Date</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Description</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Group Type</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Production</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Company</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Status</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Deadline Date</span>
                                  </th>
                                  <th scope="col" width="10%">
                                    <span class="font-weight-bold">Coordinator</span>
                                  </th>
                                </tr>
                              </thead>
                              <tbody>
                                <apex:repeat value="{!gls.lsTasks}" var="tw">
                                  <tr>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.followUpDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>
                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                          <apex:param value="{!tw.tripStartDate_air}" />
                                        </apex:outputText>
                                    </td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.tripEndDate_air}" />
                                      </apex:outputText>
                                    </td>
                                    <td>{!tw.tripDescription_air}</td>
                                    <td>{!tw.tripGroupType_air}</td>
                                    <td>
                                      {!tw.production}
                                    </td>
                                    <td>
                                      {!tw.companies}
                                    </td>
                                    <td>{!tw.status}</td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.deadlineDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>{!tw.coordinator}</td>
                                  </tr>
                                </apex:repeat>
                              </tbody>
                            </table>
                        </div>
                      </div>
                    </apex:repeat>
                  </apex:outputPanel>
                  <!-- END -->

                  <!-- START - Group Traces Contract List Air -->
                  <apex:outputPanel layout="block" rendered="{!taskWrappers.lsGroupsTW_Air_AllOther.size > 0}">
                    <apex:variable var="item_number" value="0" />
                    <!-- Init -->
                    <h3>All Contract Traces</h3>
                    <apex:repeat value="{!taskWrappers.lsGroupsTW_Air_AllOther}" var="gls">
                      <apex:variable var="item_number" value="{!VALUE(item_number) + 1}" />
                      <div class="card mb-3">
                        <div class="card-body card-header p-1">
                          <h3>{!gls.groupTitle} ({!gls.totalTasks})</h3>
                        </div>
                        <div class="collapse show" id="gls_air_{!item_number}">
                            <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                              <thead class="thead-light font-weight-bold">
                                <tr>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Follow Up Date</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trip Start Date</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trip End Date</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Description</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Group Type</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Trip Type</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Production</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Company</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Vendor</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Status</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Coordinator</span>
                                  </th>
                                </tr>
                              </thead>
                              <tbody>
                                <apex:repeat value="{!gls.lsTasks}" var="tw">
                                  <tr>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}" styleClass="text-danger">
                                        <apex:param value="{!tw.followUpDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>
                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                          <apex:param value="{!tw.tripStartDate_air}" />
                                        </apex:outputText>
                                    </td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.tripEndDate_air}" />
                                      </apex:outputText>
                                    </td>
                                    <td>{!tw.tripDescription_air}</td>
                                    <td>{!tw.tripGroupType_air}</td>
                                    <td>{!tw.tripType_air}</td>
                                    <td>
                                      {!tw.production}
                                    </td>
                                    <td>
                                      {!tw.companies}
                                    </td>
                                    <td>
                                      {!tw.vendor}
                                    </td>
                                    <td>{!tw.status}</td>
                                    <td>{!tw.coordinator}</td>
                                  </tr>
                                </apex:repeat>
                              </tbody>
                            </table>
                        </div>
                      </div>
                    </apex:repeat>
                  </apex:outputPanel>
                </apex:outputPanel>
                <!-- END -->
              </apex:outputPanel>
        <!-- END:AIR-->
        
        <!-- START ALL OTHER -->
              <apex:outputPanel >
                <apex:outputPanel layout="block" rendered="{!IF(lsTrace_AllOther.size > 0, true, false)}">
                  <h2 style="text-align:center">All Other Traces</h2>
                  <!-- START - Traces -->
                  <div class="card mb-3">
                    <!--<apex:outputPanel layout="block" rendered="{!lsTrace_AllOther.size > 0}" styleClass="card mb-3">-->
                    <div class="card-body card-header p-1">
                      <h3>Traces</h3>
                    </div>
                    <div class="collapse show" id="lsTrace_AllOther">
                        <table border="1px" cellspacing="0px" class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                          <thead class="thead-light font-weight-bold">
                            <tr>
                              <th scope="col" width="8%">
                                <span class="font-weight-bold">Trace Date</span>
                              </th>
                              <th scope="col">
                                <span class="font-weight-bold">Trace Subject</span>
                              </th>
                              <th scope="col" width="8%">
                                <span class="font-weight-bold">Deadline Date</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Trace Owner</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Assigned To</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Status</span>
                              </th>
                            </tr>
                          </thead>
                          <tbody>
                            <apex:repeat value="{!lsTrace_AllOther}" var="t">
                              <tr>
                                <td>
                                  <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                    <apex:param value="{!t.ActivityDate}" />
                                  </apex:outputText>
                                </td>
                                <td>
                                  <apex:outputPanel rendered="{!t.IsForCloseOut__c == true}">
                                    {!t.Subject}
                                </apex:outputPanel>
                                <apex:outputPanel rendered="{!t.subject=='Request to Resend Contract'}">
									{!t.Subject}
                                </apex:outputPanel>
                                <apex:outputPanel rendered="{!t.subject=='Lodging Itinerary Received in Community'}">
                                    {!t.Subject}
                                </apex:outputPanel>
                                <apex:outputPanel rendered="{!and(t.IsForCloseOut__c == false,t.Subject!='Request to Resend Contract',
                                                            t.Subject!='Lodging Itinerary Received in Community')}">
                                    {!t.Subject}
                                </apex:outputPanel>
                                </td>
                                <td>
                                  <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                    <apex:param value="{!t.Deadline_Date__c}" />
                                  </apex:outputText>
                                </td>
                                <td>
                                  <span class="show-data">{!t.CreatedBy.Name}</span>
                                </td>
                                <td>
                                  <span class="show-data">{!t.Owner.Name}</span>
                                </td>
                                <td>
                                  <span class="show-data">{!t.Status}</span>
                                </td>
                              </tr>
                            </apex:repeat>
                          </tbody>
                        </table>
                    </div>
                    <!--</apex:outputPanel>-->
                  </div>
                  <!-- END -->
                </apex:outputPanel>
              </apex:outputPanel>
              <!-- END ALL OTHER -->
    </div>
</apex:component>
```


# Last Modified


# Usage
