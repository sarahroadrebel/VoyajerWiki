---
layout: default
title: Dashboard_Tab_Close_Out
parent: components
grand_parent: Metadata
---
# Metadata Type
components


# Filename 
Dashboard_Tab_Close_Out


# Raw XML
```
<!--
  @description       : 
  @author            : sfdc cb
  @group             : 
  @last modified on  : 09-03-2021
  @last modified by  : sfdc cb
-->
<apex:component >

    <apex:attribute type="Revenue__c[]" name="monthlypickupsBidRevenues" description="The rebates for the monthly pickups" access="PUBLIC" />

    <div class="row">
        <div class="col-md-12">
            <span style="font-weight:bold;">Revenue Details</span>
            <table class="table table-sm table-revenues-bid" style="margin-top:5px;margin-bottom:0;">
                <thead class="thead-light">
                    <tr>
                        <th width="10%">Revenue Type</th>
                        <th width="10%">Rebate For</th>
                        <th width="10%">Charge Type</th>
                        <th width="15%">Amount/Percentage</th>
                        <th width="15%">Rebate Per</th>
                        <th width="15%">Total #</th>
                        <th width="10%">Invoiced amount</th>
                        <th width="15%"></th>
                    </tr>
                </thead>
            </table>
                <table class="table table-sm table-revenues-bisd">
                    <tbody>
                        <apex:repeat value="{!monthlypickupsBidRevenues}" var="revenuemonthly">
                            {!revenuemonthly}
                            <tr>
                                <td width="10%">
                                    {!revenuemonthly.Revenue_Type__c}
                                </td>
                                <td width="10%">
                                    <span class="">{!revenuemonthly.Rebate_For__c}</span>
                                </td>
                                <td width="10%">
                                    <span class="">
                                        {!IF(
                                            revenuemonthly.Revenue_Type__c == 'Rebate',IF(revenuemonthly.Charge_Type__c == 'Amount','Rebate $','Rebate %'),
                                        IF(revenuemonthly.Revenue_Type__c == 'Commission',IF(revenuemonthly.Charge_Type__c == 'Amount','Commission $','Commission %'),
                                        IF(revenuemonthly.Charge_Type__c == 'Amount','Service fee $','Service fee %')
                                        ))}
                                    </span>
                                </td>
                                <td width="15%">
                                    <span class="show-data">
                                        {!ROUND(IF(
                                        revenuemonthly.Revenue_Type__c == 'Rebate',IF(revenuemonthly.Charge_Type__c == 'Amount',revenuemonthly.Rebate_currency__c,revenuemonthly.Rebate__c),
                                        IF(revenuemonthly.Revenue_Type__c == 'Commission',IF(revenuemonthly.Charge_Type__c == 'Amount',revenuemonthly.Commission__c,revenuemonthly.Commission_Percent__c),
                                        IF(revenuemonthly.Charge_Type__c == 'Amount',revenuemonthly.Service_Fees__c,revenuemonthly.Service_Fees_Percent__c)
                                        )),2)}
                                    </span>
                                </td>
                                <td scope="row" width="15%">
                                    <span class="show-data">{!revenuemonthly.Rebate_Per__c}</span>
                                </td>
                                <td width="15%">
                                    <span class="show-data">{!revenuemonthly.Total__c}</span>
                                </td>
                                <td width="10%">
                                    <span class="show-data">{!revenuemonthly.Invoice_Amount__c}</span>
                                </td>
                                <td class="text-center" width="15%">
                                </td>
                            </tr>
                        </apex:repeat>

                    </tbody>
                </table>
        </div>
    </div>
</apex:component>
```


# Last Modified


# Usage
