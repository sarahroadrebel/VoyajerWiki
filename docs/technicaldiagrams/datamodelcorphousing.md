---
layout: default
title: Data Model - Corp Housing
parent: Technical Diagrams
---

# Data Model
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Scope

This diagram covers the Important connections for Bids in Corporate Housing stay types.  Not a complete list of every single connection and object but highlited or shown in terms of relevance.  Should not be used as a complete reference to the entire Data Model.

## Diagram

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vSxlx_rGCuAMIxpWPu_qFyufv-MUAOWCEtY-kRUf7O0KpoybHlGL-41l7tkSXhyuqTWyCovO-P4tJVu/embed?start=false&loop=false&delayms=3000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

## Details

The Corporate Housing Record Type and Bid Selection process varies in that it requires a provider to be selected first.
Bid is created on the Stay Tab on Dashboard for a Provider
Bid with Provider populated and empty Vendor is a potential building a Provider would supply.

Bid_c (Object)
○ Account (Provider_c) (Lookup Field)
○ Account (Vendor_c) (Lookup Field)
When the Bid is in the state of making contact with the Vendor it would have Journals added to it

Bid Journals
○ Attached to Bid_c in their Journal__c record
These journals need to be available when the Provider were to match on the Journals' Bid records
When the Vendor is selected and the bid is created for the Vendor the Bid would then have both Provider_c and Vendor_c populated. A second Bid for that provider to link with a Vendor Account would be created if a second bid was to be created for that Provider.

The solution that would be best would be if we were to link the Providers and the Journals in addition to the Bids so that we can query bids where that Provider Id is the one that was stamped in a created journal for that providers' bid.

Journal entered by Coordinator for Provider > Journal created also copied Provider_c to new lookup and creates the bid Journal the same way.

With the Housing statuses after talking to Sarah it seems we are OK as the status change stamps would be on a Stay level and applicable to all bids for a Parent Housing status change. The manually entered journals in Corporate Housing almost always would be the manually entered ones but since we don't have to worry about omitting the status changes I think we are OK to skip that.

To be clear your solution was solid and would have worked, the Providers first Bid associated record would chronologically happen first, but it is the second portion that makes me think stamping provider Id would be the best bet for identifying it later given what should be shown.

Recap:

Provider and no Vendor (Building) for data on the bid is a Bid about to be associated with a Building that coordinators are coordinating
Vendor and no Provider data on the bid would be for a Building not working through a provider
Vendor and Provider Populated is a Building for a provider grouped on the Stay by the Provider Id
Contracting happens after the selection is finally made at the end for the Bid record that is selected by Client.
Solution
○ Journal Creation from the Bid (in Corporate Housing record type only) try to write the Providerc from the Bid to the Journal Record via a lookup created on Journalc to Provider__c object.
Change Query for Bid Journals to show Bid Journals where the Provider and Bid matched (for corporate housing, not relevant in other record types).
Workflow Example and Outcome
Create a Bid for a Provider
Log some journals
The Bid journals on that bid are what we expect to be on a new bid under this stay for that provider
Add Vendor
Create another bid for the Provider
Attach Vendor to Providers 2nd bid and ensure the Bid Journals logged for the initial bid are also present.


|Object (RecordType)|Description|Linkage|
|-------------|
|Housing (Preferred Room Types)|The selections on the Housing Details tab that are at the beginning tab of the Dashboard|Production_CC__c|
|Housing (Preferred Room Types)|The selections on the Housing Details tab that are at the beginning tab of the Dashboard|Sales_Housing__c (links to Stay, not Sales Housing record Type)|
|Housing (Sales Housing)|The container for Stays under a Production use record type *Sales Housing* and have children Stays|Sales_Housing__c on Hotel Housing/CH/IR|
|Housing (Hotel Housing/CH/IR)|The "Stay" that represents the timeframe at the Hotel for a data range|Sales_Housing__c parent and Production_CC__c grandparent|
|Bid (Housing Bid)|The Bid which is a child of the Stay record and is the parent of the final room type children record that have Rate Information|Housing__c on Bid up to Production|
|Housing (Room Types)|The representations of the different rooms on the Bid itself which contain Rate information and tie to Revenue records further down|Bid__c parent|
|Account (Provider)|The Provider chosen as the Provider for the Bid.  Is a lookup to Account and is used with Record Type *Corporate Housing Vendor*
|Account (Vendor)|The Vendor chosen as the Vendor for the Bid.  Is a lookup to Account and is used with Record Type *Vendor*
|Account (Venue)|The Venue chosen as the Venue for the Bid.  Is a lookup to Account and is used with Record Type *Venue*
