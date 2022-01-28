---
layout: default
title: DB Sync
parent: Technical Documentation
---

# DB Sync
{: .no_toc }

## Scope
{: .fs-6 .fw-300 }
Covers the technical side of the DB Sync implementation:

1. Portal Access
2. Workflows in Portal
3. Automation in SF
4. Setup in RR

## Details

DB Sync is a 3rd party application in SF that facilitates Quickbooks integration items, and runs logic to work with Customers (Accounts) and Vendors (Hotels) to generate invoices and Accounting specific details from Salesforce data.  The major impacted areas are Revenue__c records, Bid__c records, and fields labeled "Sync to QB".  The portal has access to connect to a Quickbooks file on the Quickbooks side and an org on the Salesforce side to run the Workflow logic against, and will sync and create records when triggered to run.  Ultimately it will run on a schedule or be able to be done on demand.

### Portal
You will need a github account to connect in VSCode,  since the Wiki is hosted on Github.  It will be a one time creation step of the account and access granted to your user, and after that the login would be for any subsequent updates that require an edit to the files on the Server.

### Workflows
VSCode is a very popular IDE (Code Editor) and the website will direct you to the proper download for Windows or Mac.  Link here: [Download VS Code](https://code.visualstudio.com/)

### Automation in SF
Once downloaded the prompts and all defaults can be used on VSCode.  You should get to a point where you are at the entry point in VSCode where it is asking you for a workspace or folder to start to work out of.   At this point you are as far as you need to be and it's installed.  Now we can "Clone" the repository (which is ultimately just copying the files as-is now, to a folder that has the capabilities of watching for changes in the files in that folder ("Git" on the filesystem)).

Luckily they make this very easy and it's a copy and paste of a URL into a button.   The link is on Github.com on the Repository homepage.

1. Navigate to the repo [https://github.com/sfdcboss/voyajerwiki](https://github.com/sfdcboss/voyajerwiki).
2. Click the "Code" button and copy the HTTPS URL for the Repository
    - ![](https://sfdcboss.github.io/voyajerwiki/assets/images/clonerepo.jpg)
3. Take this URL and plug it into VSCode under the "Clone Repository" option.  It will copy the files and enable the folder it creates to talk to Github.com later for you to post changes and new files.
    - ![](https://sfdcboss.github.io/voyajerwiki/assets/images/clone-from-github.gif)
4. Allow it to create the folder and finish and you are complete
    - *Note: You will be prompted to "Open" the folder it created that will take you this folder to work in.*

## References
- https://code.visualstudio.com/docs/editor/github