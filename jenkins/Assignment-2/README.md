# Jenkins Assignment 2 --- User Authentication & Authorization

## Overview

This assignment demonstrates Jenkins **User Authentication and
Authorization** for Developer, Testing, and DevOps teams, along with
Google SSO using OAuth 2.0.

Jenkins URL:

`http://localhost:8181`

## Part 1 --- User Authorization

### Jenkins Jobs

Nine dummy jobs were created:

-   Developer: `dev-1`, `dev-2`, `dev-3`
-   Testing: `test-1`, `test-2`, `test-3`
-   DevOps: `devops-1`, `devops-2`, `devops-3`

### Users

**Developer** - `developer-1` - `developer-2` - Access to Developer
jobs - Build, Configure, Workspace permissions

**Testing** - `testing-1` - `testing-2` - Access to Testing jobs and
read access to Developer jobs - Build, Configure, Workspace permissions
on Testing jobs

**DevOps** - `devops-1` - `devops-2` - Access to DevOps jobs, plus read
access to Developer and Testing jobs - Build, Configure, Workspace
permissions on DevOps jobs

**Administrator** - `admin-1` - Full Jenkins access

## Role-Based Authorization

The **Role-Based Strategy** plugin was used.

### Item Roles

  Role          Pattern         Permissions
  ------------- --------------- -----------------------------------
  `developer`   `^dev-.*$`      Build, Configure, Read, Workspace
  `dev-read`    `^dev-.*$`      Read
  `testing`     `^test-.*$`     Build, Configure, Read, Workspace
  `test-read`   `^test-.*$`     Read
  `devops`      `^devops-.*$`   Build, Configure, Read, Workspace

### Role Assignments

  User            Roles
  --------------- -----------------------------------
  `developer-1`   `developer`
  `developer-2`   `developer`
  `testing-1`     `testing`, `dev-read`
  `testing-2`     `testing`, `dev-read`
  `devops-1`      `devops`, `dev-read`, `test-read`
  `devops-2`      `devops`, `dev-read`, `test-read`

## Verification

### Developer

`developer-1` was verified to see:

`dev-1`, `dev-2`, `dev-3`

The account has **Build Now, Configure, and Workspace** permissions.

### Testing

`testing-1` was verified to see:

`dev-1`, `dev-2`, `dev-3`, `test-1`, `test-2`, `test-3`

The account has the required permissions on Testing jobs.

### DevOps

`devops-1` was verified to see all nine jobs:

-   `dev-1`, `dev-2`, `dev-3`
-   `test-1`, `test-2`, `test-3`
-   `devops-1`, `devops-2`, `devops-3`

The account has the required permissions on DevOps jobs.

# Part 2 --- Google SSO

A Google Cloud project named **Jenkins-SSO** was created.

A Web Application OAuth 2.0 client was created and configured with this
authorized redirect URI:

`http://localhost:8181/securityRealm/finishLogin`

The Jenkins **Google Login** plugin was installed.

Jenkins was configured with:

-   Security Realm: **Login with Google**
-   Authorization: **Role-Based Strategy**

Google authentication successfully redirected back to Jenkins. The
initial test produced an Access Denied message because the authenticated
Google account did not yet have `Overall/Read`; after assigning the
required Jenkins role, Google SSO successfully reached the Jenkins
dashboard.

After SSO verification, Jenkins authentication was restored to the
normal Jenkins username/password security realm for subsequent
assignments. The Role-Based Strategy authorization configuration remains
in place.

> **Security:** Never commit OAuth client secrets to GitHub. Any
> screenshot containing a client secret must have the secret completely
> masked.

# Screenshot Evidence

1.  All 9 Jenkins jobs
2.  Developer user job access
3.  Developer job permissions
4.  Testing user job access
5.  Testing job permissions
6.  DevOps user job access
7.  DevOps job permissions
8.  Item role definitions
9.  Role assignments
10. Role-Based Strategy authorization
11. Google Cloud Jenkins-SSO project
12. Google OAuth Web Application client
13. OAuth redirect URI
14. Jenkins Login with Google configuration
15. Google authentication result

# Technologies / Plugins

-   Jenkins
-   Role-Based Authorization Strategy
-   Google Login plugin
-   Google Cloud Console
-   OAuth 2.0

# Conclusion

This assignment demonstrates Jenkins user authentication, team-based
authorization, Role-Based Strategy configuration, job-level permissions,
and Google OAuth SSO integration.
