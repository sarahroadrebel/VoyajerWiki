---
layout: default
title: SFDX - Authorize an Org
nav_order: 1
parent: Development
---

# SFDX - Authorize an Org

## Scope

Authorizing an Org from VSCode so that you have SFDX connected to it.  The VSCode -> SF Extensions setup is completed and now we need to add a Sandbox.

## Details

- CMD SHIFT P for Command Pallette
- SFDX: Authorize an Org command
- Select Sandbox (means https://test.salesforce.com will be where you get directed to for login)
- After successful login you should have it set as your default Org listed in VScode and the status window for Authorization should have updated to Complete
- SFDX stores an access token in the background for you to now use the token to communicate with the sandbox for anything you are doing in VSCode

## Reference

- SFDX Commands "org"
