---
layout: default
title: Dashboard_Contract_CloseOut
parent: components
grand_parent: Metadata
---
# Metadata Type
components


# Filename 
Dashboard_Contract_CloseOut


# Raw XML
```
<apex:component controller="DashboardController" allowDML="true">
    <apex:attribute type="Revenue__c" name="newRevenueBid" description="The Id of the record consulted" />
    <apex:attribute type="String" name="totalroomrev" description="The Id of the record consulted" />
    <apex:attribute type="Revenue__c[]" name="revenuesBid" description="The Id of the record consulted" />
    <apex:attribute type="Revenue__c[]" name="monthlypickupsBid" description="The Id of the record consulted" />
    <apex:attribute type="Revenue__c[]" name="rebatesBidMonthly" description="The Id of the record consulted" />

    <div class="row">
        <div class="col-md-12">
            <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="newRevenueBid();"><i class="fas fa-plus"></i> Add Revenue</button>
        </div>
    </div>
    <div class="row" style="margin-top:0px !important;">
    <div class="col-md-12">
        <!-- Rebates -->
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
                    <tbody>
                        <tr class="new-revenue-bid" style="display:none;">
                            <td>
                                <apex:inputField value="{!newRevenueBid.Revenue_Type__c}" styleClass="form-control form-control-sm newdata" onchange="changeRevenuePer(this);" />
                            </td>
                            <td>
                                <apex:inputField value="{!newRevenueBid.Rebate_For__c}" styleClass="form-control form-control-sm newdata" />
                            </td>
                            <td>
                                <apex:inputField value="{!newRevenueBid.Charge_Type__c}" styleClass="form-control form-control-sm newdata chargetype" onblur="calculateInvoiced(this,{!totalroomrev});" />
                            </td>
                            <td>
                                <apex:inputField value="{!newRevenueBid.Rebate_currency__c}" styleClass="form-control form-control-sm newdata number" onblur="calculateInvoiced(this,{!totalroomrev});" />
                            </td>
                            <td>
                                <span class="newrevenue-rebate-per" style="display:none;"><apex:inputField value="{!newRevenueBid.Rebate_Per__c}" styleClass="form-control form-control-sm newdata" /></span>
                            </td>
                            <td>
                                <apex:inputField value="{!newRevenueBid.Total__c}" styleClass="form-control form-control-sm newdata total" onblur="calculateInvoiced(this,{!totalroomrev});" />
                            </td>
                            <td>
                                <apex:inputField value="{!newRevenueBid.Invoice_Amount__c}" styleClass="form-control form-control-sm newdata invoiceamount" />
                            </td>
                            <td class="text-center">
                                <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="saveRevenueBid();"><i class="fas fa-check"></i> Save</button>
                                <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="cancelRevenueBid();"><i class="fas fa-ban"></i> Cancel</button>
                            </td>
                        </tr>
                    </tbody>
                </table>
                <apex:outputPanel id="revenuesBidPanel">
                    <table class="table table-sm table-revenues-bid">
                        <tbody>
                            <apex:repeat value="{!revenuesBid}" var="revenue">
                                <tr>
                                    <td width="10%">
                                        <input type="hidden" value="{!revenue.Id}" class="id"  />
                                        <span class="show-data">{!revenue.Revenue_Type__c}</span>
                                        <apex:inputField value="{!revenue.Revenue_Type__c}" styleClass="form-control form-control-sm data revenuetype" onchange="changeRevenuePer(this);" style="display:none;" />
                                    </td>
                                    <td width="10%">
                                        <span class="show-data">{!revenue.Rebate_For__c}</span>
                                        <apex:inputField value="{!revenue.Rebate_For__c}" styleClass="form-control form-control-sm data rebatefor" style="display:none;" />
                                    </td>
                                    <td width="10%">
                                        <span class="show-data">
                                            {!IF(
                                            revenue.Revenue_Type__c == 'Rebate',IF(revenue.Charge_Type__c == 'Amount','Rebate $','Rebate %'),
                                            IF(revenue.Revenue_Type__c == 'Commission',IF(revenue.Charge_Type__c == 'Amount','Commission $','Commission %'),
                                            IF(revenue.Charge_Type__c == 'Amount','Service fee $','Service fee %')
                                            ))}
                                        </span>
                                        <apex:inputField value="{!revenue.Charge_Type__c}" styleClass="form-control form-control-sm data chargetype" onchange="changeRebateField(this);calculateInvoiced(this,{!totalroomrev});" style="display:none;" />
                                    </td>
                                    <td width="15%">
                                        <span class="show-data">
                                            {!ROUND(IF(
                                            revenue.Revenue_Type__c == 'Rebate',IF(revenue.Charge_Type__c == 'Amount',revenue.Rebate_currency__c,revenue.Rebate__c),
                                            IF(revenue.Revenue_Type__c == 'Commission',IF(revenue.Charge_Type__c == 'Amount',revenue.Commission__c,revenue.Commission_Percent__c),
                                            IF(revenue.Charge_Type__c == 'Amount',revenue.Service_Fees__c,revenue.Service_Fees_Percent__c)
                                            )),2)}
                                        </span>
                                        <input type="text" value="{!IF(revenue.Revenue_Type__c == 'Rebate',IF(revenue.Charge_Type__c == 'Amount',revenue.Rebate_currency__c,revenue.Rebate__c),IF(revenue.Revenue_Type__c == 'Commission',IF(revenue.Charge_Type__c == 'Amount',revenue.Commission__c,revenue.Commission_Percent__c),IF(revenue.Charge_Type__c == 'Amount',revenue.Service_Fees__c,revenue.Service_Fees_Percent__c)))}" class="form-control form-control-sm data number" style="display:none;" onblur="calculateInvoiced(this,{!totalroomrev});" />
                                    </td>
                                    <td scope="row" width="15%">
                                        <span class="show-data">{!revenue.Rebate_Per__c}</span>
                                        <span class="newrevenue-rebate-per-data" style="{!IF(revenue.Revenue_Type__c == 'Rebate','','display:none;')}"><apex:inputField value="{!revenue.Rebate_Per__c}" styleClass="form-control form-control-sm data rebateper" style="display:none;" /></span>
                                    </td>
                                    <td width="15%">
                                        <span class="show-data">{!revenue.Total__c}</span>
                                        <input type="text" class="form-control form-control-sm data total" value="{!revenue.Total__c}" style="display:none;" onblur="calculateInvoiced(this,{!totalroomrev});" />
                                    </td>
                                    <td width="10%">
                                        <span class="show-data">{!revenue.Invoice_Amount__c}</span>
                                        <input type="text" class="form-control form-control-sm data invoiceamount" value="{!revenue.Invoice_Amount__c}" style="display:none;" />
                                    </td>
                                    <td class="text-center" width="15%">
                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-save" onclick="saveEditRevenueBid(this);" style="display:none;"><i class="fas fa-check"></i> Save</button>
                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-edit" onclick="editRevenue(this);"><i class="fas fa-pencil-alt"></i> Edit</button>
                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-cancel" onclick="cancel(this);" style="display:none;"><i class="fas fa-ban"></i> Cancel</button>
                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-delete" onclick="deleteRebate('{!revenue.Id}');"><i class="fas fa-times"></i> Delete</button>
                                    </td>
                                </tr>
                            </apex:repeat>

                        </tbody>
                    </table>
                </apex:outputPanel>
            </div>
        </div>
        <!-- END Rebates -->

        <!-- Monthly Pick Up -->
        <!--<div class="row">
            <div class="col-md-12">
                <apex:outputPanel id="btnMonthlyPickupPanel">
                    <button type="button" class="btn btn-secondary btn-sm btn-custom btn-monthly-pickup" style="{!IF(revenueCommission.Is_this_a_monthly_Pick_Up__c == 'Yes','','display:none;')}" onclick="newMonthlyPickup();"><i class="fas fa-plus"></i> Add Monthly Pickup</button>
                </apex:outputPanel>
            </div>
        </div>-->
        <div class="row monthly-pickup-section" style="{!IF(revenueCommission.Is_this_a_monthly_Pick_Up__c == 'Yes','','display:none;')}">

            <div class="col-md-12">
                <span style="font-weight:bold;">Monthly Pick Up Details</span>
                <table class="table table-sm table-revenues-bid" style="margin-top:5px;margin-bottom:0;">
                    <thead class="thead-light">
                        <tr>
                            <th width="20%">Indicate Dates</th>
                            <th width="15%">Room Type</th>
                            <th width="10%">Room Nights</th>
                            <th width="10%">Room Rate</th>
                            <th width="10%">Commission</th>
                            <th width="15%">Invoiced Date</th>
                            <th width="20%"></th>
                        </tr>
                    </thead>
                    <!--<tbody>
                        <tr class="new-pickup-bid" style="display:none;">
                            <td>
                                <apex:inputField value="{!newPickupBid.Indicate_Dates__c}" styleClass="form-control form-control-sm newdata" />
                            </td>
                            <td>
                                <apex:inputField value="{!newPickupBid.Charge_Type__c}" styleClass="form-control form-control-sm newdata" />
                            </td>
                            <td>
                                <apex:inputField value="{!newPickupBid.Commission__c}" styleClass="form-control form-control-sm newdata" />
                            </td>
                            <td>
                                <apex:inputField value="{!newPickupBid.Commission_Due__c}" styleClass="form-control form-control-sm newdata" />
                            </td>
                            <td>
                                <apex:inputField value="{!newPickupBid.Invoice_Date__c}" styleClass="form-control form-control-sm newdata" />
                            </td>
                            <td class="text-center">
                                <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="savePickupBid();"><i class="fas fa-check"></i> Save</button>
                                <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="cancelPickupBid();"><i class="fas fa-ban"></i> Cancel</button>
                            </td>
                        </tr>
                    </tbody>-->
                </table>
                <apex:outputPanel id="monthlyPickupBidPanel">
                    <table class="table table-sm table-revenues-bid">
                        <tbody>
                            <apex:repeat value="{!monthlypickupsBid}" var="pickup">
                                <tr>
                                    <td width="20%">
                                        <span class="show-data">{!pickup.Indicate_Dates__c}</span>
                                        <apex:inputField value="{!pickup.Indicate_Dates__c}" styleClass="form-control form-control-sm data indicatedates" style="display:none;" />
                                        <input type="hidden" value="{!pickup.Id}" class="id"  />
                                    </td>
                                    <td width="15%">
                                        <span class="show-data">{!pickup.Room_Type_Name__c}</span>
                                        <apex:inputField value="{!pickup.Room_Type_Name__c}" styleClass="form-control form-control-sm data roomtypename" style="display:none;" />
                                    </td>
                                    <td width="10%">
                                        <span class="show-data">{!pickup.Room_Nights__c}</span>
                                        <input type="text" value="{!pickup.Room_Nights__c}" class="form-control form-control-sm data roomnights" style="display:none;" />
                                    </td>
                                    <td width="10%">
                                        <span class="show-data">{!pickup.Rate_currency__c}</span>
                                        <input type="text" value="{!pickup.Rate_currency__c}" class="form-control form-control-sm data rate" style="display:none;" />
                                    </td>
                                    <td width="10%">
                                        <span class="show-data">{!pickup.Commission_Per_Room__c}</span>
                                        <input type="text" value="{!pickup.Commission_Per_Room__c}" class="form-control form-control-sm data commission" style="display:none;" />
                                    </td>
                                    <td width="15%">
                                        <span class="show-data">
                                            <apex:outputText value="{0,date,dd-MMMM-yyyy}">
                                                <apex:param value="{!pickup.Invoice_Date__c}" />
                                            </apex:outputText>
                                        </span>
                                        <span class="data" style="display:none;">
                                            <apex:inputField value="{!pickup.Invoice_Date__c}" styleClass="form-control form-control-sm invoicedate" />
                                        </span>
                                    </td>
                                    <td class="text-center" width="20%">
                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-save" onclick="saveEditPickupBid(this);" style="display:none;"><i class="fas fa-check"></i> Save</button>
                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-edit" onclick="editRevenue(this);"><i class="fas fa-pencil-alt"></i> Edit</button>
                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-cancel" onclick="cancel(this);" style="display:none;"><i class="fas fa-ban"></i> Cancel</button>
                                        <button type="button" class="btn btn-secondary btn-sm btn-custom btn-delete" onclick="deleteRebate('{!pickup.Id}');"><i class="fas fa-times"></i> Delete</button>
                                    </td>
                                </tr>
                            </apex:repeat>

                        </tbody>
                    </table>
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
                                <tbody>
                                    <tr class="new-revenue-bid" style="display:none;">
                                        <td>
                                            <apex:inputField value="{!newRevenueBid.Revenue_Type__c}" styleClass="form-control form-control-sm newdata" onchange="calculateInvoiced(this,{!totalroomrev});" />
                                        </td>
                                        <td>
                                            <apex:inputField value="{!newRevenueBid.Rebate_For__c}" styleClass="form-control form-control-sm newdata" />
                                        </td>
                                        <td>
                                            <apex:inputField value="{!newRevenueBid.Charge_Type__c}" styleClass="form-control form-control-sm newdata chargetype" onblur="calculateInvoiced(this,{!totalroomrev});" />
                                        </td>
                                        <td>
                                            <apex:inputField value="{!newRevenueBid.Rebate_currency__c}" styleClass="form-control form-control-sm newdata number" onblur="calculateInvoiced(this,{!totalroomrev});" />
                                        </td>
                                        <td>
                                            <span class="newrevenue-rebate-per" style="display:none;"><apex:inputField value="{!newRevenueBid.Rebate_Per__c}" styleClass="form-control form-control-sm newdata" /></span>
                                        </td>
                                        <td>
                                            <apex:inputField value="{!newRevenueBid.Total__c}" styleClass="form-control form-control-sm newdata total" onblur="calculateInvoiced(this,{!totalroomrev});" />
                                        </td>
                                        <td>
                                            <apex:inputField value="{!newRevenueBid.Invoice_Amount__c}" styleClass="form-control form-control-sm newdata invoiceamount" />
                                        </td>
                                        <td class="text-center">
                                            <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="saveRevenueBid();"><i class="fas fa-check"></i> Save</button>
                                            <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="cancelRevenueBid();"><i class="fas fa-ban"></i> Cancel</button>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                            <apex:outputPanel id="revenuesRebatesBidPanel">
                                <table class="table table-sm table-revenues-bid">
                                    <tbody>
                                        <apex:repeat value="{!revenuesBid}" var="revenue">
                                            <tr>
                                                <td width="10%">
                                                    <input type="hidden" value="{!revenue.Id}" class="id"  />
                                                    <span class="show-data">{!revenue.Revenue_Type__c}</span>
                                                    <apex:inputField value="{!revenue.Revenue_Type__c}" styleClass="form-control form-control-sm data revenuetype" onchange="changeRevenuePer(this);" style="display:none;" />
                                                </td>
                                                <td width="10%">
                                                    <span class="show-data">{!revenue.Rebate_For__c}</span>
                                                    <apex:inputField value="{!revenue.Rebate_For__c}" styleClass="form-control form-control-sm data rebatefor" style="display:none;" />
                                                </td>
                                                <td width="10%">
                                                    <span class="show-data">
                                                        {!IF(
                                                        revenue.Revenue_Type__c == 'Rebate',IF(revenue.Charge_Type__c == 'Amount','Rebate $','Rebate %'),
                                                        IF(revenue.Revenue_Type__c == 'Commission',IF(revenue.Charge_Type__c == 'Amount','Commission $','Commission %'),
                                                        IF(revenue.Charge_Type__c == 'Amount','Service fee $','Service fee %')
                                                        ))}
                                                    </span>
                                                    <apex:inputField value="{!revenue.Charge_Type__c}" styleClass="form-control form-control-sm data chargetype" onchange="changeRebateField(this);calculateInvoiced(this,{!totalroomrev});" style="display:none;" />
                                                </td>
                                                <td width="15%">
                                                    <span class="show-data">
                                                        {!ROUND(IF(
                                                        revenue.Revenue_Type__c == 'Rebate',IF(revenue.Charge_Type__c == 'Amount',revenue.Rebate_currency__c,revenue.Rebate__c),
                                                        IF(revenue.Revenue_Type__c == 'Commission',IF(revenue.Charge_Type__c == 'Amount',revenue.Commission__c,revenue.Commission_Percent__c),
                                                        IF(revenue.Charge_Type__c == 'Amount',revenue.Service_Fees__c,revenue.Service_Fees_Percent__c)
                                                        )),2)}
                                                    </span>
                                                    <input type="text" value="{!IF(revenue.Revenue_Type__c == 'Rebate',IF(revenue.Charge_Type__c == 'Amount',revenue.Rebate_currency__c,revenue.Rebate__c),IF(revenue.Revenue_Type__c == 'Commission',IF(revenue.Charge_Type__c == 'Amount',revenue.Commission__c,revenue.Commission_Percent__c),IF(revenue.Charge_Type__c == 'Amount',revenue.Service_Fees__c,revenue.Service_Fees_Percent__c)))}" class="form-control form-control-sm data number" style="display:none;" onblur="calculateInvoiced(this,{!totalroomrev});" />
                                                </td>
                                                <td scope="row" width="15%">
                                                    <span class="show-data">{!revenue.Rebate_Per__c}</span>
                                                    <span class="newrevenue-rebate-per-data" style="{!IF(revenue.Revenue_Type__c == 'Rebate','','display:none;')}"><apex:inputField value="{!revenue.Rebate_Per__c}" styleClass="form-control form-control-sm data rebateper" style="display:none;" /></span>
                                                </td>
                                                <td width="15%">
                                                    <span class="show-data">{!revenue.Total__c}</span>
                                                    <input type="text" class="form-control form-control-sm data total" value="{!revenue.Total__c}" style="display:none;" onblur="calculateInvoiced(this,{!totalroomrev});" />
                                                </td>
                                                <td width="10%">
                                                    <span class="show-data">{!revenue.Invoice_Amount__c}</span>
                                                    <input type="text" class="form-control form-control-sm data invoiceamount" value="{!revenue.Invoice_Amount__c}" style="display:none;" />
                                                </td>
                                                <td class="text-center" width="15%">
                                                    <button type="button" class="btn btn-secondary btn-sm btn-custom btn-save" onclick="saveEditRevenueBid(this);" style="display:none;"><i class="fas fa-check"></i> Save</button>
                                                    <button type="button" class="btn btn-secondary btn-sm btn-custom btn-edit" onclick="editRevenue(this);"><i class="fas fa-pencil-alt"></i> Edit</button>
                                                    <button type="button" class="btn btn-secondary btn-sm btn-custom btn-cancel" onclick="cancel(this);" style="display:none;"><i class="fas fa-ban"></i> Cancel</button>
                                                    <button type="button" class="btn btn-secondary btn-sm btn-custom btn-delete" onclick="deleteRebate('{!revenue.Id}');"><i class="fas fa-times"></i> Delete</button>
                                                </td>
                                            </tr>
                                        </apex:repeat>

                                    </tbody>
                                </table>
                            </apex:outputPanel>
                        </div>
                    </div>
                </apex:outputPanel>

            </div>


        </div>

        <!-- END Monthly Pick Up -->
    </div>
</div>
<apex:actionFunction action="{!addRebateBid}" name="saveRebateBidJs" status="loading" reRender="rebatesBidPanel,revenuesBidPanel" />
<apex:actionFunction action="{!addRevenueBid}" name="saveRevenueBidJs" status="loading" reRender="revenuesBidPanel,rebatesBidPanel" />
<script>
    function newRebateBid() {
    $('.newdata').val('');
    $('.new-rebate-bid').show();
    $('.table-rebates-bid').show();

    function saveRevenueBid() {
    $('.new-revenue-bid').hide();
    saveRevenueBidJs();
}
</script>

</apex:component>
```


# Last Modified


# Usage
