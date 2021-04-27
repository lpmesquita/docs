---
title: Migrate From Bintray
lang: en-US
---

# Migrating From Bintray
**April 26th, 2021**

## Migration Instructions
:::warning
Rundeck has rotated the signing key used to sign release packages. All previously released
`deb`, `rpm`, and `war` packages have been re-signed and uploaded. The new public key can be found [here in the Rundeck packaging repo](https://github.com/rundeck/packaging/blob/main/pubring.gpg).
:::


:::::::: tabs

::::::: tab Enterprise

:::: tabs
::: tab Deb
### Quick setup script
The quick setup script will configure the Rundeck Enterprise repository,
import the new repository signing key, and update apt. Legacy configuration
will be replaced.

```bash
sudo bash <(curl https://raw.githubusercontent.com/rundeck/packaging/main/scripts/deb-setup.sh) rundeckpro
```

### Manual setup

Import the repo signing key:
```bash
curl -L https://packages.rundeck.com/pagerduty/rundeckpro/gpgkey | sudo apt-key add -
```

Add the following to `/etc/apt/sources.list.d/rundeck.list` replacing existing entries:
```
deb https://packages.rundeck.com/pagerduty/rundeckpro/any/ any main
deb-src https://packages.rundeck.com/pagerduty/rundeckpro/any/ any main
```

Update apt cache:
```bash
sudo apt-get update
```

:::

::: tab Rpm
### Quick setup script
The quick setup script will configure the Rundeck Enterprise repository. Legacy configuration
will be replaced.

```bash
sudo bash <(curl https://raw.githubusercontent.com/rundeck/packaging/main/scripts/rpm-setup.sh) rundeckpro
```

### Manual setup

Remove `bintray-rundeckpro-rpm.repo` if it exists.

Add the following entries to `/etc/yum.repos.d/rundeck.repo` replacing any existing entries:
```properties
[rundeckpro]
name=rundeckpro
baseurl=https://packages.rundeck.com/pagerduty/rundeckpro/rpm_any/rpm_any/$basearch
repo_gpgcheck=1
gpgcheck=0
enabled=1
gpgkey=https://packages.rundeck.com/pagerduty/rundeckpro/gpgkey
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
```

:::

::: tab War
Visit the [Rundeck download page](https://download.rundeck.com) for updated direct
download links.
:::
::::

:::::::


::::::: tab Community
:::: tabs
::: tab Deb
### Quick setup script
The quick setup script will configure the Rundeck Community repository,
import the new repository signing key, and update apt. Legacy configuration
will be replaced.

```bash
sudo bash <(curl https://raw.githubusercontent.com/rundeck/packaging/main/scripts/deb-setup.sh) rundeck
```

### Manual setup

Import the repo signing key:
```bash
curl -L https://packages.rundeck.com/pagerduty/rundeck/gpgkey | sudo apt-key add -
```

Add the following to `/etc/apt/sources.list.d/rundeck.list` replacing existing entries:
```bash
deb https://packages.rundeck.com/pagerduty/rundeck/any/ any main
deb-src https://packages.rundeck.com/pagerduty/rundeck/any/ any main
```

Update apt cache:
```bash
sudo apt-get update
```

:::

::: tab Rpm
### Quick setup script
The quick setup script will configure the Rundeck Enterprise repository. Legacy configuration
will be replaced.

```bash
sudo bash <(curl https://raw.githubusercontent.com/rundeck/packaging/main/scripts/rpm-setup.sh) rundeck
```

### Manual setup

Remove `bintray-rundeckpro-rpm.repo` if it exists.

Add the following entries to `/etc/yum.repos.d/rundeck.repo` replacing any existing entries:
```properties
[rundeck]
name=rundeck
baseurl=https://packages.rundeck.com/pagerduty/rundeck/rpm_any/rpm_any/$basearch
repo_gpgcheck=1
gpgcheck=0
enabled=1
gpgkey=https://packages.rundeck.com/pagerduty/rundeck/gpgkey
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
```

:::

::: tab War
Visit the [Rundeck download page](https://docs.rundeck.com/downloads.html) for updated direct
download links.
:::
:::::::

::::::::