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
- 

