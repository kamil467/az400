test
second commit
squash commit2

squash commit1
rebase 1
rebase 2
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

#
### What is the difference between TFS and git ?


Team Foundation Version Control (TFVC):
- TFVC is a centralized version control system. Typically, team members have only one version of each file on their dev machines. Historical data is maintained only on the server. Branches are path-based and created on the server.

- Git: Git is a distributed version control system. Git repositories can live locally (on a developer's machine). Each developer has a copy of the source repository on their dev machine. Developers can commit each set of changes on their dev machine, perform version control operations such as history, and compare without a network connection.
- 
### Code Review:
High-quality reviews start with high-quality feedback. The keys to great feedback in a pull request are:
- Have the right people review the pull request.
- Make sure that reviewers know what the code does.
- Give actionable, constructive feedback.
- Reply to comments promptly.

#
 ### Technical Debt:
 There are five key traits to measure for higher quality.
 most of these can be determined by runnning various quality scans on codebase.
- Reliability:Reliability measures the probability that a system will run without failure over a specific period of operation. It relates to the number of defects and availability of the software. Several defects can be measured by running a static analysis tool.
Software availability can be measured using the mean time between failures (MTBF).
Low defect counts are crucial for developing a reliable codebase.

- Maintability : It relates to the codebase's size, consistency, structure, and complexity - we have code metrics dotnet tool available for analysing maintaibility of code base.
-   Testability: Testability can be measured based on how many test cases you need to find potential faults in the system.
-   Portability: Portability measures how usable the same software is in different environments. It relates to platform independence.
                  - using different agents to build and deploying into multiple enviornments before release it to production.
                  - It's also good to set your compiler warning levels as high as possible and use at least two compilers. How to use two compilers for dotnet ?
                  - Enforcing a coding standard also helps with portability. 
- Reusability : loose coupling , shared code base - how do you find reusability ? running static analysis.

#### Placing good coding standard practices and regular code scans will helps to reduce the technical debt and maintain good code.

### Git Hooks
Git hooks allow you to run custom scripts whenever certain important events occur in the Git life cycle—for example, committing, merging, and pushing.
- client side hooks
- server side hooks
#
#### client side hooks:
- this hooks can be stored in .git/hooks folder in root repository.
- you can implement checks like pre commit, post commit, pre-push.
- scripts executes on client-side.
- Verifying work Item ID association in your commit message Preventing you and your team from committing faulty code.
- Pre , post checkout events

#

#### Server side hooks
  - executes on server side.
  - gitHub : it fires certain event when git operations are performed. those can be handled using webhooks. like trigger an API call when certain code committed.
    
#
#### Purge Git Repository
The most common situations are where you want to:
Significantly reduce the size of a repository by removing history.
Remove a large file that was accidentally uploaded.
Remove a sensitive file that shouldn't have been uploaded.

-  `git filter-repo` tool can be used to rewrite history.
-  BFG Repo-Cleaner
        - BFG Repo-Cleaner is a commonly used open-source tool for deleting or "fixing" content in repositories. It's easier to use than the git filter-branch command. For a single file or set of files, use the --delete-files option:

#
#### Type of Quality Process in each stages

- Continuous deployment should include passive penetration tests as well as SSL and infrastructure scans.
- Nightly test runs should include infrastructure scans and active penetration tests.
- Continuous integration should include an Open-Source Software (OSS) vulnerability scan.
-  The integrated development environment/pull request step should include static code analysis and code reviews.

  

