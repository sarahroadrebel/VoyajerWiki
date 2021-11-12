---
layout: default
title: Sandboxes
nav_order: 1
parent: Development
---

# Sandboxes
{: .no_toc }

Details related to DevOps and developing Voyajer on the Salesforce platform.
{: .fs-6 .fw-300 }

## Sandbox List

| Sandbox    | Purpose   | Type |
|:---------------|:---------------------|:-------------------------|
| rrdev | QA testing org where features are tested | DEVELOPER_PRO |
| preprod | UAT testing org where we perform UAT in addition to staging for Production deployments | Partial |
| Hotfix Sandbox | A sandbox created at the time of a bug being reported, direct path to Production.  Does not follow the same rrdev preprod path | Partial |

## Sandbox Data

Below is a script that can be run to create data in a sandbox.  Just run the task from VSCode to create the data in whatever your default Org is set to in VSCode and it will update you from there.

This should contain: 
- An Account (Vendor)
- A Contact (customer)
- A Production
- A Production Association for Primary Contract Coordinator and Primary Housing Coordinator
- A Stay
- Preferred Room Types


