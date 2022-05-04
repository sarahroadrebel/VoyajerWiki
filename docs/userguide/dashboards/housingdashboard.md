---
layout: default
title: Housing Dashboard
parent: Dashboards
grand_parent: User Guide
---

# Housing Dashboard
{: .no_toc }

The user guide is broken down into the functional areas of the dashboards, broken down by service and then by tabs inside of the Service Dashboard.
{: .fs-6 .fw-300 }
## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}
<br/>
## Scope
This user guide has individual sections for each major tab of the internal Dashboards.  It should cover the following in each separate screen at a minimum:
* Business Processes
* Expected Workflows
* Any black box magic the code does
<br/>
## Housing Details
<img src="https://rr-salesforce.github.io/voyajerwiki/assets/images/housing-details.gif"/>

### Scope
Covers the *Housing Details* tab and the fields / business logic contained within it.  Also gives high level detail on the functionality behind buttons on this tab but does not describe preferred room types as a whole in depth or concessions.

### User / Business Processes

The step after Production creation and going further down the workflow would be the "Sales Housing" represented by the data in the "Housing Details" tab.   The first Housing in the chain of the children records of production records, it holds values for the items listed in the table below and also defaults for the stays that originate from there.  (Clay needs more detail).

The system is setup to create this Sales Housing record the first time a Production is visited in the Dashboard via the search in the top left.

The following business processes and custom functionality live on this tab:
- Preferred Room Types stored as default for Production
- Production Journals can be maintained
- Preferences for the Stay as Bids are entered per Stay
- Concessions are stored as Stay level preferences
- Contracting Requirements are loaded based on Office Location
- Billing Options and Payment Information stored on the Stay
- Internal notes and Deadline Trace Date Management

### Technical Details
The Dashboard has specific events that kick off certain decisions and custom code exists for that to work.  Here are some of the business logics inside of the Housing Details tab:
- Page load functions:
    - Contracting Requirements that load
    - Biling options and Payment options that specifically load
    - Concessions that are specifically defaulted based on PRoduction settings
    - Automation of the record with "Sales Housing" record type being created (see data model below)

#### Data Model

The inputs on the page are all derived from the "Housing__c" record attached to the "Opportunity" (Production) record.
The record type used is "Sales Housing" on the "Housing__c" object

| Name | Object / Field API Name | Details | 
|:---------------|:---------------------|
| Hotel Class | Housing__c.Hotel_Class__c | Picklist field.|
| Star Preference | Housing__c.Star_Preference__c | Picklist field.|
| Distance To Venue | Housing__c.Distance_To_Venue__c | Picklist field.|
| Brand Preference | Housing__c.Brand_Preference__c | Picklist field.|
| Concessions | Housing__c.Concessions__r | Picklist field.|
| Contracting Requirements | Housing__c.Contracting_Requirememts__c | Picklist field.|
| Payment Information | Housing__c.Payment_Information__c | Picklist field.|
| Billing Options | Housing__c.Billing_Options__c | Picklist field.|
| Budget | Housing__c.Budget__c | Picklist field.|
| Internal Notes | Housing__c.Internal_Notes__c | Picklist field.|
| Deadline Trace Date | Housing__c.Deadline_Trace_Date__c | Picklist field.|


#### Code 
#### Data Model

### Resources

## Itinerary Details
### Scope
### User Details
### Technical Details
### Resources
## Stay Details
### Scope
### User Details
### Technical Details
### Resources
## Bid Details
### Scope
### User Details
### Technical Details
### Resources
## Contracting Details
### Scope
### User Details
### Technical Details
### Resources