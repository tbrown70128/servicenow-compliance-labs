# Lab 01: Users, Groups, and Roles (Role-Based Access in ServiceNow)

## Goal
Build a small role-based access model in a ServiceNow Personal Developer Instance (Australia release) and test it by impersonating each user. The lab shows how roles assigned to groups control what each person can see, and where access turns out broader or narrower than expected.

## Environment
- ServiceNow Personal Developer Instance (PDI), Australia release
- Admin account used for setup, then impersonation to test each test user
- All users below are fake test accounts with example.com emails

## What I built

**Users (4)**

| User ID | Purpose |
|---|---|
| test.requester | Submits access requests |
| test.manager | Approves requests (used in Lab 2) |
| test.fulfiller | Works and fulfills approved requests |
| test.auditor | Reviews access and exceptions |

**Groups (2)**

| Group | Members | Roles assigned |
|---|---|---|
| Access Fulfillment | test.fulfiller | itil |
| Compliance Review | test.auditor | report_user |

Roles are assigned to groups, not directly to users, so access can be reviewed and changed in one place.

## How I tested
I used Impersonate User to log in as each test user, opened the All navigator, and searched for "users" to check whether User Administration was reachable.

## Results

| User | Group | What the navigator showed | User administration |
|---|---|---|---|
| test.fulfiller | Access Fulfillment | Broad menu: Incident, CMDB Workspace, Configuration, Password Reset, Service Catalog, Asset, Process Mining, Dependency Views, Compliance, CSDM, Email Client, Security Center, Service Level Management, and more | Not reachable. Searching "users" returned only unrelated configuration items |
| test.requester | none | Short menu: Self-Service, App Engine, Content Taxonomy, Document Management, Platform Analytics, Usage Tracking Consent, Password Reset, Process Mining, System OAuth, Targeted Communications | Not reachable. Searching "users" returned no results |
| test.auditor | Compliance Review | Same short menu as the requester | Not reachable. Searching "users" returned no results |

Other things I opened as test.fulfiller:
- **Follow On Tasks:** loaded, filtered to tasks assigned to the user, no records.
- **Security Center > Security Tasks:** loaded, with 0 tasks in every count.
- **Compliance:** the menu section contains one entry, My Follow On Tasks. It opens the same Follow On Tasks list, which is empty. The section name suggests broad compliance access, but in practice it only exposes a task list.

## Key findings
1. **The fulfiller role is broad.** The fulfiller reached many operational areas, including Security Center, even though the account only needs to work request tasks. The user record explains why: assigning the single itil role through the group produced a long list of inherited roles on the user, such as sn_incident_write, task_editor, sn_change_read, cmdb_query_builder_read, and dependency_views, each marked as inherited. One role assignment can carry a lot of access, so in a real environment a fulfillment group should be reviewed against least privilege.
2. **The requester and auditor menus matched.** Adding report_user to the auditor group did not change the top-level menu compared with the requester. A menu entry alone does not show whether someone can read the records, so a real auditor needs explicit read access to the records being audited (requests, approvals, exceptions).
3. **No test user can manage users.** Only the admin account has User Administration, which is the expected result for these roles.

## Gap to address
The auditor account currently has no clear way to review requests or approvals. I plan to revisit this in Lab 3 when the policy exception process exists, and document the roles needed for read access.

## Compliance relevance
The lab touches common access control ideas that appear in NIST SP 800-53 under the Access Control (AC) family, such as account management, access enforcement, and least privilege. I have not yet verified the exact control numbers against the publication, so I will add the mapping after checking the control text.

## What I learned
- Assigning roles to groups keeps access reviewable.
- Testing with impersonation catches surprises that reading role names does not.
- "Least privilege" has to be checked against what a role actually opens up, not what it is called.

## Screenshots to include
- Users list filtered to `test.`
- Group list showing Access Fulfillment and Compliance Review
- Roles tab for each group
- Navigator as test.fulfiller, test.requester, and test.auditor
- "users" search result for each test user
- Security Tasks and Follow On Tasks pages as test.fulfiller

