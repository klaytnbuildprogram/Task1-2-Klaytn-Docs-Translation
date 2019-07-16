# Installation SCN

There are package/RPM installation. You can choose it.

## Package
### Linux
The process of installation on Linux is as follows.

Download the Klaytn package.

Uncompress the package.

Configure an SCN.

Start an SCN.

The Klaytn Linux package consists of the executable binary and the configuration file structured as follows.

- bin
  |- kscn
  |- kscnd
- conf
  |- kscnd.conf
File Name

File Description

bin/kscn

SCN executable file

bin/kscnd

SCN start/termination script file

conf/kscnd.conf

SCN configuration file

### Package Download
You can download the latest version of KSCN package KSCN is the package of SCN. (kscn-vX.X.X-XXXXX-amd64.tar.gz) on Download page.

### Package Installation
The installation is the uncompression of the downloaded package.

$ tar zxf kscn-vX.X.X-XXXXX-amd64.tar.gz
## RPM(RHEL/CentOS/Fedora)
The RPM installation steps are as follows.

Download the latest version of Klaytn's RPM.

Install the downloaded Klaytn RPM.

Configure a Klaytn SCN.

### RPM Installation
You can download the latest version of the KSCN RPM package (kscnd-vX.X.X.el7.x86_64.rpm) on Download page.

### Installation
You can install the downloaded RPM file with the following yum command.

$ yum install kscnd-vX.X.X.el7.x86_64.rpm
### SCN Configuration
The Klaytn Linux package consists of the executable binary and the configuration file structured as follows.

The SCN configuration is the similar procedure as the package setup above apart from the fact that the RPM installation must use the following path.

File Name

Location

kscn

/usr/bin/kscn

kscnd.conf

/etc/kscnd/conf/kscnd.conf

