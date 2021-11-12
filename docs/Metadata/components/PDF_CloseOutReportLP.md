---
layout: default
title: PDF_CloseOutReportLP
parent: components
grand_parent: Metadata
---
# Metadata Type
components


# Filename 
PDF_CloseOutReportLP


# Raw XML
```
<apex:component controller="PDF_CloseOutReportLPController">

<apex:attribute name="showError" type="Boolean" description="" />

  <div class="content">

    <table width="100%" valign="top" cellspacing="0" cellpadding="0" border="0">
      <thead>
        <tr>
          <th width="10%" align="left" style="">
            <apex:image url="{!$Resource.Logo}" style="width: 120px" />
          </th>
          <th width="90%" colspan="5" align="right" style="font-size: 32px; font-weight: bold">PRODUCTION CLOSE OUT REPORT</th>
        </tr>
        <tr>
          <th width="10%" height="8" colspan="1" style="border-bottom: 1px solid rgb(143, 161, 152)"></th>
          <th colspan="5"></th>
        </tr>
        <tr>
          <th height="8" colspan="6" style="border-bottom: 1px solid rgb(143, 161, 152)"></th>
        </tr>
        <tr>
          <th align="center" style="
              padding: 5px 3px 5px 3px;
              border-top: 1px solid rgb(143, 161, 152);
              border-bottom: 1px solid rgb(143, 161, 152);
              font-size: 9px;
            ">
            <strong>NAME:</strong>
            <br/> {!thebid.Vendor_Contact__r.Name}
          </th>
          <th align="center" style="
              padding: 5px 3px 5px 3px;
              border-top: 1px solid rgb(143, 161, 152);
              border-bottom: 1px solid rgb(143, 161, 152);
              font-size: 9px;
            ">
            <strong>PROPERTY:</strong>
            <br/> {!thebid.Vendor__r.Name}
          </th>
          <th align="center" style="
              padding: 5px 3px 5px 3px;
              border-top: 1px solid rgb(143, 161, 152);
              border-bottom: 1px solid rgb(143, 161, 152);
              font-size: 9px;
            ">
            ADDRESS:
            <br/> {!thebid.Vendor__r.ShippingStreet} {!thebid.Vendor__r.ShippingCity}, {!thebid.Vendor__r.ShippingState} {!thebid.Vendor__r.ShippingPostalCode}
          </th>
          <th align="center" style="
              padding: 5px 3px 5px 3px;
              border-top: 1px solid rgb(143, 161, 152);
              border-bottom: 1px solid rgb(143, 161, 152);
              font-size: 9px;
            ">
            DATE CREATED:
            <br/>
            <apex:outputText value="{0,date,dd-MMM-yyyy}">
              <apex:param value="{!thebid.CreatedDate}" />
            </apex:outputText>
          </th>
          <th align="center" style="
              padding: 5px 3px 5px 3px;
              border-top: 1px solid rgb(143, 161, 152);
              border-bottom: 1px solid rgb(143, 161, 152);
              font-size: 9px;
            ">
            ID #:
            <br/> {!thebid.Name}
          </th>
          <th align="center" style="
              padding: 5px 3px 5px 3px;
              border-top: 1px solid rgb(143, 161, 152);
              border-bottom: 1px solid rgb(143, 161, 152);
              font-size: 9px;
            ">
            STAY ID #:
            <br/> {!housing.Name}
          </th>
        </tr>

      </thead>
    </table>
    <br/>
    <!--
    <table width="100%" style="padding: 3px 3px 3px 25px; background: rgb(143, 161, 152); font-size: 18px">
      <tr>
        <td>BID OFFER</td>
      </tr>
    </table>
    -->
    <apex:outputPanel rendered="{!IF(showError==true,false,true)}">
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
                        <td align="left" style="padding: 5px; font-size: 10px">COMPANY:</td>
                        <td>
                          <strong style="font-size: 12px">{!housing.Production_CC__r.Account.Name}</strong>
                          <br />
                        </td>
                      </tr>
                    </td>
                  </tr>
                </tbody>
              </table>
            </td>
          </tr>

        </tbody>
      </table>
      <table width="100%" cellspacing="0" cellpadding="0" border="0">
        <tbody>
          <tr>
            <td width="100%" style="">
              <table width="100%" cellspacing="0" cellpadding="0" border="0">
                <tbody>
                  <tr>
                    <th height="8" style="border-bottom: 2px solid rgb(143, 161, 152);padding:5px"></th>
                  </tr>
                  <tr>
                    <td align="center">
                      <br/> Upon check-out, please send the Production Master Folio with this document as the cover sheet to Road
                      Rebel.
                      <br/> Road Rebel does not accept outside Group Pickup forms.
                    </td>
                  </tr>
                  <tr>
                    <th height="8" style="border-bottom: 1px solid rgb(143, 161, 152)"></th>
                  </tr>
                </tbody>
              </table>
            </td>
          </tr>
        </tbody>
      </table>
      <br/>
      <br/>
      <table width="100%" cellspacing="0" cellpadding="0" border="0">
        <tbody>
          <tr>
            <td width="100%">
              <table width="100%" cellspacing="1">
                <tbody>
                  <tr>
                    <td colspan="2" align="center" style="font-size: 10px">
                      <table style="border-spacing: 2px;" align="center" width="80%" cellspacing="1" cellpadding="1">
                        <thead>
                          <tr style="padding: 3px 3px 3px 25px; font-size: 16px">
                            <th width="50%" align="center" style="background: rgb(198, 208, 203); padding: 5px">
                              ARRIVAL
                            </th>
                            <th width="50%" align="center" style="background: rgb(198, 208, 203); padding: 5px">
                              DEPARTURE
                            </th>
                          </tr>
                        </thead>
                        <tbody>
                          <tr>
                            <td width="40%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
                              <apex:outputText value="{0,date,dd-MMM-yyyy}">
                                <apex:param value="{!housing.Date_In__c}" />
                              </apex:outputText>
                            </td>
                            <td width="40%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
                              <apex:outputText value="{0,date,dd-MMM-yyyy}">
                                <apex:param value="{!housing.Date_Out__c}" />
                              </apex:outputText>
                            </td>
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


        </tbody>
      </table>
      <br/>
      <table width="100%" cellspacing="0" cellpadding="0" border="0">
        <tbody>
          <tr>
            <td width="100%" style="">
              <table width="100%" cellspacing="0" cellpadding="0" border="0">
                <tbody>
                  <tr>
                    <th height="8" style="border-bottom: 2px solid rgb(143, 161, 152);padding:5px"></th>
                  </tr>
                  <tr>
                    <td align="center">
                      <br/> * If arrival and/or departure differ from what is noted, please contact us.

                    </td>
                  </tr>
                  <tr>
                    <th height="8" style="border-bottom: 1px solid rgb(143, 161, 152)"></th>
                  </tr>
                </tbody>
              </table>
            </td>
          </tr>
        </tbody>
      </table>
      <br/>
      <table width="100%" cellspacing="0" cellpadding="0" border="0">
        <tbody>
          <tr>
            <td width="100%" style="">
              <table width="100%" cellspacing="0" cellpadding="0" border="0">
                <tbody>
                  <tr>
                    <td align="center">
                    </td>
                  </tr>
                </tbody>
              </table>
            </td>
          </tr>
        </tbody>
      </table>
      <table style="border-spacing: 2px;" align="center" width="80%" cellspacing="0" cellpadding="0" border="0">
        <thead>
          <tr>




            <th width="25%" align="center" style="background: rgb(198, 208, 203); padding: 5px"></th>
            <th width="10%" align="center" style="background: rgb(198, 208, 203); padding: 5px">ROOM NIGHTS</th>
            <th width="10%" align="center" style="background: rgb(198, 208, 203); padding: 5px">COMPS</th>
            <th width="15%" align="center" style="background: rgb(198, 208, 203); padding: 5px">ROOM RATE</th>
            <th width="10%" align="center" style="background: rgb(198, 208, 203); padding: 5px">ROOM REVENUE</th>
            <!--  <th width="30%" align="center" style="background: rgb(198, 208, 203); padding: 5px">COMMISSION DUE ROAD REBEL: (<apex:outputText value="{!therevenue.Commission_Percent__c}"/> %)</th>-->
          </tr>
        </thead>
        <tbody>

          <apex:repeat value="{!bidsMap}" var="key">
            <apex:repeat value="{!bidsMap[key]}" var="bid">
              <apex:repeat value="{!bid.Housing__r}" var="roomType">
                <tr>
                  <td width="25%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
                    {!roomType.Unit_Type__c}
                  </td>
                  <td width="10%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
                    {!roomType.Total_Room_Nights__c}
                  </td>
                  <td width="10%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
                    {!roomType.Comps__c}
                  </td>
                  <td width="15%" align="center" style="background: rgb(226, 235, 230); padding: 5px">

                    <apex:outputText value="{0, Number, Currency}">
                      <apex:param value="{!roomType.Rate__c}" />
                    </apex:outputText>

                  </td>
                  <td width="10%" align="center" style="background: rgb(226, 235, 230); padding: 5px">

                    <apex:outputText value="{0, Number, Currency}">
                      <apex:param value="{!roomType.Room_Nights_x_Rate_Pickup_Report__c}" />


                    </apex:outputText>
                  </td>
                  <!-- remove commission details
                  <td width="30%" align="center" style="background: rgb(226, 235, 230); padding: 5px">

                  </td>
                  -->

                </tr>
              </apex:repeat>
            </apex:repeat>
          </apex:repeat>
          <tr>
            <td width="25%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
            </td>
            <td width="10%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
            </td>
            <td width="10%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
            </td>
            <td width="15%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
              <strong>Total Room Revenue</strong>
            </td>
            <td width="10%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
              <apex:outputText value="{0, Number, Currency}">
                <apex:param value="{!theRoomTypeTotal}" />
              </apex:outputText>
            </td>
            <!-- remove commmission details
          <td width="10%" align="center" style="background: rgb(226, 235, 230); padding: 5px">
            <apex:outputText value="{0, Number, Currency}">
              <apex:param value="{!theCommissionTotal}"/>
            </apex:outputText>
          </td>
        -->
          </tr>
        </tbody>
      </table>
      <br/>
      <table width="100%" cellspacing="0" cellpadding="0" border="0">
        <tbody>
          <tr>
            <td width="20%">
              <tr>
                <td align="left" style="padding: 5px; font-size: 10px">Do You Need an Invoice Sent?:</td>
                <td>

                  <strong style="font-size: 12px">
                    <apex:outputPanel rendered="{!if(therevenue.Do_you_need_invoice_sent__c=='Yes',true,false)}">
                      Yes
                    </apex:outputPanel>
                    <apex:outputPanel rendered="{!if(therevenue.Do_you_need_invoice_sent__c=='No',true,false)}">
                      No
                    </apex:outputPanel>
                    <apex:outputPanel rendered="{!if(therevenue.Do_you_need_invoice_sent__c=='',true,false)}">
                      No
                    </apex:outputPanel>
                  </strong>
                  <br />
                </td>
                <td>
                </td>
              </tr>
            </td>
          </tr>
          <tr>
            <td width="20%">
              <tr>
                <td align="left" style="padding: 5px; font-size: 10px">Dates?:</td>
                <td>
                  <strong style="font-size: 12px">
                    <strong style="font-size: 12px">
                      <apex:outputText value="{!theIndicateDates}" />
                    </strong>
                  </strong>
                </td>

              </tr>
            </td>
          </tr>

          <tr>
            <td width="20%">
              <tr>
                <td align="left" style="padding: 5px; font-size: 10px">Name of Person Preparing Report:</td>
                <td>
                  <strong style="font-size: 12px">{!thebid.coVendorName__c}</strong>

                </td>

              </tr>
            </td>
          </tr>
        </tbody>
      </table>
      <br/>

      <table width="100%" style="border-spacing: 2px;padding:2px">
        <tr>
          <th style="padding: 3px 3px 3px 25px; background: rgb(143, 161, 152); font-size: 18px;padding:5px" width="100%" align="left"
            colspan="2">
            PAYMENT INFO
          </th>

        </tr>
        <tr>
          <td width="50%">
            <br/>
            <strong>Road Rebel Entertainment Touring, Inc</strong>
            <br/> 2869 Historic Decatur Rd.
            <br/> San Diego CA 92106
            <br/> Ph (619) 640-1001
            <br/> Fax (619) 640-1011
            <br/>
          </td>
          <td width="50%">
            <br/>
            <Strong>California Corporation:</strong>
            <br/> Tax ID #: 33-0909027
            <br/> IATA #: 05-56078-5
            <br/>
          </td>
        </tr>
      </table>
    </apex:outputPanel>
    <apex:outputPanel rendered="{!IF(showError==true,true,false)}">

    <div class="isa_error" align="center">
      <i class="fa fa-times-circle"></i>
      An error occured generating the PDF.  Please contact Road Rebel for assistance.
    </div>
    </apex:outputPanel>

  </div>

</apex:component>
```


# Last Modified


# Usage
