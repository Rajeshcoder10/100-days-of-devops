# Day 70: Configure Jenkins User Access

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/1_task.png" alt="Image">
</div>

## Content:

> Today I worked on configuring user access and permissions in Jenkins for the Nautilus DevOps team.

> The objective was to create a new Jenkins user, implement Project-based Matrix Authorization Strategy, configure global permissions, remove anonymous access, and grant limited access to an existing Jenkins job.

* * *

## 🔹 What I Learned

*   Creating users in Jenkins
    
*   Understanding Jenkins authorization strategies
    
*   Configuring Project-based Matrix Authorization
    
*   Managing global user permissions
    
*   Restricting anonymous access
    
*   Assigning job-level permissions
    
*   Implementing role-based access control principles
    
*   Securing Jenkins environments through least-privilege access
    

* * *

## 🔹 Task Requirement

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/2_task_details.png" alt="Image">
</div>

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/3_tak_details.png" alt="Image">
</div>

The Nautilus DevOps team required Jenkins user access configuration with the following specifications.

### Jenkins Access Requirement

| Requirement | Value |
| --- | --- |
| Username | admin |
| Password | Adm!n321 |
| Access Method | Jenkins Web UI |

### User Creation Requirement

| Field | Value |
| --- | --- |
| Username | jim |
| Password | YchZHRcLkL |
| Full Name | Jim |

### Permission Requirements

| User | Permission |
| --- | --- |
| admin | Overall Administer |
| jim | Overall Read |
| jim (job level) | Job Read Only |
| anonymous | No Permissions |

* * *

## 🔹 Steps I Followed

### 1\. Accessed Jenkins Web Interface

Clicked the Jenkins button from the lab top navigation bar.

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/4_jenkins_button.png" alt="Image">
</div>

Successfully reached the Jenkins login page.

* * *

### 2\. Logged into Jenkins

Entered administrator credentials.

Username:

admin

Password:

Adm!n321

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/5_admin_login.png" alt="Image">
</div>

Successfully logged into the Jenkins dashboard.

Observed sections such as:

*   Dashboard
    
*   Build History
    
*   Manage Jenkins
    
*   Credentials
    
*   Nodes
    

* * *

### 3\. Created a New Jenkins User

Navigated to:

Manage Jenkins → Security → Users

Selected:

Create User

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/6_manage_jenkins.png" alt="Image">
</div>

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/7_users.png" alt="Image">
</div>

Entered the following details:

Username:

jim

Password:

YchZHRcLkL

Confirm Password:

YchZHRcLkL

Full Name:

Jim

Clicked:

Create User
<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/8_create_users.png" alt="Image">
</div>

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/9_user_creation.png" alt="Image">
</div>

Verified that the new user was successfully created.


<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/10_user_verified.png" alt="Image">
</div>
* * *

### 4\. Verified Authorization Strategy Plugin Availability

Checked whether the Project-based Matrix Authorization Strategy was available.

In environments where the plugin is not installed, Jenkins requires installation of the Matrix Authorization Strategy plugin.

If required:

Manage Jenkins → Plugins → Available Plugins

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/11_manage_jenkins.png" alt="Image">
</div>

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/12_plugins.png" alt="Image">
</div>

Searched for:

Matrix Authorization Strategy

Installed the plugin and restarted Jenkins.

Waited for the Jenkins login page to reappear before continuing.

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/13_matrix_authorization_strategy.png" alt="Image">
</div>

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/14_download.png" alt="Image">
</div>

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/15_restarting.png" alt="Image">
</div>

Logged in again using administrator credentials.

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/16_admin.png" alt="Image">
</div>

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/17_plugin_verification.png" alt="Image">
</div>

* * *

### 5\. Configured Project-based Matrix Authorization Strategy

Navigated to:

Manage Jenkins → Security

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/18_manage_jenkins.png" alt="Image">
</div>

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/19_security.png" alt="Image">
</div>

Located the Authorization section.

Selected:

Project-based Matrix Authorization Strategy

This enabled granular permission control at both global and project levels.

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/20_authorization.png" alt="Image">
</div>

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/21_add_user.png" alt="Image">
</div>

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/22_user.png" alt="Image">
</div>

* * *

### 6\. Configured Global Permissions for Admin User

Added the admin user to the authorization matrix.

Verified that admin retained:

Overall → Administer

This permission grants full administrative control over Jenkins.

* * *

### 7\. Configured Global Permissions for Jim

Added user:

jim

Granted only:

Overall → Read

No additional permissions were assigned.

This allowed Jim to access Jenkins while preventing administrative or configuration changes.

* * *

### 8\. Removed Anonymous User Permissions

Located the anonymous user entry in the permission matrix.

Removed all assigned permissions.

Verified that anonymous users no longer had access to:

*   Jenkins Dashboard
    
*   Jobs
    
*   Configuration Pages
    
*   Administrative Features
    

This improved Jenkins security by preventing unauthenticated access.

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/23_permissions.png" alt="Image">
</div>

* * *

### 9\. Saved Global Security Configuration

Clicked:

Save

Jenkins successfully applied the updated authorization settings.

Verified:

*   Admin retained full control
    
*   Jim had read-only global access
    
*   Anonymous access was removed
    

* * *

### 10\. Configured Job-Level Permissions

Opened the existing Jenkins job.

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/24_job.png" alt="Image">
</div>

Navigated to:

Job → Configure

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/25_job_configure.png" alt="Image">
</div>


Located project authorization settings.

Added user:

jim

Granted only:

Job → Read

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/26_enable.png" alt="Image">
</div>

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/27_user.png" alt="Image">
</div>

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/28_permissions.png" alt="Image">
</div>

Ensured all other permissions remained unchecked, including:

*   Build
    
*   Configure
    
*   Delete
    
*   Workspace
    
*   Discover
    
*   SCM
    
*   Agent
    
*   Credentials
    

Saved the job configuration.

* * *

### 11\. Verified User Access

Logged out from the admin account.

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/29_signout.png" alt="Image">
</div>

Logged in using:

Username:

jim

Password:

YchZHRcLkL

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/30_user_login.png" alt="Image">
</div>

Verified that:

*   Jenkins dashboard was accessible
    
*   Existing job was visible
    
*   Job details could be viewed
    
*   Build and configuration options were unavailable
    

This confirmed that permissions were working as expected.

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/31_user_permissions.png" alt="Image">
</div>


* * *

## 🔹 Simple Explanation of Jenkins Authorization

### User Management

Manage Jenkins → Security → Users

Jenkins allows administrators to create multiple user accounts.

Each user can be assigned specific permissions based on organizational requirements.

* * *

### Project-based Matrix Authorization Strategy

Project-based Matrix Authorization Strategy

This authorization model allows administrators to:

*   Define global permissions
    
*   Define project-level permissions
    
*   Assign permissions to individual users
    
*   Implement least-privilege access control
    

It provides much more flexibility than simple authorization methods.

* * *

### Overall Read Permission

Overall → Read

This permission allows users to:

*   Access Jenkins
    
*   View dashboards
    
*   View available jobs
    

Without this permission, users cannot log into Jenkins successfully.

* * *

### Overall Administer Permission

Overall → Administer

This is the highest permission level in Jenkins.

It allows administrators to:

*   Manage users
    
*   Configure security
    
*   Install plugins
    
*   Create and modify jobs
    
*   Control the Jenkins server
    

* * *

### Anonymous User Access

Anonymous User

Anonymous represents users who have not logged in.

Removing permissions from anonymous users helps secure Jenkins by preventing unauthorized access.

* * *

### Job Read Permission

Job → Read

This permission allows users to:

*   View job details
    
*   View build history
    
*   Monitor job status
    

It does not allow users to:

*   Trigger builds
    
*   Modify jobs
    
*   Delete jobs
    
*   Access sensitive configuration
    

* * *

### Principle of Least Privilege

Least Privilege

The least-privilege principle means users receive only the permissions required to perform their tasks.

In this task:

*   Admin receives full administrative control.
    
*   Jim receives read-only access.
    
*   Anonymous users receive no access.
    

This minimizes security risks and protects CI/CD infrastructure.

* * *

## 🔹 My Understanding

This task strengthened my understanding of Jenkins security and access control mechanisms.

I learned how Jenkins authorization strategies work, how permissions can be assigned at both global and project levels, and how implementing the principle of least privilege improves the security of CI/CD environments.

* * *

## 🔹 What I Found Interesting

I found it interesting how Jenkins provides very granular permission management through the Project-based Matrix Authorization Strategy.

Rather than giving users broad permissions, administrators can precisely control what each user can view or modify. This makes Jenkins highly suitable for enterprise environments where different teams require different levels of access while maintaining strong security practices.

* * *

### Topics Covered

- ***Jenkins***
- ***Jenkins-users***
- ***Jenkins-authorization***
- ***user-permissions***
- ***Jenkins-server***
- ***Jenkins-plugins***


**Previous Task**: [Day 69: Install Jenkins Plugins](../Day_69/day_69.md)

**Next Task**: [Day 71: Configure Jenkins Job for Package Installation](../Day_71/day_71.md)