---
layout: default
title: CS 318 Pintos Project Guide
---

## Pintos Project Guide

A significant element of this class are programming projects using
[Pintos](http://pintos-os.org). Pintos is a teaching operating system 
for 80x86. It is simple and small (compared to Linux). On the other hand,
it is realistic enough to help you understand core OS concepts in depth. 
It supports kernel threads, virtual memory, user programs, and file system. 
But its original implementations are premature or incomplete. Through the 
projects, you will be strengthening all of these areas of Pintos to make 
it complete.

These projects are hard. They have a reputation of taking a lot of time. But
they are also as rewarding as they are challenging. Since Pintos is designed
for 80x86 architecture, at the end of the projects, you could run theoretically 
the OS that you built on a regular IBM-compatible PC! Of course, during development, 
running Pintos on bare metal machines each time could be time consuming. Instead,
you will run the projects in an x86 emulator, in particular, [Bochs](http://bochs.sourceforge.net)
or [QEMU](http://fabrice.bellard.free.fr/qemu/). Pintos has also been tested with
[VMWare Player](http://www.vmware.com/).

We will start with a pre-project and then do four substantial projects:

<table class="table table-bordered table-striped table-hover" id="schedule-table">
  <thead>
    <tr class="info">
      <th>Project</th>
      <th>Due</th>
    </tr>
  </thead>
  <tbody>
  <tr>
    <td><a href="project0.html">Lab 0: Jump Start</a></td>
    <td>09/07 11:59 pm</td>
  </tr>
  <tr>
    <td><a href="project1.html">Lab 1: Threads</a></td>
    <td>09/26 11:59 pm</td>
  </tr>
  <tr>
    <td><a href="project2.html">Lab 2: User Programs</a></td>
    <td>10/17 11:59 pm</td>
  </tr>
  <tr>
    <td><a href="project3.html">Lab 3: Virtual Memory</a></td>
    <td>11/09 11:59 pm</td>
  </tr>
  <tr>
    <td><a href="project4.html">Lab 4: File Systems</a></td>
    <td>12/07 11:59 pm</td>
  </tr>
  </tbody>
</table>


### Groups
Lab 0 is an individual project. From Lab 1 and onwards, you can work in groups of 
1-3 people. We will overlap Lab 0 with the stage of forming groups. So start
talking with your classmates around once the course begins! Note that, though,
larger team size doesn't always yield better performance for the projects.

### Getting Started
To get started, you can get a copy of the Pintos source code distribution.
```bash
git clone https://github.com/ryanphuang/pintos
```
or
```bash
wget https://cs.jhu.edu/~huang/teaching/cs318/fa17/pintos.tar.gz
```
<div class="panel panel-warning">
  <div class="panel-heading">
    <strong>Warning!</strong>
  </div>
  <div class="panel-body">
    We have made some customization to the official Pintos distribution. So you 
    should be only getting the source code from the above channels. In other words,
    doo not download from other websites.
  </div>
</div>

Before you can compile and develop on Pintos, you will need to have a machine
with the appropriate environment setup. The CS department's lab machines support 
Pintos development. We will be test your code on these machines. If you decide to 
work on the projects on your own machine (e.g., Ubuntu, Fedora, Mac OS), you can 
refer to the [setup guide](setup.html) for instructions.

### Documentation


### Source Tree Overview

Within the pintos source distribution that you just downloaded (extract it if
necessary), you should see in <Q><TT>pintos/src</TT></Q>. Refer to the [brief overview](listing_0.html)
of the source tree.

### Version Control
