# CentOS 7
In this guide we will install Pterodactyl's Wings v1.X — including all of it's dependencies — and configure it to use a SSL connection.

[[toc]]

::: tip
This guide is based off the [official installation documentation](/wings/1.0/installing.md) but is tailored specifically for CentOS 7.
:::

## Install Requirements
We will first begin by installing all of Wings' [required](/wings/1.0/installing.md#dependencies) dependencies.

### Docker

```bash
yum install -y yum-utils device-mapper-persistent-data lvm2

sudo yum remove docker-ce docker-ce-cli containerd.io

yum install -y https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.2.6-3.3.el7.x86_64.rpm


sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

sudo yum install -y docker-ce docker-ce-cli

systemctl enable docker
systemctl start docker
```

### Server Ports
```bash
firewall-cmd --add-port 8080/tcp --permanent
firewall-cmd --add-port 2022/tcp --permanent
firewall-cmd --permanent --zone=trusted --change-interface=docker0
firewall-cmd --reload
```

## Installing the Wings
Great, now all of the dependencies and firewall rules have been dealt with. From here follow the [official Wings installation documentation](/wings/1.0/installing.md#installing-wings-1).
