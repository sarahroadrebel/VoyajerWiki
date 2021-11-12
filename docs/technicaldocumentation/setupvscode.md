---
layout: default
title: Wiki - Set Up VSCode
parent: Technical Documentation
---

# Setup VS Code
{: .no_toc }

## Scope
{: .fs-6 .fw-300 }
Covers the installation of VSCode specifically for contributing to the wiki, not setting up for Salesforce Development.  Should cover installation and how to submit an edit or new entry to the Wiki as an alternative to making edits directly at the Github URL.

1. Signup for Github
2. Download VSCode
3. Install and Clone Repository (contains documentation)
4. Submit documentation change for Publishing

*Note:  This is the alternative to doing edits directly to the files on Github.com and gives flexibility to view previews and many other things.

## Details

### Signup for Github
You will need a github account to connect in VSCode,  since the Wiki is hosted on Github.  It will be a one time creation step of the account and access granted to your user, and after that the login would be for any subsequent updates that require an edit to the files on the Server.

### Download VS Code
VSCode is a very popular IDE (Code Editor) and the website will direct you to the proper download for Windows or Mac.  Link here: [Download VS Code](https://code.visualstudio.com/)

### Install and Clone Repository
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