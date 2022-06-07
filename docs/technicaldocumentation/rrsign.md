---
layout: default
title: RRSign
parent: Technical Documentation
---

# RRSign
Details about the RRSign app.

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

## Scope
{: .fs-6 .fw-300 }
Any details relating to the functionality of the RRSign app.

### Sequence of Events/Components
- Housing Dashboard - DashboardVFP
- DashboardController Apex Class - Bid Search
- Housing Contract - DashboardVFP, DashboardHousingScript JS static resource
- DashboardHousingScript - rrsignEntryPoint method calls actionfunction after modal rendering
- Dashboard Controller - has original object of data sent to it regarding the transaction
- DashboardController - saveRateAgreement called to start process of sending
- DashboardVFP - Renders the proper modal (Document Generation)
- DashboardVFP - Gets renderBoolean value of correct modal to set, renders div for modal, and acts accordingly
- DashboardVFP - Gets render for doc generation
- DashboardVFP - Gets doc generation complete event from component (LWC) (docgenevent)
- DashboardVFP - docgenevent handled by the page (theNextDestination is where it forwards to)
- Preview or Send Signer?
- Email - Will email attachment with PDF based on "Form Type" (c__formName) dashboardcontroller properties (form_title, rate_agreementtype, )
- PreviewAndTagApp aura  - Loads wv_instance with the preview context and buttons hidden
- Send Signer - 
  - Preview and Tag - Complete button saves document with XFDF to be signed
  - Send Now - Sends documents
    - both of these should update "Pending Signature = true" and SENT

## References
- https://code.visualstudio.com/docs/editor/github