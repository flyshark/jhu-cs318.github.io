---
layout: project
title: Pintos Project Grading Policies
---

## Grading

We will grade your assignments based on test results and design quality,
which comprises **70%** and **30%** of your grade, respectively. 

<HR SIZE="6">
### Test Results
<P>

Your test result grade will be based on our tests.  Each project has
several tests, each of which has a name beginning with <Q><TT>tests</TT></Q>.
To completely test your submission, invoke <CODE>make check</CODE> from the
project <Q><TT>build</TT></Q> directory.  This will build and run each test and
print a &quot;pass&quot; or &quot;fail&quot; message for each one.  When a test fails,
<CODE>make check</CODE> also prints some details of the reason for failure.
After running all the tests, <CODE>make check</CODE> also prints a summary
of the test results.
</P>
<P>

For project 1, the tests will probably run faster in Bochs.  For the
rest of the projects, they will run much faster in QEMU.
<CODE>make check</CODE> will select the faster simulator by default, but
you can override its choice by specifying <CODE><SAMP>SIMULATOR=--bochs</SAMP></CODE> or
<CODE><SAMP>SIMULATOR=--qemu</SAMP></CODE> on the <CODE>make</CODE> command line.
</P>
<P>

You can also run individual tests one at a time.  A given test <VAR>t</VAR>
writes its output to <Q><TT><VAR>t</VAR>.output</TT></Q>, then a script scores the
output as &quot;pass&quot; or &quot;fail&quot; and writes the verdict to
<Q><TT><VAR>t</VAR>.result</TT></Q>.  To run and grade a single test, <CODE>make</CODE>
the <Q><TT>.result</TT></Q> file explicitly from the <Q><TT>build</TT></Q> directory, e.g.
<CODE>make tests/threads/alarm-multiple.result</CODE>.  If <CODE>make</CODE> says
that the test result is up-to-date, but you want to re-run it anyway,
either run <CODE>make clean</CODE> or delete the <Q><TT>.output</TT></Q> file by hand.
</P>
<P>

By default, each test provides feedback only at completion, not during
its run.  If you prefer, you can observe the progress of each test by
specifying <Q><SAMP>VERBOSE=1</SAMP></Q> on the <CODE>make</CODE> command line, as in
<CODE>make check VERBOSE=1</CODE>.  You can also provide arbitrary options to the
<CODE>pintos</CODE> run by the tests with <Q><SAMP>PINTOSOPTS='<small>...</small>'</SAMP></Q>,
e.g. <CODE>make check PINTOSOPTS='-j 1'</CODE> to select a jitter value of 1
(see section <A HREF="pintos_1.html#SEC6">1.1.4 Debugging versus Testing</A>).
</P>
<P>

All of the tests and related files are in <Q><TT>pintos/src/tests</TT></Q>.
Before we test your submission, we will replace the contents of that
directory by a pristine, unmodified copy, to ensure that the correct
tests are used.  Thus, you can modify some of the tests if that helps in
debugging, but we will run the originals.
</P>
<P>

All software has bugs, so some of our tests may be flawed.  If you think
a test failure is a bug in the test, not a bug in your code,
please point it out.  We will look at it and fix it if necessary.
</P>
<P>

<div class="panel panel-warning">
  <div class="panel-heading">
    <strong>Warning!</strong>
  </div>
  <div class="panel-body">
Please don't try to take advantage of our generosity in giving out our
test suite.  Your code has to work properly in the general case, not
just for the test cases we supply.  For example, it would be unacceptable
to explicitly base the kernel's behavior on the name of the running
test case.  Such attempts to side-step the test cases will receive no
credit.  If you think your solution may be in a gray area here, please ask us.
</div>
</div>
</P>
<P>

<HR SIZE="6">
<H3>Design</H3>
<P>

We will judge your design based on the design document and the source
code that you submit.  We will read your entire design document and much
of your source code.  
</P>
<P>

Don't forget that design quality, including the design document, is 30%
of your project grade.  It
is better to spend one or two hours writing a good design document than
it is to spend that time getting the last 5% of the points for tests and
then trying to rush through writing the design document in the last 15
minutes.
</P>

<HR SIZE="6">
<H4>Design Document</H4>
<P>

We provide a design document template for each project.  For each
significant part of a project, the template asks questions in four
areas: 
</P>
<P>

</P>
<DL COMPACT>
<DT><STRONG>Data Structures</STRONG>
<DD><P>

The instructions for this section are always the same:
</P>
<P>

<BLOCKQUOTE>
Copy here the declaration of each new or changed <CODE>struct</CODE> or
<CODE>struct</CODE> member, global or static variable, <CODE>typedef</CODE>, or
enumeration.  Identify the purpose of each in 25 words or less.
</BLOCKQUOTE>
<P>

The first part is mechanical.  Just copy new or modified declarations
into the design document, to highlight for us the actual changes to data
structures.  Each declaration should include the comment that should
accompany it in the source code (see below).
</P>
<P>

We also ask for a very brief description of the purpose of each new or
changed data structure.  The limit of 25 words or less is a guideline
intended to save your time and avoid duplication with later areas.
</P>
<P>

</P>
<DT><STRONG>Algorithms</STRONG>
<DD><P>

This is where you tell us how your code works, through questions that
probe your understanding of your code.  We might not be able to easily
figure it out from the code, because many creative solutions exist for
most OS problems.  Help us out a little.
</P>
<P>

Your answers should be at a level below the high level description of
requirements given in the assignment.  We have read the assignment too,
so it is unnecessary to repeat or rephrase what is stated there.  On the
other hand, your answers should be at a level above the low level of the
code itself.  Don't give a line-by-line run-down of what your code does.
Instead, use your answers to explain how your code works to implement
the requirements.
</P>
<P>

</P>
<DT><STRONG>Synchronization</STRONG>
<DD><P>

An operating system kernel is a complex, multithreaded program, in which
synchronizing multiple threads can be difficult.  This section asks
about how you chose to synchronize this particular type of activity.
</P>
<P>

</P>
<DT><STRONG>Rationale</STRONG>
<DD><P>

Whereas the other sections primarily ask &quot;what&quot; and &quot;how,&quot; the
rationale section concentrates on &quot;why.&quot;  This is where we ask you to
justify some design decisions, by explaining why the choices you made
are better than alternatives.  You may be able to state these in terms
of time and space complexity, which can be made as rough or informal
arguments (formal language or proofs are unnecessary).
</DL>
<P>

An incomplete, evasive, or non-responsive design document or one that
strays from the template without good reason may be penalized.
Incorrect capitalization, punctuation, spelling, or grammar can also
cost points.  See section <A HREF="pintos_9.html#SEC142">D. Project Documentation</A>, for a sample design document
for a fictitious project.
</P>
<P>

<HR SIZE="6">
<H4> Source Code </H4>

Your design will also be judged by looking at your source code.  We will
typically look at the differences between the original Pintos source
tree and your submission, based on the output of a command like
<CODE>diff -urpb pintos.orig pintos.submitted</CODE>.  We will try to match up your
description of the design with the code submitted.  Important
discrepancies between the description and the actual code will be
penalized, as will be any bugs we find by spot checks.
</P>
<P>

The most important aspects of source code design are those that specifically
relate to the operating system issues at stake in the project.  For
example, the organization of an inode is an important part of file
system design, so in the file system project a poorly designed inode
would lose points.  Other issues are much less important.  For
example, multiple Pintos design problems call for a &quot;priority
queue,&quot; that is, a dynamic collection from which the minimum (or
maximum) item can quickly be extracted.  Fast priority queues can be
implemented many ways, but we do not expect you to build a fancy data
structure even if it might improve performance.  Instead, you are
welcome to use a linked list (and Pintos even provides one with
convenient functions for sorting and finding minimums and maximums).
</P>
<P>

Pintos is written in a consistent style.  Make your additions and
modifications in existing Pintos source files blend in, not stick out.
In new source files, adopt the existing Pintos style by preference, but
make your code self-consistent at the very least.  There should not be a
patchwork of different styles that makes it obvious that three different
people wrote the code.  Use horizontal and vertical white space to make
code readable.  Add a brief comment on every structure, structure
member, global or static variable, typedef, enumeration, and function
definition.  Update
existing comments as you modify code.  Don't comment out or use the
preprocessor to ignore blocks of code (instead, remove it entirely).
Use assertions to document key invariants.  Decompose code into
functions for clarity.  Code that is difficult to understand because it
violates these or other &quot;common sense&quot; software engineering practices
will be penalized.
</P>
<P>

In the end, remember your audience.  Code is written primarily to be
read by humans.  It has to be acceptable to the compiler too, but the
compiler doesn't care about how it looks or how well it is written.
</P>
