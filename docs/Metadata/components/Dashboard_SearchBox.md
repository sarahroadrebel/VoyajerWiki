---
layout: default
title: Dashboard_SearchBox
parent: components
grand_parent: Metadata
---
# Metadata Type
components


# Filename 
Dashboard_SearchBox


# Raw XML
```
<apex:component layout="block" controller="Dashboard_SearchBoxController">
    <apex:attribute type="DashboardConfigurationWrapper" name="variables" description="The variables of the VFP" />
    <apex:attribute type="String" name="parentObject" description="The type of parent object for the Bid" />
    <style>
        .search-form-element {
            margin-bottom: 0 !important;
        }
        .inputpicker-overflow-hidden{width:100%;}
    </style>
    <div class="slds-box slds-box_x-small slds-grid slds-theme_default">
        <apex:outputPanel id="informationProdPanel" style="width: 750px;">
            <div class="slds-col">
                <div class="slds-grid" style="align-items: center;">
                    <button type="button" class="btn btn-secondary btn-sm btn-custom" dir="up" onclick="expand(this);"><i class="fas fa-angle-double-up"></i></button>
                    <div class="slds-form-element slds-form-element_horizontal search-form-element">
                        <label class="slds-form-element__label" for="production" style="margin: 0.4em 1em 0.4em 3em;">Productions</label>
                        <div class="slds-form-element__control searchProduction" style="display: flex;padding-left: 0;">
                            <input type="hidden" id="production" class="productionSearch" value="{!variables.productionId}" />
                            <input id="productionname" class="form-control form-control-sm" name="productionname" value="{!variables.productionName}" onkeyup="setInputProduction();" />
                            <a href="javascript:void(0);" onclick="openProductionDetail()"><i class="fas fa-info-circle" style="font-size: 30px;margin-left: 10px;"></i></a>
                            <script>
                            createAutocompleteProduction = false;
                            $('input[id$=production]').data('pre',$('input[id$=production]').val());
                            </script>
                        </div>
                    </div>
                </div>
            </div>
        </apex:outputPanel>
        <div class="slds-col slds-size_1-of-6">
            <div class="slds-form-element slds-form-element_horizontal search-form-element" style="margin-top: 0.4em; text-align: end;">
                <span class="slds-radio">
                    <input type="radio" id="searchByParent" value="searchByParent" name="options" checked="" />
                    <label class="slds-radio__label" for="searchByParent">
                        <span class="slds-radio_faux"></span>
                        <span class="slds-form-element__label" style="{!IF(parentObject='Housing','','display: none;')}">Stay ID</span>
                        <span class="slds-form-element__label" style="{!IF(OR(parentObject='Ground',parentObject='Freight',parentObject='Air'),'','display: none;')}">Trip ID</span>
                    </label>
                </span>
                <span class="slds-radio">
                    <input type="radio" id="searchByBid" value="searchByBid" name="options" checked="true" />
                    <label class="slds-radio__label" for="searchByBid">
                        <span class="slds-radio_faux"></span>
                        <span class="slds-form-element__label">Bid ID</span>
                    </label>
                </span>
            </div>
        </div>
        <div class="slds-col slds-size_1-of-6">
            <div class="slds-form-element search-form-element">
                <div class="slds-form-element__control">
                    <input type="text" class="slds-input searchByRecordId" id="searchByRecordId" />
                </div>
            </div>
        </div>
        <div class="slds-col">
            <div class="slds-form-element" style="margin: 0.4em 1em 0.4em 1em;">
                <div class="slds-form-element__control">
                    <div class="slds-checkbox">
                        <input type="checkbox" name="searchAll" id="searchAll" value="searchAll" checked="" />
                        <label class="slds-checkbox__label" for="searchAll">
                            <span class="slds-checkbox_faux"></span>
                            <span class="slds-form-element__label">All</span>
                        </label>
                    </div>
                </div>
            </div>
        </div>
        <div class="slds-col">
            <div class="slds-form-element" style="margin: 0.4em 1em 0.4em 1em;">
                <div class="slds-form-element__control">
                    <button type="button" class="btn btn-danger btn-sm btn-custom" onclick="openModal('myModalProductionMerge');" >Merge Productions</button>
                </div>
            </div>
        </div>
    </div>
    <div class="modal fade" id="myModalProductionMerge" role="dialog" style="padding-right: 18px;">
        <div class="modal-dialog modal-lg">
            <div class="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title">Delete/Merge Duplicate Production</h4>
                    <button type="button" class="close" onclick="closeMergeProductionsJs('','');">&times;</button>
                </div>
                <apex:outputPanel id="productionMergePanel" layout="block">
                    <c:Dashboard_Merge_Productions />
                </apex:outputPanel>
            </div>
        </div>
    </div>
    
    <script>
    function openProductionDetail(){
        var productionid = $('input[id$=production]').val();
        if(productionid != null && productionid != ''){
            window.open('/' + productionid);
        }
    }
    function setInputProduction(){
        if(createAutocompleteProduction == false){
            createAutocompleteProduction = true;
            $( "input[id$=productionname]" ).autocomplete({
                lookup: function (query, done) {
                    var all = $('input[id$=searchAll]').prop('checked');
                    Visualforce.remoting.Manager.invokeAction(
                        '{!$RemoteAction.Dashboard_SearchBoxController.searchProd}',query,all,
                        function(result, event){
                            if (event.status) {
                                var t1 = result;
                                var results = t1.replace(/(&quot\;)/g,"\"").replace(/&#39;/g,"'").replace(/(&amp\;)/g,"&");
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
                autoSelectFirst: false,
                beforeRender: function (container,suggestions) {
                    container.find('.autocomplete-suggestion').each(function(i, suggestion){
                        if(i == 0) $(this).before("<table width='100%' class='table-inputpicker'><tr><td width='38%'><span class='inputpicker-list-item'>Production Name</span></td><td width='28%'><span class='inputpicker-list-item'>Company</span></td><td width='12%'><span class='inputpicker-list-item'>Status</span></td><td width='20%'><span class='inputpicker-list-item'>Office Location</span></td></tr></table>")
                    });
                },
                formatResult: function(suggestion, currentValue){
                    return "<table width='100%' class='table-inputpicker'><tr><td width='38%'><span class='inputpicker-list-item-sug'>"+suggestion.value+"</span></td><td width='28%'><span class='inputpicker-list-item-sug'>"+suggestion.extra2+"</span></td><td width='12%'><span class='inputpicker-list-item-sug'>"+suggestion.extra1+"</span></td><td width='20%'><span class='inputpicker-list-item-sug'>"+suggestion.extra3+"</span></td></tr></table>";
                },
                onSelect: function (suggestion) {
                    $('input[id$=production]').val(suggestion.data);
                    console.log('now: ' + $('input[id$=production]').val() );
                    console.log('last: ' + $('input[id$=production]').data('pre') );
                    if($('input[id$=production]').data('pre') != $('input[id$=production]').val() || $('input[id$=searchByRecordId]').val() != ''){
                        $('input[id$=productionname]').val(suggestion.value);
                        $('input[id$=production]').data('pre',$('input[id$=production]').val());
                        $('input[id$=searchByRecordId]').val('');
                        searchInformationJs(suggestion.data);
                    }
                }
            });
        }
    }
    
    function expand(val) {
        $('.expand').slideToggle('slow');
    }
    
    $('body').off('keyup','.searchByRecordId');
    $('body').on('keyup','.searchByRecordId', function(e){
        console.log('test: '+$('input[name$=options]:checked').val());
        if($('input[name$=options]:checked').val() == undefined){
            alert('Select the criteria of your search: Stay ID or Bid ID.');
        }else{
            if (e.which == 13) {
                var radioValue = $('input[name$=options]:checked').val();
                var search = $('input[id$=searchByRecordId]').val();
                console.log(radioValue);
                console.log(search);
                searchProductionJs(radioValue,search);
            }
        }
    });
    
    $('body').off('click','#searchAll');
    $('body').on('click','#searchAll', function(e){
        if($(this).is(':checked')) searchAll = true;
        else searchAll = false;
    });
    </script>
</apex:component>
```


# Last Modified


# Usage
