---
author: ["Lucas Trevizan"]
title: "The XZ backdoor"
date: "2024-04-05"
description: "A wild backdoor appears."
summary: "Mantainer Jia Tan tried but failed to compromise millions of computers" 
tags: ["linux","malware"]
categories: ["linux"]
ShowToc: false
TocOpen: false
---

On March 29th, a Microsoft developer using Debian Unstable noticed that their SSH login was taking significantly longer (about 500 milliseconds more than usual) while benchmarking PostgreSQL. This prompted the developer to investigate the cause. After checking multiple potential culprits, the developer narrowed down the issue to the libzma library, which led them to examine the XZ Utils for any bugs.

The investigation revealed that the code had been injected into the tarball, within a binary "test file", by Jia Tan, the current maintainer of XZ Utils (JiaT75 on GitHub). The backdoor was capable of remote code execution (RCE) and only required an open SSH port, which most servers have, to carry out the attack.

It is suspected that Jia Tan is not a real person and is likely a fake profile used by a hacking group. The group had spent nearly 4 years gaining the trust of the open-source community and attempting to become the maintainer of an important package in order to execute this attack.

Fortunately, the backdoor was discovered early and only affected the following distributions:

- Fedora Beta and Rawhide
- OpenSUSE Tumbleweed
- Debian Unstable (Sid)


Other distributions, such as Fedora Stable, Ubuntu, Debian Stable, and OpenSUSE Leap, did not receive the compromised package and were not affected by the backdoor.

Some distributions, like Gentoo and Arch, had received the backdoored package but were not vulnerable due to not directly linking OpenSSH to liblzma (in Arch's case) and not having an OpenSSH version patched to work with systemd-notify support (in Gentoo's case).