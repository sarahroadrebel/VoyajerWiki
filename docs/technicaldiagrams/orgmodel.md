---
layout: default
title: Development Org Model
parent: Technical Diagrams
---

# Org Model for Deployments
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Scope

This diagram should cover all system connections at a high level without getting into the technical details.

## Diagram

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vTQunR9nwT8r4D54AtjhEvSVMlTBIGlQf48isHGt5FSmb-Jc0ZRaTVMPVs2CuPFG6MT_ruGZz3e-89L/embed?start=true&loop=false&delayms=3000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

## Details

### Sandbox/Org Breakdown

The diagram above shows orgs of a few different types which are listed in the following table

| Sandbox    | Purpose   | Type |
|:---------------|:---------------------|:-------------------------|
| rrdev | QA testing org where features are tested | DEVELOPER_PRO |
| preprod | UAT testing org where we perform UAT in addition to staging for Production deployments | Partial |
| Hotfix Sandbox | A sandbox created at the time of a bug being reported, direct path to Production.  Does not follow the same rrdev preprod path | Partial |