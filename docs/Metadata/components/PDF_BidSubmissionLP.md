---
layout: default
title: PDF_BidSubmissionLP
parent: components
grand_parent: Metadata
---
# Metadata Type
components


# Filename 
PDF_BidSubmissionLP


# Raw XML
```
<apex:component controller="PDF_BidSubmissionLPController" access="GLOBAL">
  <div class="content">
    <table width="100%" valign="top" cellspacing="0" cellpadding="0" border="0">
      <thead>
        <tr>
          <th width="20%" align="left" style="">
            <apex:image url="{!$Resource.Logo}" style="width: 120px" />
          </th>
          <th width="20%" align="left" style=""></th>
          <th width="80%" align="right" style="font-size: 32px; font-weight: bold">HOUSING BID</th>
        </tr>
        <tr>
          <th height="8" colspan="2" style="border-bottom: 1px solid rgb(143, 161, 152)"></th>
        </tr>
        <tr>
          <th height="8" colspan="2"></th>
        </tr>
        <tr>
          <th height="8" colspan="2"></th>
        </tr>
        <tr>
          <th
            width="20%"
            align="left"
            style="
              padding: 5px 3px 5px 3px;
              border-top: 1px solid rgb(143, 161, 152);
              border-bottom: 1px solid rgb(143, 161, 152);
              font-size: 9px;
            "
          >
            NAME: {!thebid.Vendor_Contact__r.Name}
          </th>
          <th
            width="20%"
            align="left"
            style="
              padding: 5px 3px 5px 3px;
              border-top: 1px solid rgb(143, 161, 152);
              border-bottom: 1px solid rgb(143, 161, 152);
              font-size: 9px;
            "
          >
            PROPERTY: {!thebid.Vendor__r.Name}
          </th>
          <th
            width="60%"
            align="right"
            style="
              padding: 5px 3px 5px 3px;
              border-top: 1px solid rgb(143, 161, 152);
              border-bottom: 1px solid rgb(143, 161, 152);
              font-size: 9px;
              font-weight: bold;
            "
          >
            DATE CREATED:
            <apex:outputText value="{0,date,dd-MMM-yyyy}"
              ><apex:param value="{!thebid.CreatedDate}" />
            </apex:outputText>
            BID ID #: {!thebid.Name}
          </th>
        </tr>
        <tr>
          <th height="8" colspan="2"></th>
        </tr>
      </thead>
    </table>
    <table width="100%" style="padding: 3px 3px 3px 25px; background: rgb(143, 161, 152); font-size: 18px">
      <tr>
        <td>BID OFFER</td>
      </tr>
    </table>
    <table width="100%" cellspacing="0" cellpadding="0" border="0">
      <tbody>
        <tr>
          <td width="80%" style="">
            <table width="100%" cellspacing="0" cellpadding="0" border="0">
              <tbody>
                <tr>
                  <td width="20%">
                    <tr>
                      <td align="left" style="padding: 5px; font-size: 10px">PRODUCTION:</td>
                      <td>
                        <strong style="font-size: 12px">{!housing.Production_CC__r.Name}</strong>
                        <br />
                      </td>
                    </tr>
                    <tr>
                      <td align="left" style="padding: 5px; font-size: 10px">LOCATION:</td>
                      <td>
                        <strong style="font-size: 12px">{!housing.Production_CC__r.Office_Location__c}</strong>
                        <br />
                      </td>
                    </tr>
                    <tr>
                      <td align="left" style="padding: 5px; font-size: 10px">CITY:</td>
                      <td>
                        <strong style="font-size: 12px">{!housing.City__r.Name}</strong>
                      </td>
                    </tr>
                  </td>
                  <td width="100%">
                    <table align="center" width="100%" style="background: rgb(226, 235, 230); padding: 5px">
                      <tr>
                        <td align="center">
                          <strong>ROOMS RELEASE DATE:</strong>
                        </td>
                      </tr>
                      <tr>
                        <td align="center">
                          <apex:outputText value="{0,date,dd-MMM-yyyy}"
                            ><apex:param value="{!thebid.Room_Rate_Release_date__c}" />
                          </apex:outputText>
                        </td>
                      </tr>
                    </table>
                  </td>
                </tr>
                <br />
                <br />
                <br />
              </tbody>
            </table>
          </td>
        </tr>
      </tbody>
    </table>
    <table style="border-spacing: 2px;" width="100%" cellspacing="0" cellpadding="0" border="0">
      <tbody>
        <tr>
          <td width="100%" style="">
            <table  style="border-spacing: 2px;" width="100%" cellspacing="0" cellpadding="0" border="0">
              <tbody>
                <tr>
                  <td colspan="2" align="center" style="font-size: 10px">
                    <table style="border-spacing: 2px;" width="100%" cellspacing="0" cellpadding="0" border="0">
                      <thead>
                        <tr>
                          <th width="10%" align="center" style="background: rgb(198, 208, 203); padding: 5px">
                            DATE IN
                          </th>
                          <th width="10%" align="center" style="background: rgb(198, 208, 203); padding: 5px">
                            DATE OUT
                          </th>
                          <th width="10%" align="center" style="background: rgb(198, 208, 203); padding: 5px">QTY</th>
                          <th width="30%" align="center" style="background: rgb(198, 208, 203); padding: 5px">
                            UNIT TYPE
                          </th>
                          <th width="10%" align="center" style="background: rgb(198, 208, 203); padding: 5px">
                            NIGHTS
                          </th>
                          <th width="10%" align="center" style="background: rgb(198, 208, 203); padding: 5px">
                            RATE
                          </th>
                          <th width="50%" align="center" style="background: rgb(198, 208, 203); padding: 5px">
                            SPECIAL NOTES
                          </th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr>
                          <apex:repeat value="{!bidsMap}" var="key">
                            <apex:repeat value="{!bidsMap[key]}" var="bid">
                              <apex:repeat value="{!bid.Housing__r}" var="roomType">
                                <tr>
                                  <td width="10%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
                                    <apex:outputText value="{0,date,dd-MMM-yyyy}"
                                      ><apex:param value="{!roomType.Date_In__c}" />
                                    </apex:outputText>
                                  </td>
                                  <td width="10%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
                                    <apex:outputText value="{0,date,dd-MMM-yyyy}"
                                      ><apex:param value="{!roomType.Date_Out__c}" />
                                    </apex:outputText>
                                  </td>
                                  <td width="10%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
                                    <apex:outputText value="{!FLOOR(roomType.Units__c)}"/>
                                    
                                  </td>
                                  <td width="30%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
                                    {!roomType.Unit_Type__c}
                                  </td>
                                  <td width="10%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
                                    <apex:outputText value="{!FLOOR(roomType.Nights_CC__c)}"/>
                                  </td>
                                  <td width="10%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
                                    <apex:outputText value="{0, Number, Currency}">
                                      <apex:param value="{!roomType.Rate__c}"/>
                                    </apex:outputText>
                                  </td>
                                  <td width="50%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
                                    {!roomType.Special_Notes__c}<apex:outputText value="{!thebid.coVendorName__c}"/>

                                  </td>
                                </tr>
                              </apex:repeat>
                            </apex:repeat>
                          </apex:repeat>
                        </tr>
                      </tbody>
                    </table>
                  </td>
                </tr>
              </tbody>
            </table>
          </td>
        </tr>
        <br />
        <br />
        <tr>
          <td>
            <table style="border-spacing: 2px;" width="100%" cellspacing="0" cellpadding="0" border="0" class="housing-options" valign="top">
              <tbody>
                <tr>
                  <td width="20%" align="center" style="background: rgb(226, 235, 230); padding: 5px">

                  </td>
                  <td width="20%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
                    Currency: {!therevenue.CurrencyISOCode}
                  </td>
                  <td width="20%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
                    Tax: {!therevenue.Tax__c}<br />Included in Rate:&nbsp;&nbsp;
                    <apex:outputField value="{!therevenue.Tax_Included__c}" />
                  </td>
                  <td width="20%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
                    Surcharge: {!therevenue.Surcharge__c} <br />Included in Rate:&nbsp;&nbsp;
                    <apex:outputField value="{!therevenue.Surcharge_included__c}" />
                  </td>
                  <td width="20%" align="center" style="background: rgb(143, 161, 152); padding: 5px">
                    <strong>ROAD REBEL COMMISSION: </strong>
                    10% Commission on Total Rate: &nbsp;&nbsp;<apex:outputField value="{!therevenue.Commission_Agreed__c}"
                    />
                  </td>
                </tr>
                <tr>
                  <td colspan="1" align="left" style="background: rgb(226, 235, 230); padding: 5px">
                    <strong> Concessions</strong><br />
                  </td>
                  <td colspan="4" style="background: rgb(226, 235, 230); padding: 5px">
                    
                      <apex:repeat value="{!bidsMap}" var="key">
                        <apex:repeat value="{!bidsMap[key]}" var="bid">
                         <apex:repeat value="{!bid.Concessions__r}" var="concession">
                           <table>
                             <tr>
                               <td style="width:200px;">
                                Concession
                               </td>
                               <td>
                                Agreed?
                              </td>
                             </tr>
                             <tr>
                               <td>
                                <apex:outputField value=" {!concession.Concessions_Requested__c}"/>
                               </td>
                               <td>
                                <apex:outputField value=" {!concession.Agreed__c}"/>
                               </td>
                             </tr>
                           </table>
                      </apex:repeat>
                      </apex:repeat>
                      </apex:repeat>
          
                  </td>
                </tr>
                <tr>
                  <td  valign="center" colspan="1" align="left" style="background: rgb(226, 235, 230); padding: 5px">
                    <strong>Comments</strong>
                  </td>
                  <td valign="center" colspan="4" style="background: rgb(226, 235, 230); padding: 5px">
                    {!thebid.Vendor_Bid_Notes__c}<br /><br />
                  </td>
                </tr>
                <tr>
                  <td  valign="center" colspan="1" align="left" style="background: rgb(226, 235, 230); padding: 5px">
                    <strong>Reason for Not Bidding</strong>
                  </td>
                  <td valign="center" colspan="4" style="background: rgb(226, 235, 230); padding: 5px">
                    <apex:outputText value="{!thebid.No_Bid_reason__c}"/>
                    <br /><br />
                  </td>
                </tr>
              </tbody>
            </table>
          </td>
        </tr>
      </tbody>
    </table>
    <br/>
    <strong>Name: </strong><apex:outputText value="{!thebid.responseVendorName__c}"/><br/>
    <strong>Title: </strong><apex:outputText value="{!thebid.responseVendorTitle__c}"/><br/>
    <strong>Email: </strong><apex:outputText value="{!thebid.responseVendorEmail__c}"/><br/>
    <strong>Phone: </strong><apex:outputText value="{!thebid.responseVendorPhone__c}"/><br/>
  </div>
</apex:component>
```


# Last Modified


# Usage
