---
layout: default
title: DB Sync
parent: Technical Documentation
---

# DB Sync
DB Sync is a 3rd party application in SF that facilitates Quickbooks integration items, and runs logic to work with Customers (Accounts) and Vendors (Hotels) to generate invoices and Accounting specific details from Salesforce data.  The major impacted areas are Revenue__c records, Bid__c records, and fields labeled "Sync to QB".  The portal has access to connect to a Quickbooks file on the Quickbooks side and an org on the Salesforce side to run the Workflow logic against, and will sync and create records when triggered to run.  Ultimately it will run on a schedule or be able to be done on demand.
## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

## Scope
{: .fs-6 .fw-300 }
Covers the technical side of the DB Sync implementation:

1. Portal Access
2. Workflows in Portal
3. Automation in SF
4. Setup in RR

## Details
### Portal
The portal is hosted by DBSync and is where you can view logs, jobs, and connection settings and anything else related to DBSync.<br/>
URL: [Portal Login](https://app03.mydbsync.com/appcenter/login)<br/>
User: autumn@roadrebel.com<br/>
Password:  see clay/sarah<br/><>

<img src="https://rr-salesforce.github.io/voyajerwiki/assets/images/dbsync-login.jpg"/>
<br/>
<img src="https://rr-salesforce.github.io/voyajerwiki/assets/images/dbsync-login2.jpg"/>


### Workflows

### Automation in SF

## References
- https://code.visualstudio.com/docs/editor/github