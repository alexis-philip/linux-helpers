# SFTP users & groups

SFTP users and groups guide.

Original guide:
[DevAnswers](https://devanswers.co/configure-sftp-web-server-document-root/).


## General setup

In `/etc/ssh/sshd_config` replace this line.

```bash
#Subsystem sftp /usr/lib/openssh/sftp-server
Subsystem sftp internal-sftp
```

!> After each `sshd_config` modification : restart SSH & SSHD service.

```bash
service ssh restart
service sshd restart
```

## Users

In `/etc/ssh/sshd_config` add a `Match User` directive.

```bash
Match User {UNIX_USER}
	ChrootDirectory /var/www/{DIRECTORY}
	ForceCommand internal-sftp -u 0022
	X11Forwarding no
	AllowTcpForwarding no
	PasswordAuthentication yes
```

> The `ForceCommand internal-sftp -u 0022` forces the UNIX user to access through SFTP, so it **restricts** access to bash.


## Groups

In `/etc/ssh/ssh_config` add a `Match Group` directive.

```bash
Match Group {UNIX_GROUP}
	ChrootDirectory /var/www/{DIRECTORY}
	ForceCommand internal-sftp
	X11Forwarding no
	AllowTcpForwarding no
	PasswordAuthentication yes
```


## Troubleshooting

Check `auth` SSDH logs for errors.

```
tail -f /var/log/auth.log
tail -f /var/log/auth.log | grep 'sshd'
```
