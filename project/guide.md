---
layout: project
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
      <th>Weight</th>
      <th>Due</th>
    </tr>
  </thead>
  <tbody>
  <tr>
    <td><a href="project0.html">Lab 0: Jump Start</a></td>
    <td>2%</td>
    <td>09/12 11:59 pm</td>
  </tr>
  <tr>
    <td><a href="project1.html">Lab 1: Threads</a></td>
    <td>8%</td>
    <td>09/26 11:59 pm</td>
  </tr>
  <tr>
    <td><a href="project2.html">Lab 2: User Programs</a></td>
    <td>10%</td>
    <td>10/13 11:59 pm</td>
  </tr>
  <tr>
    <td><a href="project3.html">Lab 3: Virtual Memory</a></td>
    <td>14%</td>
    <td>11/04 11:59 pm</td>
  </tr>
  <tr>
    <td><a href="project4.html">Lab 4: File Systems</a></td>
    <td>16%</td>
    <td>11/30 11:59 pm</td>
  </tr>
  </tbody>
</table>


<HR SIZE="6">
### Groups
Lab 0 is an individual project. From Lab 1 and onwards, you can work in groups of 
1-3 people. We will overlap Lab 0 with the stage of forming groups. So start
talking with your classmates around once the course begins! Note that, though,
larger team size doesn't always yield better performance for the projects.

<HR SIZE="6">
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

<HR SIZE="6">
### Documentation

* Pintos source code 
  - [Brief overview of the source tree](listing_0.html)
  - [Reference guide](pintos_6.html)
* The original Pintos [paper](https://benpfaff.org/papers/pintos.pdf)
* **The original Pintos reference** in [PDF](pintos.pdf), [HTML](pintos.html). *Note that 
  we've customized it a bit and our version is the official one for this class.*{: .text-info}
* The reference [page](/references.html) contains instructions on how to read the Pintos
  reference.

<HR SIZE="6">
### Version Control

We will be using Git for version control in the class. If you are new to Git, there
are plenty of tutorials online that you can read, e.g., [this one](https://www.atlassian.com/git/tutorials).

<HR SIZE="6">
### Grading

We will grade your assignments based on test results (**70% of your grade**)
as well as design quality (**30% of your grade**). Note that the testing grades
are fully automated. So please turn in working code or there is no credit. 
The [grading policy page](grading.html) lists detailed information about how 
grading is done.

<HR SIZE="6">
### Submission

We will be using [GitHub classroom](https://education.github.com) to distribute 
and collect assignments. You do not have to do anything special to submit your project. 
We will use a snapshot of your GitHub repository as it exists at the deadline, and 
grade that version. You can still make changes to your repository after the deadline.
But we will be only using the snapshot of your code as of the deadline.

<HR SIZE="6">
### Cheating and Collaboration
<div class="panel panel-danger">
  <div class="panel-heading">
    <strong>Warning!</strong>
  </div>
  <div class="panel-body">
  This class has zero tolerance for cheating. We will run tools to check your submission 
  against a comprehensive database of solutions including past and present submissions 
  for potential cheating. The consequences are very high. Please
  read the JHU CS department's <a href="https://www.cs.jhu.edu/academic-integrity-code">academic integrity code</a>.
</div>
</div>

The basic policies are:
* Never share code or text on the project. *That also means do not make your solutions
  public on the Internet, e.g., GitHub public repo*{: .text-danger}.
* Never use someone else's code or text in your solutions.
* Never consult project code or text found on the Internet.
* You may read but not copy Linux or BSD source code. *But you must cite any code
  that inspired your code*{: .text-danger}. As long as you cite what you used, it's
  not cheating. In the worst case, we deduct points if it undermines 
  the assignment.

On the other hand, we encourage collaboration in the following form:
* Share ideas (but do not give code to others).
* Explain your code to someone to see if they know why it does not work.
* Help someone else debug if they've got stuck.
