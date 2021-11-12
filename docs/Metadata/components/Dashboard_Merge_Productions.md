---
layout: default
title: Dashboard_Merge_Productions
parent: components
grand_parent: Metadata
---
# Metadata Type
components


# Filename 
Dashboard_Merge_Productions


# Raw XML
```
<apex:component layout="block" controller="Dashboard_Merge_Productions" allowDML="true">
    <!--<apex:attribute type="String" name="recordId" assignTo="{!relativeRecordId}" description="The Id of the record consulted" />
    <apex:attribute type="String" name="parentSObject" assignTo="{!relativeParentSObjectName}" description="The name of the parent object of the record consulted" />
    <apex:attribute type="String" name="productionId" assignTo="{!opportunityId}" description="The Id of the production loaded" />
    <apex:attribute type="Boolean" name="contract" assignTo="{!isBidContract}" default="false" description="The target of the Document Modal" />-->
    <style>
        .colButton { padding: 0.25em 0.75em !important; max-width: 20%; flex-grow: 1; flex-basis: 20%; flex-shrink: 0; }
        .colButton button { border-radius: 4px !important; width: 100% !important; }
        .btn-nav-modal { width: 1.5rem; height: 1.5rem; border-radius: 12px; border: 1px solid #c5c5c5 !important; margin: 1px 2px !important; font-size: 0.8rem !important; padding: 0; line-height: 20px; color: #2e2e2e !important; background: transparent; opacity: 1 !important; }
        .pageActive { border: 1px solid #f0713a; background-image: none,linear-gradient(to bottom,#fe761b 0,#e15613 100%); color: #fff !important; }
        .btn-secondary:disabled { background-color: inherit !important; }
        #titleField { display: flex; align-items: center; height: 100%; padding: 0 1em; flex: 1; border-right: 1px solid #c5c5c5; cursor: pointer; }
        #dateUploadedField { display: flex; align-items: center; height: 100%; padding: 0 1em; width: 15em; border-right: 1px solid #c5c5c5; cursor: pointer; }
        .tableField span:hover { text-decoration: underline; }
        .sortFieldAsc:after { flex: 1; text-align: start; padding-left: 0.25rem; font-family: "Font Awesome 5 Free"; font-weight: 900; content: "0de"; }
        .sortFieldDesc:after { flex: 1; text-align: start; padding-left: 0.25rem; font-family: "Font Awesome 5 Free"; font-weight: 900; content: "0dd"; }
        .emailFormLabel { padding: 0.5em 1em; }
        .highlighted span, .highlighted a { color: #fff !important; }
    </style>
    <input type="hidden" id="message_production_merge" value="{!messageMerge}" />
    <input type="hidden" id="keep_name_merge" value="{!nameMerge}" />
    <input type="hidden" id="keep_id_merge" value="{!mergeId}" />
    <div class="modal-body" style="font-size:12px; flex-direction: column;">
		<div class="row" style="margin-top: 0px !important;">
            <div class="col-md-12">
                <div style="width: 100%;border-bottom: 1px solid #e9ecef;">
                    <span style="font-size:20px;">Please enter Production info below</span>
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col-md-4">
                <span style="color:red;">Delete Production</span><br/>
                <span style="float:left;margin-top: 5px;margin-right: 10px;">Id:</span>
                <span style="float:left;"><input type="text" id="delete_production_merge" class="form-control form-control-sm" /> </span>
            </div>
            <div class="col-md-2">
                <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="confirmProduction('delete');" style="margin-top: 18px;">Confirm</button>
            </div>
            <div class="col-md-4" style="padding-top: 20px;font-size: 14px;">
                <apex:outputPanel id="deleteProductionMergePanel">
                    <apex:outputPanel rendered="{!IF(deleteProduction.Id != null,true,false)}">
                    	<span style="font-weight:bold;">Name:</span>&nbsp;<span>{!deleteProduction.Name}</span>
                    </apex:outputPanel>
                </apex:outputPanel>
            </div>
        </div>
        <div class="row">
            <div class="col-md-4">
                <span style="color:red;">Keep Production</span><br/>
                <span style="float:left;margin-top: 5px;margin-right: 10px;">Id:</span>
                <span style="float:left;"><input type="text" id="keep_production_merge" class="form-control form-control-sm" /> </span>
            </div>
            <div class="col-md-2">
                <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="confirmProduction('keep');" style="margin-top: 18px;">Confirm</button>
            </div>
            <div class="col-md-4" style="padding-top: 20px;font-size: 14px;">
                <apex:outputPanel id="keepProductionMergePanel">
                    <apex:outputPanel rendered="{!IF(keepProduction.Id != null,true,false)}">
                    	<span style="font-weight:bold;">Name:</span>&nbsp;<span>{!keepProduction.Name}</span>
                    </apex:outputPanel>
                </apex:outputPanel>
            </div>
        </div>
    </div>
    <div class="modal-footer" style="display: block;">
        <button type="button" class="btn btn-danger btn-sm btn-send" onclick="mergeProductions();" >Submit</button>
        <button type="button" class="btn btn-danger btn-sm btn-send" onclick="closeMergeProductionsJs('','');" >Cancel</button>
    </div>
    
    <apex:actionFunction name="confirmProductionJs" action="{!confirmProductions}" status="loading" reRender="deleteProductionMergePanel,keepProductionMergePanel">
        <apex:param assignTo="{!deleteProductionId}" name="deleteProductionId" value=""/>
        <apex:param assignTo="{!keepProductionId}" name="keepProductionId" value="" />
    </apex:actionFunction>
    <apex:actionFunction name="closeMergeProductionsJs" action="{!confirmProductions}" status="loading" reRender="deleteProductionMergePanel,keepProductionMergePanel" oncomplete="$('input[id$=delete_production_merge]').val('');$('input[id$=keep_production_merge]').val('');closeModal('myModalProductionMerge');">
        <apex:param assignTo="{!deleteProductionId}" name="deleteProductionId" value=""/>
        <apex:param assignTo="{!keepProductionId}" name="keepProductionId" value="" />
    </apex:actionFunction>
    <apex:actionFunction name="confirmProductionJs" action="{!confirmProductions}" status="loading" reRender="deleteProductionMergePanel,keepProductionMergePanel">
        <apex:param assignTo="{!deleteProductionId}" name="deleteProductionId" value=""/>
        <apex:param assignTo="{!keepProductionId}" name="keepProductionId" value="" />
    </apex:actionFunction>
    <apex:actionFunction name="mergeProductionsJs" action="{!mergeProductions}" status="loading" reRender="productionMergePanel" oncomplete="showAfterMerge();">
        <apex:param assignTo="{!deleteProductionId}" name="deleteProductionId" value=""/>
        <apex:param assignTo="{!keepProductionId}" name="keepProductionId" value="" />
    </apex:actionFunction>
    <script>
    function showAfterMerge(){
        var message_production_merge = $('input[id$=message_production_merge]').val();
        alert(message_production_merge);
        if(message_production_merge.includes('completed')){
            closeModal('myModalProductionMerge');
            $('input[id$=productionname]').val($('input[id$=keep_name_merge]').val());
            $('input[id$=production]').data('pre',$('input[id$=keep_id_merge]').val());
            searchInformationJs($('input[id$=keep_id_merge]').val());
        }
    }
    function mergeProductions(){
        var delete_production_id = $('input[id$=delete_production_merge]').val();
        var keep_production_id = $('input[id$=keep_production_merge]').val();
        
        if(delete_production_id == '' || keep_production_id == ''){
            alert('Both ID\'s are required');
        }else{
            if(delete_production_id == keep_production_id){
                alert('Both ID\'s can not same');
            }else{
                var confirmAction = confirm('Are you sure you want to delete and merge this production?');
                if(confirmAction) mergeProductionsJs(delete_production_id,keep_production_id);
            }
        }
    }
    function confirmProduction(typez){
        var delete_production_id = $('input[id$=delete_production_merge]').val();
        var keep_production_id = $('input[id$=keep_production_merge]').val();
        var enterValidation = true;
        if(typez == 'delete'){
            if(delete_production_id == ''){
                enterValidation = false;
                alert('Please Enter ProductionId');
            }
        }
        if(typez == 'keep'){
            if(keep_production_id == ''){
                enterValidation = false;
                alert('Please Enter ProductionId');
            }
        }
        if(enterValidation){
            if(delete_production_id == keep_production_id){
                alert('Both ID\'s can not same');
            }else{
                confirmProductionJs(delete_production_id,keep_production_id);
            }
        }
    }
    </script>
</apex:component>
```


# Last Modified


# Usage
