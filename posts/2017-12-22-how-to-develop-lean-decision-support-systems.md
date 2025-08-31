# How to develop lean decision support systems?
#### 12/22/2017

![waste-lean](/img/waste-lean.jpeg)

Lately, I was reading about different new hashtags-concepts around agile software development. Many of them make sense in the lean decision support system (DSS) domain. Some of them are #noestimate and #nobacklog. To those, I would also add #nostories and #noprioritization.

### No Backlog (#nobacklog)

The backlog may still exist, but it should not be managed by the DSS developers. The best people to manage a backlog are the business owners. We should stop trying to extract the backlog information from them under pressure. The only thing the developers want to know, really, is "What do you need next?". How the owners find what they need next is really not our business. If they like spreadsheets, or Trello, or post-its or just their memory, it is fine. The owners only need to find what is the next most valuable feature to build.

### No Estimates (#noestimates)

The DSS developers' role is to deliver what the owners need next. Estimations are used to spread a long list of users' stories across time and releases. It is a real waste of time from the point of view of delivering the next most valuable feature. Estimates can also get toxic when they are turned into implied commitments and deadlines. They put unwarranted pressure on developers to deliver on the expected delivery date. Estimates are just that: “estimates”, and if they are unbiased you should expect to miss them half the time. When management inadvertently turns them into deadlines it makes developers lower the quality of what they deliver, in order to meet often arbitrary timelines. This has a pernicious knock-on effect when lowering quality increases the technical debt and weakens the foundation of any future work.

### No Stories (#nostories)

If we agree that we don't need a backlog and that we don't need estimates we really don't need to create a wasteful long list of user stories that require grooming and management. Again, if you bump into a business owner in the elevator he can tell you right away 3 or 4 things they need YESTERDAY. They don't need to fire up Rally or Jira to answer you.

### No Prioritization (#noprioritization)

Yes, the business owners know, always, 3 or 4 things they need YESTERDAY. They don't need to sort a long backlog of 100 stories during a 6-hour work session ... and to do it again every 4 weeks.

### What do you need next?

Basically, we just ask "What do you need next?" 

For each "next" feature, we need to discuss its value and feasibility. If the feature is clearly valuable and feasible, we build it. If we are not sure if it is valuable or feasible we can choose to build a prototype and re-discuss the feature later. If, after discussion, we don't think it is as valuable as it was expected or if we discover that it is not feasible in the current state of our business then we just stop and ask, "What do you need next?".

When we abandon a feature because it is not feasible, the owners will remember that it is not feasible and will not bring it again ... for a little while. One day, they will forget and ask for it again. This is exactly what you want. We want to re-discuss those features in case they are now feasible. 

So, assuming that we don't need all those artifacts (stories, backlog, estimations and priorities), we can now simplify the DSS workflow. Here is the lean decision support system workflow:

![lean-dss](/img/the_lean_dss_workflow.jpg)

### Specifications

When we agree to build, we can still eliminate waste. Owners and Engineers work together to define the specifications as automated tests. The tests are added to a library that keeps growing over time. A test starts its life as a development tool (TDD) and when a feature is delivered the test automatically turns into a regression test. The tests are kept forever and while we develop a feature, they must all be executed to assure we are not breaking any existing features. The Test Library is a much better way to document the requirements. The tests will be written closer to a natural language using, for example, Gherkin and they will be directly executable as-is. That way they stay up to date. This is why some people call those tests "Living Documentation" or "Executable Specifications".

### The owner / developer relationship

There are a lot of pair-programming fans out there. There are also teams that grab “tickets” at random. I understand the efficiency gain from the IT point-of-view and the impression that it reduces bottlenecks and improves knowledge transfer. In reality, what does it bring to our users? Owners of a specific system **love** dealing with the same person every day. They don't have to explain the same thing over and over. They also know where to go for getting help. The vibes of the user group get in sync with the vibes of the developer and it creates friendliness, happiness and a different kind of efficiency. I hate to point that out, but for our users we are like a dentist. Would you want to see a different dentist every time you go for an appointment?

So, **assign a business owner to a specific developer** and let them work together for a long time. Once in a while, when the timing is right, you can re-assign people. But, it should not be forced as part of some master knowledge transfer plan.

Developers can still (and should) ask other developers for help but they should remain the point of contact for their business owner. One last note, by “owners” I don’t mean “business analysts”.

### Conclusion

You build an agile and lean development team by:
* directly connecting developers and business owners.
* removing all the wasteful artifacts and ceremonies from your development process.
* using one set of documents as specifications, documentation and tests. 
* letting the business owners manage their own priorities and needs.

... and asking: "**What do you need next?**"
