# ServiceNow Compliance Labs

Hands-on labs in a free ServiceNow Personal Developer Instance (Australia release), focused on the access, approval, exception, and reporting work that compliance and GRC teams do. Each lab has its own folder with a write-up, what I built, what I found, and screenshots.

## About this project
I am building ServiceNow experience as part of a move into governance, risk, and compliance (GRC) work. These labs are practice projects in a developer instance, not production experience. All users and data are fake test accounts.

## Labs

| Lab | Topic | Status |
|---|---|---|
| [Lab 01](lab-01-users-groups-roles) | Users, groups, and roles: a role-based access model tested with impersonation | Complete |
| Lab 02 | Access request catalog item with manager approval and fulfillment tasks | Planned |
| Lab 03 | Policy exception tracking with approvals, expiration, and control mapping | Planned |
| Lab 04 | Compliance reports and a metrics dashboard | Planned |

## What each lab covers
- **Lab 01:** How roles assigned to groups control access, and where a role turns out broader than expected.
- **Lab 02:** A request and approval process with an audit trail, built in Flow Designer.
- **Lab 03:** A process for requesting, approving, tracking, and expiring policy exceptions, tied to NIST SP 800-53 control families.
- **Lab 04:** Reports and a dashboard for request volume, approval times, and exception risk.

## Tools
- ServiceNow Personal Developer Instance
- Flow Designer, Service Catalog, reports and dashboards
- NIST SP 800-53 as a reference for control mapping

## Notes
- No credentials or instance details are stored in this repository.
- Control mappings are added only after checking them against the NIST text.
