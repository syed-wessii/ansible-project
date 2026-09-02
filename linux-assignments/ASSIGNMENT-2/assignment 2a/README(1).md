# Linux Assignment 2.1

## Basic Linux Commands – Users, Groups, Permissions and User Management

### Objective

This assignment covers Linux user and group management, primary and secondary groups, directory permissions, access testing, login shells, password management, `umask`, and deletion of users and groups.

---

## 1. Create Users

```bash
sudo useradd -m neha
sudo useradd -m vipul
sudo useradd -m abhishek
```

### Verification

```bash
getent passwd neha vipul abhishek
```



---

## 2. Create Groups

```bash
sudo groupadd linux
sudo groupadd sigma
```

### Verification

```bash
getent group linux sigma
```


> 

---

## 3. Change Primary Group

```bash
sudo usermod -g sigma neha
sudo usermod -g sigma abhishek
```

### Verification

```bash
id neha
id abhishek
```


> 

---

## 4. Add Secondary Group

```bash
sudo usermod -aG linux neha
sudo usermod -aG linux abhishek
```

### Verification

```bash
id neha
id abhishek
```


> 

---

## 5. Create Alpha Group

```bash
sudo groupadd alpha
```

### Verification

```bash
getent group alpha
```


> 

---

## 6. Create Nkhil and Priyashi

```bash
sudo useradd -m -G linux,alpha nkhil
sudo useradd -m -G linux,alpha priyashi
```

### Verification

```bash
id nkhil
id priyashi
```


> 

---

## 7. Set Home Directory Permissions

Required:
- Owner: read, write, execute
- Group: read, execute
- Others: execute only

```bash
sudo chmod 751 /home/neha
sudo chmod 751 /home/vipul
sudo chmod 751 /home/abhishek
sudo chmod 751 /home/nkhil
sudo chmod 751 /home/priyashi
```

### Verification

```bash
ls -ld /home/neha /home/vipul /home/abhishek /home/nkhil /home/priyashi
```


> 

---

## 8. Create Team and Linux Directories

```bash
for user in neha vipul abhishek nkhil priyashi
do
    sudo mkdir -p /home/$user/team
    sudo mkdir -p /home/$user/linux
done
```

### Verification

```bash
sudo find /home/neha /home/vipul /home/abhishek /home/nkhil /home/priyashi -maxdepth 1 -type d
```


> 

---

## 9. Configure Team Directory Permissions

### Sigma team

```bash
sudo chown root:sigma /home/neha/team
sudo chown root:sigma /home/abhishek/team
sudo chmod 770 /home/neha/team
sudo chmod 770 /home/abhishek/team
```

### Alpha team

```bash
sudo chown root:alpha /home/nkhil/team
sudo chown root:alpha /home/priyashi/team
sudo chmod 770 /home/nkhil/team
sudo chmod 770 /home/priyashi/team
```

### Verification

```bash
ls -ld /home/neha/team /home/abhishek/team /home/nkhil/team /home/priyashi/team
```


> 

---

## 10. Configure Linux Directory Permissions

Replace `linuxtrainer` with the actual Linux trainer username.

```bash
sudo chown linuxtrainer:linux /home/neha/linux
sudo chown linuxtrainer:linux /home/abhishek/linux
sudo chown linuxtrainer:linux /home/nkhil/linux
sudo chown linuxtrainer:linux /home/priyashi/linux
sudo chown linuxtrainer:linux /home/vipul/linux

sudo chmod 770 /home/neha/linux
sudo chmod 770 /home/abhishek/linux
sudo chmod 770 /home/nkhil/linux
sudo chmod 770 /home/priyashi/linux
sudo chmod 770 /home/vipul/linux
```

### Verification

```bash
ls -ld /home/*/linux
```


> 

---

## 11. Check Alpha User Access to Sigma Team Directory

```bash
su - nkhil
ls -ld /home/neha/team
ls /home/neha/team
exit
```

Expected result:

```text
Permission denied
```



---

## 12. Check Vipul Access to Sigma Team Directory

```bash
su - vipul
ls -ld /home/neha/team
ls /home/neha/team
exit
```


> 

---

## 13. Change Vipul Shell to Service User

```bash
sudo usermod -s /usr/sbin/nologin vipul
```

### Verification

```bash
getent passwd vipul
```

The last field should be:

```text
/usr/sbin/nologin
```


> 

---

## 14. Force Abhishek to Change Password

```bash
sudo chage -d 0 abhishek
```

### Verification

```bash
sudo chage -l abhishek
```


> 

---

## 15. Change Nkhil Password

```bash
sudo passwd nkhil
```

### Verification

```bash
sudo passwd -S nkhil
```

> 

---

## 16. List Created Users and Groups

### Users

```bash
getent passwd | grep -E '^(neha|vipul|abhishek|nkhil|priyashi):'
```

### Groups

```bash
getent group | grep -E '^(linux|sigma|alpha):'
```


> 

---

## 17. Check Neha's Default Shell

```bash
getent passwd neha
```

The last field is the default login shell, commonly `/bin/bash`.


> 

---

## 18. Check Default File and Directory Permissions

```bash
umask
umask -S

touch /tmp/testfile
mkdir /tmp/testdir

ls -l /tmp/testfile
ls -ld /tmp/testdir
```

Change the temporary `umask`:

```bash
umask 027
```

Verify:

```bash
umask
umask -S
```

Create new objects:

```bash
touch /tmp/testfile2
mkdir /tmp/testdir2

ls -l /tmp/testfile2
ls -ld /tmp/testdir2
```


> 

---

## 19. Delete Vipul User

```bash
sudo userdel -r vipul
```

### Verification

```bash
getent passwd vipul
ls -ld /home/vipul
```

No output from `getent passwd vipul` confirms deletion.


> 

---

## 20. Delete Linux Group

Complete all Linux-group verification before deleting it.

```bash
sudo groupdel linux
```

### Verification

```bash
getent group linux
```

No output confirms deletion.


> 

---

## Final Verification

### Remaining users

```bash
getent passwd | grep -E '^(neha|abhishek|nkhil|priyashi):'
```

### Remaining groups

```bash
getent group | grep -E '^(sigma|alpha):'
```

### Deleted user and group

```bash
getent passwd vipul
getent group linux
```

---


---

## Important Note

For the Linux trainer permission requirement, replace `linuxtrainer` with the actual Linux trainer username before running the `chown` commands.
