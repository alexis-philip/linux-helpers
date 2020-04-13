# UNIX users & groups

UNIX users and groups guide.

Original guides:
[LinuxAcademy](https://linuxacademy.com/guide/12659-understanding-linux-users-and-groups/),
[LinuxIze](https://linuxize.com/post/how-to-add-user-to-group-in-linux/).

## Users

Users can be **human** or **system**. Watch their reserved ID range with `grep UID /etc/login.defs`.

### List users

```bash
cat /etc/passwd
```

### List user groups

```bash
id {USERNAME}
```

### Create user

```bash
useradd -c "{User description here}" -m -s /bin/bash {USERNAME}
```
 - `-c` comment
 - `-m` creates users home directory in `/home`
 - `-s` assigns the shell to the user

### Create / update password

```bash
passwd {USERNAME}
```

### Update username

```bash
usermod -l {NEW_USERNAME} {OLD_USERNAME}
```

### Update /home directory

Useful when creating a `projects` /home directory, common for multiple users.
```bash
usermod -m -d /home/{NEW_HOME_DIR} {NEW_USERNAME}
```

### Update user ID

```bash
usermod -u {NEW_USER_ID} {USERNAME}
```

### Delete user

Removes user and all files in `/home/USERNAME`

```bash
userdel -r {USERNAME}
```

### Lock / unlock user

```bash
usermod -L {USERNAME}
usermod -U {USERNAME}
```


## Groups

[Linux groups](https://linuxize.com/post/how-to-list-groups-in-linux/).

Groups can be **human** (created by the creation of a user) or **system**. Watch their reserved ID range with `grep GID /etc/login.defs`.

Info about your current group:

```bash
grep $(whoami) /etc/group
```

### List groups

```bash
cat /etc/group
```

### Create group

```bash
groupadd {GROUP_NAME}
```

### Update group ID

```bash
groupmod -g {ID} {GROUP_NAME}
```

### Update group name

```bash
groupmod -n {NEW_GROUP_NAME} {OLD_GROUP_NAME}
```

### Delete group

```bash
groupdel {GROUP_NAME}
```

## Managing groups

`gpasswd` command can be used to add users to a group, remove them, and set admins for the group.

!> `gid` (primary group) will be included `groups` automatically.<br>
Ex: adding `my-group` to `gid` will automatically add this group to `groups`.

### Update FROM USER

#### Add user PRIMARY GROUP

```bash
usermod -g {GROUP} {USER}
```

#### Add user SECONDARY GROUPS

Overwrite groups from the start (eg: g1,g2,g3 then appends g1, will overwrite g2,g3)

```bash
usermod -G {GROUP1,GROUP2} {USER}
```

Appends groups

```bash
usermod -a -G {GROUP1,GROUP2} {USER}
```

### Update FROM GROUP

#### Add user(s)

```bash
gpasswd -a {USER} {GROUP}
gpasswd -M {USER1,USER2} {GROUP}
```

#### Remove user(s)

```bash
gpasswd -d {USER} {GROUP}
```

#### Make user GROUP ADMIN

```bash
gpasswd -A {USER} {GROUP}
```


