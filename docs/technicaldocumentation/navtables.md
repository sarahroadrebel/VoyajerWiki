---
layout: default
title: NAV Tables Documentation
parent: Technical Documentation
---

# Nav Tables Documentation
{: .no_toc }

## Scope
{: .fs-6 .fw-300 }
Below are some details about the NAV data and what the approach was and how it is documented.  The scope of Accounts and Contacts, along with Bids/Productions/PA should be in the document.
## Details

- SQL .bak file provided by Rakesh (NAV .net developer) as a way to get data from NAV into SF
- Tables in backup file are detailed in first tab in sheet
- Data Model is very different and there are multiple tables in NAV for both contacts and accounts 
- “EntityType” is synonymous with RecordTypeId for the most part when looking at types of NAV contacts/Accounts
- “Landing Zone” objects in the Preprod org are flattened objects to accept all fields from all types of NAV tables in order to then do logic on the data from 1 row in the Landing zone object (Batch query rows and then with Landing Zone data query - accounts and contacts and act acfordingly).
- Logic in PersonAccountAnalyzerBatch that was created to convert business contacts to person accounts was going to try and be used to assist in the searching of matching contacts
- Fields were not consistent across NAV tables so the staggered layout of the documentation table columns indicates each field and a common field across columns in a row means that both tables have the field

## References
- https://docs.google.com/document/d/1PRolH45ja-zjJhRRk2OEdMKN7oznQDXmd3D9d8gkZe8/edit#
- https://docs.google.com/spreadsheets/d/1XpkrCVYczLeDc9EMxltqdLQ692E73XUefsNYNItLUCk/edit
