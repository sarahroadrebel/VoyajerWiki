---
layout: default
title: Data Model - Room Types
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

This diagram covers the areas where Room Types are used and attached to several different objects. (*Housing__c* Object - *Room Types and Ops* Record Type)

## Diagram

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vR6dIWlPMqIG181z12-nYEqZxoFaXDZ4KfYPdSqi8qKL9pTht-ia3b1jfMc6J9OULV97XKwQfetE7t7/embed?start=false&loop=false&delayms=3000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

## Details

|Object (RecordType)|Description|Linkage|
|-------------|
|Housing (Preferred Room Types)|The selections on the Housing Details tab that are at the beginning tab of the Dashboard|Production_CC__c|
|Housing (Preferred Room Types)|The selections on the Housing Details tab that are at the beginning tab of the Dashboard|Sales_Housing__c (links to Stay, not Sales Housing record Type)|
|Housing (Sales Housing)|The container for Stays under a Production use record type *Sales Housing* and have children Stays|Sales_Housing__c on Hotel Housing/CH/IR|
|Housing (Hotel Housing/CH/IR)|The "Stay" that represents the timeframe at the Hotel for a data range|Sales_Housing__c parent and Production_CC__c grandparent|
|Bid (Housing Bid)|The Bid which is a child of the Stay record and is the parent of the final room type children record that have Rate Information|Housing__c on Bid up to Production|
|Housing (Room Types)|The representations of the different rooms on the Bid itself which contain Rate information and tie to Revenue records further down|Bid__c parent|
