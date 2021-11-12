---
layout: default
title: PT - Overview
parent: Project Management
---
# Pivotal Trackerr

<img src="https://sfdcboss.github.io/voyajerwiki/assets/img/quick_start_1@1x.png">

## What is Pivotal Tracker?
Pivotal Tracker is a straightforward **project-planning** tool that helps **software development teams** form realistic expectations about when work might be completed based on the team’s ongoing performance. Tracker visualizes your projects in the form of stories (virtual cards) moving through your workflow, encouraging you to break down projects into manageable chunks and have important conversations about deliverables and scope. As your team estimates and prioritizes those stories, Tracker divides them into future iterations, learning from your team’s natural pace of work to accurately predict when you will complete future work. Tracker’s transparent team view of priorities means that everyone knows what needs to be done, what is being done, and when it will be completed. Tracker’s agile philosophy not only helps your team keep pace and plan work, but adjust and change course when the unexpected happens, so your team can deliver earlier and more consistently.

Pivotal Tracker encourages a practical **agile software development** process :white_check_mark:, as pioneered by VMware Pivotal Labs.

***
## Story Workflow Diagrams

- Stories can be Chores, Features, Or Bugs. 
- The flow is similar with the exception of chores don't have an Accept/Reject stage prior to being Done. 
  * This is because chores don't follow the QA process which is the reason Accept/Reject would be used.

<img src="<img src="https://sfdcboss.github.io/voyajerwiki/assets/trackers_workflow_1@1x.png">

***

## Story Statuses

- Each status in the Tracker workflow has specific Owners and has specific actions at that step that make up the workflow. 

- The below diagram has information about each step and intended audience and actions.

  * <img src="<img src="https://sfdcboss.github.io/voyajerwiki/assets/storystates.png">

***
### Statuses Continued

> Tracker stories may be in one of several <a href="../terminology#state">states</a>. Valid states for a story depend on the story type and on whether they are in a project with <a href="../     automatic_vs_manual_planning">automatic or manual planning</a>. The following diagram illustrates how Tracker’s workflow progresses as you click through the state buttons located on a story.

- **Unscheduled**
  * All stories in a project’s <a href="../managing_the_Icebox">Icebox</a> are in the <strong>unscheduled</strong> state. 
  * They are waiting to be <a href="prioritizing_stories">prioritized into the Backlog</a>. 
  * You’ll see a <strong>Start</strong> button on unscheduled stories. 
  * Unscheduled stories are always shaded a light blue color.
- **Unstarted**
  * Stories in the <a href="../terminology#backlog">Backlog</a> and <a href="../terminology#current">Current</a> panels that have a <strong>Start</strong> button showing are in the <strong>unstarted</strong> state. 
  * They’re prioritized, but no work is actively being done on them. 
  * Unstarted stories are always shaded a light grey color.
- **Planned**
  * If your project settings specify to <a href="../automatic_vs_manual_planning">NOT plan the Current iteration automatically</a>, you can drag any unscheduled or unstarted story into the Current iteration, regardless of project <a href="../understanding_velocity">velocity</a>. Once these unscheduled or unstarted stories are in the Current iteration of a manually planned project, they are in the <strong>planned</strong> state. The team intends to work on them in the Current iteration. They still appear as unstarted stories, with a <strong>Start</strong> button. Planned stories are always shaded a light grey color.
- **Started**
  * Once you click the <strong>Start</strong> button for any unscheduled or unstarted story, it will move to the <strong>started</strong> state. You’ll see a <strong>Finish</strong> button in all started stories. When you click the Start button, you will be automatically assigned as a story <a href="../story_owners">owner</a>. Unstarted stories are always shaded a light yellow color.
- **Finished**
  * Each team has their own criteria for considering a story “finished”. Tracker was designed with the idea that story owners will click the <strong>Finish</strong> button once they are satisfied that all the necessary development tasks are completed, which may include all testing tasks, and all the code is <a href="../adding_code_commit_comments_to_stories">committed</a> to the source code control system. Your team may have additional criteria, such as completing a code review. You can set up a post-commit hook in your Source Control Management (SCM) system to automatically change the story to the finished state. Finished stories have a <strong>Deliver</strong> button. Finished stories are always shaded a light yellow color.</p>
- **Delivered**
  * Tracker’s <strong>delivered</strong> state is intended to denote that the code for the story has been deployed to an environment where it can be acceptance tested. Each team has their own process for this. Typically, there is a build and deploy pipeline which does continuous integration, runs automated regression tests, and does other activities (which may be automated or manual) to check whether the code is ready for testing. You can set up a <a href="../adding_code_commit_comments_to_stories">post-commit hook</a> in your Source Control Management (SCM) system to automatically change the story to delivered state.
  Delivered stories have two buttons: <strong>Accept</strong> and <strong>Reject</strong>. Delivered stories are always shaded a light yellow color.
- **Rejected**
  * When you discover an issue with a delivered story and need to do more work on it, you can click the <strong>Reject</strong> button to send it back to the queue of work in the Current iteration. When you click the reject button without first expanding a story, you’ll get a popup window where you can add a comment describing what additional work is needed. Rejected stories have a <strong>Restart</strong> button. Clicking the restart button puts the story into the <strong>started</strong> state. Rejected stories are always shaded a light yellow color.
- **Accepted**
  * Each team has their own <a href="https://www.agilealliance.org/glossary/definition-of-done/">definition of done</a> with criteria for accepting a story. It may involve having multiple people such as testers, designers, and product owners agreeing that the story is ready to accept. Tracker is designed with the assumption that clicking the <strong>Accept</strong> button means the story is ready to deploy to production. However, more steps are usually needed in the team’s deploy pipeline before the story’s code is actually released to production. You can use <a href="../organizing_releases">release type stories</a> to denote when a group of stories has been deployed to production by clicking the <strong>Finish</strong> button on the release story after the deploy occurs.</p>


> Accepted stories turn green and move to the top of the Current iteration. You can click <strong>Hide accepted stories</strong> at the top of the panel if you’d rather not see them. 
> When a new iteration begins, the accepted stories are moved to the Done panel. Stories in other states in the Current iteration will remain.</p>
> > For more examples on how states contribute to the workflow, please see <a href="../workflow_overview">Workflow overview</a> on the following page.</p>

***

# A story in the life

## Here’s the life cycle of a typical Example Tracker story (non Road Rebel):

- The _Product Owner_ (PO) prioritizes a story in the Backlog. Then puts a “Design” review on it so the story will be queued up in the design team’s “Design” reviews search results.

- A label is added to a story and then appears in a search panel's results when filtering for that label.

- A designer adds the initial mock-ups to the story and sets their Design review to “Pass”.

  * Design Reviews passed
  * Design Reviews passed

- The _PO and designer_ meet with a tester and a programmer for a “three amigos”-style discovery workshop , two days in advance of an iteration planning meeting (IPM). They discuss this story, using example mapping to elicit examples of desired behavior, specify rules for the story, and document outstanding questions.
Documenting story rules, examples of desired behavior, and outstanding questions

- The whole team gets together two days later for the IPM. They discuss the rules and examples for the story. The PO has the answer to the outstanding question. They talk about the dependency on the server side story, and various options for implementing it. They estimate the story at 3 points. However, as noted in the description with the story link, the story depends on a server side story that is not yet done, so the PO adds a “blocker” to the story. A 'blocked' blocker showing in a story preview

- The blocking server-side story is accepted, automatically resolving the story’s blocker. When the story is the next unstarted story in the Current panel, a developer pair starts it, which automatically assigns them as story owners. They test drive the code at the unit level, as well as with automated acceptance tests based on the story rules and examples. They explore different searches, such as using regular expressions, and consult with the tester and PO as new questions come up. They click the Finish button, but feel the story needs more exploratory testing, and that they should double-check design implementation, so they add the “Test (QA)” and “Design” Reviews to it. 

*** 
### Reviews on stories

- When the CI build for the story’s code passes, the artifacts are automatically deployed to a test environment. The tester verifies this, and clicks the Deliver button. The tester pairs with the designer to verify the look and feel of the search. The designer is satisfied with the results and sets the “Design” review to “Pass”. After more exploratory testing, the tester identifies two minor issues that are outside the scope of the story. They add new stories for these in the “shopping” epic. Satisfied that the story provides the right value for users, the tester sets the “Test (QA)” review to “Pass”, and adds a “Product Owner (PO)” review so that the PO notices the story is ready for them to do final acceptance. Reviews on stories

- Note: The My Work panel will show all stories in Delivered status (i.e., ready for to be accepted or rejected) for which you are the requester, so you can easily see which are ready to accept.
- The PO notices a cosmetic issue, but it’s not something that has to be fixed before the beta release. They create another story in the “shopping” epic to address it later, rather than reject the story. They accept the story, which moves up into the green accepted stories at the top of the Current panel.

### How is your team doing?
- All stories are not created equal. Straightforward ones may be accepted within hours of being started. With more complicated ones, we may find that some rules were missed or the feature can’t quite be implemented as designed after all. Clicking that Reject button may sound harsh, but it just means there’s a bit more to be done, and iterating a few times is sometimes necessary. When rejecting a story, add comments with details about why it was rejected, including screenshots and any other useful information.

- Keep tabs on story cycle time and rejection rate by checking the Cycle time report in the Analytics section of Tracker. Your team can use this information to identify problem areas and try experiments to shorten cycle time and reduce rejection rate.

- Watch the Cumulative Flow chart to see story states by day during the iteration. This helps identify problem areas such as falling into a “mini waterfall” scenario, with no stories being completed until the end of the iteration.

- Need more control over planning the current iteration? Tracker provides a way to let you manually plan the current iteration. Check out the Automatic vs. Manual Planning section in Using Projects.

### Tips for handling bugs
- As noted in the Getting Started article on Tracker’s workflow, bug stories follow the same workflow as feature stories. However, bugs sometimes follow different paths. You may want to preserve the information in a bug story, even if the team isn’t going to do any work specifically on that story.

- Your team may decide not to fix a particular bug. When this happens, teams typically mark the bug story accepted, and tag it with an appropriate label, such as “wont fix.” It’s always helpful to add a comment describing the reason.

- An issue reported as a bug may turn out to be a missing feature, or it could be expected behavior. You might prefer to change the story type from bug to feature. Or, you could tag it with a “not a bug” label and change the state to Accepted.

- While fixing bugs as soon as possible is a good practice, sometimes a bug story may linger long enough that it is fixed by a different story. An option is to comment on what was tried then tag it with a “not reproducible” label and change the state to accepted.

### Tips for using Chores and Releases
- Chores are stories that are necessary but provide no direct, obvious value to the customer (e.g., “Update SSL Certs”). Because they don’t typically require extra validation when they’re finished, the states for chores are just unscheduled (when in the Icebox), unstarted, started, and accepted.

- Releases are milestone markers that allow your team to track progress toward concrete goals (e.g., stakeholder or investor demos, software launches, etc.). It’s possible to specify target dates for releases. All stories for a milestone or release should go above the marker for it. Releases are automatically placed in the started state upon being created or dragged in the Backlog, and also have the unscheduled (when in the Icebox) and accepted states. For more please see Organizing releases.

# Videos
<h2 id="video-demos">Video Demos</h2>

<p>If you have a few more minutes to spare, get to know Tracker better with these short videos. You can watch all of them here, or find them in the relevant topics as you go through the rest of the Getting Started guide.</p>

<p>If you’ve time for a deeper dive, we’ve also provided a pre-recorded “Intro to Tracker” webinar that includes a 20 minute guided tour of Tracker, followed by some great Q&amp;A!</p>

<div class="video-group">
  <div class="video-item">
    <a id="getting_started" href="https://www.youtube-nocookie.com/watch?v=wKFkZWAH1vw" class="video-item__video" data-lity="">
      <img class="" src="https://www.pivotaltracker.com/help/kb_assets/getting_started@1x.png" srcset="https://www.pivotaltracker.com/help/kb_assets/getting_started@1x.png 1x,
             https://www.pivotaltracker.com/help/kb_assets/getting_started@2x.png 2x" alt="&amp;#39Getting Started&amp;#39 video" />

    </a>

    <h3> Getting Started (2:50) </h3> This quick tour covers the basics, as well as Tracker's fundamental units of work: stories.
  </div>

  <div class="video-item">
    <a href="https://www.youtube-nocookie.com/watch?v=grFxyiJpjuU" class="video-item__video" data-lity="">
      <img class="" src="https://www.pivotaltracker.com/help/kb_assets/writing_stories@1x.png" srcset="https://www.pivotaltracker.com/help/kb_assets/writing_stories@1x.png 1x,
             https://www.pivotaltracker.com/help/kb_assets/writing_stories@2x.png 2x" alt="&amp;#39Writing Stories&amp;#39 video" />

    </a>

    <h3> Writing Stories (3:08) </h3> Learn how to write stories, as well as all you need to know to start adding features, bugs, and chores to your project.
  </div>
</div>

<div class="video-group">
  <div class="video-item">
    <a href="https://www.youtube-nocookie.com/watch?v=v5y5Bt6MilI" class="video-item__video" data-lity="">
      <img class="" src="https://www.pivotaltracker.com/help/kb_assets/prioritizing@1x.png" srcset="https://www.pivotaltracker.com/help/kb_assets/prioritizing@1x.png 1x,
             https://www.pivotaltracker.com/help/kb_assets/prioritizing@2x.png 2x" alt="&amp;#39Prioritizing and Estimating Complexity&amp;#39 video" />

    </a>

  <h3> Prioritizing and Estimating Complexity (1:46) </h3>  Understand how to prioritize your stories in Tracker and estimate their complexity, so you can start to see what can be completed when.
  </div>

  <div class="video-item">
    <a href="https://www.youtube-nocookie.com/watch?v=nvXEGWC50rc" class="video-item__video" data-lity="">
      <img class="" src="https://www.pivotaltracker.com/help/kb_assets/delivering_stories@1x.png" srcset="https://www.pivotaltracker.com/help/kb_assets/delivering_stories@1x.png 1x,
             https://www.pivotaltracker.com/help/kb_assets/delivering_stories@2x.png 2x" alt="&#39;Delivering Stories&#39; video" />

    </a>

    <h3> Delivering Stories (1:45) </h3> Follow the process of taking your stories in Tracker from start to delivered.
  </div>
</div>

<div class="video-group">
  <div class="video-item">
    <a href="https://www.youtube-nocookie.com/watch?v=gOmfnWj7cK8" class="video-item__video" data-lity="">
      <img class="" src="https://www.pivotaltracker.com/help/kb_assets/velocity@1x.png" srcset="https://www.pivotaltracker.com/help/kb_assets/velocity@1x.png 1x,
             https://www.pivotaltracker.com/help/kb_assets/velocity@2x.png 2x" alt="&amp;#39Velocity and Story Acceptance&amp;#39 video" />

    </a>

    <h3> Velocity and Story Acceptance (2:56) </h3> Make sure your stories are ready for release and learn how Tracker sets your team's velocity.
  </div>

  <div class="video-item">
    <a href="https://www.youtube-nocookie.com/T-w_GUTtO9I?rel=0" class="video-item__video" data-lity="">
      <img class="img-bordered" src="https://www.pivotaltracker.com/help/kb_assets/tracker_webinar@1x.png" srcset="https://www.pivotaltracker.com/help/kb_assets/tracker_webinar@1x.png 1x,
             https://www.pivotaltracker.com/help/kb_assets/tracker_webinar@2x.png 2x" alt="&#39;Intro to Tracker Webinar&#39; video" />

    </a>

    <h3> Intro to Tracker webinar (64:12) </h3> One of our recent webinars, with a tour of Tracker and some great Q&amp;A!
  </div>
</div>
