### [References](https://www.hostinger.com/tutorials/linux-commands)

# Table of Contents

- [User, Group](#user--group)
  - [User](#user)
  - [Group](#group)
- [Permission](#permission)
  - [Change User ownership of folders/files](#change-user-ownership-of-foldersfiles)
  - [Change Group ownership of folders/files](#change-group-ownership-of-foldersfiles)
  - [Change permission on directory/files](#change-permission-for-foldersfiles)
- [Storage](#storage)
  - [Hard disk listing](#hard-disk-listing)
  - [Files/Folders sizes](#files--folders)
  - [Format Hard Drive file system](#format-hard-drive-file-system)
  - [Mount Hard drive](#mount-hard-drive)
- [Hardware Information](#hardware-information)
  - [Listing Hard Drive](#listing-hard-drive)
  - [CPU](#cpu)
  - [Listing Hardware](#listing-hardware)
  - [Memory / Swap](#memory--swap)
- [Transferring](#transferring)
  - [File](#file)
  - [Folder](#folder)
- [SSH](#ssh)
  - [Generate SSH key](#generate-ssh-key)
  - [Get MD5 fingerprint](#get-the-md5-fingerprint-of-public-key)
  - [Copy SSH key to server](#copy-ssh-key-to-server)
- [Process](#process)
  - [Listing processes are running](#listing-processes-are-running)
  - [Listing ports are running](#listing-ports-are-running)
  - [Stop ports are running](#kill)
- [Network layer protocol](#network-layer-protocol)
  - [Get public IP](#get-public-ip)
  - [Check connection](#check-connection)
- [Service](#service)
- [History command](#history-command)
- [Show OS architecture](#show-os-architecture)
- [Change user's password](#change-users-password)
- [GUI Application](#gui-application)
  - [Update Chrome](#update-chrome)
  - [Create web shortcut on desktop](#create-web-shortcut-on-desktop)

# User & Group

## User

### Show User

```bash
echo ${USER}
```

### Create new User

```bash
adduser ${USERNAME}
```

### Switch to User

```bash
su - ${USERNAME}
```

### Remove User

```bash
deluser ${USERNAME}
rm -rf /home/${USERNAME}
```

## Group

### Listing Groups

```bash
groups
```

### Create new Group

```bash
sudo groupadd ${GROUP_NAME}
```

### Add User to Group

```bash
sudo usermod -aG ${GROUP_NAME} ${USER}
```

# Permission

```bash
$ ls -l some_dir
d rwx rwx r-x ${LINK_COUNT} ${GROUP} ${OWNER} ${SIZE} ${DATE_TIME} some_dir/
^ 421 421 421       ^
| ^^^ ^^^ ^^^       |
| \|/ \|/ \|/       |______ hard links point (1 if this is a file)
|  |   |   |_______________ Other permission
|  |   |___________________ Group permission
|  |_______________________ Owner permission
|__________________________ directory (d) | file (-) | shortcut (l)
```

## Change User ownership of folders/files

```bash
chown -R ${USER} ${PATH}
```

## Change Group ownership of folders/files

```bash
chgrp -R ${GROUP_NAME} ${PATH}
```

## Change permission for folders/files

### With symbols

Grant permissions to user, group and other

```bash
chmod -R u=rwx,g=rx,o=r ${PATH}
```

### With octal number

Permisson code can get from here https://chmodcommand.com

```bash
chmod -R ${PERMISSION_CODE} ${PATH}
```

# Storage

## Hard disk listing

How many hard-disk are available and how much were consumed

```bash
df -h
```

## Files / Folders

Listing files/folders in path together with their size, sort reversed

```bash
sudo du -h -d 1 ${PATH} | sort -rh
```

Count total files

```bash
ls | wc -f
```

Quickly accessing the last few lines of a given text file
Default 10 lines
Optional -n ${NUMBER} output the last NUMBER lines

```bash
tail -f /path-of-file
```

## Format Hard Drive file system

Should use `fdisk` first to know ${DEVICE_PATH}

```bash
sudo mkfs -t ext4 ${DEVICE_PATH}
```

## Mount Hard Drive

```
sudo mount ${DEVICE_PATH} ${ABSOLUTE_PATH}
```

# Hardware Information

## Listing Hard Drive

```bash
sudo fdisk -l
```

## CPU

```bash
lscpu
```

## Listing Hardware

```bash
lshw
```

## Memory / Swap

```bash
htop
top
```

```bash
free
```

# Transferring

## File

```bash
rsync -ravzh ${SOURCE_PATH} ${DESTINATION_PATH}
scp ${USERNAME}@${IP}:/server-path /local-path
```

## Folder

```bash
scp -r ${USERNAME}@${IP}:/server-path /local-path
```

# SSH

## Generate SSH key

```bash
ssh-keygen -t rsa
ssh-keygen -t ed25519
```

## Get the MD5 fingerprint of public key

```bash
ssh-keygen -l -E md5 -f /path-of-public-key
```

## Copy SSH key to server

```bash
ssh-copy-id -i ${PUBLIC_KEY}.pub ${SERVER_USER}@${SERVER_IP}
```

Or you can copy the public key content directly to the server into file

```bash
cat ~/.ssh/${PUBLIC_KEY}.pub
```

# Process

## Listing processes are running

```bash
ps aux
```

## Listing ports are running

```bash
sudo lsof -i -P -n | grep LISTEN
sudo lsof -i -P -n | grep ${PORT}
```

## Kill

### Single process

```bash
sudo kill ${PID}
```

Or forces stop immediately. Unsaved progress will be lost

```bash
sudo kill -9 ${PID}
```

### Multiple process

```bash
kill -9 $(lsof -ti:${PORT_1},${PORT_2},${PORT_3},...)
```

# Network layer protocol

## Get public IP

```bash
curl -s http://api.ipify.org
```

Or finding at

```bash
https://whatismyipaddress.com
```

## Check connection

```bash
telnet ${IP} ${PORT}
```

# Service

```bash
systemctl status ${SERVICE_NAME}
systemctl enable ${SERVICE_NAME}
systemctl start ${SERVICE_NAME}
systemctl restart ${SERVICE_NAME}
systemctl stop ${SERVICE_NAME}
```

# History command

```bash
history
history | grep ${COMMAND}
```

Or view all commands history of another user

```bash
cat /home/${USERNAME}/.bash_history
```

# Show OS architecture

```bash
uname -a
```

# Change user's password

```bash
passwd
```

# GUI Application

## Update Chrome

```bash
sudo apt update
sudo apt upgrade google-chrome-stable
```

## Create web shortcut on desktop

Create new file ${SHORTCUT_NAME}.desktop

```bash
# https://askubuntu.com/a/1296032
[Desktop Entry]
Name=${NAME}
Comment=""
Exec=google-chrome-stable ${LINK}
Icon=/path-icon.png
# create shortcut from the web to get the icon
Icon=chrome-eilembjdkfgodjkcjnpgpaenohkicgjd-Default # or local path
Terminal=false
Type=Application
```

Then right click on the gear icon, select "Allow Launching" and move this file to

```bash
/usr/share/applications (global - required)
~/.local/share/applications (local - optional)
```

---
