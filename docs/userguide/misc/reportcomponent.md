---
layout: default
title: Report Component
parent: Misc
grand_parent: User Guide
---

# Report Component
{: .no_toc }

A component that allows for embedding of reports on Account (currently only Account) and the specification of the report data to display.   Also has a second field for filtering if the Account Id you need to use is on a separate object.
## Scope
The reportComponent and how to use on Lightning Pages.   Includes steps to setup and description of what it expects for configuration inputs.  Does not cover Lightning Page Editor assignments and Activation, just component configuration.

## User Details
Used when you want to show an embedded report specific to an Account on an Account lightning page.  It requires creation of the report before hand so that it can be configured inside the Lightning Page Editor.
- Create report to be displayed on a per Account basis
    - Any report can be used as long as it contains filter for Account Id
    - If the Account.Id field is not a filter (top level Account filtering in Report), filter field must be specified in Lightning Page Editor
        - Top Level Account Filter means in the List of Objects in the Field Selections object it is the "Id" field from the "Account" object fields
        - ![](https://sfdcboss.github.io/voyajerwiki/assets/images/reportComponentEx1.jpg)
        - ![](https://sfdcboss.github.io/voyajerwiki/assets/images/reportComponentEx2.jpg)
- Drag reportComponent onto Lightning Record Page and click once to get configuration options:
        - ![](https://sfdcboss.github.io/voyajerwiki/assets/images/reportComponentOverview.jpg)

- Save Lightning Record Page and confirm expected Report shows with filtering
- A Summary Report will show the details in groupings
    - Note the grey row headers listing the Bid Name above
- A Tabular Report will show the details without grouping rows.
    - White rows with no header

## Technical Details
- Aura Component
    - reportComponent
    - reportSearchComponent
- Apex Classes
    - AnalyticsUtils
    - LightningReportController
    - LightningReportControllerTest
- Tests
    - LightningReportControllerTest
        - Ex test
        - Ex test
## References
- Report Types
- Summary Report
