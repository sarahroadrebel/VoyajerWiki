---
layout: default
title: Data Model - Traces
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

This diagram shows specific connections between Tasks and their parent objects.  The Parent Object dictates what type of "Trace" it is.  Each type of trace has a parent/child representation in the diagram separated out.

## Diagram

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vSrOzyEVxgp8CvUMwelQDrdG5XSAxLLaYSIPBdR_8xp9OvqBEG-OfzjBgEsjEdWnqgrXojupF6MkOYm/embed?start=false&loop=false&delayms=3000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

## Details

|Field|Usage|
|-------------|
|OwnerId|Used for task assignment and is the Coordinator responsible for finishing the task.|
|ActivityDate|Used as a Date field that is a due date for the specific task to be done.|
|Subject|Standard field that gets populated with a "Trace Subject" which is a workflow action to be done, or a status based identifier for a task.|
|Status|Open and Completed are the statuses and an Open status would be set for active traces.  Completed traces have the `Status=Completed` and that omits it from dashboards.|
|Priority|The priority of Housing Status Traces is set and is either No Follow Up, Low Follow Up, Urgent Follow Up and is a selection that can be made by Coordinators for searches on the Trace Dashboard and when they set Housing Statuses.|
|WhatId (Related To Id)|Object Id of either Production,Bid_c,Housing_c, which are "All Other Tasks", "Contract Tasks", and "Housing Status Traces" respectively.|
