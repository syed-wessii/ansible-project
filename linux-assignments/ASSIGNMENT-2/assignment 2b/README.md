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
<img width="1050" height="310" alt="image" src="https://github.com/user-attachments/assets/eab60a79-41b0-4a99-bb63-b3a797793ee0" />

```bash
getent group amigo
getent group unixkings
getent group ninja
```



---

## 2. Verify Users and Team Membership
<img width="1050" height="278" alt="image" src="https://github.com/user-attachments/assets/18dd0cfd-940a-4639-93b2-79f7365f5e79" />

```bash
id Rakesh
id Nitish
id Sandeep
id Abhishek
```



---

## 3. Verify Home Directory Permissions
<img width="1050" height="338" alt="image" src="https://github.com/user-attachments/assets/0893d7e7-b35b-4119-951e-e1e561381c7c" />

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
<img width="1050" height="115" alt="image" src="https://github.com/user-attachments/assets/c7137468-1a38-4102-bf4b-0e0db1ecb9ba" />

```bash
ls -ld /home/Rakesh/team
ls -ld /home/Nitish/team
ls -ld /home/Sandeep/team
ls -ld /home/Abhishek/team
```

---

## 6. Verify Ninja Directory
<img width="1050" height="238" alt="image" src="https://github.com/user-attachments/assets/121c8f18-b413-42d2-bd93-387ae64c0c54" />

```bash
ls -ld /home/Rakesh/ninja
ls -ld /home/Nitish/ninja
ls -ld /home/Sandeep/ninja
ls -ld /home/Abhishek/ninja
```

---

## 7. Verify Same-Team Home Access
<img width="1050" height="177" alt="image" src="https://github.com/user-attachments/assets/fd78bdae-a88b-419a-b4b9-912ca950a50f" />

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
<img width="1050" height="177" alt="image" src="https://github.com/user-attachments/assets/78b9a1f8-98bf-48b9-b2f1-0d9368d39f0c" />

```bash
sudo -u Rakesh touch /home/Rakesh/team/rakesh_test
sudo -u Nitish ls -l /home/Rakesh/team
sudo -u Nitish touch /home/Rakesh/team/nitish_test
ls -l /home/Rakesh/team
```

---

## 10. Verify Ninja Shared Directory
<img width="1050" height="349" alt="image" src="https://github.com/user-attachments/assets/6615e9bb-3c0c-4382-89de-2ea63c2ce569" />

```bash
sudo -u Rakesh touch /home/Rakesh/ninja/rakesh_ninja_test
sudo -u Sandeep ls -l /home/Rakesh/ninja
sudo -u Sandeep touch /home/Rakesh/ninja/sandeep_ninja_test
ls -l /home/Rakesh/ninja
```

---

## 11. Verify Shell Change
<img width="1050" height="267" alt="image" src="https://github.com/user-attachments/assets/9d25eb50-fef6-4c21-a444-d6dd9cc2731e" />

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
<img width="1050" height="172" alt="image" src="https://github.com/user-attachments/assets/23bf1769-381a-4d7f-ad39-06944d056f4b" />

```bash
sudo ./assignment2-2.sh changePasswd Rakesh
```

Verify:

```bash
sudo passwd -S Rakesh
```

---

## 13. Verify User Listing
<img width="1050" height="357" alt="image" src="https://github.com/user-attachments/assets/ee946c72-fd19-4a80-bbd1-37155ed9465e" />

```bash
sudo ./assignment2-2.sh ls User
```

---

## 14. Verify Team Listing
<img width="1050" height="383" alt="image" src="https://github.com/user-attachments/assets/f7d5b65b-f36c-4b40-bf22-dcda0b670ada" />

```bash
sudo ./assignment2-2.sh ls Team
```

---

## 15. Verify User Deletion
<img width="1050" height="209" alt="image" src="https://github.com/user-attachments/assets/ba8c5e0e-f75e-4f41-ad48-e837de704902" />

```bash
sudo ./assignment2-2.sh delUser Abhishek
getent passwd Abhishek
ls -ld /home/Abhishek
```

---

## 16. Verify Team Deletion
<img width="1050" height="209" alt="image" src="https://github.com/user-attachments/assets/8a476ecc-55f2-4d74-aad4-0df88d18aea4" />

Delete remaining users from the team first, then:

```bash
sudo ./assignment2-2.sh delTeam unixkings
getent group unixkings
```

---

