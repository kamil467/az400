  ### Skills Measured
  - Configure process and communications 10-20 %
  - Design and implement Source Control
  - Design and Implement build and release pipelines - 40 - 45 %
  - Develop a security compilance plan
  - Implement an instrumentation strategy


### Sorter Cycle Time:

When you adopt DevOps practices:
- You shorten your cycle time by working in smaller batches. ( features)
- Using more automation. (build , test , review , deployment tools)
- Hardening your release pipeline. ( PR , code quality , status checks and scans)
- Improving your telemetry. ( logs)
- Deploying more frequently.

#

#### Design and implement Source Control
#
Choosing repo stragety ?
Monorepo vs multi repo advantages and challenges

| Monorepo | Multi-repo|
| ---- | ---|
| Advantages: easy to share and maintain code, easy for applying tools and policies , single view of discoverability | helps in microservices architecture, team ownership, individual teams own the repos, promote code decoupling |
| Challenges : too complex to maintain when code base large , single code change could affect multiple teams |  applying policies , maintaining standards will be difficult acorss repositories , lack of shared code support |

# 
- branch stragety - feature, release branches
- PR process
- Work Item correlation
- Merge methods in PR ( rebase, squash)
- content recovery for repos and branches( recover content from accidental deletion)
- Access policies (repos and branch level)

### Git branching workflow startegy:

Trunk-based development ( also known as feature branch development)
- Trunk-based development is a logical extension of Centralized Workflow.
- The core idea behind the Feature Branch Workflow is that all feature development should take place in a dedicated branch instead of the main branch.
- This encapsulation makes it easy for multiple developers to work on a particular feature without disturbing the main codebase.
- It also means the main branch should never contain broken code, which is a huge advantage for continuous integration environments.
#
Forking workflow
The Forking Workflow is fundamentally different than the other workflows discussed in this tutorial.
Instead of using a single server-side repository to act as the "central" codebase, it gives every developer a server-side repository.
It means that each contributor has two Git repositories:
- A private local one.
- A public server-side one.

It is best suit for open-source projects.
- Typically ,you fork the official repo and keep a forked copy of that repo in online.
- This new copy serves as their personal public repository—no other developers can push to it, but they can pull changes from it (we'll see why this is necessary in a moment).
- When they're ready to publish a local commit, they push the commit to their public repository—not the official one.
- the contributor can accept your commits without giving you access to main repo.
- Then, they file a pull request with the main repository, which lets the project maintainer know that an update is ready to be integrated.

  The following is a step-by-step example of this workflow:
  #
  
- A developer 'forks' an 'official' server-side repository. It creates their server-side copy.
- The new server-side copy is cloned to their local system.
- A Git remote path for the 'official' repository is added to the local clone.
- A new local feature branch is created.
- The developer makes changes to the new branch.
- New commits are created for the changes.
- The branch gets pushed to the developer's server-side copy.
- The developer opens a pull request from the new branch to the 'official' repository.
- The pull request gets approved for merge and is merged into the original server-side repository.

#
 ### Main/develop branch characteristics:

- The main branch is the only way to release anything to production.
- The main branch should always be in a ready-to-release state.
- Protect the main branch with branch policies.
- Any changes to the main branch flow through pull requests only.
- Tag all releases in the main branch with Git tags.
   tags are best for managing releases
     scenarios :
   - each PR megre should create a new version of branch.
   - it is always better to create a tag and deploy the code from that tag
     
### Feature Branch
#
- Use feature branches for all new features and bug fixes.
- Use feature flags to manage long-running feature branches.
- Changes from feature branches to the main only flow through pull requests.
- Name your feature to reflect its purpose.

### Pull Request

- Review and merge code with pull requests.
- Automate what you inspect and validate as part of pull requests. - adding status checks jobs in PR such as code quality , unit test , build task for head branch, rebase branch from target branch. 
- Tracks pull request completion duration and set goals to reduce the time it takes. - I will look how long a PR takes time for completion.
- 
### release branch cycle :

A critical bug is identified in production how to roll-out the fix ?

- we know every PR/ release we do create tags, just create a feature branch from the release tag.
- fix the bugs in that feature branch
- deploy the code from feature branch to production.
- Now it is time for merge feature branch bug fix to main branch.
- create tag in feature branch for bug release  and create PR for merging the feature branch bug fixes to main branch. ( you know why we creating tag ? from feature branch ? - once your PR merged, you will probably delete the feature branch but tags will remain available in the history )

There is an alternative approach instead of directly deploying from feature branch , you can merge your changes into main branch and trigger the pipeline.
in most scenarios your main pipeline configured with well set of jobs and policies. so it is a best practice that deploying code from main branch.

some times , you will not have time for testing your biug fixes in other environment , it might be a super priority bug fix - you will choose the right deployment model for this.

#

### Forking vs. cloning
- It's essential to note that "forked" repositories and "forking" aren't special operations.
- Forked repositories are created using the standard git clone command.
- Forked repositories are generally "server-side clones" managed and hosted by a Git service provider such as Azure Repos.
- There's no unique Git command to create forked repositories.
- A clone operation is essentially a copy of a repository and its history.


