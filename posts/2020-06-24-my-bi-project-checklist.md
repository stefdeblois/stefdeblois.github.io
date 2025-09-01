# My Checklist for Business Intelligence and Data Warehousing
#### 06/24/2020

Once in a while, I dump my brain into a list of high-level principles. This is a check list of things to keep in mind when developing data pipelines for Business Intelligence.

#### Do you have automated tests for your transformations?

A good way to document the transformation specifications is to create a library of automated tests that show, with examples, what each transformation should do. The tests are use during development (TDD), get re-executed in future development (regression tests) and become the "living" documentation of your BI system.

#### Do you have an Ingestion Layer?

The Ingestion Layer is a place where the raw data is archived, forever, unchanged. It can be use to recompute everything upstream.

#### Do you have an Integration Layer?

The Integration Layer is a place where the data is cleaned, organized and integrated independently from presentation requirements. The integration is usually supported by a data model of the business.

#### Do you have a Curation Layer?

The Curation Layer is a place where the data is customized and organized for the specific needs of applications and group of users.

#### Do you have a Presentation Layer?

The Presentation Layer is a place where the applications or users can execute queries and receive the data they are looking for.

#### Do you have someone assign to each user group?

Do your users know who to talk to to get new features and datasets?

#### Do you automate as many task as possible?

Are you building a system that perform administrative tasks automatically when possible?

#### Do you generate as much code as possible?

Are you building a system that generate/execute repetitive code automatically?

#### Do you build alerts as reports?

Are you building a system that generate alerts as just another report and from the same source as the regular reports?

#### Do you value users happiness over technical prowess?

Without happy users the system you are building is worthless, no matter how clever it is.

#### Do you use a release backlog?

Short iterations, no estimate far in the future, just enough estimate for the next 2 releases

#### Do you let the architecture emerge?

There is no amount of meetings and brainstorming sessions that will make the perfect solution just emerge. Prototyping and testing ideas will make things happen much faster.

#### Do the developers talks directly to the users?

Are you playing the "telephone game" by inserting business analysts between the data developer and the data consumer?

#### Do you build an immutable process?

no delete, no update, just insert/overwrite

#### Do you keep projects isolated unless they share something?

Are you following some technical dream of building a fully shareable set of tools across all your data products? It is a noble goal but in reality you also want to read your pipelines code like a book for ease of maintenance and improvement. It is about balancing maintainability and complexity.

#### Does your code avoid the balloon effect?

Like using unpartitioned enormous folders of thousands of small files.

#### Do you handle bi-temporality ... and more?

For example, for each event, knowing when it really happen (event-time) vs when it was extracted/loaded (extract-time).

#### Are you respecting your architecture?

Vendors tends to throw your layers away to paint you in the corner.

#### Are you making devops complicated for no reason?

Doing something manually is not a sin if it keeps things simple and clear.
