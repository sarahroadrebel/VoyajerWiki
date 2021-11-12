---
layout: default
title: Dashboard_Tab_Contract_Forms
parent: components
grand_parent: Metadata
---
# Metadata Type
components


# Filename 
Dashboard_Tab_Contract_Forms


# Raw XML
```
<apex:component layout="block" controller="Dashboard_Tab_Contract_Forms" allowDML="true">
    <apex:attribute type="String" name="formBidId" assignTo="{!bidContractId}" description="The Id of the bid related" required="true"/>
    <apex:attribute type="String" name="formBidParentSObject" assignTo="{!bidParentSObject}" description="The sObject name of the bid's parent" required="true"/>
    <apex:attribute type="SelectOption[]" name="formClients" description="The clients available" />

    <style>
        .colFormHeader { display: flex; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; align-items: center; }
        .colFormLabel { display: flex; justify-content: flex-end; }
        .colFormLabel span { margin-top: 0.35rem; }
        /*---bidAgreementModal---*/
        .bidAgreementModal table>thead{
            background-color:rgba(0,0,0,.05);
        }
        .bidAgreementModal table th{
            padding:5px !important;
        }
        .bidAgreementModal table td{
            padding:5px !important;
        }
        .bidAgreementModal tbody tr:nth-of-type(even) {
            background-color: rgba(0,0,0,.02);
        }
        /*---attachGCQModal---*/
        .attachGCQModal table>thead{
            background-color:rgba(0,0,0,.05);
        }
        .attachGCQModal table th{
            padding:5px !important;
        }        
        .attachGCQModal .table-hover > tbody > tr{
            cursor: pointer;
        }
        .attachGCQModal .table > tbody tr:nth-of-type(even) {
            background-color: rgba(0,0,0,.02);
        }
        .attachGCQModal .table-hover > tbody > tr:hover{
            background-color: #deedf7;
        }
        .attachGCQModal table td{
            padding:5px !important;
            vertical-align: middle;
        }
        .gcqSelected{
            background-color: #88cbf7 !important;
        }
        /*----Override slds--------*/
        .input-group span.dateFormat{
            display:none !important;
        }
        /*----Messages--------*/
        .saveMessage{
            color:red;
            font-weight:bold;
        }
        .has-error {
            color: red;
        }
    </style>
    <div class="row" style="margin-top: 0 !important; margin-bottom: 0.75em;">
        <div class="col"><apex:inputHidden id="bidParentSObjectInput" value="{!bidParentSObject}"/></div>
        <apex:outputPanel id="contractForms" layout="block" styleClass="col-md-8">
            <apex:outputPanel layout="block" rendered="{!bidParentSObject = 'Ground' || bidParentSObject = 'Freight'}" styleClass="row">
                <div class="col">
                    <apex:repeat value="{!formList1}" var="formButton">
                        <apex:outputPanel layout="block" rendered="{!formButton.value != 'Send Signer'}" styleClass="row">
                            <div class="col-md-4" style="display: flex; align-items: center; justify-content: flex-end;"><span><b>{!formButton.draftCode}</b></span></div>
                            <div class="col-md-8">
                                <button class="btn btn-danger btn-sm" onclick="openFormJs('{!formButton.label}','{!formButton.value}','{!formButton.draftCode}');" type="button" style="width: 100%; color: white; font-weight: bold;">{!formButton.label}</button>
                            </div>
                        </apex:outputPanel>
                        <apex:outputPanel layout="block" rendered="{!formButton.value = 'Send Signer'}" styleClass="row">
                            <div class="col-md-4" style="display: flex; align-items: center; justify-content: flex-start;"></div>
                            <div class="col-md-8">
                                <button class="btn btn-danger btn-sm" onclick="congaSendSign('{!formBid.id}');" type="button" style="width: 100%; color: white; font-weight: bold;">{!formButton.label}</button>
                            </div>
                        </apex:outputPanel>
                    </apex:repeat>
                </div>
                <div class="col">
                    <apex:repeat value="{!formList2}" var="formButton">
                        <div class="row">
                            <div class="col-md-8">
                                <button class="btn btn-danger btn-sm" onclick="openFormJs('{!formButton.label}','{!formButton.value}','{!formButton.draftCode}');" type="button" style="width: 100%; color: white; font-weight: bold;">{!formButton.label}</button>
                            </div>
                            <div class="col-md-4" style="display: flex; align-items: center; justify-content: flex-start;"><span><b>{!formButton.draftCode}</b></span></div>
                        </div>
                    </apex:repeat>
                </div>
            </apex:outputPanel>
            <apex:outputPanel layout="block" rendered="{!bidParentSObject = 'Air'}" styleClass="row">
                <div class="col">
                    <div class="card">
                        <div class="card-header">
                            <h2>Send Reminder</h2>
                        </div>
                        <div class="card-body">
                            <apex:repeat value="{!formList1}" var="formButton">
                                <apex:outputPanel layout="block" rendered="{!formButton.value != 'Send Signer'}" styleClass="row">
                                    <div class="col-md-8">
                                        <button class="btn btn-danger btn-sm" onclick="openFormJs('{!formButton.label}','{!formButton.value}','{!formButton.draftCode}');" type="button" style="width: 100%; color: white; font-weight: bold;">{!formButton.label}</button>
                                    </div>
                                    <div class="col-md-4" style="display: flex; align-items: center; justify-content: flex-start;"><span><b>{!formButton.draftCode}</b></span></div>
                                </apex:outputPanel>
                                <apex:outputPanel layout="block" rendered="{!formButton.value = 'Send Signer'}" styleClass="row">
                                    <div class="col-md-8">
                                        <button class="btn btn-danger btn-sm" onclick="congaSendSign('{!formBid.id}');" type="button" style="width: 100%; color: white; font-weight: bold;">{!formButton.label}</button>
                                    </div>
                                    <div class="col-md-4" style="display: flex; align-items: center; justify-content: flex-start;"></div>
                                </apex:outputPanel>
                            </apex:repeat>
                        </div>
                    </div>
                </div>
                <div class="col">
                    <div class="card">
                        <div class="card-header">
                            <h2>Forms</h2>
                        </div>
                        <div class="card-body">
                            <apex:repeat value="{!formList2}" var="formButton">
                                <div class="row">
                                    <div class="col-md-8">
                                        <button class="btn btn-danger btn-sm" onclick="openFormJs('{!formButton.label}','{!formButton.value}','{!formButton.draftCode}');" type="button" style="width: 100%; color: white; font-weight: bold;">{!formButton.label}</button>
                                    </div>
                                    <div class="col-md-4" style="display: flex; align-items: center; justify-content: flex-start;"><span><b>{!formButton.draftCode}</b></span></div>
                                </div>
                            </apex:repeat>
                        </div>
                    </div>
                </div>
            </apex:outputPanel>
        </apex:outputPanel>
        <div class="col"></div>
    </div>
    <!-- Modal content-->
    <div class="modal fade" id="myGroundModalForm" role="dialog">
        <apex:outputPanel id="myGroundModalContent" layout="block" styleClass="modal-dialog modal-xl" style="height: 90%;">
            <apex:outputPanel id="bidAgreementModal" layout="block" rendered="{!isBidAgreementRendered}" styleClass="modal-content bidAgreementModal" style="max-height:98%;">
                <div class="modal-header">
                    <h4 class="modal-title">{!formLabel}</h4>
                    <button type="button" class="close" onclick="closeBidAgreementJs(false);">&times;</button>
                    <apex:inputHidden id="bidJournal_recordtype" value="{!journal_bidjournalRT}"/>
                    <apex:inputHidden id="bidAgreement_congaEmailFromId" value="{!bidAgreement_congaEmailFromId}"/>
                    <apex:inputHidden id="gcq_user" value="{!user.Housing_Preference__c}"/>
                </div>
                <div class="modal-body" style="font-size:12px;padding-top: 0px;">
                    <apex:outputPanel id="BidAgreementPanel">
                        <apex:outputPanel layout="block" rendered="{!bidParentSObject = 'Ground' || bidParentSObject = 'Freight'}">
                            <apex:outputPanel layout="block" rendered="{!formLabel = 'Rate Agreement' || formLabel = 'Transportation Contract'}" styleClass="row">
                                <div class="col-md-12">
                                    <div class="fieldset" style="margin-top: 0 !important;">
                                        <div class="row" style="margin-top: 0 !important;">
                                            <div class="col-md-6">
                                                Trip ID : <strong>{!If(bidParentSObject = 'Ground', formBid.GT__r.Name, formBid.Freight__r.Name)}</strong>&nbsp;&nbsp;&nbsp;Production ID : <strong>{!formBid.Production__r.Production_ID__c}</strong>
                                            </div>
                                            <div class="col-md-6 text-right">
                                                Bid ID : <strong>{!formBid.Name}</strong>&nbsp;&nbsp;&nbsp;Vendor ID: <strong>{!formBid.Vendor__r.Vendor_ID__c}</strong>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </apex:outputPanel>
                            <!--  Changes Added as per 175349270  (Added full Section)--> 
                            <apex:outputPanel layout="block" rendered="{!formLabel == 'Ground Transportation Procedures'}" styleClass="row">
                                <div class="col-md-12">
                                    <div class="fieldset" style="margin-top: 0 !important;">
                                        <div class="row" style="margin-top: 0 !important;">
                                            <div class="col-md-6">
                                                <div class="row" style="">
                                                    <div class="col-md-4" style="display: flex; align-items: center;">Production :</div>
                                                    <div class="col-md-8" style="display: flex; align-items: center;"><a href="/{!formBid.Production__c}" target="_blank">{!formBid.Production__r.Name}</a></div>
                                                </div>
                                                <div class="row" style="">
                                                    <div class="col-md-4" style="display: flex; align-items: center;">Vendor :</div>
                                                    <div class="col-md-8" style="display: flex; align-items: center;"><a href="/{!formBid.Vendor__c}" target="_blank">{!formBid.Vendor__r.Name}</a></div>
                                                </div>
                                            </div>
                                            <div class="col-md-6">
                                                <div class="row" style="">
                                                    <div class="col-md-4" style="display: flex; align-items: center;">Status :</div>
                                                    <div class="col-md-8" style="display: flex; align-items: center;"><b>{!formBid.Form_GT_GCIP__c}</b></div>
                                                </div>
                                                <div class="row">
                                                    <div class="col-md-4" style="display: flex; align-items: center;">GCIP Id:</div>
                                                    <div class="col-md-8" style="display: flex; align-items: center;"><b>{!formBid.Form_GT_GCIP__c}</b></div>
                                                </div>
                                            </div>
                                        </div>
                                        <apex:outputPanel id="formContactToPanel" layout="block">
                                            <div class="row">
                                                <div class="col-md-2" style="display: flex; align-items: center;">Attention :</div>
                                                <div class="col-md-4" style="display: flex; align-items: center;">
                                                    <apex:selectList size="1" id="form_attention" styleClass="form-control form-control-sm" value="{!form_attention}" onchange="changeAttentionForm();">
                                                        <apex:selectOptions value="{!form_attentionList}" />
                                                    </apex:selectList>

                                                </div>
                                                <div class="col-md-2" style="display: flex; align-items: center;">Fax :</div>
                                                <div class="col-md-4" style="display: flex; align-items: center;"><b>{!bidAgreementAttentionContact_Fax}</b></div>
                                            </div>
                                            <div class="row" style="">
                                                <div class="col-md-2" style="display: flex; align-items: center;">Title :</div>
                                                <div class="col-md-4" style="display: flex; align-items: center;"><b>{!bidAgreementAttentionContact_Title}</b></div>
                                                <div class="col-md-2" style="display: flex; align-items: center;">Email :</div>
                                                <div class="col-md-4" style="display: flex; align-items: center;"><a class="form-to-ctclient" href="mailto:{!bidAgreementAttentionContact_Email}">{!bidAgreementAttentionContact_Email}</a></div>
                                            </div>
                                            <div class="row">
                                                <div class="col-md-2" style="display: flex; align-items: center;">To :</div>
                                                <div class="col-md-4" style="display: flex; align-items: center;"><a id="form_to" class="form-to" href="mailto:{!bidAgreementAttentionContact.Email}">{!bidAgreementAttentionContact_Email}</a></div>
                                                <div class="col-md-6"></div>
                                            </div>
                                        </apex:outputPanel>
                                        <div class="row">
                                            <div class="col-md-2" style="align-items: center;">CC :</div>
                                            <div class="col-md-10" style="align-items: center;">
                                                <div class="all-cc-email-form"></div>
                                                <input type="text" id="form_cc" value="" class="form-control form-control-sm cc-email-form" />
                                            </div>
                                        </div>
                                        <div class="row">
                                            <div class="col-md-2" style="align-items: center;">BCC :</div>
                                            <div class="col-md-10" style="align-items: center;">
                                                <div class="all-bcc-email-form"></div>
                                                <input type="text" id="form_bcc" value="" class="form-control form-control-sm bcc-email-form" />
                                            </div>
                                        </div>

                                    </div>
                                </div>
                            </apex:outputPanel>
                            <!-- Changes Added as per 175349270  -->
                            <!-- <div class="row"> -->
                                <apex:outputPanel layout="block" rendered="{!formLabel != 'Ground Transportation Procedures'}" styleClass="row">
                                    <div class="col-md-12">
                                        <div class="fieldset" style="margin-top: 0 !important;">
                                            <div class="form-group row">
                                                <apex:outputLabel value="To :" for="" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                                <div class="col-sm-10">
                                                    <apex:outputPanel id="bidAgreementToPanel">
                                                        <div id="bidAgreement_primarycontactemail" class="bidAgreement-to">
                                                            <apex:inputField value="{!bidAgreementPrimaryContact['Email']}" styleClass="form-control form-control-sm" rendered="{!formLabel = 'Rate Agreement' || formLabel = 'Transportation Contract' || formLabel = 'Contract To Client' || formLabel = 'Final Contract' || formLabel = 'Email Confirmation'}" required="false" html-disabled="true"/>
                                                            <apex:inputField value="{!bidAgreementAttentionContact.Email}" styleClass="form-control form-control-sm" rendered="{!formLabel != 'Rate Agreement' && formLabel != 'Transportation Contract' && formLabel != 'Contract To Client' && formLabel != 'Final Contract' && formLabel != 'Email Confirmation'}" required="false" html-disabled="true"/>
                                                            <apex:inputHidden id="bidAgreement_to_name" value="{!bidAgreementPrimaryContact['Name']}" rendered="{!formLabel = 'Email Confirmation'}"/>
                                                        </div>
                                                    </apex:outputPanel>
                                                </div>
                                            </div>
                                            <div class="form-group row">
                                                <apex:outputLabel value="CC :" for="bidAgreement_cc" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                                <div class="col-sm-10">
                                                    <div class="all-cc-email-bidAgreement"></div>
                                                    <input type="text" id="bidAgreement_cc" value="{!draft.CC__c}" class="form-control form-control-sm cc-email-bidAgreement"/>
                                                </div>
                                            </div>
                                            <div class="form-group row">
                                                <apex:outputLabel value="BCC :" for="bidAgreement_bcc" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                                <div class="col-sm-10">
                                                    <div class="all-bcc-email-bidAgreement"></div>
                                                    <input type="text" id="bidAgreement_bcc" value="{!draft.BCC__c}" class="form-control form-control-sm bcc-email-bidAgreement"/>
                                                </div>
                                            </div>
                                            <div class="form-group row">
                                                <apex:outputLabel value="Subject :" for="bidAgreement_subject" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                                <div class="col-sm-10">
                                                    <apex:inputField id="bidAgreement_subject" value="{!draft.Subject__c}" styleClass="form-control form-control-sm subject-bidAgreement" /> 
                                                </div>
                                            </div>
                                            <div class="form-group row">
                                                <apex:outputLabel value="Attached :" for="bidAgreement_attachs" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                                <div class="col-sm-4">
                                                    <apex:selectList size="4" id="bidAgreement_attachs" styleClass="form-control" style="width:100%;"/>
                                                </div>
                                                <div class="col-sm-6">
                                                    <button type="button" class="btn btn-secondary btn-custom" onclick="removeAttachDocs('bidAgreement_attachs');" style="float: left;margin-right: 5px;">Remove</button>
                                                    <div class="upload-btn-wrapper" style="display: block;float: left;margin-right: 5px;">
                                                        <button class="btn btn-secondary btn-custom" onclick="javascript:void(0);">Attach</button>
                                                        <input type="file" id="fileBidAgreement" onchange="remoteLocationPostLast(event,'Rate Agreement','bidAgreement_attachs', '{!formBid.Id}');" />
                                                    </div>
                                                    <button type="button" class="btn btn-secondary btn-custom" onclick="openAttachDocs('bid','{!formBid.Id}','bidAgreementModal');">Attach Contracting Docs</button>
                                                    <apex:inputHidden value="{!body}" id="output"/>
                                                    <input type="hidden" id="attachment_new_charge"/>
                                                    <apex:outputPanel id="newAttachmentPanel">
                                                        <input type="hidden" id="attachment_new_id" value="{!newattachment_id}" />
                                                        <input type="hidden" id="attachment_new_name" value="{!newattachment_name}" />
                                                    </apex:outputPanel>
                                                    <button type="button" class="btn btn-secondary btn-custom" onclick="openAttachGcqJs();" style="{!If(formValue = 'Form_Email_Confirmation__c', '', 'display:none;')}">Attach {!If(bidParentSObject = 'Ground', 'G', 'F')}CQ</button>
                                                </div>
                                            </div>
                                            <apex:outputPanel layout="block" styleClass="form-group row">
                                                <apex:outputLabel value="Salutation:" for="bidAgreement_salutation" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                                <div class="col-sm-10">
                                                    <apex:inputField id="bidAgreement_salutation" value="{!draft.Salutation__c}" styleClass="form-control form-control-sm"/>
                                                </div>
                                            </apex:outputPanel>
                                            <div class="form-group row">
                                                <apex:outputLabel value="Message:" for="bidAgreement_message" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                                <div class="col-sm-10">
                                                    <apex:inputTextarea id="bidAgreement_message" value="{!draft.Body__c}" rows="5" styleClass="form-control form-control-sm" />
                                                    <script>
                                                    CKEDITOR.replace('{!$Component.bidAgreement_message}', {
                                                        language: 'en',
                                                        extraAllowedContent: 'th{color,background,background-color}'
                                                    });
                                                    </script>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </apex:outputPanel>
                                <!-- Changes Added as per 175349270  -->
                                <apex:outputPanel layout="block" id="op" rendered="{!formLabel = 'Ground Transportation Procedures'}" styleClass="row">
                                <div class="container">
                                    <div class="row">
                                        <div class="col-sm" style="text-align: center;">
                                        <label for="form_date"><b>GCIP Created Date</b><br/>(mm/dd/yy)</label>
                                        <input type="hidden" id="old_form_date_gcip" value="{!draft.Date__c}" />
                                        <div id="hidden_gcid_date" style="display: none;">
                                            <apex:outputText id="old_form_date_gcip_date" value="{0,date,MM'-'dd'-'yyyy}">
                                                <apex:param value="{!draft.Date__c}" /> 
                                            </apex:outputText>
                                        </div>
                                        
                                        <!-- <apex:inputText value="{!draft.Date__c}" style="width: 100%;" styleClass="form-control form-control-sm date-form"/> -->
                                        <input type="text" id="new_form_date_gcip" value="{!form_date}" class="form-control form-control-sm date-form" style="text-align: center;" onchange="validateMMDDYY('form_date_gcip');" /> 
                                        </div>
                                        <div class="col-sm">
                                        <br/>
                                        <label for="form_date"><b>Arrival Date</b></label>
                                        <input type="text" id="form_date_gcip_arrival" value="{!form_date_gcip_arrival}" class="form-control form-control-sm date-form" />
                                        </div>
                                        <div class="col-sm">
                                        <br/>
                                        <label for="form_date"><b>Departure Date</b></label>
                                        <input type="text" id="form_date_gcip_departure" value="{!form_date_gcip_departure}" class="form-control form-control-sm date-form" />
                                        
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-12">
                                            <label for="form_subject"><b>Subject</b></label>
                                            <input type="text" id="form_subject" value="{!draft.Subject__c}" class="form-control form-control-sm subject-form" />
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-8">
                                            <label for="form_subject" style=""><b>Salutation</b></label>
                                            <!-- Fix By Clay 28 Dec, 2020
                                            <input type="text" value="{!bidAgreementAttentionContact_Salutation}" class="form-control form-control-sm subject-form" />-->
                                            <input type="text" id="form_salutation" value="{!bidAgreementAttentionContact_Salutation}" class="form-control form-control-sm subject-form" />
                                        </div>
                                        
                                    </div>
                                    <div class="row">
                                        <div class="col-md-8">
                                            <b>Attached:</b><br/>
                                            <apex:selectList size="4" id="form_attachs" style="width:100%;" />
                                        </div>
                                        <div class="col-md-4" style="margin-top:30px;">
                                            <button type="button" class="btn btn-secondary btn-custom" onclick="removeAttachDocs('form_attachs');" style="float: left;margin-right: 5px;">Remove</button>
                                            <div class="upload-btn-wrapper" style="display: block;float: left;margin-right: 5px;">
                                            <button class="btn btn-secondary btn-custom" onclick="javascript:void(0);">Attach</button>
                                            <input type="file" id="fileBidForm" onchange="remoteLocationPostLast(event,'form','form_attachs');" />
                                            </div>
                                            <button type="button" class="btn btn-secondary btn-custom" onclick="">Attach Contracting Docs</button>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-12">
                                            <label><b>Message Body</b></label>
                                            <!-- <textarea id="form_body" rows="5" class="form-control form-control-sm">{!draft.Body__c}
                                            </textarea>
                                            <script>
                                            CKEDITOR.replace('{!$Component.form_body}', {
                                                language: 'en',
                                                extraAllowedContent: 'th{color,background,background-color}'
                                            });
                                            </script> -->
                                            <apex:inputTextarea id="form_body" value="{!draft.Body__c}" rows="5" styleClass="form-control form-control-sm data description" />
                                            <script>
                                            CKEDITOR.replace('{!$Component.form_body}', {
                                                language: 'en',
                                                extraAllowedContent: 'th{color,background,background-color}'
                                            });
                                            </script>
                                        </div>
                                    </div>

                                    <div class="row">
                                        <div class="col-md-12">
                                            <div class="fieldset" style="margin-top: 0 !important;">
                                                <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="newFormGCIPTask();"><i class="fas fa-plus"></i> Add new item</button>
                                                <table class="table table-sm" style="margin-top:5px;margin-bottom:0;">
                                                    <thead class="thead-light">
                                                        <tr>
                                                            <th width="10%">Priority</th>
                                                            <th width="15%">Task Name</th>
                                                            <th>Attribute</th>
                                                            <th width="15%"></th>
                                                        </tr>
                                                    </thead>
                                                    <tbody>
                                                        <tr class="new-form-gcip-task" style="display:none;">
                                                            <td><apex:inputText value="{!form_gcip_new_task.Priority__c}" styleClass="form-control form-control-sm newdata" onchange="this.value = this.value.replace(/(\..*)\./g, '$1').replace(/[^0-9]/g, '');" /></td>
                                                            <td><apex:inputText value="{!form_gcip_new_task.Subject}" styleClass="form-control form-control-sm newdata" /></td>
                                                            <td><apex:inputText value="{!form_gcip_new_task.Description}" styleClass="form-control form-control-sm newdata" /></td>
                                                            <td class="text-center">
                                                                <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="saveFormGCIPTask();"><i class="fas fa-check"></i> Save</button>
                                                                <button type="button" class="btn btn-secondary btn-sm btn-custom" onclick="cancelFormGCIPTask();"><i class="fas fa-ban"></i> Cancel</button>
                                                            </td>
                                                        </tr>
                                                    </tbody>
                                                </table>
                                                <apex:outputPanel id="formGCIPPanel">
                                                    <table class="table table-sm">
                                                            <!-- <tr gcipId="{!detail.Id}"> -->
                                                            <!-- <tr>
                                                                <td width="10%">
                                                                    <input type="hidden" value="" class="gcipId" />
                                                                    <span class="show-data">10</span>
                                                                    <input type="number" oninput="this.value = this.value.replace(/(\..*)\./g, '$1').replace(/[^0-9]/g, '');" class="form-control form-control-sm data priority" value="" style="display:none;" />
                                                                </td>
                                                                <td width="15%">
                                                                    <span class="show-data">Deliver GCIP</span>
                                                                    <input type="text" class="form-control form-control-sm data subject" value="" style="display:none;" />
                                                                </td>
                                                                <td>
                                                                    <span class="show-data">Deliver a copy of this document to the Front Office Manager.Front Office Manager:____________________ Person Checking Group In:____________________</span>
                                                                    <input type="text" class="form-control form-control-sm data description" value="" style="display:none;" />
                                                                </td>
                                                                <td class="text-center" width="15%">
                                                                    <button type="button" class="btn btn-secondary btn-sm btn-custom btn-save" onclick="saveEditFormGCIPTask(this);" style="display:none;"><i class="fas fa-check"></i> Save</button>
                                                                    <button type="button" class="btn btn-secondary btn-sm btn-custom btn-edit" onclick="edit(this);"><i class="fas fa-pencil-alt"></i> Edit</button>
                                                                    <button type="button" class="btn btn-secondary btn-sm btn-custom btn-cancel" onclick="cancel(this);" style="display:none;"><i class="fas fa-ban"></i> Cancel</button>
                                                                    <button type="button" class="btn btn-secondary btn-sm btn-custom btn-delete" onclick="deleteFormGCIPTask('');"><i class="fas fa-times"></i> Delete</button>
                                                                </td>
                                                            </tr> -->
                                                            <tbody>
                                                                <apex:repeat value="{!form_gcip_details_wrapper}" var="detail" id="rep">
                                                                    <tr gcipId="{!detail.Id}" id="{!detail.Id}">
                                                                        <td width="10%">
                                                                            <input type="hidden" value="{!detail.Id}" class="gcipId" />
                                                                            <span class="show-data">{!detail.Priority}</span>
                                                                            <input type="number" oninput="this.value = this.value.replace(/(\..*)\./g, '$1').replace(/[^0-9]/g, '');" class="form-control form-control-sm data priority" value="{!detail.Priority}" style="display:none;" />
                                                                        </td>
                                                                        <td width="15%">
                                                                            <span class="show-data">{!detail.Subject}</span>
                                                                            <input type="text" class="form-control form-control-sm data subject" value="{!detail.Subject}" style="display:none;" />
                                                                        </td>
                                                                        <td>
                                                                            <span class="show-data">{!detail.DescriptionOutput}</span>
                                                                            <!-- <input type="text" class="form-control form-control-sm data description" value="{!detail.Description}" style="display:none;" /> -->
                                                                            <!--Fix By Clay 28 Dec, 2020-->
                                                                            <span class="show-when-edit" style="display:none;">
                                                                            <apex:inputTextarea id="form_body_new" value="{!detail.Description}" rows="5" styleClass="form-control form-control-sm data description" style="margin-top: -110px; display:none;" />
                                                                            <script>
                                                                            CKEDITOR.replace('{!$Component.form_body_new}', {
                                                                                language: 'en',
                                                                                extraAllowedContent: 'th{color,background,background-color}'
                                                                            });
                                                                            </script>
                                                                            <!--Fix By Clay 28 Dec, 2020-->    
                                                                            </span>
                                                                        </td>
                                                                        <td class="text-center" width="15%">
                                                                            <button type="button" class="btn btn-secondary btn-sm btn-custom btn-save" onclick="saveEditFormGCIPTask(this);" style="display:none;"><i class="fas fa-check"></i> Save</button>
                                                                            <button type="button" class="btn btn-secondary btn-sm btn-custom btn-edit" onclick="edit(this);"><i class="fas fa-pencil-alt"></i> Edit</button>
                                                                            <button type="button" class="btn btn-secondary btn-sm btn-custom btn-cancel" onclick="cancel(this);" style="display:none;"><i class="fas fa-ban"></i> Cancel</button>
                                                                            <button type="button" class="btn btn-secondary btn-sm btn-custom btn-delete" onclick="deleteFormGCIPTask('{!detail.Id}');"><i class="fas fa-times"></i> Delete</button>
                                                                        </td>
                                                                    </tr>
                                                                </apex:repeat>
                                                            </tbody>
                                                    </table>
                                                </apex:outputPanel>
                                            </div>
                                        </div>
                                    </div>
                                    <!-- Changes as per 175349270 -->
                                    <!-- <div class="row">
                                        <div class="col-md-12">
                                            <label><b>Guarantee, Billing And Payment Information:</b></label>
                                            <textarea id="form_gaurantee" rows="5" value="" class="form-control form-control-sm subject-form"></textarea>
                                        </div>
                                    </div> -->
                                    <div class="row">
                                        <div class="col-md-12">
                                            <label><b>Closing:</b></label>
                                            <textarea id="form_gaurantee" rows="5" class="form-control form-control-sm subject-form">
Please reply to this email to confirm all details above will be met at time of the trip. If you have any further questions, feel free to contact us.

With kind regards,
{!primaryCoordinatorName}
{!dashboard} Coordinator
                                            </textarea>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-12">
                                            <div class="fieldset" style="margin-top: 0 !important; padding:30px;">
                                                <div class="row" style="margin-top: 0 !important;">
                                                    <div class="col-md-3">
                                                        <div class="row" style="">
                                                            <div class="col-md-5" style="display: flex; align-items: center;">Created By :</div>
                                                            <div class="col-md-7" style="display: flex; align-items: center;"><b>{!formBid.CreatedBy.Name}</b></div>
                                                        </div>
                                                        <div class="row" style="">
                                                            <div class="col-md-5" style="display: flex; align-items: center;">Modified By :</div>
                                                            <div class="col-md-7" style="display: flex; align-items: center;"><b>{!formBid.LastModifiedBy.Name}</b></div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="row" style="">
                                                            <div class="col-md-5" style="display: flex; align-items: center;">Created On :</div>
                                                            <div class="col-md-7" style="display: flex; align-items: center;">
                                                            <b>
                                                                <apex:outputText value="{0,date,MM'-'dd'-'yyyy}">
                                                                    <apex:param value="{!formBid.CreatedDate}" /> 
                                                                </apex:outputText>
                                                            </b>
                                                        </div>
                                                        </div>
                                                        <div class="row">
                                                            <div class="col-md-5" style="display: flex; align-items: center;">Modified On :</div>
                                                            <div class="col-md-7" style="display: flex; align-items: center;">
                                                                <b>
                                                                    <apex:outputText value="{0,date,MM'-'dd'-'yyyy}">
                                                                        <apex:param value="{!formBid.LastModifiedDate}" /> 
                                                                    </apex:outputText>
                                                                </b>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="row" style="">
                                                            <div class="col-md-4" style="display: flex; align-items: center;">Sent By :</div>
                                                            <div class="col-md-8" style="display: flex; align-items: center;"><b>{!formBid.Form_Create_GCIP_Last_Send_Date__c}</b></div>
                                                        </div>
                                                        <div class="row">
                                                            <div class="col-md-4" style="display: flex; align-items: center;">Sent Via :</div>
                                                            <div class="col-md-8" style="display: flex; align-items: center;"><b></b></div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="row" style="">
                                                            <div class="col-md-4" style="display: flex; align-items: center;">Sent On :</div>
                                                            <div class="col-md-8" style="display: flex; align-items: center;"><b>{!formBid.Form_Create_GCIP_Last_Send_Date__c}</b></div>
                                                        </div>
                                                        <div class="row">
                                                            <div class="col-md-4" style="display: flex; align-items: center;"></div>
                                                            <div class="col-md-8" style="display: flex; align-items: center;"><b></b></div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                </apex:outputPanel>
                            <!-- </div> -->
                            <!-- End of Changes Added as per 175349270  -->

                            <!-- Changes Added as per 175349270 Added && formLabel != 'Ground Transportation Procedures' Condition -->
                            <apex:outputPanel layout="block" rendered="{!formLabel != 'Rate Agreement' && formLabel != 'Transportation Contract' && formLabel != 'Ground Transportation Procedures'}" styleClass="row">
                                <div class="col-md-12">
                                    <div class="fieldset" style="margin-top: 0 !important;">
                                        <div class="row" style="margin-top: 0 !important;">
                                            <div class="col-md-3">
                                                <div class="row">
                                                    <div class="{!if(formLabel = 'Email Confirmation', 'col-md-5', 'col-md-12')}">
                                                        <apex:outputLabel value="Vendor :" for="bidAgreementAttentionVendorLink" rendered="{!formLabel != 'Contract To Client' && formLabel != 'Email Confirmation'}"/>
                                                        <apex:outputLabel value="Production :" for="bidAgreementProductionLink" rendered="{!formLabel = 'Contract To Client' || formLabel = 'Email Confirmation'}"/>
                                                    </div>
                                                    <div class="{!if(formLabel = 'Email Confirmation', 'col-md-7', 'col-md-12')}">
                                                        <apex:outputLink id="bidAgreementAttentionVendorLink" value="/{!formBid.Vendor__c}" target="_blank" rendered="{!formLabel != 'Contract To Client' && formLabel != 'Email Confirmation'}">{!formBid.Vendor__r.Name}</apex:outputLink>
                                                        <apex:outputLink id="bidAgreementProductionLink" value="/{!formBid.Production__c}" target="_blank" rendered="{!formLabel = 'Contract To Client' || formLabel = 'Email Confirmation'}">{!formBid.Production__r.Name}</apex:outputLink>
                                                    </div>
                                                </div>
                                            </div>
                                            <apex:outputPanel layout="block" rendered="{!formValue != 'Form_Email_Confirmation__c'}" styleClass="col-md-9">
                                                <div class="row">
                                                    <apex:outputPanel layout="block" rendered="{!formValue = 'Form_Contract_to_Client__c' || formValue = 'Form_Final_Contract__c'}" styleClass="col-md-4">
                                                        <apex:outputLabel value="Attention: " for="bidAgreementAttentionProductionAssociationContactsSelect" style="font-weight:bold;"/>
                                                        <apex:selectList size="1" id="bidAgreementAttentionProductionAssociationContactsSelect" styleClass="form-control form-control-sm" value="{!draft.Production_Assoc_Contact_Id__c}">
                                                            <apex:selectOptions value="{!BidAgreementProductionAssociationContacts}" />
                                                            <apex:actionSupport event="onchange" action="{!changeBidAgreementProductionAssociationContact}" status="loading" reRender="bidAgreementToPanel,bidAgreement_salutation"/>
                                                        </apex:selectList>
                                                    </apex:outputPanel>
                                                    <apex:outputPanel layout="block" rendered="{!formValue = 'Form_Trip_Details_Update__c' || formValue = 'Form_Counter_Needed__c' || formValue = 'Form_Credit_Card_Change__c' || formValue = 'Form_Cancellation_Letter__c'}" styleClass="col-md-4">
                                                        <apex:outputLabel value="Attention: " for="bidAgreementAttentionContactSelect" style="font-weight:bold;"/>
                                                        <apex:selectList size="1" id="bidAgreementAttentionContactSelect" styleClass="form-control form-control-sm" value="{!draft.Attention__c}">
                                                            <apex:selectOptions value="{!contactsBidsByVendor}"/>
                                                            <apex:actionSupport event="onchange" action="{!changeBidAgreementAttentionContact}" status="loading" reRender="bidAgreementAttentionContactTitleLink,bidAgreementAttentionContactEmailLink,bidAgreementToPanel,bidAgreement_salutation"/>
                                                        </apex:selectList>
                                                    </apex:outputPanel>
                                                    <div class="col-md-4">
                                                        <apex:outputPanel layout="block" rendered="{!formLabel = 'Trip Details Update'}" styleClass="row">
                                                            <div class="col-md-12">
                                                                <apex:outputLabel value="Title :" for="bidAgreementAttentionContactTitleLink"/>
                                                            </div>
                                                            <div class="col-md-12">
                                                                <apex:outputLink id="bidAgreementAttentionContactTitleLink" value="/{!bidAgreementAttentionContact.id}" target="_blank">{!bidAgreementAttentionContact.Title}</apex:outputLink>
                                                            </div>
                                                        </apex:outputPanel>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <apex:outputPanel layout="block" rendered="{!formLabel = 'Trip Details Update'}" styleClass="row">
                                                            <div class="col-md-12">
                                                                <apex:outputLabel value="Email :" for="bidAgreementAttentionContactEmailLink"/>
                                                            </div>
                                                            <div class="col-md-12">
                                                                <apex:outputLink id="bidAgreementAttentionContactEmailLink" value="mailto:{!bidAgreementAttentionContact.Email}" target="_blank">{!bidAgreementAttentionContact.Email}</apex:outputLink>
                                                            </div>
                                                        </apex:outputPanel>
                                                    </div>
                                                </div>
                                            </apex:outputPanel>
                                            <apex:outputPanel layout="block" rendered="{!formValue = 'Form_Email_Confirmation__c'}" styleClass="col-md-9">
                                                <div class="row">
                                                    <input type="hidden" id="emailconfirmation_type" value="{!draft.Production_Assoc_Type__c}" />
                                                    <div class="col-md-6" style="text-align:right;">
                                                        <span class="slds-radio">
                                                            <input type="radio" id="searchByProductionContacts" value="production_contacts" name="options_emailc" onclick="changeContactData(this);" />
                                                            <label class="slds-radio__label" for="searchByProductionContacts">
                                                                <span class="slds-radio_faux"></span>
                                                                <span class="slds-form-element__label">Production Contacts</span>
                                                            </label>
                                                        </span>
                                                        <span class="slds-radio">
                                                            <input type="radio" id="searchByGTCoordinators" value="coordinators" name="options_emailc" onclick="changeContactData(this);" />
                                                            <label class="slds-radio__label" for="searchByGTCoordinators">
                                                                <span class="slds-radio_faux"></span>
                                                                <span class="slds-form-element__label">GT Coordinators</span>
                                                            </label>
                                                        </span>
                                                    </div>
                                                    <div class="col-md-6">
                                                        <apex:outputPanel id="emailConfirmationDataContactPanel">
                                                            <apex:selectList id="emailconfirmation_select" size="1" value="{!draft.Production_Assoc_Contact_Id__c}" styleClass="form-control form-control-sm" style="width:350px;" onchange="changeContactDataSelected();">
                                                                <apex:selectOptions value="{!dataContactPL}" />
                                                            </apex:selectList>
                                                        </apex:outputPanel>
                                                    </div>
                                                </div>
                                            </apex:outputPanel>
                                        </div>
                                    </div>
                                </div>
                            </apex:outputPanel>
                            <apex:outputPanel layout="block" rendered="{!formLabel = 'Rate Agreement' || formLabel = 'Transportation Contract'}" styleClass="row">
                                <div class="col-md-6">
                                    <div class="fieldset" style="height: 200px;margin-top: 0 !important;">
                                        <div class="row" style="margin-top: 0 !important;">
                                            <div class="col-md-3">
                                                Vendor :
                                            </div>
                                            <div class="col-md-9">
                                                <a href="/{!formBid.Vendor__c}" target="_blank">{!formBid.Vendor__r.Name}</a>
                                            </div>
                                        </div>
                                        <div class="row">
                                            <div class="col-md-3">
                                                Address : 
                                            </div>
                                            <div class="col-md-9">
                                                <span style="font-weight:bold;"><apex:outputText value="{!SUBSTITUTE(formBid.Vendor_Address__c,'<br>',', ')}" escape="true" /></span>
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
                                                    <a href="{!bidAgreementPrimaryContact['Phone']}">{!bidAgreementPrimaryContact['Phone']}</a>
                                                </div>
                                            </div>
                                            <div class="row">
                                                <div class="col-md-3">
                                                    Email : 
                                                </div>
                                                <div class="col-md-9">
                                                    <a href="mailto:{!bidAgreementPrimaryContact['Email']}">{!bidAgreementPrimaryContact['Email']}</a>
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
                                                <input type="text" value="{!formBid.Production__r.Name}" class="form-control form-control-sm" />
                                            </div>
                                        </div>
                                        <div class="row">
                                            <div class="col-md-3">
                                                Company : 
                                            </div>
                                            <div class="col-md-9">
                                                {!formBid.Production__r.Account.Name}
                                            </div>
                                        </div>
                                        <div class="row">
                                            <div class="col-md-3">
                                                Address : 
                                            </div>
                                            <div class="col-md-9">
                                                <span style="font-weight:bold;">
                                                    <apex:outputText value="{!SUBSTITUTE(formBid.Production__r.Account.Physical_Address__c,'<br>',', ')}" escape="true" />
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
                            <!-- <div class="row">
                                <div class="col-md-12">
                                    <div class="fieldset" style="margin-top: 0 !important;">
                                        <div class="form-group row">
                                            <apex:outputLabel value="To :" for="" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                            <div class="col-sm-10">
                                                <apex:outputPanel id="airbidAgreementToPanel">
                                                    <div id="bidAgreement_primarycontactemail" class="bidAgreement-to">
                                                        <apex:inputField value="{!bidAgreementPrimaryContact['Email']}" styleClass="form-control form-control-sm" rendered="{!formLabel = 'Rate Agreement' || formLabel = 'Transportation Contract' || formLabel = 'Contract To Client' || formLabel = 'Final Contract' || formLabel = 'Email Confirmation'}" required="false" html-disabled="true"/>
                                                        <apex:inputField value="{!bidAgreementAttentionContact.Email}" styleClass="form-control form-control-sm" rendered="{!formLabel != 'Rate Agreement' && formLabel != 'Transportation Contract' && formLabel != 'Contract To Client' && formLabel != 'Final Contract' && formLabel != 'Email Confirmation'}" required="false" html-disabled="true"/>
                                                        <apex:inputHidden id="bidAgreement_to_name" value="{!bidAgreementPrimaryContact['Name']}" rendered="{!formLabel = 'Email Confirmation'}"/>
                                                    </div>
                                                </apex:outputPanel>
                                            </div>
                                        </div>
                                        <div class="form-group row">
                                            <apex:outputLabel value="CC :" for="bidAgreement_cc" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                            <div class="col-sm-10">
                                                <div class="all-cc-email-bidAgreement"></div>
                                                <input type="text" id="bidAgreement_cc" value="{!draft.CC__c}" class="form-control form-control-sm cc-email-bidAgreement"/>
                                            </div>
                                        </div>
                                        <div class="form-group row">
                                            <apex:outputLabel value="BCC :" for="bidAgreement_bcc" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                            <div class="col-sm-10">
                                                <div class="all-bcc-email-bidAgreement"></div>
                                                <input type="text" id="bidAgreement_bcc" value="{!draft.BCC__c}" class="form-control form-control-sm bcc-email-bidAgreement"/>
                                            </div>
                                        </div>
                                        <div class="form-group row">
                                            <apex:outputLabel value="Subject :" for="bidAgreement_subject" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                            <div class="col-sm-10">
                                                <apex:inputField id="bidAgreement_subject" value="{!draft.Subject__c}" styleClass="form-control form-control-sm subject-bidAgreement" /> 
                                            </div>
                                        </div>
                                        <div class="form-group row">
                                            <apex:outputLabel value="Attached :" for="bidAgreement_attachs" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                            <div class="col-sm-4">
                                                <apex:selectList size="4" id="bidAgreement_attachs" styleClass="form-control" style="width:100%;"/>
                                            </div>
                                            <div class="col-sm-6">
                                                <button type="button" class="btn btn-secondary btn-custom" onclick="removeAttachDocs('bidAgreement_attachs');" style="float: left;margin-right: 5px;">Remove</button>
                                                <div class="upload-btn-wrapper" style="display: block;float: left;margin-right: 5px;">
                                                    <button class="btn btn-secondary btn-custom" onclick="javascript:void(0);">Attach</button>
                                                    <input type="file" id="fileBidAgreement" onchange="remoteLocationPostLast(event,'Rate Agreement','bidAgreement_attachs', '{!formBid.Id}');" />
                                                </div>
                                                <button type="button" class="btn btn-secondary btn-custom" onclick="openAttachDocs('bid','{!formBid.Id}','bidAgreementModal');">Attach Contracting Docs</button>
                                                <apex:inputHidden value="{!body}" id="output"/>
                                                <input type="hidden" id="attachment_new_charge"/>
                                                <apex:outputPanel id="newAttachmentPanel">
                                                    <input type="hidden" id="attachment_new_id" value="{!newattachment_id}" />
                                                    <input type="hidden" id="attachment_new_name" value="{!newattachment_name}" />
                                                </apex:outputPanel>
                                                <button type="button" class="btn btn-secondary btn-custom" onclick="openAttachGcqJs();" style="{!If(formValue = 'Form_Email_Confirmation__c', '', 'display:none;')}">Attach {!If(bidParentSObject = 'Ground', 'G', 'F')}CQ</button>
                                            </div>
                                        </div>
                                        <apex:outputPanel layout="block" styleClass="form-group row">
                                            <apex:outputLabel value="Salutation:" for="bidAgreement_salutation" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                            <div class="col-sm-10">
                                                <apex:inputField id="bidAgreement_salutation" value="{!draft.Salutation__c}" styleClass="form-control form-control-sm"/>
                                            </div>
                                        </apex:outputPanel>
                                        <div class="form-group row">
                                            <apex:outputLabel value="Message:" for="bidAgreement_message" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                            <div class="col-sm-10">
                                                <apex:inputTextarea id="bidAgreement_message" value="{!draft.Body__c}" rows="5" styleClass="form-control form-control-sm" />
                                                <script>
                                                CKEDITOR.replace('{!$Component.bidAgreement_message}', {
                                                    language: 'en',
                                                    extraAllowedContent: 'th{color,background,background-color}'
                                                });
                                                </script>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div> -->
                            <apex:outputPanel layout="block" rendered="{!formLabel = 'Rate Agreement' || formLabel = 'Transportation Contract' || formLabel = 'Trip Details Update'}" styleClass="row">
                                <div class="col-md-12">
                                    <h2>
                                        <strong>Trip Details</strong>
                                    </h2>
                                </div>
                                <apex:repeat value="{!bidAgreementSubTrips}" var="bidSubTrip">
                                    <div class="col-md-12">
                                        <div class="accordion" id="accordionFive">
                                            <div class="card">
                                                <div class="card-header" id="headingFive">
                                                    <h2 class="mb-0">
                                                        Trip {!bidSubTrip['Trip_Order__c']}
                                                    </h2>
                                                </div>
                                                <div id="collapseFive" class="collapse show" aria-labelledby="headingFive" data-parent="#accordionFive">
                                                    <div class="card-body card-body-trip card-body-{!bidSubTrip['Trip_Order__c']}" style="min-height: 235px;">
                                                        <div class="row" style="margin-top:0 !important;">
                                                            <div class="col-md-2">
                                                                <label style="font-weight:bold;">Trip Type</label><br/>
                                                                <apex:outputField value="{!bidSubTrip['Sub_Trip_Type__c']}" styleClass="form-control form-control-sm"  />
                                                            </div>
                                                            <div class="col-md-4">
                                                                <label style="font-weight:bold;">Description</label><br/>
                                                                 <apex:outputField value="{!bidSubTrip['Description__c']}" styleClass="form-control form-control-sm"  />
                                                            </div>
                                                            <div class="col-md-6">
                                                            </div>
                                                        </div>
                                                        <div class="row">
                                                            <div class="col-md-12">
                                                                <span style="font-weight:bold;">{!If(bidParentSObject = 'Ground', 'Travel ', 'Equipment ')}Information</span>
                                                            </div>
                                                        </div>
                                                        <div class="row">
                                                            <div class="col-md-12">
                                                                <apex:outputPanel id="travelsByTripPanel">
                                                                    <table class="table table-sm" style="margin-top:5px;margin-bottom:0;">
                                                                        <thead class="thead-light" style="background-color:rgba(0,0,0,.03);">
                                                                            <tr>
                                                                                <th width="10%">{!If(bidParentSObject = 'Ground', 'Vehicle', 'Equipment')}</th>
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
                                                                            <apex:repeat value="{!bidSubTrip[If(bidParentSObject = 'Ground', 'GTTravels__r', 'FreightEquipments__r')]}" var="bidTravel">
                                                                                <tr class="new-travel">
                                                                                    <td>
                                                                                        <apex:outputField value="{!bidTravel[If(bidParentSObject = 'Ground', 'Vehicle_Ref__c', 'Equipment__c')]}" styleClass="form-control form-control-sm"/>
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:outputField value="{!bidTravel['Start_Date__c']}" styleClass="form-control form-control-sm"/>
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:outputField value="{!bidTravel['Start_Date_Time__c']}" styleClass="form-control form-control-sm"/>
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:outputField value="{!bidTravel['End_Date__c']}" styleClass="form-control form-control-sm"/>
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:outputField value="{!bidTravel['End_Date_Time__c']}" styleClass="form-control form-control-sm"/>
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:outputField value="{!bidTravel['Travel_Type__c']}" styleClass="form-control form-control-sm"/>
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:outputField value="{!bidTravel['Group_Type__c']}" styleClass="form-control form-control-sm"/>
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:outputField value="{!bidTravel['Location_Type__c']}" styleClass="form-control form-control-sm"/>
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:outputField value="{!bidTravel['Location_Details__c']}" styleClass="form-control form-control-sm"/>
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:outputField value="{!bidTravel['Location_Drop_Off_Type__c']}" styleClass="form-control form-control-sm"/>
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:outputField value="{!bidTravel['Location_Details_Drop_Off__c']}" styleClass="form-control form-control-sm"/>
                                                                                    </td>
                                                                                    <td>
                                                                                        <apex:outputField value="{!bidTravel['Airline_Info_Special_Notes__c']}" styleClass="form-control form-control-sm"/>
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
                                                                <apex:outputField value="{!bidSubTrip['Sub_Trip_Notes__c']}" styleClass="form-control form-control-sm" />
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </apex:repeat>
                                <div class="col-md-12" style="margin-top: 1rem !important;">
                                    <strong>Vehicle Information</strong>
                                </div>
                                <div class="col-md-12">
                                    <div class="accordion">
                                        <div class="card">
                                            <div id="collapseFive" class="collapse show" aria-labelledby="headingFive" data-parent="#accordionFive">
                                                <div class="card-body">
                                                    <table class="table table-sm" style="margin-top:5px;margin-bottom:0;">
                                                        <thead class="thead-light" style="background-color:rgba(0,0,0,.03);">
                                                            <tr>
                                                                <th width="15%">{!If(bidParentSObject = 'Ground', 'Vehicle', 'Equipment')}</th>
                                                                <th width="15%">Vehicle Type</th>
                                                                <th width="10%">Capacity</th>
                                                                <th width="10%">Make/Model</th>
                                                                <th width="10%">Year</th>
                                                                <th width="10%" style="{!If(bidParentSObject = 'Ground', 'display:none;', '')}">Freight Truck</th>
                                                                <th width="15%">{!If(bidParentSObject = 'Ground', 'Amenities', 'Equipment Requested')}</th>
                                                            </tr>
                                                        </thead>
                                                        <tbody>
                                                            <apex:repeat value="{!bidAgreementVehicles}" var="bidVehicle">
                                                                <tr>
                                                                    <td>
                                                                        <apex:outputField value="{!bidVehicle[If(bidParentSObject = 'Ground', 'Vehicle_Ref__c', 'Equipment__c')]}" styleClass="form-control form-control-sm"/>
                                                                    </td>
                                                                    <td>
                                                                        <apex:outputField value="{!bidVehicle['Vehicle_Type__c']}" styleClass="form-control form-control-sm"/>
                                                                    </td>
                                                                    <td>
                                                                        <apex:outputField value="{!bidVehicle['Capacity__c']}" styleClass="form-control form-control-sm"/>
                                                                    </td>
                                                                    <td>
                                                                        <apex:outputField value="{!bidVehicle['Make_Model__c']}" styleClass="form-control form-control-sm"/>
                                                                    </td>
                                                                    <td>    
                                                                        <apex:outputField value="{!bidVehicle['Year__c']}" styleClass="form-control form-control-sm"/>
                                                                    </td>
                                                                    <td style="{!If(bidParentSObject = 'Ground', 'display:none;', '')}">    
                                                                        <apex:outputField value="{!bidVehicle['Freight_Truck_Sq_Ft__c']}" styleClass="form-control form-control-sm" rendered="{!bidParentSObject = 'Freight'}"/>
                                                                    </td>
                                                                    <td>
                                                                        <apex:outputField value="{!bidVehicle[If(bidParentSObject = 'Ground', 'Amenities__c', 'Equipment_requested__c')]}" styleClass="form-control form-control-sm"/>{!IF(bidParentSObject = 'Ground' && !ISNULL(bidVehicle['Other_Amenities__c']), ',' + bidVehicle['Other_Amenities__c'], '')}
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
                                <div class="col-md-12">
                                    <strong>Payment info:</strong>
                                </div>
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
                                                        <apex:repeat value="{!bidAgreementConcessions}" var="bidConcession"><p>{!bidConcession.Concession_Provided__c}</p></apex:repeat>
                                                    </div>
                                                    <apex:outputPanel layout="block" rendered="{!formLabel == 'Transportation Contract'}" styleClass="form-group">
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
                            </apex:outputPanel>
                            <apex:outputPanel layout="block" rendered="{!formLabel = 'Rate Agreement' || formLabel = 'Transportation Contract'}" styleClass="row">
                                <div class="col-md-12">
                                    <label style="font-weight:bold;">Terms</label>
                                    <apex:inputTextarea id="bidAgreement_terms" value="{!draft.Terms__c}" rows="5" styleClass="form-control form-control-sm" />
                                    <script>
                                        CKEDITOR.replace('{!$Component.bidAgreement_terms}', {
                                            language: 'en',
                                            extraAllowedContent: 'th{color,background,background-color}'
                                        });
                                    </script>
                                </div>
                            </apex:outputPanel>
                            <!-- Changes Added as per 175349270  Added rendered="{!formLabel != 'Ground Transportation Procedures'}-->
                            <apex:outputPanel id="bidAgreementAuditFields" rendered="{!formLabel != 'Ground Transportation Procedures'}" layout="block" styleClass="row" style="margin-top: 1rem !important;">
                                <div class="col">
                                    <div class="row" style="margin-top: 0 !important;">
                                        <div class="col-md-5" style="text-align: right;">Created By :</div>
                                        <div class="col" style="padding: 0;">
                                            <b>{!draft.CreatedBy.Name}</b>
                                        </div>
                                    </div>
                                    <div class="row" style="margin-top: 0 !important;">
                                        <div class="col-md-5" style="text-align: right;">Modified By :</div>
                                        <div class="col" style="padding: 0;">
                                            <b>{!draft.LastModifiedBy.Name}</b>
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
                                                <apex:outputField value="{!formBid.Rate_Agreement_Last_Send_By__c}" rendered="{!formValue = 'Form_Rate_Agreement__c'}"/>
                                                <apex:outputField value="{!formBid.Trip_Details_Update_Last_Send_By__c}" rendered="{!formValue = 'Form_Trip_Details_Update__c'}"/>
                                                <apex:outputField value="{!formBid.Transportation_Contract_Last_Send_By__c}" rendered="{!formValue = 'Form_Transportation_Contract__c'}"/>
                                                <apex:outputField value="{!formBid.Contract_to_Client_Last_Send_By__c}" rendered="{!formValue = 'Form_Contract_to_Client__c'}"/>
                                                <apex:outputField value="{!formBid.Counter_Needed_Last_Send_By__c}" rendered="{!formValue = 'Form_Counter_Needed__c'}"/>
                                                <apex:outputField value="{!formBid.Final_Contract_Last_Send_By__c}" rendered="{!formValue = 'Form_Final_Contract__c'}"/>
                                                <apex:outputField value="{!formBid.Email_Confirmation_Last_Send_By__c}" rendered="{!formValue = 'Form_Email_Confirmation__c'}"/>
                                                <apex:outputField value="{!formBid.Credit_Card_Last_Send_By__c}" rendered="{!formValue = 'Form_Credit_Card_Change__c'}"/>
                                                <apex:outputField value="{!formBid.Cancellation_Last_Send_By__c}" rendered="{!formValue = 'Form_Cancellation_Letter__c'}"/>
                                            </b>
                                        </div>
                                    </div>
                                </div>
                                <div class="col">
                                    <div class="row" style="margin-top: 0 !important;">
                                        <div class="col-md-5" style="text-align: right;">Sent On :</div>
                                        <div class="col" style="padding: 0;">
                                            <b>
                                                <apex:outputField value="{!formBid.Rate_Agreement_Last_Send_Date__c}" rendered="{!formValue = 'Form_Rate_Agreement__c'}"/>
                                                <apex:outputField value="{!formBid.Trip_Details_Update_Last_Send_Date__c}" rendered="{!formValue = 'Form_Trip_Details_Update__c'}"/>
                                                <apex:outputField value="{!formBid.Transportation_Contract_Last_Send_Date__c}" rendered="{!formValue = 'Form_Transportation_Contract__c'}"/>
                                                <apex:outputField value="{!formBid.Contract_to_Client_Last_Send_Date__c}" rendered="{!formValue = 'Form_Contract_to_Client__c'}"/>
                                                <apex:outputField value="{!formBid.Counter_Needed_Last_Send_Date__c}" rendered="{!formValue = 'Form_Counter_Needed__c'}"/>
                                                <apex:outputField value="{!formBid.Final_Contract_Last_Send_Date__c}" rendered="{!formValue = 'Form_Final_Contract__c'}"/>
                                                <apex:outputField value="{!formBid.Email_Confirmation_Last_Send_Date__c}" rendered="{!formValue = 'Form_Email_Confirmation__c'}"/>
                                                <apex:outputField value="{!formBid.Credit_Card_Last_Send_Date__c}" rendered="{!formValue = 'Form_Credit_Card_Change__c'}"/>
                                                <apex:outputField value="{!formBid.Cancellation_Last_Send_Date__c}" rendered="{!formValue = 'Form_Cancellation_Letter__c'}"/>
                                            </b>
                                        </div>
                                    </div>
                                </div>
                            </apex:outputPanel>
                        </apex:outputPanel>
                        <apex:outputPanel layout="block" rendered="{!bidParentSObject = 'Air'}">
                            <apex:outputPanel layout="block">
                                <div class="row">
                                    <div class="col-md-{!If(formLabel = 'Final Choice' || formLabel = 'Ticketed Confirmation' || formLabel = 'Final Air Confirmation', '6', '12')}">
                                        <strong style="font-size:16px;{!If(formLabel = 'Final Choice' || formLabel = 'Ticketed Confirmation' || formLabel = 'Final Air Confirmation', '', 'display:none;')}">Production Information</strong>
                                        <div class="fieldset" style="height:{!If(formLabel = 'Final Choice' || formLabel = 'Ticketed Confirmation' || formLabel = 'Final Air Confirmation', '220px', '100px')};margin-top: 0 !important;">
                                            <div class="row">
                                                <div class="col-md-{!If(formLabel = 'Final Choice' || formLabel = 'Ticketed Confirmation' || formLabel = 'Final Air Confirmation', '3', '2')}">
                                                    <strong>Production :</strong>
                                                </div>
                                                <div class="col-md-9">
                                                    <apex:outputLink value="/{!formBid.Production__c}" target="_blank">{!formBid.Production__r.Name}</apex:outputLink>
                                                </div>
                                            </div>
                                            <div class="row">
                                                <div class="col-md-12"></div>
                                            </div>
                                            <div class="row">
                                                <div class="col-md-{!If(formLabel = 'Final Choice' || formLabel = 'Ticketed Confirmation' || formLabel = 'Final Air Confirmation', '3', '2')}">
                                                    <apex:outputLabel value="Attention: " for="airbidAgreementAttentionContactSelect" style="font-weight:bold;" rendered="{!formLabel = 'Deposit Due' || formLabel = 'Utilization' || formLabel = 'Names & Final Payment'}"/>
                                                    <apex:outputLabel value="Contact: " for="airbidAgreementProductionAssociationContactSelect" style="font-weight:bold;" rendered="{!formLabel = 'Final Choice' || formLabel = 'Ticketed Confirmation' || formLabel = 'Final Air Confirmation'}"/>
                                                </div>
                                                <div class="col-md-{!If(formLabel = 'Final Choice' || formLabel = 'Ticketed Confirmation' || formLabel = 'Final Air Confirmation', '9', '3')}">
                                                    <apex:selectList size="1" id="airbidAgreementAttentionContactSelect" styleClass="form-control form-control-sm" value="{!draft.Attention__c}" rendered="{!formLabel = 'Deposit Due' || formLabel = 'Utilization' || formLabel = 'Names & Final Payment'}">
                                                        <apex:selectOptions value="{!BidAgreementProductionAssociationContacts}"/>
                                                        <apex:actionSupport event="onchange" action="{!changeBidAgreementAttentionContact}" status="loading" reRender="airbidAgreementToPanel,airbidAgreement_salutation"/>
                                                    </apex:selectList>
                                                    <apex:selectList size="1" id="airbidAgreementProductionAssociationContactSelect" styleClass="form-control form-control-sm" value="{!draft.Production_Assoc_Contact_Id__c}" rendered="{!formLabel = 'Final Choice' || formLabel = 'Ticketed Confirmation' || formLabel = 'Final Air Confirmation'}">
                                                        <apex:selectOptions value="{!BidAgreementProductionAssociationContacts}"/>
                                                        <apex:actionSupport event="onchange" action="{!changeBidAgreementProductionAssociationContact}" status="loading" reRender="airbidAgreementContactPanel,airbidAgreementToPanel,airbidAgreement_salutation"/>
                                                    </apex:selectList>
                                                </div>
                                            </div>
                                            <div class="row">
                                                <div class="col-md-12"></div>
                                            </div>
                                            <apex:outputPanel id="airbidAgreementContactPanel"  rendered="{!formLabel = 'Final Choice' || formLabel = 'Ticketed Confirmation' || formLabel = 'Final Air Confirmation'}">
                                                <div class="row">
                                                    <div class="col-md-3">
                                                        <strong>Title :</strong>
                                                    </div>
                                                    <div class="col-md-9">
                                                        {!bidAgreementPrimaryContact['Title']}
                                                    </div>
                                                </div>
                                                <div class="row">
                                                    <div class="col-md-12"></div>
                                                </div>
                                                <div class="row">
                                                    <div class="col-md-3">
                                                        <strong>Phone :</strong>
                                                    </div>
                                                    <div class="col-md-9">
                                                        <a href="{!bidAgreementPrimaryContact['Phone']}">{!bidAgreementPrimaryContact['Phone']}</a>
                                                    </div>
                                                </div>
                                                <div class="row">
                                                    <div class="col-md-12"></div>
                                                </div>
                                                <div class="row">
                                                    <div class="col-md-3">
                                                        <strong>Email :</strong>
                                                    </div>
                                                    <div class="col-md-9">
                                                        <a href="mailto:{!bidAgreementPrimaryContact['Email']}">{!bidAgreementPrimaryContact['Email']}</a>
                                                    </div>
                                                </div>
                                            </apex:outputPanel>
                                        </div>
                                    </div>
                                    <apex:outputPanel layout="block" rendered="{!formLabel = 'Final Choice' || formLabel = 'Ticketed Confirmation' || formLabel = 'Final Air Confirmation'}" styleClass="col-md-6">
                                        <strong style="font-size:16px;">User Information</strong>
                                        <apex:outputPanel id="airBidAgreementAuditFields" layout="block" styleClass="fieldset" style="height: 220px;margin-top: 0 !important;">
                                            <div class="row">
                                                <div class="col-md-3"><strong>Created By :</strong></div>
                                                <div class="col" style="padding: 0;">
                                                    {!draft.CreatedBy.Name}
                                                </div>
                                            </div>
                                            <div class="row">
                                                <div class="col-md-3"><strong>Modified By :</strong></div>
                                                <div class="col" style="padding: 0;">
                                                    {!draft.LastModifiedBy.Name}
                                                </div>
                                            </div>
                                            <div class="row">
                                                <div class="col-md-12"></div>
                                            </div>
                                            <div class="row">
                                                <div class="col-md-3"><strong>Created On :</strong></div>
                                                <div class="col" style="padding: 0;">
                                                    <apex:outputField value="{!draft.CreatedDate}"/>
                                                </div>
                                            </div>
                                            <div class="row">
                                                <div class="col-md-3"><strong>Modified On :</strong></div>
                                                <div class="col" style="padding: 0;">
                                                    <apex:outputField value="{!draft.LastModifiedDate}"/>
                                                </div>
                                            </div>
                                            <div class="row">
                                                <div class="col-md-12"></div>
                                            </div>
                                            <div class="row">
                                                <div class="col-md-3"><strong>Sent By :</strong></div>
                                                <div class="col" style="padding: 0;">
                                                    <apex:outputField value="{!formBid.Deposit_Due_Last_Send_By__c}" rendered="{!formValue = 'Form_Deposit_Due__c'}"/>
                                                    <apex:outputField value="{!formBid.Utilization_Last_Send_By__c}" rendered="{!formValue = 'Form_Utilization__c'}"/>
                                                    <apex:outputField value="{!formBid.Names_Final_Payment_Last_Send_By__c}" rendered="{!formValue = 'Form_Names_Final_Payment__c'}"/>
                                                    <apex:outputField value="{!formBid.Final_Choice_Last_Send_By__c}" rendered="{!formValue = 'Form_Final_Choice__c'}"/>
                                                    <apex:outputField value="{!formBid.Ticketed_Confirmation_Last_Send_By__c}" rendered="{!formValue = 'Form_Ticketed_Confirmation__c'}"/>
                                                    <apex:outputField value="{!formBid.Final_Air_Confirmation_Last_Send_By__c}" rendered="{!formValue = 'Form_Final_Air_Confirmation__c'}"/>
                                                </div>
                                            </div>
                                            <div class="row">
                                                <div class="col-md-3"><strong>Sent On :</strong></div>
                                                <div class="col" style="padding: 0;">
                                                    <apex:outputField value="{!formBid.Deposit_Due_Last_Send_Date__c}" rendered="{!formValue = 'Form_Deposit_Due__c'}"/>
                                                    <apex:outputField value="{!formBid.Utilization_Last_Send_Date__c}" rendered="{!formValue = 'Form_Utilization__c'}"/>
                                                    <apex:outputField value="{!formBid.Names_Final_Payment_Last_Send_Date__c}" rendered="{!formValue = 'Form_Names_Final_Payment__c'}"/>
                                                    <apex:outputField value="{!formBid.Final_Choice_Last_Send_Date__c}" rendered="{!formValue = 'Form_Final_Choice__c'}"/>
                                                    <apex:outputField value="{!formBid.Ticketed_Confirmation_Last_Send_Date__c}" rendered="{!formValue = 'Form_Ticketed_Confirmation__c'}"/>
                                                    <apex:outputField value="{!formBid.Final_Air_Confirmation_Last_Send_Date__c}" rendered="{!formValue = 'Form_Final_Air_Confirmation__c'}"/>
                                                </div>
                                            </div>
                                        </apex:outputPanel>
                                    </apex:outputPanel>
                                </div>
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="fieldset" style="margin-top: 0 !important;">
                                            <div class="form-group row">
                                                <apex:outputLabel value="To :" for="" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                                <div class="col-sm-10">
                                                    <apex:outputPanel id="airbidAgreementToPanel">
                                                        <div id="bidAgreement_primarycontactemail" class="bidAgreement-to">
                                                            <apex:inputField value="{!bidAgreementAttentionContact.Email}" styleClass="form-control form-control-sm" required="false" html-disabled="true" rendered="{!formLabel = 'Deposit Due' || formLabel = 'Utilization' || formLabel = 'Names & Final Payment'}"/>
                                                            <apex:inputField value="{!bidAgreementPrimaryContact['Email']}" styleClass="form-control form-control-sm" required="false" html-disabled="true" rendered="{!formLabel = 'Final Choice' || formLabel = 'Ticketed Confirmation' || formLabel = 'Final Air Confirmation'}"/>
                                                        </div>
                                                    </apex:outputPanel>
                                                </div>
                                            </div>
                                            <div class="form-group row">
                                                <apex:outputLabel value="CC :" for="bidAgreement_cc" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                                <div class="col-sm-10">
                                                    <div class="all-cc-email-bidAgreement"></div>
                                                    <input type="text" id="bidAgreement_cc" value="{!draft.CC__c}" class="form-control form-control-sm cc-email-bidAgreement"/>
                                                </div>
                                            </div>
                                            <div class="form-group row">
                                                <apex:outputLabel value="BCC :" for="bidAgreement_bcc" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                                <div class="col-sm-10">
                                                    <div class="all-bcc-email-bidAgreement"></div>
                                                    <input type="text" id="bidAgreement_bcc" value="{!draft.BCC__c}" class="form-control form-control-sm bcc-email-bidAgreement"/>
                                                </div>
                                            </div>
                                            <div class="form-group row">
                                                <apex:outputLabel value="Subject :" for="airbidAgreement_subject" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                                <div class="col-sm-10">
                                                    <apex:inputField id="airbidAgreement_subject" value="{!draft.Subject__c}" styleClass="form-control form-control-sm subject-bidAgreement" /> 
                                                </div>
                                            </div>
                                            <div class="form-group row">
                                                <apex:outputLabel value="Attached :" for="airbidAgreement_attachs" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                                <div class="col-sm-4">
                                                    <apex:selectList size="4" id="airbidAgreement_attachs" styleClass="form-control" style="width:100%;"/>
                                                </div>
                                                <div class="col-sm-6">
                                                    <button type="button" class="btn btn-secondary btn-custom" onclick="removeAttachDocs('airbidAgreement_attachs');" style="float: left;margin-right: 5px;">Remove</button>
                                                    <div class="upload-btn-wrapper" style="display: block;float: left;margin-right: 5px;">
                                                        <button class="btn btn-secondary btn-custom" onclick="javascript:void(0);">Attach</button>
                                                        <input type="file" id="airfileBidAgreement" onchange="remoteLocationPostLast(event,'Rate Agreement','airbidAgreement_attachs', '{!formBid.Air__c}');" />
                                                    </div>
                                                    <button type="button" class="btn btn-secondary btn-custom" onclick="openAttachDocs('bid','{!formBid.Air__c}','bidAgreementModal');">Attach Contracting Docs</button>
                                                    <apex:inputHidden value="{!body}" id="airoutput"/>
                                                    <input type="hidden" id="attachment_new_charge"/>
                                                    <apex:outputPanel id="newAirAttachmentPanel">
                                                        <input type="hidden" id="attachment_new_id" value="{!newattachment_id}" />
                                                        <input type="hidden" id="attachment_new_name" value="{!newattachment_name}" />
                                                    </apex:outputPanel>
                                                    <button type="button" class="btn btn-secondary btn-custom" onclick="openAttachGcqJs();" style="{!If(formValue = 'Form_Final_Air_Confirmation__c', '', 'display:none;')}">Attach GCQ</button>
                                                </div>
                                            </div>
                                            <div class="form-group row">
                                                <apex:outputLabel value="Salutation:" for="airbidAgreement_salutation" styleClass="col-sm-1 col-form-label text-right" style="font-weight:bold;"/>
                                                <div class="col-sm-10">
                                                    <apex:inputField id="airbidAgreement_salutation" value="{!draft.Salutation__c}" styleClass="form-control form-control-sm"/>
                                                </div>
                                            </div>
                                            <div class="form-group row">
                                                <div class="col-sm-12">
                                                    <apex:inputTextarea id="bidSendConfirmation_message" value="{!draft.Body__c}" rows="5" styleClass="form-control form-control-sm" />
                                                    <script>
                                                    CKEDITOR.replace('{!$Component.bidSendConfirmation_message}', {
                                                        language: 'en',
                                                        extraAllowedContent: 'th{color,background,background-color}'
                                                    });
                                                    </script>
                                                </div>
                                            </div>
                                            <apex:outputPanel layout="block" styleClass="form-group row" style="margin-top: 1rem !important;">
                                                <div class="col">
                                                    <div class="row" style="margin-top: 0 !important;">
                                                        <div class="col-md-5" style="text-align: right;">Created By :</div>
                                                        <div class="col" style="padding: 0;">
                                                            <b>{!draft.CreatedBy.Name}</b>
                                                        </div>
                                                    </div>
                                                    <div class="row" style="margin-top: 0 !important;">
                                                        <div class="col-md-5" style="text-align: right;">Modified By :</div>
                                                        <div class="col" style="padding: 0;">
                                                            <b>{!draft.LastModifiedBy.Name}</b>
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
                                                                <apex:outputField value="{!formBid.Deposit_Due_Last_Send_By__c}" rendered="{!formValue = 'Form_Deposit_Due__c'}"/>
                                                                <apex:outputField value="{!formBid.Utilization_Last_Send_By__c}" rendered="{!formValue = 'Form_Utilization__c'}"/>
                                                                <apex:outputField value="{!formBid.Names_Final_Payment_Last_Send_By__c}" rendered="{!formValue = 'Form_Names_Final_Payment__c'}"/>
                                                                <apex:outputField value="{!formBid.Final_Choice_Last_Send_By__c}" rendered="{!formValue = 'Form_Final_Choice__c'}"/>
                                                                <apex:outputField value="{!formBid.Ticketed_Confirmation_Last_Send_By__c}" rendered="{!formValue = 'Form_Ticketed_Confirmation__c'}"/>
                                                                <apex:outputField value="{!formBid.Final_Air_Confirmation_Last_Send_By__c}" rendered="{!formValue = 'Form_Final_Air_Confirmation__c'}"/>
                                                            </b>
                                                        </div>
                                                    </div>
                                                </div>
                                                <div class="col">
                                                    <div class="row" style="margin-top: 0 !important;">
                                                        <div class="col-md-5" style="text-align: right;">Sent On :</div>
                                                        <div class="col" style="padding: 0;">
                                                            <b>
                                                                <apex:outputField value="{!formBid.Deposit_Due_Last_Send_Date__c}" rendered="{!formValue = 'Form_Deposit_Due__c'}"/>
                                                                <apex:outputField value="{!formBid.Utilization_Last_Send_Date__c}" rendered="{!formValue = 'Form_Utilization__c'}"/>
                                                                <apex:outputField value="{!formBid.Names_Final_Payment_Last_Send_Date__c}" rendered="{!formValue = 'Form_Names_Final_Payment__c'}"/>
                                                                <apex:outputField value="{!formBid.Final_Choice_Last_Send_Date__c}" rendered="{!formValue = 'Form_Final_Choice__c'}"/>
                                                                <apex:outputField value="{!formBid.Ticketed_Confirmation_Last_Send_Date__c}" rendered="{!formValue = 'Form_Ticketed_Confirmation__c'}"/>
                                                                <apex:outputField value="{!formBid.Final_Air_Confirmation_Last_Send_Date__c}" rendered="{!formValue = 'Form_Final_Air_Confirmation__c'}"/>
                                                            </b>
                                                        </div>
                                                    </div>
                                                </div>
                                            </apex:outputPanel>
                                        </div>
                                    </div>
                                </div>
                            </apex:outputPanel>
                        </apex:outputPanel>
                    </apex:outputPanel>
                </div>
                <div class="modal-footer" style="display:block;">
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="deactivateBidAgreement();" style="{!If(bidParentSObject = 'Air', 'display:none', '')}">Deactivate</button>
                    <button type="button" class="btn btn-default btn-sm" onclick="closeBidAgreementJs(false);" style="{!If((bidParentSObject = 'Ground' || bidParentSObject = 'Freight') && (formValue = 'Form_Email_Confirmation__c' || formValue = 'Form_Credit_Card_Change__c' || formValue = 'Form_Cancellation_Letter__c'), '', 'display:none;')}">Close</button>
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="saveBidAgreement();">Save</button>
                    <!-- Fix By Clay 28 Dec, 2020
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="alert('GCIp Btn');" style="{!formValue = 'Form_Create_GCIP__c'}">Send Email</button>
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="congaSendHandler();" style="{!If(((bidParentSObject = 'Ground' || bidParentSObject = 'Freight') && formValue != 'Form_Create_GCIP__c'  && formValue != 'Form_Credit_Card_Change__c' && formValue != 'Form_Cancellation_Letter__c') || (bidParentSObject = 'Air' && (formValue = 'Form_Final_Choice__c' || formValue = 'Form_Ticketed_Confirmation__c' || formValue = 'Form_Final_Air_Confirmation__c')), '', 'display:none;')}">Send Email</button>
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="sendEmail();" style="{!If(((bidParentSObject = 'Ground' || bidParentSObject = 'Freight') && formValue = 'Form_Credit_Card_Change__c' || formValue = 'Form_Cancellation_Letter__c') || (bidParentSObject = 'Air' && formValue != 'Form_Final_Choice__c' && formValue != 'Form_Ticketed_Confirmation__c' && formValue != 'Form_Final_Air_Confirmation__c' && formValue = 'Form_Create_GCIP__c'), '', 'display:none;')}">Send Email</button>
                    -->
                    <!-- Changes as per 176564037 -->
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="sendEmail();" style="{!If(((bidParentSObject = 'Ground' || bidParentSObject = 'Freight') && formValue != 'Form_Credit_Card_Change__c' && formValue != 'Form_Cancellation_Letter__c') || (bidParentSObject = 'Air' && (formValue = 'Form_Final_Choice__c' || formValue = 'Form_Ticketed_Confirmation__c' || formValue = 'Form_Final_Air_Confirmation__c')), '', 'display:none;')}">Send PDF</button><!--congaSendHandler();-->
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="sendEmail();" style="{!If(((bidParentSObject = 'Ground' || bidParentSObject = 'Freight') && formValue = 'Form_Credit_Card_Change__c' || formValue = 'Form_Cancellation_Letter__c') || (bidParentSObject = 'Air' && formValue != 'Form_Final_Choice__c' && formValue != 'Form_Ticketed_Confirmation__c' && formValue != 'Form_Final_Air_Confirmation__c'), '', 'display:none;')}">Send Email</button>
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="deactivateBidAgreement();" style="{!If(bidParentSObject = 'Air', '', 'display:none')}">Deactivate</button>
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="closeBidAgreementJs(false);" style="{!If(bidParentSObject = 'Air', '', 'display:none;')}">Cancel</button>
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="congaPreviewHandler();" style="{!If((bidParentSObject = 'Ground' || bidParentSObject = 'Freight') && (formValue = 'Form_Rate_Agreement__c' || formValue = 'Form_Transportation_Contract__c' || formValue = 'Form_Trip_Details_Update__c'), '', 'display:none;')}">Preview</button>
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="openPreviewFinalTicketedConfirmationJs();" style="{!If(And(bidParentSObject = 'Air', Or(formValue = 'Form_Final_Choice__c', formValue = 'Form_Ticketed_Confirmation__c')), '', 'display:none;')}">Preview {!formLabel} PDF</button>
                    <!-- //Changes Added as per 175349270 -->
                    <button type="button" class="btn btn-danger btn-sm btn-send" onclick="congaSignHandler();" style="{!If((bidParentSObject = 'Ground' || bidParentSObject = 'Freight') && formValue != 'Form_Final_Contract__c' && formValue != 'Form_Credit_Card_Change__c' && formValue != 'Form_Email_Confirmation__c' && formValue != 'Form_Cancellation_Letter__c' && formValue != 'Form_Create_GCIP__c', '', 'display:none;')}">Send Signer</button>
                    <span id="saveBidAgreementMessage" class="saveMessage" style="display:none;">Saved Successfully</span>
                </div>
            </apex:outputPanel>
        </apex:outputPanel>
    </div>
    <!-- End Modal -->
    <!-- Modal content-->
    <div class="modal fade" id="myModalAttachDocuments" role="dialog">
        <apex:outputPanel id="myModalAttachDocuments" layout="block" styleClass="modal-dialog modal-lg">
            <apex:outputPanel layout="block" rendered="{!isAttachsRendered}" styleClass="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title">Documents</h4>
                    <button type="button" class="close" onclick="closeModal('myModalAttachDocuments');viewModalIndex('bidAgreementModal');">&times;</button>
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
                                        <tr onclick="selectDocumentProdRow(this);" vid="{!attachDocument.Id}" vname="{!attachDocument.Title + '.' + attachDocument.FileExtension}">
                                            <td>
                                                {!attachDocument.Title}.{!attachDocument.FileExtension}
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
                    <button type="button" class="btn btn-secondary btn-custom" onclick="selectAttachDocument('bidAgreementModal','bidAgreement_attachs');">Attach</button>
                </div>
            </apex:outputPanel>
        </apex:outputPanel>
    </div>
    <!-- End Modal -->
    <!-- Modal content-->
    <div class="modal fade" id="myModalAttachGCQ" role="dialog">
        <apex:outputPanel id="myModalAttachGCQ" layout="block" styleClass="modal-dialog modal-xl attachGCQModal">
            <apex:outputPanel layout="block" rendered="{!isAttachGCQRendered}" styleClass="modal-content" style="min-height:550px;">
                <div class="modal-header">
                    <h4 class="modal-title">Attach {!If(bidParentSObject = 'Ground' || bidParentSObject = 'Air', 'G', 'F')}CQ</h4>
                    <button type="button" class="close" onclick="closeModal('myModalAttachGCQ');viewModalIndex('bidAgreementModal');">&times;</button>
                </div>
                <div class="modal-body" style="font-size:12px;">
                    <div class="row">
                        <div class="col-md-12">
                            <div class="card">
                                <div class="card-body">
                                    <apex:outputPanel layout="block" id="gcqSearchSection" styleClass="row">
                                        <div class="col-xs-12 col-sm-6 col-md-4">
                                            <div class="form-group row">
                                                <apex:outputLabel value="Start Date:" for="attachGcq_startDateInput" styleClass="col-xs-12 col-sm-4 col-form-label" style="font-weight:bold;"/>
                                                <div class="col-xs-12 col-sm-7">
                                                    <div class="input-group date">
                                                        <input type="text" id="attachGcq_startDateInput" class="form-control form-control-sm"/>
                                                        <div class="input-group-append">
                                                            <span class="input-group-text"><i class="far fa-calendar-alt"></i></span>                    
                                                        </div>
                                                        <apex:inputHidden id="attachGcq_startDate" value="{!attachGcq_departureDate}"/>
                                                    </div>
                                                </div>
                                                <div class="col-xs-12 col-sm-12">
                                                    <span class="text-danger" style="display: none;">
                                                        Please specify start date
                                                    </span>                                                
                                                </div>
                                            </div>
                                        </div>
                                        <div class="col-xs-12 col-sm-6 col-md-4">
                                            <div class="form-group row" id="attachGcq_endDateDiv">
                                                <apex:outputLabel value="End Date:" for="attachGcq_endDateInput" styleClass="col-xs-12 col-sm-4 col-form-label" style="font-weight:bold;"/>
                                                <div class="col-xs-12 col-sm-7">
                                                    <div class="input-group date">
                                                        <input type="text" id="attachGcq_endDateInput" class="form-control form-control-sm"/>
                                                        <div class="input-group-append">
                                                            <span class="input-group-text"><i class="far fa-calendar-alt"></i></span>                    
                                                        </div>
                                                        <apex:inputHidden id="attachGcq_endDate" value="{!attachGcq_arrivalDate}"/>
                                                    </div>
                                                </div>
                                                <div class="col-xs-12 col-sm-12">
                                                    <span class="text-danger" style="display: none;">
                                                        Please specify end date
                                                    </span>                                                
                                                </div>
                                            </div>
                                        </div>
                                        <div class="col-xs-12 col-sm-6 col-md-2 text-left">
                                            <div class="row">
                                                <div class="col-xs-12">
                                                    <button type="button" class="btn btn-info btn-sm" onclick="searchAttachGcq()" style="color:white;">Search</button>
                                                    <button type="button" class="btn btn-danger btn-sm" onclick="attachGcq()" style="{!If(bidParentSObject = 'Air', '', 'display:none;')}">Attach</button>
                                                    <button type="button" class="btn btn-default btn-sm" onclick="clearAttachGcq()" >Clear</button>
                                                    <span id="topGcqMessage" class="text-danger" style="display:none;font-weight:bold;">Please select one GCQ</span>
                                                </div>
                                            </div>
                                        </div>
                                    </apex:outputPanel>
                                </div>
                            </div>                    
                        </div>
                        <apex:outputPanel layout="block" id="gcqsSection" styleClass="col-md-12">
                            <apex:outputPanel layout="block" rendered="{!!isGcqEmpty}" styleClass="table-responsive" style="max-height:500px;">
                                <div class="card" style="margin-top:10px;">
                                    <apex:outputPanel layout="block" rendered="{!bidParentSObject = 'Ground' || bidParentSObject = 'Freight'}" styleClass="card-body">
                                        <table class="table table-striped table-hover gcqTable">
                                            <thead class="thead-light">
                                                <tr>
                                                    <th width="20%">Trip Id</th>
                                                    <th width="20%">Trip Description</th>
                                                    <th width="15%">Sub Trip Date</th>
                                                    <th width="25%">Sub Trip Description</th>
                                                    <th width="20%">{!If(bidParentSObject = 'Ground', 'G', 'F')}CQ ID</th>
                                                </tr>
                                            </thead>
                                            <tbody>
                                                <apex:repeat value="{!gcqSubtripsMap}" var="gcq">
                                                    <tr onclick="selectGcq(this)" data-tripid="{!gcqSubtripsMap[gcq][0]['Bid_Sub_Trip__r'][If(bidParentSObject = 'Ground', 'GT__c', 'Freight__c')]}" data-bidid="{!gcqSubtripsMap[gcq][0]['Bid_Sub_Trip__c']}" data-gcqid="{!gcq['Id']}" data-gcqname="{!gcq['Name']}">
                                                        <td>
                                                            {!gcqSubtripsMap[gcq][0]['Bid_Sub_Trip__r'][If(bidParentSObject = 'Ground', 'GT__r', 'Freight__r')]['Name']}
                                                        </td>
                                                        <td>
                                                            {!gcqSubtripsMap[gcq][0]['Bid_Sub_Trip__r'][If(bidParentSObject = 'Ground', 'GT__r', 'Freight__r')]['Description__c']}
                                                        </td>
                                                        <td>
                                                            <apex:repeat value="{!gcqSubtripsMap[gcq]}" var="subtrip">
                                                                <apex:repeat value="{!bidSubtripsMap[subtrip['id']][If(bidParentSObject = 'Ground', 'GTTravels__r', 'FreightEquipments__r')]}" var="travel">
                                                                    <apex:outputText value="{0,date,dd-MMMM-yyyy}">
                                                                        <apex:param value="{!travel['Start_Date__c']}" />
                                                                    </apex:outputText><br/>
                                                                </apex:repeat>
                                                            </apex:repeat>
                                                        </td>
                                                        <td>
                                                            <apex:repeat value="{!gcqSubtripsMap[gcq]}" var="subtrip">
                                                                {!subtrip['Description__c']}<br/>
                                                            </apex:repeat>
                                                        </td>
                                                        <td>
                                                            {!gcq['Name']}
                                                        </td>
                                                    </tr>
                                                </apex:repeat>
                                        </tbody>
                                        </table>
                                    </apex:outputPanel>
                                    <apex:outputPanel layout="block" rendered="{!bidParentSObject = 'Air'}" styleClass="card-body">
                                        <table class="table table-striped table-hover gcqTable">
                                            <thead class="thead-light">
                                                <tr>
                                                    <th width="15%">Trip Id</th>
                                                    <th width="25%">Trip Description</th>
                                                    <th width="15%">Travel Date</th>
                                                    <th width="30%">Travel Description</th>
                                                    <th width="15%">GCQ ID</th>
                                                </tr>
                                            </thead>
                                            <tbody>
                                                <apex:repeat value="{!searchGcqsMap}" var="gcqId">
                                                    <tr onclick="selectGcq(this)" data-gcqid="{!gcqId}" data-gcqname="{!searchGcqsMap[gcqId].gcqName}" data-bidid="{!searchGcqsMap[gcqId].bidId}">
                                                        <td>
                                                            {!searchGcqsMap[gcqId].tripId}
                                                        </td>
                                                        <td>
                                                            {!searchGcqsMap[gcqId].tripDescription}
                                                        </td>
                                                        <td>
                                                            <apex:repeat value="{!searchGcqsMap[gcqId].itinerarySegmentsMap}" var="itinerary">
                                                                <strong>Main Flight</strong><br/>
                                                                <apex:repeat value="{!searchGcqsMap[gcqId].itinerarySegmentsMap[itinerary]}" var="itinerarySegment">
                                                                    <apex:outputText value="{0,date,dd-MMM-yyyy}">
                                                                        <apex:param value="{!itinerarySegment.Departure_Date__c}"/>
                                                                    </apex:outputText><br/>
                                                                </apex:repeat>
                                                            </apex:repeat>
                                                            <apex:repeat value="{!searchGcqsMap[gcqId].deviationSegmentsMap}" var="deviation">
                                                                <strong>Deviation {!deviation.Deviation_Order_Formula_Conga__c}</strong><br/>
                                                                <apex:repeat value="{!searchGcqsMap[gcqId].deviationSegmentsMap[deviation]}" var="deviationSegment">
                                                                    <apex:outputText value="{0,date,dd-MMM-yyyy}">
                                                                        <apex:param value="{!deviationSegment.Departure_Date__c}"/>
                                                                    </apex:outputText><br/>
                                                                </apex:repeat>
                                                            </apex:repeat>
                                                        </td>
                                                        <td>
                                                            <apex:repeat value="{!searchGcqsMap[gcqId].itinerarySegmentsMap}" var="itinerary">
                                                                {!itinerary.Description__c}<br/>
                                                            </apex:repeat>
                                                            <apex:repeat value="{!searchGcqsMap[gcqId].deviationSegmentsMap}" var="deviation">
                                                                {!deviation.Description__c}<br/>
                                                            </apex:repeat>
                                                        </td>
                                                        <td>
                                                            {!searchGcqsMap[gcqId].gcqName}
                                                        </td>
                                                    </tr>
                                                </apex:repeat>
                                            </tbody>
                                        </table>
                                    </apex:outputPanel>
                                </div>
                            </apex:outputPanel>
                            <apex:outputPanel layout="block" rendered="{!isGcqSearched && isGcqEmpty}" styleClass="col-xs-12 text-danger">
                                No records found
                            </apex:outputPanel>
                        </apex:outputPanel>
                    </div>
                </div>
                <apex:outputPanel layout="block" rendered="{!bidParentSObject = 'Ground' || bidParentSObject = 'Freight'}" styleClass="modal-footer text-right">
                    <span id="bottomGcqMessage" class="text-danger" style="display:none;font-weight:bold;">Please select one GCQ</span>
                    <button type="button" class="btn btn-default btn-sm" onclick="closeModal('myModalAttachGCQ');viewModalIndex('bidAgreementModal');">Close</button>
                    <button type="button" class="btn btn-danger btn-sm" onclick="congaPreviewGCQ('{!JSENCODE(bidAgreement_congaQueriesJson)}', '{!bidAgreement_congaTemplateId}');">Preview</button>
                    <button type="button" class="btn btn-danger btn-sm" onclick="attachGcq()" >Attach</button>
                </apex:outputPanel>
            </apex:outputPanel>
        </apex:outputPanel>
    </div>
    <!-- End Modal -->
    <!-- Actionfunctions -->
    <apex:actionFunction name="loadFormsJs" action="{!loadForms}" status="loadingSubTab" reRender="contractForms" />
    <!-- BidAgreement -->
    <apex:actionFunction name="changeAttentionFormJs" action="{!bindAttentionDetails}" status="loading" reRender="contractForms,myGroundModalContent">
    </apex:actionFunction>
    <!-- //Changes as per 175349270 -->
    <!-- <apex:actionFunction action="{!sendEmailFormWithAttachs}" name="sendEmailFormWithAttachsJs" status="loading" reRender="formMessagePanel,contractStatusPanel,tournamentStatusPanel,bidJournalsPanel2" oncomplete="finalMessage();">
        <apex:param assignTo="{!form_to}" name="emailTo" value="" />
        <apex:param assignTo="{!form_cc}" name="emailCC" value="" />
        <apex:param assignTo="{!form_bcc}" name="emailBCC" value="" />
        <apex:param assignTo="{!form_subject}" name="emailSubject" value="" />
        <apex:param assignTo="{!form_date}" name="form_date" value="" />
        <apex:param assignTo="{!form_body}" name="emailBody" value="" />
        <apex:param assignTo="{!form_closing}" name="emailClosing" value="" />
        <apex:param assignTo="{!emailAttachs}" name="emailAttachs" value="" />
        <apex:param assignTo="{!form_salutation}" name="form_salutation" value="" />
    </apex:actionFunction> -->
    <apex:actionFunction name="openFormJs" action="{!openForm}" status="loading" reRender="contractForms,myGroundModalContent" oncomplete="setupForm();openModal('myGroundModalForm');hideCK();">
        <apex:param assignTo="{!formLabel}" name="formLabel" value="" />
        <apex:param assignTo="{!formValue}" name="formValue" value="" />
        <apex:param assignTo="{!draftCode}" name="draftCode" value="" />
    </apex:actionFunction>
    <apex:actionFunction name="closeBidAgreementJs" status="loading" reRender="myGroundModalContent" oncomplete="closeModal('myGroundModalForm');">
        <apex:param assignTo="{!isBidAgreementRendered}" name="isBidAgreementRendered" value="" />
    </apex:actionFunction>
    <apex:actionFunction name="saveBidAgreementJs" action="{!saveBidAgreement}" status="loading" reRender="bidAgreementAuditFields" oncomplete="saveBidAgreementMessage();">
        <apex:param assignTo="{!draft.Body__c}" name="bidAgreement_message" value="" />
        <apex:param assignTo="{!draft.Terms__c}" name="bidAgreement_terms" value="" />
    </apex:actionFunction>
    <apex:actionFunction name="congaPreviewJs" action="{!saveBidAgreement}" status="loading" reRender="bidAgreementAuditFields" oncomplete="saveBidAgreementMessage();congaPreview('{!formBid.id}', '{!formBid.Name}', '{!If(bidParentSObject = 'Ground', formBid.GT__c, If(bidParentSObject = 'Freight', formBid.Freight__c, If(bidParentSObject = 'Air', formBid.Air__c, '')))}', '{!If(bidParentSObject = 'Ground', formBid.GT__r.Name, If(bidParentSObject = 'Freight', formBid.Freight__r.Name, If(bidParentSObject = 'Air', formBid.Air__r.Name, '')))}', '{!JSENCODE(bidAgreement_congaQueriesJson)}', '{!bidAgreement_congaTemplateId}')">
        <apex:param assignTo="{!draft.Body__c}" name="bidAgreement_message" value="" />
        <apex:param assignTo="{!draft.Terms__c}" name="bidAgreement_terms" value="" />
    </apex:actionFunction>
    <apex:actionFunction name="congaSendJs" action="{!saveBidAgreement}" status="loading" reRender="bidAgreementAuditFields, airBidAgreementAuditFields" oncomplete="saveBidAgreementMessage();congaSend('{!formBid.id}', '{!formBid.Name}', '{!If(bidParentSObject = 'Ground', formBid.GT__c, If(bidParentSObject = 'Freight', formBid.Freight__c, If(bidParentSObject = 'Air', formBid.Air__c, '')))}', '{!If(bidParentSObject = 'Ground', formBid.GT__r.Name, If(bidParentSObject = 'Freight', formBid.Freight__r.Name, If(bidParentSObject = 'Air', formBid.Air__r.Name, '')))}', '{!JSENCODE(bidAgreement_congaQueriesJson)}', '{!bidAgreement_congaEmailTemplateId}', '{!bidAgreement_congaTemplateId}');">
        <apex:param assignTo="{!draft.Body__c}" name="bidAgreement_message" value="" />
        <apex:param assignTo="{!draft.Terms__c}" name="bidAgreement_terms" value="" />
        <apex:param assignTo="{!selectedGcqId}" name="selectedGcqId" value=""/>
    </apex:actionFunction>
    <apex:actionFunction name="congaSignJs" action="{!saveBidAgreement}" status="loading" reRender="bidAgreementAuditFields, airBidAgreementAuditFields" oncomplete="saveBidAgreementMessage();congaSign('{!formBid.id}', '{!formBid.Name}', '{!If(bidParentSObject = 'Ground', formBid.GT__c, If(bidParentSObject = 'Freight', formBid.Freight__c, If(bidParentSObject = 'Air', formBid.Air__c, '')))}', '{!If(bidParentSObject = 'Ground', formBid.GT__r.Name, If(bidParentSObject = 'Freight', formBid.Freight__r.Name, If(bidParentSObject = 'Air', formBid.Air__r.Name, '')))}', '{!JSENCODE(bidAgreement_congaQueriesJson)}', '{!bidAgreement_congaSignTemplateId}', '{!JSENCODE(emailResult)}');">
        <apex:param assignTo="{!form_to}" name="form_to" value="" />
        <apex:param assignTo="{!form_cc}" name="form_cc" value="" />
        <apex:param assignTo="{!form_bcc}" name="form_bcc" value="" />
        <apex:param assignTo="{!draft.Body__c}" name="bidAgreement_message" value="" />
        <apex:param assignTo="{!draft.Terms__c}" name="bidAgreement_terms" value="" />
        <apex:param assignTo="{!isCongaSignSent}" name="isCongaSignSent" value="false"/>
    </apex:actionFunction>
    <apex:actionFunction action="{!deactivateBidAgreement}" name="deactivateBidAgreementJs" status="loading" reRender="contractForms" oncomplete="closeModal('myGroundModalForm');"/>
    <apex:actionFunction name="changeContactDataJs" action="{!searchContactData}" status="loading" reRender="emailConfirmationDataContactPanel, bidAgreementToPanel" oncomplete="$('input[id$=emailconfirmation_to]').val('');">
        <apex:param assignTo="{!draft.Production_Assoc_Type__c}" name="chkContactSelected" value="" />
    </apex:actionFunction>
    <apex:actionFunction name="changeContactDataSelectedJs" action="{!changeContactDataSelected}" status="loading" reRender="bidAgreementToPanel, bidAgreement_salutation">
        <apex:param assignTo="{!draft.Production_Assoc_Type__c}" name="chkContactSelected" value="" />
        <apex:param assignTo="{!draft.Production_Assoc_Contact_Id__c}" name="recordContactSelected" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!sendEmail}" name="sendEmailJs" status="loading" reRender="myGroundModalContent" oncomplete="emailMessage();">
        <apex:param assignTo="{!form_to}" name="form_to" value="" />
        <apex:param assignTo="{!form_cc}" name="form_cc" value="" />
        <apex:param assignTo="{!form_bcc}" name="form_bcc" value="" />
        <apex:param assignTo="{!form_subject}" name="form_subject" value="" />
        <apex:param assignTo="{!form_body}" name="form_body" value="" />
        <apex:param assignTo="{!form_attachs}" name="form_attachs" value="" />
        <!--Fix By Clay 29 Dec, 2020 -->
        <apex:param assignTo="{!form_closing}" name="form_closing" value="" />
    </apex:actionFunction>
    <!-- End BidAgreement -->
    <!-- Final Choice -->
    <apex:actionFunction action="{!openPreviewFinalTicketedConfirmation}" name="openPreviewFinalTicketedConfirmationJs" status="loading" reRender="noneRender" oncomplete="congaPreview('{!formBid.Id}', '{!formBid.Name}', '{!formBid.Air__c}', '{!formBid.Air__r.Name}', '{!JSENCODE(bidAgreement_congaQueriesJson)}', '{!bidAgreement_congaTemplateId}')"/>
    <!-- End Final Choice -->
    <!-- Attach GCQ -->
    <apex:actionFunction name="openAttachGcqJs" action="{!openAttachGcq}" status="loading" reRender="myModalAttachGCQ" oncomplete="setupAttachGcq();openModal('myModalAttachGCQ');"/>
    <apex:actionFunction name="searchAttachGcqJs" action="{!searchAttachGcq}" status="loading" reRender="gcqsSection"/>
    <!-- End Attach GCQ -->
    <!-- Attachs -->
    <apex:actionFunction action="{!openAttachDocs}" name="openAttachDocsJs" status="loading" reRender="myModalAttachDocuments" oncomplete="openModal('myModalAttachDocuments');">
        <apex:param assignTo="{!attachdocument_objectid}" name="attachdocument_objectid" value="" />
    </apex:actionFunction>
    <apex:actionFunction action="{!doAttachmentLast}" name="passToControllerLast" status="loading" reRender="newAttachmentPanel,newAirAttachmentPanel,documentsHousingPanel,documentsBidContracted,documentsBidPanel" oncomplete="setDataToSelect()">
        <apex:param assignTo="{!filename}" name="filename" value="" />
        <apex:param assignTo="{!documentRelationId}" name="documentRelationId" value="" />
    </apex:actionFunction>
    <!-- End Attachs -->
    <!-- End Actionfunctions -->
    <script>
    $(document).ready(function() {
        loadFormsJs();
    });
    function hideCK(){
        //alert('Trying to hide all ckedito');
        $( "[id*='form_body_new']" ).hide();
    }
    function changeAttentionForm(){                                                                 //Changes Added as per 175349270
        changeAttentionFormJs();
    }
    function newFormGCIPTask(){                                                                  //Changes Added as per 175349270
        $(".new-form-gcip-task").css('display','');
    }
    function cancelFormGCIPTask(){                                                          //Changes Added as per 175349270
        $(".new-form-gcip-task").css('display','none');
    }
    function openForm(parentSObject,formLabel,formValue,draftCode) {
        openFormJs(formLabel,formValue,draftCode);
    }
    function changeContactDataSelected(){
        var radioValue = $('input[name$=options_emailc]:checked').val();
        var selected = $('select[id$=emailconfirmation_select]').val();
        changeContactDataSelectedJs(radioValue,selected);
    }
    function changeContactData(val){
        var radioValue = $('input[name$=options_emailc]:checked').val();
        changeContactDataJs(radioValue);
    }
    function saveBidAgreement() {
        var message = '';
        for(instance in CKEDITOR.instances) if(instance.includes('bidAgreement_message') || instance.includes('bidSendConfirmation_message')) message = CKEDITOR.instances[instance].getData();
        var terms = '';
        for(instance in CKEDITOR.instances) if(instance.includes('bidAgreement_terms') || instance.includes('bidSendConfirmation_message')) terms = CKEDITOR.instances[instance].getData();
        saveBidAgreementJs(message, terms);
    }
    function saveBidAgreementMessage(){
        $("span#saveBidAgreementMessage").show();
        setTimeout(function(){$('span#saveBidAgreementMessage').fadeOut('slow');}, 2000);
    }
    function deactivateBidAgreement() {
        if(confirm("Are you sure you want to deactivate this contract?")) deactivateBidAgreementJs();
    }
    function setupForm(){
        $('#myGroundModalForm input.cc-email-bidAgreement').autocomplete({
            lookup: function (query, done){
                Visualforce.remoting.Manager.invokeAction(
                    '{!$RemoteAction.Dashboard_Tab_Contract_Forms.searchContactEmail}',query,
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
        $('#myGroundModalForm input.bcc-email-bidAgreement').autocomplete({
            lookup: function (query, done){
                Visualforce.remoting.Manager.invokeAction(
                    '{!$RemoteAction.Dashboard_Tab_Contract_Forms.searchContactEmail}',query,
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
        if($('div[id$=bidAgreementModal] .modal-title').text() == 'Email Confirmation'){
            if($('input[id$=emailconfirmation_type]').val() == 'production_contacts') $('input[id$=searchByProductionContacts]').attr('checked', true);
            else $('input[id$=searchByGTCoordinators]').attr('checked', true);
        }
    }
    //Email Inputs
    function addCCEmail(e, input){
        $(input).removeClass('error-custom');
        if (e.keyCode == 13 || e.keyCode == 32) {
            console.log('e.keyCode: ' + e.keyCode);
            var getValue = $(input).val();
            if(validateEmail(getValue)) {
                $(input).prev('.all-cc-email-bidAgreement').append('<span class="email-ids">'+ getValue +' <span class="cancel-email" onclick="cancelEmail(this)">x</span></span>');
                $(input).val('');
            }else{
                $(input).addClass('error-custom');
            }
        }
    }
    function addBCCEmail(e, input){
        $(input).removeClass('error-custom');
        if (e.keyCode == 13 || e.keyCode == 32) {
            var getValue = $(input).val();
            if(validateEmail(getValue)) {
                $(input).prev('.all-bcc-email-bidAgreement').append('<span class="email-ids">'+ getValue +' <span class="cancel-email" onclick="cancelEmail(this)">x</span></span>');
                $(input).val('');
            }else{
                $(input).addClass('error-custom');
            }
        }
    }
    function validateEmail(email) {
        var re = /^(([^<>()\[\]\.,;:\s@"]+(\.[^<>()\[\]\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
        return re.test(String(email).toLowerCase());
    }
    function cancelEmail(span){
        $(span).parents('.email-ids').remove();
    }
    //End Email Inputs
    //Attach GCQ
    function setupAttachGcq(){
        var dateFormat = $('input[id$=gcq_user]').val() == 'RRE' ? 'DD-MMM-YYYY' : 'MMM-DD-YYYY';
        $('input[id$=attachGcq_startDateInput], input[id$=attachGcq_endDateInput]').datetimepicker({
            format: dateFormat,
            useCurrent: false
        });
    }
    function searchAttachGcq(){
        var dateFormat = $('input[id$=gcq_user]').val() == 'RRE' ? 'DD-MMM-YYYY' : 'MMM-DD-YYYY';
        var dates = validateDatesAttachGcq(new Array($('input[id$=attachGcq_startDateInput]'), $('input[id$=attachGcq_endDateInput]')));
        if(dates){
            $('input[id$=attachGcq_startDate]').val(moment($('input[id$=attachGcq_startDateInput]').val(), dateFormat).format('YYYY-MM-DD'));
            $('input[id$=attachGcq_endDate]').val(moment($('input[id$=attachGcq_endDateInput]').val(), dateFormat).format('YYYY-MM-DD'));
            searchAttachGcqJs();
        } 
    }
    function clearAttachGcq(){
        $('input[id$=attachGcq_startDateInput]').val(null);
        $('input[id$=attachGcq_startDate]').val(null);
        $('input[id$=attachGcq_endDateInput]').val(null);
        $('input[id$=attachGcq_endDate]').val(null);
        $('.attachGCQModal .form-group').removeClass("has-error");
        $('.attachGCQModal .form-group span.text-danger').hide();
    }
    function validateDatesAttachGcq(inputs){
        var result = true;
        var dateFormat = $('input[id$=gcq_user]').val() == 'RRE' ? 'DD-MMM-YYYY' : 'MMM-DD-YYYY';
        inputs.forEach(function(input, index){
            if($(input).val().trim() == ""){
                $(input).parents(".form-group").addClass("has-error");
                if(index == 0) $(input).parents(".form-group").find("span.text-danger").text('Please specify start date');
                $(input).parents(".form-group").find("span.text-danger").show();
                result = false;
            }
            else{
                $(input).parents(".form-group").removeClass("has-error");
                $(input).parents(".form-group").find("span.text-danger").hide();
            }
        }); 
        if(!result) return false;
        if(inputs.length == 2){
            if(!moment($(inputs[0]).val(), dateFormat).isSameOrBefore($(inputs[1]).val())){
                $(inputs[0]).parents(".form-group").addClass("has-error");
                $(inputs[0]).parents(".form-group").find("span.text-danger").text('Start Date cannot be greater than End Date').show();
                return false;
            }
            else{
                $(inputs[0]).parents(".form-group").removeClass("has-error");
                $(inputs[0]).parents(".form-group").find("span.text-danger").hide();
            }
        }
        return true;
    }
    function selectGcq(tr){
        $(tr).parents('tbody').children('tr').each(function(){
            if($(this).hasClass("gcqSelected")) $(this).removeClass("gcqSelected");
        });
        $(tr).addClass("gcqSelected");
    }
    function attachGcq(tr){
        var tripId = bidId = gcqId = gcqName = '';
        $('div[id$=gcqsSection] tbody>tr.gcqSelected').each(function(){
            tripId = $(this).data('tripid');
            bidId = $(this).data('bidid');
            gcqId = $(this).data('gcqid');
            gcqName = $(this).data('gcqname');
        });
        if(gcqId.trim() != ''){
            $('select[id$=bidAgreement_attachs] > option.attachedGcq').remove();
            $('select[id$=bidAgreement_attachs]').append('<option value="" class="attachedGcq" data-tripid="' + tripId + '" data-bidid="' + bidId + '" data-gcqid="' + gcqId + '">' + ($('input[id$=bidParentSObjectInput]').val() == "Ground" ? 'GT' : $('input[id$=bidParentSObjectInput]').val()) + ' Email Confirmation-'+ gcqName +'</option>');
            closeModal('myModalAttachGCQ');
        } 
        else{
            if($('input[id$=bidParentSObjectInput]').val() == "Ground" || $('input[id$=bidParentSObjectInput]').val() == "Freight"){
                $(".attachGCQModal span#bottomGcqMessage").show();
                setTimeout(function(){$('.attachGCQModal span#bottomGcqMessage').fadeOut('slow');}, 2000);
            }
            else if($('input[id$=bidParentSObjectInput]').val() == "Air"){
                $(".attachGCQModal span#topGcqMessage").show();
                setTimeout(function(){$('.attachGCQModal span#topGcqMessage').fadeOut('slow');}, 2000);
            }
        }
    }
    //End Attach GCQ
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
        fileData = $('input[id$=fileBidAgreement]').val()        
        $('input[id$=attachment_new_charge]').val(charge);
        var pieces = fileData.split('\');
        var filename = pieces[pieces.length-1];
        var fileBlob = $('input[id$=output]').val();
        passToControllerLast(filename,recordId);
    }
    function openAttachDocs(typez,object_id,modal_parent) {
        $('#'+modal_parent).css('z-index','1039');
        openAttachDocsJs(object_id);
    }
    function selectAttachDocument(modal_parent, modal_select) {
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
            $('input[id$=document-attach-ids]').val(document_ids);
            $('input[id$=document-attach-names]').val(document_names);
            for(x=0; x < document_ids.length; x++){
                $('select[id$='+modal_select+']').append('<option value="'+document_ids[x]+'">' + document_names[x] +'</option>');
            }
            
            viewModalIndex(modal_parent);
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
    //Send Email
    function sendEmail(){
    /** Fix By Clay 28 Dec, 2020
        var emailTo = '';
        emailTo = $('div[id$=bidAgreementModal] .modal-title').text() == 'Email Confirmation' ? $('select[id$=emailconfirmation_select]').val() : $('input[id$=bidParentSObjectInput]').val() == "Air" ? $('select[id$=ContactSelect]').val() : $('select[id$=bidAgreementAttentionContactSelect]').val();
        var cc_emails = '';
        $(".all-cc-email-bidAgreement span.email-ids").each(function(){
            cc_emails = cc_emails.trim() != "" ? cc_emails + ',' + $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','') : $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','');
        });
        var bcc_emails = '';
        $(".all-bcc-email-bidAgreement span.email-ids").each(function(){
            bcc_emails = bcc_emails.trim() != "" ? bcc_emails + ',' + $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','') : $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','');
        });
        var subject = $('input[id$=bidAgreement_subject]').val();
        var emailBody = '';
        for(instance in CKEDITOR.instances ) if(instance.includes('bidAgreement_message') || instance.includes('bidSendConfirmation_message')) emailBody = ($('input[id$=bidParentSObjectInput]').val() == "Air" && $('input[id$=bidAgreement_salutation]').val() != null && $('input[id$=bidAgreement_salutation]').val().trim() != '' ? $('input[id$=bidAgreement_salutation]').val() + '<br/>' : '') + CKEDITOR.instances[instance].getData();
        var attachments = '';
        $("select[id$=bidAgreement_attachs] option").each(function(){
            attachments = attachments.trim() != "" ? attachments + ',' + $(this).val() : $(this).val();
        });
        if(emailTo.trim() == "") alert('Enter the recipient email.');
        else sendEmailJs(emailTo, cc_emails, bcc_emails, subject, emailBody, attachments);**/
        var emailTo = '';
        emailTo = $('div[id$=bidAgreementModal] .modal-title').text() == 'Email Confirmation' ? $('select[id$=emailconfirmation_select]').val() : $('input[id$=bidParentSObjectInput]').val() == "Air" ? $('select[id$=ContactSelect]').val() : $('select[id$=bidAgreementAttentionContactSelect]').val();
        var cc_emails = '';
        
        if(!emailTo || emailTo == null || emailTo.trim() == '') {
            emailTo = $(".form-to").text();
        }
        $(".cc-email-form").each(function(){
            cc_emails = cc_emails.trim() != "" ? cc_emails + ',' + $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','') : $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','');
        });
        var bcc_emails = '';
        $(".bcc-email-form").each(function(){
            bcc_emails = bcc_emails.trim() != "" ? bcc_emails + ',' + $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','') : $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','');
        });
        var subject = $('input[id$=form_subject]').val();
        var emailBody = '';
        var salutation;
        if($('input[id$=bidParentSObjectInput]').val() == "Ground") {
            salutation = $('input[id$=form_salutation]').val();
        } else if($('input[id$=bidParentSObjectInput]').val() == "Air") {
            salutation = $('input[id$=bidAgreement_salutation]').val();
        }
        if(salutation != null && salutation.trim() != '') {
            emailBody = salutation + '<br/>';
        }
        for(instance in CKEDITOR.instances ) {
            if(instance.includes('bidAgreement_message') || instance.includes('bidSendConfirmation_message') || instance.includes('form_body')) {
                emailBody += CKEDITOR.instances[instance].getData();
            }
        }
        var formClosing = $('textarea[id$=form_gaurantee]').val();
           
        var attachments = '';
        $("select[id$=bidAgreement_attachs] option").each(function(){
            attachments = attachments.trim() != "" ? attachments + ',' + $(this).val() : $(this).val();
        });

        if(!emailTo || emailTo.trim() == "") alert('Enter the recipient email.');
        else sendEmailJs(emailTo, cc_emails, bcc_emails, subject, emailBody, attachments, formClosing);
    }
    function emailMessage() {
        alert('Email has been sent successfully.');
        closeBidAgreementJs('false');
    }
    /*---@Conga: Update for Conga---*/
    function congaPreviewHandler() {
        var message = '';
        for(instance in CKEDITOR.instances) if(instance.includes('bidAgreement_message') || instance.includes('bidSendConfirmation_message')) message = CKEDITOR.instances[instance].getData();
        var terms = '';
        for(instance in CKEDITOR.instances) if(instance.includes('bidAgreement_terms') || instance.includes('bidSendConfirmation_message')) terms = CKEDITOR.instances[instance].getData();
        congaPreviewJs(message, terms);
    }
    function congaPreview(bidId, bidName, tripId, tripName, congaQueriesJson, congaTemplateId) {
        var primary_contact = $('div[id$=bidAgreementModal] .modal-title').text() == 'Rate Agreement' ? $('select[id$=bidAgreementContactSelect]').val() : $('div[id$=bidAgreementModal] .modal-title').text() == 'Trip Details Update' ? $('select[id$=bidAgreementAttentionContactSelect]').val() : $('div[id$=bidAgreementModal] .modal-title').text() == 'Transportation Contract' ? $('select[id$=bidAgreementContactSelect]').val() : '';
        var client_contact = $('select[id$=bidAgreementProductionAssociationContactsSelect]').val();
        var congaQueriesMap = JSON.parse(congaQueriesJson);
        if($('input[id$=bidParentSObjectInput]').val() == "Ground"){
            if($('div[id$=bidAgreementModal] .modal-title').text() == 'Rate Agreement') window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('GT - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['GT - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&OFN=GT+Rate+Agreement-' + tripName + '&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=800, resizable=yes, toolbar=no, location=no, status=yes');
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Trip Details Update') window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&OFN=GT+Trip+Details+Update-' + tripName + '&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=800, resizable=yes, toolbar=no, location=no, status=yes');
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Transportation Contract') window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('GT - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['GT - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&OFN=GT+Transportation+Contract-' + tripName + '&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=800, resizable=yes, toolbar=no, location=no, status=yes');
        }
        else if($('input[id$=bidParentSObjectInput]').val() == "Freight"){
            if($('div[id$=bidAgreementModal] .modal-title').text() == 'Rate Agreement') window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('Freight - ContactById') ? ',[Contact]' + congaQueriesMap['Freight - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('Freight - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['Freight - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&OFN=Freight+Rate+Agreement-' + tripName + '&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=800, resizable=yes, toolbar=no, location=no, status=yes');
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Trip Details Update') window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('Freight - ContactById') ? ',[Contact]' + congaQueriesMap['Freight - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&OFN=Freight+Trip+Details+Update-' + tripName + '&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=800, resizable=yes, toolbar=no, location=no, status=yes');
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Transportation Contract') window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('Freight - ContactById') ? ',[Contact]' + congaQueriesMap['Freight - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('Freight - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['Freight - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&OFN=Freight+Transportation+Contract-' + tripName + '&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=800, resizable=yes, toolbar=no, location=no, status=yes');
        }
        else if($('input[id$=bidParentSObjectInput]').val() == "Air"){
            if($('div[id$=bidAgreementModal] .modal-title').text() == 'Final Choice') window.open('/apex/APXTConga4__Conga_Composer?id=' + tripId + (congaQueriesMap.hasOwnProperty('Air - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Air - BidById'].Id + '?pv0=' + bidId : '') + '&TemplateId=' + congaTemplateId + '&OFN=Final+Choice-' + tripName + '&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Ticketed Confirmation') window.open('/apex/APXTConga4__Conga_Composer?id=' + tripId + (congaQueriesMap.hasOwnProperty('Air - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Air - BidById'].Id + '?pv0=' + bidId : '') + '&TemplateId=' + congaTemplateId + '&OFN=Ticketed+Confirmation-' + tripName + '&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
        }
    }
    function congaPreviewGCQ(congaQueriesJson, congaTemplateId){ 
        var tripId = bidId = gcqId = gcqName = '';
        $('div[id$=gcqsSection] tbody>tr.gcqSelected').each(function(){
            tripId = $(this).data('tripid');
            bidId = $(this).data('bidid');
            gcqId = $(this).data('gcqid');
            gcqName = $(this).data('gcqname');
        });
        if(gcqId.trim() != ''){
            var congaQueriesMap = JSON.parse(congaQueriesJson);
            if($('input[id$=bidParentSObjectInput]').val() == "Ground") window.open('/apex/APXTConga4__Conga_Composer?id=' + tripId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByGCQId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByGCQId'].Id + '?pv0=' + gcqId : '') + (congaQueriesMap.hasOwnProperty('GT - GCQById') ? ',[GCQ]' + congaQueriesMap['GT - GCQById'].Id + '?pv0=' + gcqId : '') : '') + '&TemplateId=' + congaTemplateId + '&OFN=GT+Email+Confirmation-'+ gcqName +'&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=800, resizable=yes, toolbar=no, location=no, status=yes');            
            else if($('input[id$=bidParentSObjectInput]').val() == "Freight") window.open('/apex/APXTConga4__Conga_Composer?id=' + tripId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - SubTripsByFCQId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByFCQId'].Id + '?pv0=' + gcqId : '') + (congaQueriesMap.hasOwnProperty('Freight - FCQById') ? ',[GCQ]' + congaQueriesMap['Freight - FCQById'].Id + '?pv0=' + gcqId : '') : '') + '&TemplateId=' + congaTemplateId + '&OFN=Freight+Email+Confirmation-'+ gcqName +'&DS7=3&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=800, resizable=yes, toolbar=no, location=no, status=yes');
        } 
        else{
            $(".attachGCQModal span#gcqMessage").show();
            setTimeout(function(){$('.attachGCQModal span#gcqMessage').fadeOut('slow');}, 2000);
        }
    }
    function congaSendHandler(){
        var message = '';
        for(instance in CKEDITOR.instances) if(instance.includes('bidAgreement_message') || instance.includes('bidSendConfirmation_message') || instance.includes('form_body')) message = CKEDITOR.instances[instance].getData();
        var terms = '';
        for(instance in CKEDITOR.instances) if(instance.includes('bidAgreement_terms') || instance.includes('bidSendConfirmation_message')) terms = CKEDITOR.instances[instance].getData();
        var gcqId = '';
        if($('input[id$=bidParentSObjectInput]').val() == "Air"){
            if($('div[id$=bidAgreementModal] .modal-title').text() == 'Final Air Confirmation'){
                $('select[id$=bidAgreement_attachs] > option.attachedGcq').each(function(){
                    gcqId = $(this).data('gcqid');
                });
            }
        }
        congaSendJs(message, terms, gcqId);
    }
    function congaSend(bidId, bidName, tripId, tripName, congaQueriesJson, congaEmailTemplateId, congaTemplateId){
        /*
        alert('bidId'+bidId);
        alert('bidName'+bidName);
        alert('tripId'+tripId);
        alert('tripName'+tripName);
        alert('congaQueriesJson'+congaQueriesJson);
        alert('congaEmailTemplateId'+congaEmailTemplateId);
        alert('congaTemplateId'+congaTemplateId);
        congaEmailTemplateId = 'a0T56000000oWONEA2';
        congaTemplateId = 'a0c56000001KqBMAA0';
        */
        var primary_contact = $('div[id$=bidAgreementModal] .modal-title').text() == 'Rate Agreement' || $('div[id$=bidAgreementModal] .modal-title').text() == 'Transportation Contract' ? $('select[id$=bidAgreementContactSelect]').val() : $('div[id$=bidAgreementModal] .modal-title').text() == 'Email Confirmation' ? $('select[id$=emailconfirmation_select]').val() : $('div[id$=bidAgreementModal] .modal-title').text() == 'Trip Details Update' || $('div[id$=bidAgreementModal] .modal-title').text() == 'Counter Needed' ? $('select[id$=bidAgreementAttentionContactSelect]').val() : $('div[id$=bidAgreementModal] .modal-title').text() == 'Contract To Client' || $('div[id$=bidAgreementModal] .modal-title').text() == 'Final Contract' ? $('select[id$=bidAgreementAttentionProductionAssociationContactsSelect]').val() : $('div[id$=bidAgreementModal] .modal-title').text() == 'Final Choice' || $('div[id$=bidAgreementModal] .modal-title').text() == 'Ticketed Confirmation' || $('div[id$=bidAgreementModal] .modal-title').text() == 'Final Air Confirmation' ? $('select[id$=airbidAgreementProductionAssociationContactSelect]').val() : '';
        var primary_contactName = $('div[id$=bidAgreementModal] .modal-title').text() == 'Rate Agreement' || $('div[id$=bidAgreementModal] .modal-title').text() == 'Transportation Contract' ? $('select[id$=bidAgreementContactSelect]').children("option:selected").text() : $('div[id$=bidAgreementModal] .modal-title').text() == 'Email Confirmation' ? $('input[id$=bidAgreement_to_name]').val() : $('div[id$=bidAgreementModal] .modal-title').text() == 'Trip Details Update' || $('div[id$=bidAgreementModal] .modal-title').text() == 'Counter Needed' ? $('select[id$=bidAgreementAttentionContactSelect]').children("option:selected").text() : $('div[id$=bidAgreementModal] .modal-title').text() == 'Contract To Client' || $('div[id$=bidAgreementModal] .modal-title').text() == 'Final Contract' ? $('select[id$=bidAgreementAttentionProductionAssociationContactsSelect]').children("option:selected").text() : $('div[id$=bidAgreementModal] .modal-title').text() == 'Final Choice' || $('div[id$=bidAgreementModal] .modal-title').text() == 'Ticketed Confirmation' || $('div[id$=bidAgreementModal] .modal-title').text() == 'Final Air Confirmation' ? $('select[id$=airbidAgreementProductionAssociationContactSelect]').children("option:selected").text() : '';
        var primary_contactEmail = $('#bidAgreement_primarycontactemail>input').val();
        var client_contact = $('select[id$=bidAgreementProductionAssociationContactsSelect]').val();
        var congaEmailSubject = $('input[id$=bidAgreement_subject]').val();
        var cc_emails = '';
        $(".all-cc-email-bidAgreement span.email-ids").each(function(){
            cc_emails = cc_emails.trim() != "" ? cc_emails + ',' + $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','') : $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','');
        });
        var bcc_emails = '';
        $(".all-bcc-email-bidAgreement span.email-ids").each(function(){
            bcc_emails = bcc_emails.trim() != "" ? bcc_emails + ',' + $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','') : $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','');
        });
        var attachments = '';
        $("select[id$=bidAgreement_attachs] option").each(function(){
            if($(this).val().trim() != '') attachments = attachments.trim() != "" ? attachments + ',' + $(this).val() : $(this).val();
        });
        var updates;
        var congaQueriesMap = JSON.parse(congaQueriesJson);
        if($('input[id$=bidParentSObjectInput]').val() == "Ground"){
            if($('div[id$=bidAgreementModal] .modal-title').text() == 'Rate Agreement'){
                updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Rate_Agreement_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Rate Agreement email was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('GT - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['GT - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=GT+Rate+Agreement-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Trip Details Update'){
                updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Trip_Details_Update_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Trip Details Update was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=GT+Trip+Details+Update-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Transportation Contract'){
                updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Transportation_Contract_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Transportation Contract was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('GT - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['GT - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=GT+Transportation+Contract-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Contract To Client'){
                updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Contract_to_Client_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Contract To Client was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=GT+Contract+To+Client-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Counter Needed'){
                updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Counter_Needed_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Counter Needed was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=GT+Counter+Needed-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Final Contract'){
                updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Final_Contract_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Final Contract was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=GT+Final+Contract-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Email Confirmation'){
                var gcqId = ofn = '';
                $('select[id$=bidAgreement_attachs] > option.attachedGcq').each(function(){
                    tripId = $(this).data('tripid');
                    bidId = $(this).data('bidid');
                    gcqId = $(this).data('gcqid');
                    ofn = $(this).text();
                });
                updates = '&UF0=1' + ($('input[name$=options_emailc]:checked').val() == 'production_contacts' ? '&MFTSId0=' + bidId + '&MFTS0=Email_Confirmation_Last_Send_Date__c&MFTSValue0=Now' : '') + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Email Confirmation was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + tripId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (gcqId.trim() != '' ? (congaQueriesMap.hasOwnProperty('GT - SubTripsByGCQId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByGCQId'].Id + '?pv0=' + gcqId : '') + (congaQueriesMap.hasOwnProperty('GT - GCQById') ? ',[GCQ]' + congaQueriesMap['GT - GCQById'].Id + '?pv0=' + gcqId : '') + '&TemplateId=' + congaTemplateId : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + updates + (gcqId.trim() != '' ? '&OFN=' + ofn : '') + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            }
        }
        else if($('input[id$=bidParentSObjectInput]').val() == "Freight"){
            if($('div[id$=bidAgreementModal] .modal-title').text() == 'Rate Agreement'){
                updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Rate_Agreement_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Rate Agreement email was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('Freight - ContactById') ? ',[Contact]' + congaQueriesMap['Freight - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('Freight - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['Freight - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=Freight+Rate+Agreement-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Trip Details Update'){
                updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Trip_Details_Update_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Trip Details Update was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('Freight - ContactById') ? ',[Contact]' + congaQueriesMap['Freight - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=Freight+Trip+Details+Update-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Transportation Contract'){
                updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Transportation_Contract_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Transportation Contract was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('Freight - ContactById') ? ',[Contact]' + congaQueriesMap['Freight - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('Freight - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['Freight - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=Freight+Transportation+Contract-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Contract To Client'){
                updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Contract_to_Client_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Contract To Client was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('Freight - ContactById') ? ',[Contact]' + congaQueriesMap['Freight - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=Freight+Contract+To+Client-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Counter Needed'){
                updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Counter_Needed_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Counter Needed was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('Freight - ContactById') ? ',[Contact]' + congaQueriesMap['Freight - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=Freight+Counter+Needed-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Final Contract'){
                updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Final_Contract_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Final Contract was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('Freight - ContactById') ? ',[Contact]' + congaQueriesMap['Freight - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=Freight+Final+Contract-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Email Confirmation'){
                var gcqId = ofn = '';
                var actualBidId = bidId;
                $('select[id$=bidAgreement_attachs] > option.attachedGcq').each(function(){
                    tripId = $(this).data('tripid');
                    bidId = $(this).data('bidid');
                    gcqId = $(this).data('gcqid');
                    ofn = $(this).text();
                });
                updates = '&UF0=1' + ($('input[name$=options_emailc]:checked').val() == 'production_contacts' ? '&MFTSId0=' + actualBidId + '&MFTS0=Email_Confirmation_Last_Send_Date__c&MFTSValue0=Now' : '') + '&MFTSId1=' + actualBidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + actualBidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Email Confirmation was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + tripId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (gcqId.trim() != '' ? (congaQueriesMap.hasOwnProperty('Freight - SubTripsByFCQId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByFCQId'].Id + '?pv0=' + gcqId : '') + (congaQueriesMap.hasOwnProperty('Freight - FCQById') ? ',[GCQ]' + congaQueriesMap['Freight - FCQById'].Id + '?pv0=' + gcqId : '') + '&TemplateId=' + congaTemplateId : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + updates + (gcqId.trim() != '' ? '&OFN=' + ofn : '') + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            }
        }
        else if($('input[id$=bidParentSObjectInput]').val() == "Air"){
            if($('div[id$=bidAgreementModal] .modal-title').text() == 'Final Choice'){
                updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Final_Choice_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Final Choice email was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + tripId + (congaQueriesMap.hasOwnProperty('Air - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Air - BidById'].Id + '?pv0=' + bidId : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=Final+Choice-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1&SC0=1&SC1=SalesforceFile', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Ticketed Confirmation'){
                updates = '&UF0=1&MFTSId0=' + bidId + '&MFTS0=Ticketed_Confirmation_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + bidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + bidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Ticketed Confirmation email was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + tripId + (congaQueriesMap.hasOwnProperty('Air - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Air - BidById'].Id + '?pv0=' + bidId : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + '&TemplateId=' + congaTemplateId + updates + '&OFN=Ticketed+Confirmation-' + tripName + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1&SC0=1&SC1=SalesforceFile', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Final Air Confirmation'){
                var gcqId = ofn = '';
                var actualBidId = bidId;
                $('select[id$=bidAgreement_attachs] > option.attachedGcq').each(function(){
                    bidId = $(this).data('bidid');
                    gcqId = $(this).data('gcqid');
                    ofn = $(this).text();
                });
                updates = '&UF0=1&MFTSId0=' + actualBidId + '&MFTS0=Final_Air_Confirmation_Last_Send_Date__c&MFTSValue0=Now' + '&MFTSId1=' + actualBidId + '&MFTS1=New_Journal_RecordType__c&MFTSValue1=' + $("input[id$=bidJournal_recordtype]").val() + '&MFTSId2=' + actualBidId + '&MFTS2=New_Journal_Entry__c&MFTSValue2=' + 'Final Air Confirmation was sent to ' + primary_contactName + ' ' + primary_contactEmail + (cc_emails != '' ? ', cc: ' + cc_emails : '') + (bcc_emails != '' ? ', bcc: ' + bcc_emails : '');
                window.open('/apex/APXTConga4__Conga_Composer?id=' + tripId + (congaQueriesMap.hasOwnProperty('Air - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Air - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Air - GCQById') && gcqId.trim() != '' ? ',[Gcq]' + congaQueriesMap['Air - GCQById'].Id + '?pv0=' + gcqId + '&TemplateId=' + congaTemplateId + '&OFN=' + ofn : '') : '') + '&CongaEmailTemplateId=' + congaEmailTemplateId + '&EmailSubject=' + congaEmailSubject + ($('input[id$=bidAgreement_congaEmailFromId]').val().trim() != '' ? '&EmailFromID=' + $('input[id$=bidAgreement_congaEmailFromId]').val() : '') + '&EmailToId=' + primary_contact + '&EmailCC=' + cc_emails + '&EmailBCC=' + bcc_emails + '&AttachmentID=' + attachments + updates + '&DS7=2&APDF=0&ZipFiles=0&DefaultPDF=1&SC0=1&SC1=SalesforceFile', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=850, resizable=yes, toolbar=no, location=no, status=yes');
            }
        }
    }
    function congaSignHandler(){
        var primary_contactEmail = $('#bidAgreement_primarycontactemail>input').val();
        var cc_emails = '';
        $(".all-cc-email-bidAgreement span.email-ids").each(function(){
            cc_emails = cc_emails.trim() != "" ? cc_emails + ',' + $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','') : $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','');
        });
        var bcc_emails = '';
        $(".all-bcc-email-bidAgreement span.email-ids").each(function(){
            bcc_emails = bcc_emails.trim() != "" ? bcc_emails + ',' + $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','') : $(this).html().replace(' <span class="cancel-email" onclick="cancelEmail(this)">x</span>','');
        });
        var message = '';
        for(instance in CKEDITOR.instances) if(instance.includes('bidAgreement_message') || instance.includes('bidSendConfirmation_message')) message = CKEDITOR.instances[instance].getData();
        var terms = '';
        for(instance in CKEDITOR.instances) if(instance.includes('bidAgreement_terms') || instance.includes('bidSendConfirmation_message')) terms = CKEDITOR.instances[instance].getData();
        if($('input[id$=bidParentSObjectInput]').val() == "Ground"){
            if($('div[id$=bidAgreementModal] .modal-title').text() == 'Rate Agreement'){
                if(confirm('An email will be sent before initiating the Conga Sign Process')){
                    if(primary_contactEmail.trim() != "") congaSignJs(primary_contactEmail, cc_emails, bcc_emails, message, terms, true);
                    else alert("Please you must select a vendor contact.");
                } 
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Trip Details Update'){
                if(primary_contactEmail.trim() != "") congaSignJs(primary_contactEmail, cc_emails, bcc_emails, message, terms, false);
                else alert("Please you must select a vendor contact.");
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Transportation Contract'){
                if(confirm('An email will be sent before initiating the Conga Sign Process')){
                    if(primary_contactEmail.trim() != "") congaSignJs(primary_contactEmail, cc_emails, bcc_emails, message, terms, true);
                    else alert("Please you must select a vendor contact.");
                } 
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Contract To Client'){
                if(confirm('An email will be sent before initiating the Conga Sign Process')){
                    if(primary_contactEmail.trim() != "") congaSignJs(primary_contactEmail, cc_emails, bcc_emails, message, terms, true);
                    else alert("Please you must select a vendor contact.");
                }
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Counter Needed'){
                if(primary_contactEmail.trim() != "") congaSignJs(primary_contactEmail, cc_emails, bcc_emails, message, terms, false);
                else alert("Please you must select a vendor contact.");
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Final Contract'){
                if(primary_contactEmail.trim() != "") congaSignJs(primary_contactEmail, cc_emails, bcc_emails, message, terms, false);
                else alert("Please you must select a vendor contact.");
            } 
        }
        else if($('input[id$=bidParentSObjectInput]').val() == "Freight"){
            if($('div[id$=bidAgreementModal] .modal-title').text() == 'Rate Agreement'){
                if(confirm('An email will be sent before initiating the Conga Sign Process')){
                    if(primary_contactEmail.trim() != "") congaSignJs(primary_contactEmail, cc_emails, bcc_emails, message, terms, true);
                    else alert("Please you must select a vendor contact.");
                } 
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Trip Details Update'){
                if(primary_contactEmail.trim() != "") congaSignJs(primary_contactEmail, cc_emails, bcc_emails, message, terms, false);
                else alert("Please you must select a vendor contact.");
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Transportation Contract'){
                if(confirm('An email will be sent before initiating the Conga Sign Process')){
                    if(primary_contactEmail.trim() != "") congaSignJs(primary_contactEmail, cc_emails, bcc_emails, message, terms, true);
                    else alert("Please you must select a vendor contact.");
                } 
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Contract To Client'){
                if(confirm('An email will be sent before initiating the Conga Sign Process')){
                    if(primary_contactEmail.trim() != "") congaSignJs(primary_contactEmail, cc_emails, bcc_emails, message, terms, true);
                    else alert("Please you must select a vendor contact.");
                }
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Counter Needed'){
                if(primary_contactEmail.trim() != "") congaSignJs(primary_contactEmail, cc_emails, bcc_emails, message, terms, false);
                else alert("Please you must select a vendor contact.");
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Final Contract'){
                if(primary_contactEmail.trim() != "") congaSignJs(primary_contactEmail, cc_emails, bcc_emails, message, terms, false);
                else alert("Please you must select a vendor contact.");
            } 
        }
        
    }
    function congaSign(bidId, bidName, tripId, tripName, congaQueriesJson, congaTemplateId, emailResult) {
        var primary_contact = $('div[id$=bidAgreementModal] .modal-title').text() == 'Rate Agreement' ? $('select[id$=bidAgreementContactSelect]').val() : $('div[id$=bidAgreementModal] .modal-title').text() == 'Trip Details Update' || $('div[id$=bidAgreementModal] .modal-title').text() == 'Counter Needed' ? $('select[id$=bidAgreementAttentionContactSelect]').val() : $('div[id$=bidAgreementModal] .modal-title').text() == 'Contract To Client' || $('div[id$=bidAgreementModal] .modal-title').text() == 'Final Contract' ? $('select[id$=bidAgreementAttentionProductionAssociationContactsSelect]').val() : $('div[id$=bidAgreementModal] .modal-title').text() == 'Transportation Contract' ? $('select[id$=bidAgreementContactSelect]').val() : '';
        var client_contact = $('select[id$=bidAgreementProductionAssociationContactsSelect]').val();
        var csCCRecipients = '';
        var i;
        if($(".all-bcc-email-bidAgreement span.email-ids").length != 0) alert('BCC emails will not be transferred over to conga sign.');
        if($('input[id$=bidParentSObjectInput]').val() == "Ground"){
            if($('div[id$=bidAgreementModal] .modal-title').text() == 'Rate Agreement'){
                if(emailResult.trim() == ""){
                    i = 2;
                    $(".all-cc-email-bidAgreement span.email-ids").each(function(){
                        csCCRecipients = csCCRecipients.trim() != "" ? csCCRecipients + '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC' : '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC';
                        i++;
                    });
                    var congaQueriesMap = JSON.parse(congaQueriesJson);
                    window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('GT - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['GT - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&CSRecipient1=' + primary_contact + csCCRecipients + '&csvisible=1&CSRoutingType=SERIAL&csRequestReminder=2&OFN=GT+Rate+Agreement-' + tripName + '&DS7=1141&DefaultPDF=1&contentShareType=V&contentVisibility=AllUsers', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=900, resizable=yes, toolbar=no, location=no, status=yes');
                }
                else alert(emailResult);
            }
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Trip Details Update'){
                i = 2;
                $(".all-cc-email-bidAgreement span.email-ids").each(function(){
                    csCCRecipients = csCCRecipients.trim() != "" ? csCCRecipients + '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC' : '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC';
                    i++;
                });
                var congaQueriesMap = JSON.parse(congaQueriesJson);
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&CSRecipient1=' + primary_contact + csCCRecipients + '&csvisible=1&CSRoutingType=SERIAL&csRequestReminder=2&OFN=GT+Trip+Details+Update-' + tripName + '&DS7=1141&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=900, resizable=yes, toolbar=no, location=no, status=yes');                
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Transportation Contract'){
                i = 3;
                $(".all-cc-email-bidAgreement span.email-ids").each(function(){
                    csCCRecipients = csCCRecipients.trim() != "" ? csCCRecipients + '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC' : '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC';
                    i++;
                });
                var congaQueriesMap = JSON.parse(congaQueriesJson);
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('GT - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['GT - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&CSRecipient1=' + primary_contact + csCCRecipients + '&csvisible=1&CSRoutingType=SERIAL&csRequestReminder=2&OFN=GT+Transportation+Contract-' + tripName + '&DS7=1141&DefaultPDF=1&contentShareType=V&contentVisibility=AllUsers', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=900, resizable=yes, toolbar=no, location=no, status=yes');                
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Contract To Client'){
                i = 2;
                $(".all-cc-email-bidAgreement span.email-ids").each(function(){
                    csCCRecipients = csCCRecipients.trim() != "" ? csCCRecipients + '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC' : '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC';
                    i++;
                });
                var congaQueriesMap = JSON.parse(congaQueriesJson);
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&CSRecipient1=' + primary_contact + csCCRecipients + '&csvisible=1&CSRoutingType=SERIAL&csRequestReminder=2&OFN=GT+Contract+To+Client-' + tripName + '&DS7=1141&DefaultPDF=1&contentShareType=V&contentVisibility=AllUsers', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=900, resizable=yes, toolbar=no, location=no, status=yes');                
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Counter Needed'){
                i = 2;
                $(".all-cc-email-bidAgreement span.email-ids").each(function(){
                    csCCRecipients = csCCRecipients.trim() != "" ? csCCRecipients + '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC' : '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC';
                    i++;
                });
                var congaQueriesMap = JSON.parse(congaQueriesJson);
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&CSRecipient1=' + primary_contact + csCCRecipients + '&csvisible=1&CSRoutingType=SERIAL&csRequestReminder=2&OFN=GT+Counter+Needed-' + tripName + '&DS7=1141&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=900, resizable=yes, toolbar=no, location=no, status=yes');                
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Final Contract'){
                i = 2;
                $(".all-cc-email-bidAgreement span.email-ids").each(function(){
                    csCCRecipients = csCCRecipients.trim() != "" ? csCCRecipients + '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC' : '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC';
                    i++;
                });
                var congaQueriesMap = JSON.parse(congaQueriesJson);
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['GT - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['GT - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('GT - ContactById') ? ',[Contact]' + congaQueriesMap['GT - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&CSRecipient1=' + primary_contact + csCCRecipients + '&csvisible=1&CSRoutingType=SERIAL&csRequestReminder=2&OFN=GT+Final+Contract-' + tripName + '&DS7=1141&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=900, resizable=yes, toolbar=no, location=no, status=yes');                
            } 
        }
        else if($('input[id$=bidParentSObjectInput]').val() == "Freight"){
            if($('div[id$=bidAgreementModal] .modal-title').text() == 'Rate Agreement'){
                if(emailResult.trim() == ""){
                    i = 2;
                    $(".all-cc-email-bidAgreement span.email-ids").each(function(){
                        csCCRecipients = csCCRecipients.trim() != "" ? csCCRecipients + '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC' : '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC';
                        i++;
                    });
                    var congaQueriesMap = JSON.parse(congaQueriesJson);
                    window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('Freight - ContactById') ? ',[Contact]' + congaQueriesMap['Freight - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('Freight - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['Freight - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&CSRecipient1=' + primary_contact + csCCRecipients + '&csvisible=1&CSRoutingType=SERIAL&csRequestReminder=2&OFN=Freight+Rate+Agreement-' + tripName + '&DS7=1141&DefaultPDF=1&contentShareType=V&contentVisibility=AllUsers', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=900, resizable=yes, toolbar=no, location=no, status=yes');                
                }
                else alert(emailResult);
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Trip Details Update'){
                i = 2;
                $(".all-cc-email-bidAgreement span.email-ids").each(function(){
                    csCCRecipients = csCCRecipients.trim() != "" ? csCCRecipients + '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC' : '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC';
                    i++;
                });
                var congaQueriesMap = JSON.parse(congaQueriesJson);
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('Freight - ContactById') ? ',[Contact]' + congaQueriesMap['Freight - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&CSRecipient1=' + primary_contact + csCCRecipients + '&csvisible=1&CSRoutingType=SERIAL&csRequestReminder=2&OFN=Freight+Trip+Details+Update-' + tripName + '&DS7=1141&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=900, resizable=yes, toolbar=no, location=no, status=yes');                
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Transportation Contract'){
                i = 3;
                $(".all-cc-email-bidAgreement span.email-ids").each(function(){
                    csCCRecipients = csCCRecipients.trim() != "" ? csCCRecipients + '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC' : '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC';
                    i++;
                });
                var congaQueriesMap = JSON.parse(congaQueriesJson);
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('Freight - ContactById') ? ',[Contact]' + congaQueriesMap['Freight - ContactById'].Id + '?pv0=' + primary_contact : '') + (congaQueriesMap.hasOwnProperty('Freight - ClientContactById') ? ',[ClientContact]' + congaQueriesMap['Freight - ClientContactById'].Id + '?pv0=' + client_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&CSRecipient1=' + primary_contact + csCCRecipients + '&csvisible=1&CSRoutingType=SERIAL&csRequestReminder=2&OFN=Freight+Transportation+Contract-' + tripName + '&DS7=1141&DefaultPDF=1&contentShareType=V&contentVisibility=AllUsers', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=900, resizable=yes, toolbar=no, location=no, status=yes');                
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Contract To Client'){
                i = 2;
                $(".all-cc-email-bidAgreement span.email-ids").each(function(){
                    csCCRecipients = csCCRecipients.trim() != "" ? csCCRecipients + '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC' : '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC';
                    i++;
                });
                var congaQueriesMap = JSON.parse(congaQueriesJson);
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('Freight - ContactById') ? ',[Contact]' + congaQueriesMap['Freight - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&CSRecipient1=' + primary_contact + csCCRecipients + '&csvisible=1&CSRoutingType=SERIAL&csRequestReminder=2&OFN=Freight+Contract+To+Client-' + tripName + '&DS7=1141&DefaultPDF=1&contentShareType=V&contentVisibility=AllUsers', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=900, resizable=yes, toolbar=no, location=no, status=yes');                
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Counter Needed'){
                i = 2;
                $(".all-cc-email-bidAgreement span.email-ids").each(function(){
                    csCCRecipients = csCCRecipients.trim() != "" ? csCCRecipients + '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC' : '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC';
                    i++;
                });
                var congaQueriesMap = JSON.parse(congaQueriesJson);
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('Freight - ContactById') ? ',[Contact]' + congaQueriesMap['Freight - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&CSRecipient1=' + primary_contact + csCCRecipients + '&csvisible=1&CSRoutingType=SERIAL&csRequestReminder=2&OFN=Freight+Counter+Needed-' + tripName + '&DS7=1141&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=900, resizable=yes, toolbar=no, location=no, status=yes');                
            } 
            else if($('div[id$=bidAgreementModal] .modal-title').text() == 'Final Contract'){
                i = 2;
                $(".all-cc-email-bidAgreement span.email-ids").each(function(){
                    csCCRecipients = csCCRecipients.trim() != "" ? csCCRecipients + '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC' : '&CSRecipient' + i + '=' + $(this).data('contactid') + '&CSrole' + i + '=CC';
                    i++;
                });
                var congaQueriesMap = JSON.parse(congaQueriesJson);
                window.open('/apex/APXTConga4__Conga_Composer?id=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap['Freight - BidById'].Id + '?pv0=' + bidId + (congaQueriesMap.hasOwnProperty('Freight - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap['Freight - SubTripsByBidId'].Id + '?pv0=' + bidId : '') + (congaQueriesMap.hasOwnProperty('Freight - ContactById') ? ',[Contact]' + congaQueriesMap['Freight - ContactById'].Id + '?pv0=' + primary_contact : '') : '') + '&TemplateId=' + congaTemplateId + '&CSRecipient1=' + primary_contact + csCCRecipients + '&csvisible=1&CSRoutingType=SERIAL&csRequestReminder=2&OFN=Freight+Final+Contract-' + tripName + '&DS7=1141&DefaultPDF=1', '','scrollbars=yes, menubar=no, top=70, left=400, height=600, width=900, resizable=yes, toolbar=no, location=no, status=yes');                
            } 
        }
    }
    function congaSendSign(bidId) {
        window.open('/apex/APXT_CongaSign__apxt_sendForSignature?id=' + bidId + '&routingType=SERIAL&reminderDays=2', '','scrollbars=yes, menubar=no, top=70, left=350, height=600, width=900, resizable=yes, toolbar=no, location=no, status=yes');
    }
    /*---@/Conga---*/
    </script>
</apex:component>
```


# Last Modified


# Usage
