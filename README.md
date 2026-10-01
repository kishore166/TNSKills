# Script-Controlled ACL: Restrict Record Access Based on Field Value

**ServiceNow System Administrator Capstone Project**  
**Naan Mudhalvan | SmartBridge**

## Team Members

| S. No. | Name | Role |
|---|---|---|
| 1 | Kishore Monish V S | Team Lead |
| 2 | Mohammad Shalia I | Team Member |
| 3 | Nikash R | Team Member |
| 4 | Subburaj G K | Team Member |

## Project Summary

This project implements record-level, field-value-based access control on a custom ServiceNow table. The objective is to ensure that branch users can access and manage records according to their authorized branch and assigned roles.

The project uses the **Institution Details** table (`u_institution_details`) and four Access Control List (ACL) rules to control Read, Create, Write, and Delete operations.

### ACL Configuration

| Operation | Required Role | Description |
|---|---|---|
| Read | `bb1` | Advanced ACL with the condition `Branch is EEE` and a script that allows administrators and users with the `bb1` role. |
| Create | `bb2` | Controls record creation based on role assignment. |
| Write | `bb3` | Controls record modification based on role assignment. |
| Delete | `bb4` | Controls record deletion based on role assignment. |

A test user named **EEE User** was created and assigned all four custom roles: `bb1`, `bb2`, `bb3`, and `bb4`.

### Verification Results

The configured access controls were verified through user impersonation in the ServiceNow instance.

- **EEE User:** Can view the two EEE records and perform Create, Update, and Delete operations as reported by the project tests.
- **User without the required roles:** Is blocked from accessing the protected records and receives a security constraints message.
- **System Administrator:** Can view all four sample records.

These tests demonstrate how ServiceNow ACLs can enforce role-based permissions and restrict record visibility using a field-value condition.

## Project Details

- **Platform:** ServiceNow Personal Developer Instance
- **Project Type:** System Administrator Capstone Project
- **Program:** Naan Mudhalvan
- **Training Partner:** SmartBridge
- **Custom Table:** `u_institution_details`
- **Custom Roles:** `bb1`, `bb2`, `bb3`, `bb4`
- **Build Date:** 28 September 2026
- **Instance:** [dev389813.service-now.com](https://dev389813.service-now.com/)

## Phase-Wise Submission

The project documentation follows the SmartInternz format and is organized into eight phases.

| Phase | Folder | Deliverables |
|---|---|---|
| 1 | `1. Brainstorming & Ideation` | Idea Prioritization, Define Problem Statements, Empathy Map |
| 2 | `2. Requirement Analysis` | Customer Journey Map, Data Flow Diagram, Solution Requirements, Technology Stack |
| 3 | `3. Project Design Phase` | Problem-Solution Fit, Proposed Solution, Solution Architecture |
| 4 | `4. Project Planning Phase` | Project Planning |
| 5 | `5. Project Development Phase` | Code Layout and Reusability, Coding and Solution, Functional Features |
| 6 | `6. Project Testing` | Performance Testing |
| 7 | `7. Project Documentation` | Project Executable Files, Sample Project Documentation |
| 8 | `8. Project Demonstration` | Communication, Demonstration of Proposed Features, Project Demo Planning, Scalability and Future Plan, Team Involvement |

## Repository Structure

The repository contains the implementation scripts, screenshots, demonstration video, and build documentation.

```text
TNSKills/
├── README.md
├── scripts/
│   ├── 01_create_roles_and_assign.js
│   ├── 02_create_columns_and_branch_choices.js
│   ├── 03_insert_sample_records.js
│   ├── 04_link_roles_to_acls.js
│   ├── 05_configure_read_acl_condition_and_script.js
│   └── read_acl_script.js
├── screenshots/
│   └── Milestone-wise evidence screenshots
├── demo/
│   └── demo.mp4
├── docs/
│   └── BUILD_FACTS.md
└── documentation/
    ├── 1. Brainstorming & Ideation/
    ├── 2. Requirement Analysis/
    ├── 3. Project Design Phase/
    ├── 4. Project Planning Phase/
    ├── 5. Project Development Phase/
    ├── 6. Project Testing/
    ├── 7. Project Documentation/
    └── 8. Project Demonstration/
```

### Supporting Evidence

- **`scripts/`** — Contains five background scripts used to configure roles, table columns, sample records, ACL role associations, and the Read ACL condition and script. A standalone Read ACL script is also included.
- **`screenshots/`** — Contains milestone-wise screenshots captured from the ServiceNow instance as implementation evidence.
- **`demo/demo.mp4`** — Contains a narrated walkthrough of the completed project.
- **`docs/BUILD_FACTS.md`** — Records the configuration facts and `sys_id` values for the objects created during implementation.
- **`documentation/`** — Organizes the phase-wise project submission according to the SmartInternz format.

## How to Reproduce the Project

Follow these steps to reproduce the configuration in a ServiceNow Personal Developer Instance.

### Step 1: Create the Test User

Navigate to **User Administration → Users** and create a test user named `EEE User`.

### Step 2: Create Roles and Assign Them

Run the following background script to create the four custom roles and assign them to the test user:

```text
scripts/01_create_roles_and_assign.js
```

The roles are `bb1`, `bb2`, `bb3`, and `bb4`.

### Step 3: Create the Custom Table

Create the **Institution Details** table with the following table name:

```text
u_institution_details
```

### Step 4: Create Columns and Branch Choices

Run the following script to create the seven columns and configure the Branch choices:

```text
scripts/02_create_columns_and_branch_choices.js
```

### Step 5: Insert Sample Records

Run the following script to insert the four sample records:

```text
scripts/03_insert_sample_records.js
```

The sample data contains records for ECE, EEE, and CSE branches.

### Step 6: Elevate Security Permissions

Elevate your ServiceNow session to the `security_admin` role using the user menu before modifying the relevant ACL configurations.

### Step 7: Link Roles to ACLs

Run the following script to associate the custom roles with the Read, Create, Write, and Delete ACLs:

```text
scripts/04_link_roles_to_acls.js
```

### Step 8: Configure the Read ACL

Run the following script to configure the Read ACL condition and script and remove the default role as specified by the project setup:

```text
scripts/05_configure_read_acl_condition_and_script.js
```

The Read ACL uses the `Branch is EEE` condition and the Advanced script to check whether the user has the required authorization.

### Step 9: Verify Access Control

Verify the configuration by impersonating the following users in the ServiceNow instance:

1. **EEE User:** Verify that only the two EEE records are visible and test the permitted Create, Update, and Delete operations.
2. **User without custom roles:** Verify that access to the protected records is denied.
3. **System Administrator:** Verify that all four sample records are visible.

Record the observed results and capture screenshots for the final project documentation.

## Conclusion

This project demonstrates how ServiceNow Access Control Lists can be used to implement role-based permissions and field-value-based record restrictions. By configuring separate ACLs for Read, Create, Write, and Delete operations, the project illustrates how access can be controlled according to user roles and record attributes.

The project also demonstrates the importance of testing security configurations through user impersonation to verify that authorized users receive the intended access while unauthorized users are denied access.

## Future Enhancements

- Extend branch-specific access control to additional branches.
- Implement more granular permissions based on user responsibilities.
- Expand positive and negative test coverage for all CRUD operations.
- Improve documentation and automate repeatable configuration tasks.
- Maintain updated screenshots and demonstration evidence for future reviews.

## Acknowledgements

This capstone project was completed as part of the **Naan Mudhalvan** initiative in collaboration with **SmartBridge**, using the ServiceNow platform to demonstrate system administration and access control concepts.
