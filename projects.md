---
layout: default
---
<div class="section">
  <div class="sec-header">
    <h4>Projects</h4>
  </div>
  <p>
    A significant element of this class are four programming projects using the 
    (Java version of the) Nachos instructional operating system. Although Java 
    may seem an odd choice, both the (outdated) C version of Nachos and the 
    Java version focus on OS concepts; they are rather equivalent at a high-level.
  </p>
  <p>
    The Linux machines located in EBU3B <a href="http://insci14.ucsd.edu/acs_sql/scripts/show_facilities.php?action=1&location_id=ebu3-230b">B230</a> 
    or <a href="http://insci14.ucsd.edu/acs_sql/scripts/show_facilities.php?action=1&location_id=ebu3-250b">B250</a> 
    are the recommended platform for your projects.
    For remote access, you can use ieng6-250.ucsd.edu through ieng6-254.ucsd.edu machines 
    via SSH or <a href="http://acms.ucsd.edu/info/vncgnome.html">VNC</a>).
  </p>
</div>
<div class="section">
  <div class="sec-header">
    <h4>Groups</h4>
  </div>
  <p>
    You may work alone or with a partner on projects 1 - 3 (not on project 0). 
    If you decide to work with a partner, you may need to take extra steps to 
    do so. See the <a href="groups.html">working in a group page</a> for info on 
    how to setup your development environment to accommodate group work.
  </p>
</div>
<div class="section">
  <div class="sec-header">
    <h4>Obtaining Nachos</h4>
  </div>
  <p>
    You can download a copy of the Spring 2013 CSE 120 distribution of Nachos 
    <a href="projects/nachosj-120.tar.gz">here</a>. Within this archive you will find the various java 
    classes necessary to run Nachos. Some brief usage instructions for Nachos:
    <ul>
      <li>
        <p>
        The simplest approach is to run on the B230+ machines as above on 
        ieng6 (ssh). It is recommended you try this at least once to see the 
        environment the TA does. Each project has a slightly different configuration, 
        so to build for a certain project, enter projN (where N in {0,1,2,3}) 
        directory and type make. This essentially runs javac to build your classes. 
        After this (without changing directories!), running ../bin/nachos (which 
        is basically a shell wrapper invoking the jvm) will execute nachos.
        </p>
      </li>
      <li>
        <p>
        Alternatively, you can mimic this development environment on some reasonably 
        POSIX-y machine. 
        </p>
      </li>
      <li>
        <p>
        The base nachos distribution is just java files, so you can import these 
        into your fancy IDE; note that you may need to go through some extra work 
        to make the project-specific configuration files functional. You should 
        feel free to use whatever IDE you like, however we will not be providing 
        support for (nor using) any particular IDE ourselves. So please be sure 
        your submissions will compile and run without any special IDE libraries 
        and/or configuration files.
        </p>
      </li>
    </ul>
  </p>
</div>
<div class="section">
  <div class="sec-header">
    <h4>Project Autograders</h4>
  </div>
  <p>
    Some of the projects will have corresponding scripts that you can use to 
    test your implementation. These scripts will run your code against an autograder 
    that will send you an email of your results. We are providing this facility 
    so that you can see if your implementation is on the right track. This facility 
    is to be used only as a check that your implementation is working as you expect 
    (and to some extent, as we expect). It is not a comprehensive test of all 
    the functionality that you are to implement. We are providing this as an aide 
    that will complement (not replace) your own thorough unit testing.
  </p>
  <p>
    Details of how to run the autograder tests for each project (for which it 
    is available) will be given on each project's description page.
  </p>
</div>
<div class="section">
  <div class="sec-header">
    <h4>Submitting Projects</h4>
  </div>
  <p>
    All projects will be handed in using submission scripts. During submission 
    the script will ask you to enter your login id and your partner's login id 
    (if applicable). Note that if you are working with a partner (which you can 
    only do for projects 1 - 3), only one of you must submit.
  </p>
  <p>
    To submit projects you'll run a project specific submit script. After logging 
    into your account, you'll want to run:
    <code>
      prep cs120s
    </code>
  </p>
  <p>
    This may be automatically run for you when you log in. Then move into the nachos directory and run:
    <code>
      submit-projN
    </code>
    where N corresponds to the project number (0 - 3). This script will tar up 
    your Nachos distribution and then submit it via a turnin script. Be sure 
    that your code compiles before submitting it. If your submission does not 
    compile, we cannot give you a grade. Upon successfully submitting each project, 
    you will receive a confirmation email.
  </p>
</div>
<div class="section">
  <div class="sec-header">
    <h4>Projects</h4>
  </div>
  <p>
    As promised, there are four projects. You are advised to start early and 
    get ahead if possible! Together, all the projects comprise 40% of your final 
    grade. So do not try to throw together a solution at the last minute or 
    your grade will suffer.
  </p>
  <div style="padding-left:15px;">
  <table class="table table-bordered">
    <tbody>
      <tr>
        <th class="info">Project</th>
        <th class="success">Due</th>
      </tr>
      <tr>
        <td class="span3"><a href="projects/project0.html">Project 0: Jump Start</a></td>
        <td><strike>4/11 11:59pm</strike></td>
      </tr>
      <tr>
        <td class="span3"><a href="projects/project1.html">Project 1: Threads</a></td>
        <td><strike>4/25 11:59pm</strike></td>
      </tr>
      <tr>
        <td class="span3"><a href="projects/project2.html">Project 2: Multiprogramming</a></td>
        <td>5/19 11:59pm</td>
      </tr>
      <tr>
        <td class="span3">Project 3: Demand Paging</td>
        <td>TBD</td>
      </tr>
    </tbody>
  </table>
  </div>
</div>
<div class="section">
  <div class="sec-header">
    <h4>Additional Resources</h4>
  </div>
  <ul>
    <li>
      <p>
        <a href="http://inst.eecs.berkeley.edu/~cs162/sp08/Nachos/doc/index.html">Nachos API JavaDoc</a>, which is super useful.
      </p>
    </li>
    <li>
      <p>
        <a href="http://inst.eecs.berkeley.edu/~cs162/sp08/Nachos/walk/">Nachos Java Walkthrough</a> at a high level.
      </p>
    </li>
    <li>
      <p>
        <a href="http://cseweb.ucsd.edu/classes/sp08/cse120/projects/nachos.pdf">The Nachos Paper</a> for the original C version.
      </p>
    </li>
  </ul>
</div>
<div class="section">
  <div class="sec-header">
    <h4>Recommendations</h4>
  </div>
  <ul>
    <li> 
        Lib.assertTrue() is your new best friend:
        <ul>
          <li>For entry from code which you DID write, it helps you keep track of invariants you established.</li>
          <li>For entry from code which you DID NOT write, it helps you verify that you understand the nachos environment.</li>
        </ul>
        <p>
        Note that these can be compiled out so there is essentially no performance hit.
        </p>
    </li>
    <li>
      <p>
        Look at the javadoc for the functions you use, and related functions. It 
        has lots of nachos invariants and secret tips. Reading other nachos code 
        is useful too, to see what tools are provided to you (lots!).
      </p>
    </li>
    <li>
      <p>
        When hacking fails, try pencil and paper.
      </p>
    </li>
    <li>
      <p>
        Prefer parsimony.
      </p>
    </li>
  </ul>
</div>
