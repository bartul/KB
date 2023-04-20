# Branching strategy

## Branching

Continuous Integration was invented as an antidote to the complexities caused by Branching.

Branching is about hiding information: dividing up the work, and working on it independently, in ways that team members cannot see each others’ work. Branching comes with the risk that one person’s work may be incompatible with the changes of their team-mates.

We want to limit this divergence and aim for only one interesting version of the system - the current one. We achieve this by working:

- to make small changes to Trunk/Master and continuously evaluate them, 
- to share information so that changes are transparent, and developers can see if their code works with everyone else’s on the team,
- so that when developers make a correct change, everyone else has that same version, almost instantaneously, and
- so that our software is always in a releasable state, and any of these small changes to Trunk/Master may be deployed into production.

Ideal-world Branching Strategy is: 
> “Don’t Branch!”

If branches exist at all, they should be tiny, few in number, and short-lived, i.e: merged at least once per day. When we are working well, we will merge every 10, or 15 minutes, to get fast feedback on our changes and optimise the Deployment Pipeline to be efficient and thorough.


## Trunk-based development

A source-control branching model, where developers collaborate on code in a single branch called ‘trunk’ *, resist any pressure to create other long-lived development branches by employing documented techniques. They therefore avoid merge hell, do not break the build, and live happily ever after.

* main for the Git community since 2020 (master with unsavory connotations before)



### 2022 Accelerate State of DevOps Report

Trunk-based development is the practice of continuously merging code into the trunk and avoiding long-lived feature branches. This practice is considered a complement to continuous integration and has been shown for years to accelerate software delivery velocity.

Due to the shift in demographics this year around years of experience on the job, we are able to see that experience matters when implementing trunk-based development. Last year we had 40% of respondents state they had 16+yrs on the job and this year that category represented just 13%. Continuing to validate our “Delivery Depends” theme, we see that folks with less experience overall have less positive results around trunk-based development and see:
- Decreased overall software delivery performance
- Increased amounts of unplanned work 
- Increased error-proneness
- Increased change failure rate

Individuals with 16+ years of experience that use trunk-based development realize the benefits of the practice and see:
- Increased overall software delivery performance 
- Decreased amounts of unplanned work
- Decreased error-proneness
- Decreased change failure rate

This is likely due to the additional practices required to successfully implement Trunk-based development. Teams that do not have rigorously enforced rules around never walking away from a broken trunk or that do not use gated code branches and auto-roll back code that breaks the trunk will certainly experience pain when trying to develop on the trunk.
However, the presence of trunk-based development shows a positive impact on overall organizational performance.

±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±±



Trunk base development
Branches are short livens, no need for special naming






Commit message needs to contain work item presiding with a hash (#) character, e.g. #

The solution uses a single long lived branch - main

# Main
The main branch is the latest, stable development branch that contains any code changes that have been approved through pull requests and merged in.
The main does not necessarily represent what is currently deployed to production. Instead it is the latest version of developer-approved and tested features that we have for the product. Some of these features will typically not be in production yet and the features are still subject to change in a QA/PO/Validation review.

# Short lived branch naming format
Branches should conform to the following format:

<type>/<id>/<short summary>
  │     |            └─⫸ Summary in present tense. Not capitalized. No period at the end.
  │     │
  │     └─⫸ Id of the ADO work item that is linked to this item. 
  │
  └─⫸ Commit Type: build|ci|docs|feat|fix|perf|refactor|test
The <type> and <summary> fields are mandatory, the (<scope>) field is optional.

# Pull Request Name Format

Pull Request should conform to the following format:
<type>: <short summary>
  │                 │
  │                 └─⫸ Summary in present tense. Not capitalized. No period at the end.
  │
  └─⫸ Commit Type: build|ci|docs|feat|fix|perf|refactor|test
The <type> and <summary> fields are mandatory, the (<scope>) field is optional.


Type
Must be one of the following:

build: Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
ci: Changes to our CI configuration files and scripts (examples: CircleCi, SauceLabs)
docs: Documentation only changes
feat: A new feature
fix: A bug fix
perf: A code change that improves performance
refactor: A code change that neither fixes a bug nor adds a feature
test: Adding missing tests or correcting existing tests  
