### Installing Gluster

For RPM based distributions, if you will be using InfiniBand, add the
glusterfs RDMA package to the installations. For RPM based systems, yum/dnf
is used as the install method in order to satisfy external depencies
such as compat-readline5

###### Community Packages

Packages are provided according to this [table](./Community-Packages.md).

###### For Debian with modern apt

```console
GLUSTER_VER=11
KEYRING_PATH=/etc/apt/keyrings/gluster.asc
wget -O "$KEYRING_PATH" https://download.gluster.org/pub/gluster/glusterfs/${GLUSTER_VER}/rsa.pub

DEBID=$(grep 'VERSION_ID=' /etc/os-release | cut -d '=' -f 2 | tr -d '"')
DEBVER=$(grep 'VERSION=' /etc/os-release | grep -Eo '[a-z]+')
DEBARCH=$(dpkg --print-architecture)
echo "deb [signed-by=${KEYRING_PATH}] https://download.gluster.org/pub/gluster/glusterfs/${GLUSTER_VER}/LATEST/Debian/${DEBID}/${DEBARCH}/apt ${DEBVER} main" > /etc/apt/sources.list.d/gluster.list
```

Update package list and install the server:

```console
apt update
apt install glusterfs-server
```

##### For Debian with an older apt (pre 2.4)

```console
KEYRING_PATH=/etc/apt/trusted.gpg.d/gluster.gpg
GLUSTER_VER=7
wget -O - https://download.gluster.org/pub/gluster/glusterfs/${GLUSTER_VER}/rsa.pub | gpg --dearmor > "$KEYRING_PATH"

DEBID=$(grep 'VERSION_ID=' /etc/os-release | cut -d '=' -f 2 | tr -d '"')
DEBVER=$(grep 'VERSION=' /etc/os-release | grep -Eo '[a-z]+')
DEBARCH=$(dpkg --print-architecture)
echo "deb [signed-by=/etc/apt/trusted.gpg.d/gluster.gpg] https://download.gluster.org/pub/gluster/glusterfs/${GLUSTER_VER}/LATEST/Debian/${DEBID}/${DEBARCH}/apt ${DEBVER} main" > /etc/apt/sources.list.d/gluster.list
```

Update package list:

```console
apt update
```

Install:

```console
apt install glusterfs-server
```

###### For Ubuntu

Install software-properties-common:

```console
apt install software-properties-common
```

Then add the community GlusterFS PPA:

```console
add-apt-repository ppa:gluster/glusterfs-11
apt update
```

Finally, install the packages:

```console
apt install glusterfs-server
```

_Note: GlusterFS 11 Packages exist for Ubuntu LTS Releases
24.04, 22.04, 20.04, 18.04, as well as the interim releases
23.04 and 23.10. Packages for earlier versions will cover
different Ubuntu releases._

###### For Red Hat/CentOS

RPMs for CentOS and other RHEL clones are available from the
CentOS Storage SIG mirrors.

For more installation details refer [Gluster Quick start guide](https://wiki.centos.org/SpecialInterestGroup/Storage/gluster-Quickstart) from CentOS Storage SIG.

###### For Fedora

Install the Gluster packages:

```console
dnf install glusterfs-server
```

Once you are finished installing, you can move on to [configuration](./Configure.md) section.

###### For Arch Linux

Install the Gluster package:

```console
pacman -S glusterfs
```
