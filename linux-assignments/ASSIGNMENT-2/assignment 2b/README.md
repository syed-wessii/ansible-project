# Linux Assignment 2B – iUserManager Utility

## Assignment Overview

This assignment implements an `iUserManager` utility using Bash scripting.

The utility provides:
- Team/group creation
- User creation under a team
- Home-directory permission management
- Team shared directories
- Global `ninja` shared directories
- Password and shell management
- User and team deletion
- User and team listing


## Utility Commands

### Create Teams
```bash
sudo ./assignment2-2.sh addTeam amigo
sudo ./assignment2-2.sh addTeam unixkings
```

### Create Users
```bash
sudo ./assignment2-2.sh addUser Rakesh amigo
sudo ./assignment2-2.sh addUser Nitish amigo
sudo ./assignment2-2.sh addUser Sandeep unixkings
sudo ./assignment2-2.sh addUser Abhishek unixkings
```

### Delete User
```bash
sudo ./assignment2-2.sh delUser Rakesh
```

### Delete Team
```bash
sudo ./assignment2-2.sh delTeam amigo
```

### Change Password
```bash
sudo ./assignment2-2.sh changePasswd Rakesh
```

### Change Shell
```bash
sudo ./assignment2-2.sh changeShell Rakesh /bin/bash
```

### List Users
```bash
sudo ./assignment2-2.sh ls User
```

### List Teams
```bash
sudo ./assignment2-2.sh ls Team
```


```

## Permission Requirements

### User Home Directory

Expected permission:

```text
drwxr-x--x
```

Equivalent to:

```text
751
```

| User | Permission |
|---|---|
| Owner | Read + Write + Execute |
| Team | Read + Execute |
| Others | Execute |

Verify:

```bash
ls -ld /home/Rakesh
```

### Team Directory

The `team` directory should provide full access to the owner and same-team members.

```bash
ls -ld /home/Rakesh/team
```

### Ninja Directory

The `ninja` directory should provide full access to members of the `ninja` group.

```bash
ls -ld /home/Rakesh/ninja
```

# Verification

## 1. Verify Teams

```bash
getent group amigo
getent group unixkings
getent group ninja
```



---

## 2. Verify Users and Team Membership

```bash
id Rakesh
id Nitish
id Sandeep
id Abhishek
```



---

## 3. Verify Home Directory Permissions

```bash
ls -ld /home/Rakesh /home/Nitish /home/Sandeep /home/Abhishek
```




---

## 4. Verify Directory Structure

```bash
ls -la /home/Rakesh
ls -la /home/Nitish
ls -la /home/Sandeep
ls -la /home/Abhishek
```
---

## 5. Verify Team Directory

```bash
ls -ld /home/Rakesh/team
ls -ld /home/Nitish/team
ls -ld /home/Sandeep/team
ls -ld /home/Abhishek/team
```

---

## 6. Verify Ninja Directory

```bash
ls -ld /home/Rakesh/ninja
ls -ld /home/Nitish/ninja
ls -ld /home/Sandeep/ninja
ls -ld /home/Abhishek/ninja
```

---

## 7. Verify Same-Team Home Access

Rakesh and Nitish belong to `amigo`.

```bash
sudo -u Rakesh ls /home/Nitish
sudo -u Nitish ls /home/Rakesh
```

---

## 8. Verify Different-Team Access Restriction

Rakesh belongs to `amigo` and Sandeep belongs to `unixkings`.

```bash
sudo -u Rakesh ls /home/Sandeep
sudo -u Sandeep ls /home/Rakesh
```

---

## 9. Verify Same-Team Shared Directory

```bash
sudo -u Rakesh touch /home/Rakesh/team/rakesh_test
sudo -u Nitish ls -l /home/Rakesh/team
sudo -u Nitish touch /home/Rakesh/team/nitish_test
ls -l /home/Rakesh/team
```

---

## 10. Verify Ninja Shared Directory

```bash
sudo -u Rakesh touch /home/Rakesh/ninja/rakesh_ninja_test
sudo -u Sandeep ls -l /home/Rakesh/ninja
sudo -u Sandeep touch /home/Rakesh/ninja/sandeep_ninja_test
ls -l /home/Rakesh/ninja
```

---

## 11. Verify Shell Change

```bash
sudo ./assignment2-2.sh changeShell Rakesh /bin/sh
getent passwd Rakesh
```

Restore Bash:

```bash
sudo ./assignment2-2.sh changeShell Rakesh /bin/bash
getent passwd Rakesh
```

---

## 12. Verify Password Change

```bash
sudo ./assignment2-2.sh changePasswd Rakesh
```

Verify:

```bash
sudo passwd -S Rakesh
```

---

## 13. Verify User Listing

```bash
sudo ./assignment2-2.sh ls User
```

---

## 14. Verify Team Listing

```bash
sudo ./assignment2-2.sh ls Team
```

---

## 15. Verify User Deletion

```bash
sudo ./assignment2-2.sh delUser Abhishek
getent passwd Abhishek
ls -ld /home/Abhishek
```

---

## 16. Verify Team Deletion

Delete remaining users from the team first, then:

```bash
sudo ./assignment2-2.sh delTeam unixkings
getent group unixkings
```

---

