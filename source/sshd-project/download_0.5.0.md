---
type: sshd
title: Apache SSHD 0.5.0 Release
---

# Overview

Apache Mina SSHD 0.5.0 contains a few enhancements and bug-fixes.

# Getting the Distributions

* Source distributions:
    * [Apache Mina SSHD 0.5.0 Sources (.tar.gz)](https://archive.apache.org/dist/mina/sshd/0.5.0/apache-sshd-0.5.0-src.tar.gz) [PGP](https://archive.apache.org/dist/mina/sshd/0.5.0/apache-sshd-0.5.0-src.tar.gz.asc) [SHA](https://archive.apache.org/dist/mina/sshd/0.5.0/apache-sshd-0.5.0-src.tar.gz.sha1)
    * [Apache Mina SSHD 0.5.0 Sources (.zip)](https://archive.apache.org/dist/mina/sshd/0.5.0/apache-sshd-0.5.0-src.zip) [PGP](https://archive.apache.org/dist/mina/sshd/0.5.0/apache-sshd-0.5.0-src.zip.asc) [SHA](https://archive.apache.org/dist/mina/sshd/0.5.0/apache-sshd-0.5.0-src.zip.sha1)
* Binary distributions:
    * [Apache Mina SSHD 0.5.0 Binary (.tar.gz)](https://archive.apache.org/dist/mina/sshd/0.5.0/apache-sshd-0.5.0.tar.gz) [PGP](https://archive.apache.org/dist/mina/sshd/0.5.0/apache-sshd-0.5.0.tar.gz.asc) [SHA](https://archive.apache.org/dist/mina/sshd/0.5.0/apache-sshd-0.5.0.tar.gz.sha1)
    * [Apache Mina SSHD 0.5.0 Binary (.zip)](https://archive.apache.org/dist/mina/sshd/0.5.0/apache-sshd-0.5.0.zip) [PGP](https://archive.apache.org/dist/mina/sshd/0.5.0/apache-sshd-0.5.0.zip.asc) [SHA](https://archive.apache.org/dist/mina/sshd/0.5.0/apache-sshd-0.5.0.zip.sha1) 

# Release Notes

Apache Mina SSHD 0.5.0 contains a few enhancements and bug-fixes.
Please report any feedback to [users@mina.apache.org](mailto:users@mina.apache.org).

* Bug
    * [SSHD-93](https://issues.apache.org/jira/browse/SSHD-93) - Detect SSH_MSG_DISCONNECT
    * [SSHD-94](https://issues.apache.org/jira/browse/SSHD-94) - Properly handle SFTP version communication    
* Improvement
    * [SSHD-82](https://issues.apache.org/jira/browse/SSHD-82) - Integrate with MINA FtpServer file system view
    * [SSHD-95](https://issues.apache.org/jira/browse/SSHD-95) - Allow a fixed number of concurrent connections for a single user
* New Feature
    * [SSHD-92](https://issues.apache.org/jira/browse/SSHD-92) - Patch: Server Key Verification, Expose exit code
