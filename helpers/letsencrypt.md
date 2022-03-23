# letsencrypt

Guide to install and use [`letsencrypt`](https://letsencrypt.org/).

To use `letsencrypt`, we need to use the [Certbot](certbot.eff.org) ACME client.

## Install

> [Install guide](https://certbot.eff.org/instructions?ws=apache&os=debianbuster)

1. Install [`snap`](https://snapcraft.io/docs/installing-snap-on-debian) for Debian.
    1. Install `snap`:
        ```
        apt update && apt install snapd
        ```
    1. **Restart the system**, then install snap `core`:
        ```
        snap install core
        ```
    1. Test `snap`:
        ```
        snap install hello-world
        hello-world
        snap remove hello-world
        ```
1. Install Certbot:\
    Remove old Certbot packages
    ```
    apt-get remove certbot
    ```
    Install Certbot
    ```
    snap install --classic certbot
    ```
    Ensures Certbot can be executed
    ```
    ln -s /snap/bin/certbot /usr/bin/certbot
    ```

## Usage

### Get certifications

Gets a certificate for each edits Apache sites configurations automatically: turns HTTP in a single step.

```
certbot --apache
```

OR, only gets the certificate, not changing configuration files.

```
certbot certonly --apache
```

### Test auto-renewal

The Certbot packages on your system come with a cron job or systemd timer that will renew your certificates automatically before they expire. You will not need to run Certbot again, unless you change your configuration. You can test automatic renewal for your certificates by running this command:

```
certbot renew --dry-run
```

The command to renew certbot is installed in one of the following locations:

- `/etc/crontab/`
- `/etc/cron.*/*`
- `systemctl list-timers`
