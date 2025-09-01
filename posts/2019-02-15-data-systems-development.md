# Data Systems - Development
#### 02/15/2019

In a team, over time, waste and complexity tend to naturally increase. It is also true for a data development team. We react to challenges and problems by adding new ceremonies and development steps that feel like a quick improvement but that sometimes create long term waste when the crisis is over.

Even if you consider yourself "Agile", some new artifacts and techniques can bring more benefits and eliminate waste. Let's review some of them ...

### The Release Backlog

The classic product backlog is a place where users (product owner) add every "idea", every "new features" and every "change" in a format we call "user story". Unfortunately, when the complexity increase, the backlog tend to get more and more managed by the developers. At this point, the developers keep trying to extract the backlog information from the users under pressure. 

There is no doubt that the best people to manage a backlog are the users. But, do the backlog really need to be an enormous list of "wishes" that will most likely never get completed? The only thing the developers need to know, really, is "What do you need next?". How the users find what they need next is really not our business. If they like spreadsheets, or Trello, or post-its or just their memory, it is fine. The users only need to know what are the next 2 or 3 most valuable feature to build. A lof of users can tell you that in 2 minutes while waiting at the coffee shop.

By creating the **release backlog** with just a few features or changes by release is a more efficient way of describing what we want to build next. We should create those releases as we go, keep them small (a week or two), and never plan more than 2 or 3 releases into the future. A release needs to be completed and DELIVERED before starting the next one.

In a classic "Scrum" setup, it is like working with a few short sprint backlogs without using a product backlog. We let the users manage the long term view of the system any way they want.

### Emergent Architecture

If you are the system architect and expect a long fully loaded product backlog to design "All The Things" at once you will have to adapt. First, designing using a long term multi-months backlog is a very dangerous habit. Business priorities will change and impact the value of the stories in front of you ... and those changes will occur "AFTER" the architecture is designed (and may be built). Typically, you will build complex architecture components that are "just in case" or that "we will need next year". Those things create waste in maintenance and complexity for zero immediate value. Worst, they may be never needed if the system behavior is changing. 

You have to let the architecture emerge from release to release and accept that refactoring is an important part of the development and architectural process.

### Just Enough Estimation

The developers' role is to deliver what the users need next. Classic estimation processes are spreading a long list of user stories across multiple months. It is a waste of time from the point of view of delivering the next most valuable features. 

Estimates can also get toxic when they are turned into implied commitments and deadlines. They put unwarranted pressure on developers to deliver on the expected delivery date. Estimates are just that: “estimates”, and if they are unbiased you should expect to miss them half the time. When management inadvertently turns them into deadlines it makes developers lower the quality of what they deliver, in order to meet often arbitrary timelines. This has a pernicious knock-on effect when lowering quality increases the technical debt and weakens the foundation of any future work.

By using small Release Backlogs, the need to do large multi-months estimation sessions disappear. We focus on the next few valuable things to build as defined by the users. As a team, we do some rough estimates and we draw the line where we think the stories can be delivered in a week or two. Estimating beyond those few top stories is a waste because the business priorities will change and impact the value of the remaining stories. Picking the next stories for a release is a "game day decision", happening just as we get ready to start the development.

The release backlog estimation process should take a minute if not a few seconds. At first, in a new system, the team will miss things and get the estimates wrong half of the time. It is normal. Those are estimates, not commitments. As the team grow and gets more comfortable with the system, the users and the tools the estimates will get more accurate ... but expecting perfection here is a waste. Do it quick and move on. It is better to spend your time coding than estimating.

### Pragmatic User Stories

If we agree that we don't need a product backlog and that we don't need multi-months estimates then we really don't need to create a wasteful long list of user stories that require grooming and management. Again, if you bump into a business owner in the elevator he can tell you right away 3 or 4 things they need YESTERDAY. They don't need to fire up Rally or Jira to answer you. So, the developers should work with a short release backlog describing the few things we need to build next. The users are free to manage the list of long term "features" in any way they prefer. 

### Implied Prioritization

Yes, the users know, always, 3 or 4 things they need YESTERDAY. They don't need to sort a long backlog of 100 stories during a 6-hour work session ... and to do it again every months. By using a release backlog the prioritization process is implied.

### Just-in-Time Specifications

When the planning of the next release is done, we can still eliminate waste. Users and Developers work together to define the specifications as automated tests. The tests are added to a library that keeps growing over time. A test starts its life as a development tool (TDD) and when a feature is delivered the test automatically turns into a regression test. The tests are kept forever and while we develop a feature, they must all be executed to assure we are not breaking any existing features. The Test Library is a much better way to document the requirements. 

If possible, the tests will be written closer to a natural language using, for example, Gherkin and they will be directly executable as-is. If they need to be coded in Python or other languages, it is still much better and useful than having no tests and no specifications.

### The user/developer relationship

There are a lot of pair-programming fans out there. There are also teams that grab “tickets” at random. I understand the efficiency gain from the IT point-of-view and the impression that it reduces bottlenecks and improves knowledge transfer. But, in reality, what does it bring to our users? 

Users of a specific system **love** dealing with the same person every day. They don't have to explain the same thing over and over. They also know where to go for getting help. The vibes of the users get in sync with the vibes of the developer and it creates friendliness, happiness and a different kind of efficiency. I hate to point that out, but for our users we are like a dentist. Would you want to see a different dentist every time you go for an appointment?

So, **assign a group of users to a specific developer** and let them work together for a long time. Once in a while, when the timing is right, you can re-assign people. But, it should not be forced as part of some master HR plan. You should avoid any "telephone game" by **directly** connecting **real** users to developers. Adding a layer of "business analysts" between the developers and the users just add to the confusion. Any serious developer who want to grow will appreciate being directly involved with the users and learning about the business.

Developers can still (and should) ask other developers for help but they should remain the point of contact for their users.

### Conclusion

You build a sustainable and lean development team by:
* directly connecting developers and users.
* using a small release backlog
* removing wasteful artifacts and ceremonies from your development process.
* using automated tests as specifications 
* letting the users manage their own priorities and needs.
