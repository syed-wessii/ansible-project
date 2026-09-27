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
<img width="1919" height="574" alt="image" src="https://github.com/user-attachments/assets/f0a56f14-a033-4dba-94d2-b7063fbf66e5" />

<img width="1919" height="552" alt="image" src="https://github.com/user-attachments/assets/2fd303e1-64a1-4ad0-b642-305fd152a372" />

<img width="1919" height="576" alt="image" src="https://github.com/user-attachments/assets/86faf4d3-45a2-42ee-8201-ce7c570a11ab" />



### Users

**Developer** - `developer-1` - `developer-2` - Access to Developer
jobs - Build, Configure, Workspace permissions

<img width="1918" height="568" alt="image" src="https://github.com/user-attachments/assets/3792100e-f82c-4da1-894f-f1040e3049c1" />

<img width="1916" height="579" alt="image" src="https://github.com/user-attachments/assets/1c2cfa4e-2b50-4452-b5b7-e13cb6bb5fc6" />



**Testing** - `testing-1` - `testing-2` - Access to Testing jobs and
read access to Developer jobs - Build, Configure, Workspace permissions
on Testing jobs

<img width="1914" height="669" alt="image" src="https://github.com/user-attachments/assets/a634c376-063e-4876-a391-a4d154e4af57" />

<img width="1918" height="572" alt="image" src="https://github.com/user-attachments/assets/c68aab14-5ad6-440e-9119-dd7cf6e10671" />



**DevOps** - `devops-1` - `devops-2` - Access to DevOps jobs, plus read
access to Developer and Testing jobs - Build, Configure, Workspace
permissions on DevOps jobs

<img width="1918" height="826" alt="image" src="https://github.com/user-attachments/assets/a060f7e3-763e-42f3-88b3-1c9a19221e46" />

<img width="1919" height="600" alt="image" src="https://github.com/user-attachments/assets/7625de41-1466-45e5-96f1-6b6b599a7542" />



**Administrator** - `admin-1` - Full Jenkins access

## Role-Based Authorization

<img width="1919" height="600" alt="image" src="https://github.com/user-attachments/assets/9afc19b6-c352-40b7-bfdf-ca1ccd65e842" />


The **Role-Based Strategy** plugin was used.

### Item Roles

  Role          Pattern         Permissions
  ------------- --------------- -----------------------------------
  `developer`   `^dev-.*$`      Build, Configure, Read, Workspace
  `dev-read`    `^dev-.*$`      Read
  `testing`     `^test-.*$`     Build, Configure, Read, Workspace
  `test-read`   `^test-.*$`     Read
  `devops`      `^devops-.*$`   Build, Configure, Read, Workspace

  <img width="1917" height="999" alt="image" src="https://github.com/user-attachments/assets/41931fcf-cd0f-4b0c-aa1e-d6d601e8560e" />


### Role Assignments

  User            Roles
  --------------- -----------------------------------
  `developer-1`   `developer`
  `developer-2`   `developer`
  `testing-1`     `testing`, `dev-read`
  `testing-2`     `testing`, `dev-read`
  `devops-1`      `devops`, `dev-read`, `test-read`
  `devops-2`      `devops`, `dev-read`, `test-read`

<img width="1919" height="483" alt="image" src="https://github.com/user-attachments/assets/8577bcb5-9e53-40d8-a45a-a5817c79da78" />

<img width="1919" height="495" alt="image" src="https://github.com/user-attachments/assets/83a8f495-c203-483f-a392-9147c992e585" />

<img width="813" height="741" alt="image" src="https://github.com/user-attachments/assets/c518b6db-edc0-4353-b420-edca9705d9f7" />


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

<img width="813" height="741" alt="image" src="https://github.com/user-attachments/assets/f3dd8c94-b56d-4224-8fdf-704fcf16210b" />

<img width="1909" height="991" alt="image" src="https://github.com/user-attachments/assets/ce0d6ad9-1410-4d60-b726-56ad6ca68ece" />



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
