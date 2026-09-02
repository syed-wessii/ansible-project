# Linux Assignment 2.1

## Basic Linux Commands – Users, Groups, Permissions and User Management

### Objective

This assignment covers Linux user and group management, primary and secondary groups, directory permissions, access testing, login shells, password management, `umask`, and deletion of users and groups.

---

## 1. Create Users

<img width="1065" height="356" alt="image" src="https://github.com/user-attachments/assets/13445ce8-dc9e-452c-aa8f-dc101c26756d" />

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

<img width="1065" height="261" alt="image" src="https://github.com/user-attachments/assets/06e56b81-f6b3-44a9-91db-ae907f817bdb" />

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

<img width="1065" height="174" alt="image" src="https://github.com/user-attachments/assets/8f80d56f-b71f-4da2-8524-2955e5543ae3" />

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
<img width="1065" height="174" alt="image" src="https://github.com/user-attachments/assets/8f80d56f-b71f-4da2-8524-2955e5543ae3" />

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
<img width="1065" height="194" alt="image" src="https://github.com/user-attachments/assets/dff90204-db1c-4d29-9ea3-9598e52d5d91" />

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
<img width="1065" height="158" alt="image" src="https://github.com/user-attachments/assets/65f0ffe7-74c7-47ba-adf3-21017d9d79f9" />

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
<img width="1065" height="313" alt="image" src="https://github.com/user-attachments/assets/6124fe60-850d-4e8b-b673-f41f1028b8fe" />

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
<img width="1065" height="379" alt="image" src="https://github.com/user-attachments/assets/1ed11081-835f-4737-a5e7-76e451f6c846" />

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
<img width="1065" height="310" alt="image" src="https://github.com/user-attachments/assets/96e396de-5cff-43f2-b123-55bfb0f9362c" />

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
<img width="1065" height="310" alt="image" src="https://github.com/user-attachments/assets/b3ed3f9b-78da-47eb-8e5a-66a870e2be01" />

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
<img width="1065" height="254" alt="image" src="https://github.com/user-attachments/assets/993c43f3-042e-4d0b-9a62-7bdd19018281" />

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
<img width="969" height="330" alt="image" src="https://github.com/user-attachments/assets/a5158fdd-d732-45b8-a8c0-ba9d1b10de37" />

```bash
su - vipul
ls -ld /home/neha/team
ls /home/neha/team
exit
```


## 14. Force Abhishek to Change Password
<img width="1065" height="251" alt="image" src="https://github.com/user-attachments/assets/611e7e68-aaf9-435e-b2dd-eddbbf287f21" />

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
<img width="1000" height="94" alt="image" src="https://github.com/user-attachments/assets/3818934c-7597-48bc-bf93-047763e1649d" />

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
<img width="1065" height="155" alt="image" src="https://github.com/user-attachments/assets/0735c34b-0872-4f15-93ed-950f28e15d7a" />

<img width="1065" height="122" alt="image" src="https://github.com/user-attachments/assets/ba3fd125-bd7a-4991-830b-f8b2c2750614" />


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
<img width="963" height="116" alt="image" src="https://github.com/user-attachments/assets/042073ee-17da-4f76-895a-2cb75c880572" />

```bash
getent passwd neha
```

The last field is the default login shell, commonly `/bin/bash`.


> 

---

## 18. Check Default File and Directory Permissions
<img width="891" height="106" alt="image" src="https://github.com/user-attachments/assets/e26be982-7067-4012-8f1e-5603e318ac86" />
<img width="878" height="103" alt="image" src="https://github.com/user-attachments/assets/18e46d5c-ad6e-454c-9774-5d8d56c77b5f" />

<img width="1065" height="414" alt="image" src="https://github.com/user-attachments/assets/55b98ca5-487c-4cd0-9a85-b7543392c0c7" />




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

## 20. Delete Linux Group
<img width="1011" height="102" alt="image" src="https://github.com/user-attachments/assets/2ce24933-097f-42fb-9648-991c59771e2a" />

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
<img width="1065" height="258" alt="image" src="https://github.com/user-attachments/assets/38c23458-2615-4235-9e44-dd5557230389" />

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
