---
layout: default
title: System Landscape
parent: Technical Diagrams
---

# Landscape Diagram Details
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Scope

This diagram should cover all system connections at a high level without getting into the technical details.

## Diagram

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vTE4czCGIT1pEw73YZMW9k9_ADHhZz3k6ankxX8t6ACEZn8SkDIhZDv1CcyDsZeruqCuRxuBBQC6_UA/embed?start=true&loop=false&delayms=3000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

## Details

### Connection Breakdown

The diagram above shows a legend where you can identify if something is out of the box Salesforce "native" and from Salesforce, or a third party app or integration.


#### Salesforce Native

| Functional Area    | Purpose   | Users |
|:---------------|:---------------------|:-------------------------|
| Community | Used to manage bids on a national level and allows Account related data to be shared with login authentication | External Hotel National Rep |
| Landing Pages | Force.com Sites hosted on the platform for Vendor Bid Submission and Vendor Closeout Reporting | External Hotel Vendor Rep |
| Conga Composer | Used to manage templated PDF creation for Forms | Coordinator and Hotel Rep/Client |
| Conga Sign | Used to manage Signature forms such as Hotel Contract, Rate Agreement, etc | Coordinator and Hotel Rep/Client |
| DB Sync | Used to manage invoicing and sending Revenue details to Quickbooks.  Bids and Revenue records are Sent to Quickbooks via Sync to QB flag | System/Accounting |

#### Non Salesforce Native

| Functional Area    | Purpose   | Users |
|:---------------|:---------------------|:-------------------------|
| Pivotal Tracker | Used to manage bids on a national level and allows Account related data to be shared with login authentication | External National Rep |
| Google Maps | Used to get distances between locations based on vendors and venues in the system | System |
