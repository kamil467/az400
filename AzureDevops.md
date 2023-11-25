**Azure DevOps Access Plans**
- Basic
- Basic + Test
- Stakeholder
- Visual Studio Subscription
#

** Permissions in Azure DevOps **
- Organizations levels
- Project Level

#
### Project Level: 
They are typically security groups which has colections of different permissions assigned.
A security group can be part of another security group 
Below arein-built security groups provided by DevOps
- Contributors
- Build Administrators
- Project Administrators
- Readers
- Project Valid Users
- Release Administrators
- TeamName Team eg; MedicalServices Team
#
**Case How do you give access user to a specific permission not adding to security groups ? **

#### CASE : To create and save queries on Shared Folder ,an user should be part of Project Adminstartor Group. But the group has more priviledge than what actually required for user. How do you give access user to only for shared queries ?

Answer:
 -  see below , user cannot save shared queries
<img width="1440" alt="Screenshot 2023-11-25 at 12 19 26 PM" src="https://github.com/kamil467/az400/assets/31802480/e7d990cb-a115-4dfb-8c1f-810b82f8883b">

Please find the screenshot below where you can make give premissions for queries:

<img width="1440" alt="Screenshot 2023-11-25 at 1 11 54 PM" src="https://github.com/kamil467/az400/assets/31802480/bfe98f45-25af-4006-98ad-fc6124e72cd7">

#
**How you can give permissions to edit Dashboards on Project ?***

Answer:
- similarly queries , dashboard has security settings where you can modify the particular user permission for dashboard.

#





