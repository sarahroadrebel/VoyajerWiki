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

All Contracts / Forms follow the same paradigm for options for Buttons from the Modal.  These different paths use events and some back and forth to figure out what components to load and the decisions are below:

Format: [Button (theNextDestinationString values)]

Send Email (SEND_EMAIL):
- Will email attachment with PDF based on "Form Type" (c__formName) dashboardcontroller properties (form_title, rate_agreementtype, )
- sendEmail methods are called with the appropriate attachments and recipients after handleRenderLighting()

Preview (PREVIEW):
- PreviewAndTagApp aura  - Loads rrsign_Wv_instance with the preview context and buttons hidden (preview/tag buttons and signer portal buttons , which also use rrsign_Wv_Instance)

Send Signer (SEND_SIGNER):
- Housing Dashboard - DashboardVFP start process 
- DashboardController Apex Class - Bid Search and progression to Bid detail page
- Housing Contract - DashboardVFP, DashboardHousingScript JS static resource is called by button and action functions handle staticresource>VF>apex progression.
- config_apex.js static resource events communicate with LWC to get document details and save/process logic
- DashboardHousingScript - rrsignEntryPoint method calls actionfunction after modal rendering
- Dashboard Controller - has original object of data sent to it regarding the transaction to maintain params string 'c__formName,c__bcdid,c__bidid,c__documentIds'
- DashboardController - saveRateAgreement called to start process of sending by actionFunction 
- DashboardVFP - Renders the proper modal (assumes theNextDestinationString = 'DOCUMENT_GENERATION') -- Render Booleans support outputpanel re-rendering to show div containing relevant modal.
- DashboardVFP - Gets doc generation complete event from component (LWC) (docgenevent) -- Updates param string and redirects to theNextDestinationString
- DashboardVFP - docgenevent handled by the page (theNextDestination is where it forwards to)
- Preview or Send Signer?

- Send Signer Paths- 
  - Preview and Tag (PREVIEW_TAG) - Complete button saves document with XFDF to be signed
  - Send Now - Sends documents
    - both of these should update "Pending Signature = true" and SENT

## References
- https://code.visualstudio.com/docs/editor/github