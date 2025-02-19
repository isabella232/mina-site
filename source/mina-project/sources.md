---
type: mina
title: Sources
---

## Overview

Sources for the Apache MINA projects are currently managed through GIT. Instructions on GIT use can be found at <http://git-scm.com/book/>.

For each project you can find a detailed description how to checkout and build the source on the project documentation. This page is just a short overview.


# Normal Git Access

Anyone can check code out of Git. You only need to specify a username and password in order to update the Git repository, and only MINA committers have the permissions to do that. We run Git over standard HTTPS, so hopefully you won't have problems with intervening firewalls.

## Web Access

The following is a link to the [online source repository](https://gitbox.apache.org/repos/asf?p=mina.git;a=summary).

# Cloning from the Git repo

Again, anyone can do this. Use a command like to checkout the current development version (the trunk):

### For MINA

read only access :

    $ git clone http://gitbox.apache.org/repos/asf/mina.git mina

write access :

    $ git clone https://gitbox.apache.org/repos/asf/mina.git mina

Note that you will get the full repository, and you may probably want to work on a specific branch. We currently have 2 active branches :

  * Mina 2.0
  * Mina 3.0

Cloning the MINA repository will get you to the trunk, ie the MINA 3.0 branch. If you want to work on th MINA 2.0 branch, you ought to checkout the latest 2.0 tag, after having cloned the repository :

    $ git checkout -b 2.0.10 2.0.10

For the record, here are the various branches you can see :

    $ git tag
    0.8.3
    0.8.4
    0.9.1
    ...
    0.9.5
    1.0.0
    1.0.1
    ...
    1.0.10
    1.1.0
    1.1.1
    ...
    1.1.7
    2.0.0-M1
    2.0.0-M2
    ...
    2.0.0-M6
    2.0.0-RC1
    2.0.0
    2.0.1
    ...
    2.0.10
    3.0.0-M1
    3.0.0-M2
    mina-parent-3.0.0-M1

# Building MINA

Instructions on how to build MINA can be found [here](developer-guide.html)

# Released version

The following table displays the URL of each project, and the URL where you can find information about how to build each project.

| Subproject/Documentation | Git URL |
|---|---|
| [MINA](http://mina.apache.org/mina-project/developer-guide.html) | [https://gitbox.apache.org/repos/asf/mina.git](https://gitbox.apache.org/repos/asf/mina.git) |
| [FtpServer](http://mina.apache.org/ftpserver-project/building.html) | [https://gitbox.apache.org/repos/asf/mina-ftpserver.git](https://gitbox.apache.org/repos/asf/mina-ftpserver.git) |
| [SSHD](http://mina.apache.org/sshd-project/documentation.html) | [https://gitbox.apache.org/repos/asf/mina-sshd.git](https://gitbox.apache.org/repos/asf/mina-sshd.git) |
| [Vysper](http://mina.apache.org/vysper-project/documentation.html) | [https://gitbox.apache.org/repos/asf/mina-vysper.git](https://gitbox.apache.org/repos/asf/mina-vysper.git) |
| [AsyncWeb](http://mina.apache.org/asyncweb-project) | [https://gitbox.apache.org/repos/asf/mina-asyncweb.git](https://gitbox.apache.org/repos/asf/mina-asyncweb.git) |

# Commit Changes to Git

In order to be able to push some modification, you have to be a committer.

# Documentation

The Website documentation is published via Apache SVN pubsub. The website source resides at

[https://svn.apache.org/repos/asf/mina/site/trunk](https://svn.apache.org/repos/asf/mina/site/trunk)
