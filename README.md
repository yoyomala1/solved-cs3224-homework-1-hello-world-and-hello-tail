Download Link: https://assignmentchef.com/product/solved-cs3224-homework-1-hello-world-and-hello-tail
<br>
<strong>Homework 1 </strong>

In this assignment, you’ll start getting familiar with xv6 by writing a couple simple programs that run in the xv6 OS.

As a prerequisite, make sure that you have followed the <strong>install instructions </strong> to get your build environment set up.

A common theme of the homework assignments is that we’ll start off with xv6, and then add something or modify it in some way. This assignment is no exception. Start by getting a copy of xv6 using git (commands typed at the terminal, and their output, will be shown using a monospace font; the commands type will be indicated by a $):

$ git clone https://github.com/moyix/xv6-public.git

Cloning into ‘xv6-public’…

remote: Counting objects: 4475, done. remote: Compressing objects: 100% (2679/2679), done. remote: Total 4475 (delta 1792), reused 4475 (delta 1792), pack-reused 0

Receiving objects: 100% (4475/4475), 11.66 MiB | 954.00 KiB/s, done.

Resolving deltas: 100% (1792/1792), done. Checking connectivity… done.

Make sure you can build and run xv6. To build the OS, use cd to change to the xv6 directory, and then run make to compile xv6: $ cd xv6-public

Then, to run it inside of QEMU, you can do:

QEMU should appear and show the xv6 command prompt, where you can run programs inside xv6. It will look something like:

You can play around with running commands such as ls, cat, etc. by typing them into the QEMU window; for example, this is what it looks like when you run ls in xv6:

Write a program for xv6 that, when run, prints “Hello world” to the xv6 console. This can be broken up into a few steps:

<ol>

 <li>Create a file in the xv6 directory named c</li>

 <li>Put code you need to implement printing “Hello world” into c</li>

 <li>Edit the file Makefile, find the section UPROGS (which contains a list of programs to be built), and add a line to tell it to build your Hello World program. When you’re done that portion of the Makefile should look like:</li>

</ol>

UPROGS=

_cat

_echo

_forktest

_grep

_init      _kill      _ln

_ls

_mkdir      _rm

_sh

_stressfs

_usertests

_wc

<ol start="4">

 <li>Run make to build xv6, including your new program (repeating steps 2 and 4 until you have compiling code)</li>

 <li>Run make qemu to launch xv6, and then type hello in the QEMU window. You should see “Hello world” be printed out.</li>

</ol>

Of course step 2 is where the bulk of the work lies. You will find that many things are subtly different from the programming environments you’ve used before; for example, the printf function takes an extra argument that specifies where it should print to. This is because you’re writing programs for a new operating system, and it doesn’t have to follow the conventions of anything you’ve used before. To get a feel for how programs look in xv6, and how various APIs should be called, you can look at the source code for other utilities: echo.c, cat.c, wc.c, ls.c.

<strong>Hints</strong>:

<ol>

 <li>In places where something asks for a file descriptor, you can use either an actual file descriptor (i.e., the return value of the open function), or one of the <em>standard I/O descriptors</em>: 0 is “standard input”, 1 is “standard output”, and 2 is “standard error”. Writing to either 1 or 2 will result in something being printed to the screen.</li>

 <li>The standard header files used by xv6 programs are “types.h” (to define some standard data types) and “user.h” (to declare some common functions). You can look at these files to see what code they contain and what functions they define.</li>

</ol>

<h2>A brief digression on IDEs and text editors</h2>

I do not have strong preferences as to <em>how</em> you create source code. I personally prefer to use a traditional text editor that can be run at the command line such as pico. Altough vim and emacs are great as well and there are plenty of alternatives out there. On OS X, some may prefer to use XCode, others may prefer to use something like <u><a href="https://macromates.com/">TextMate</a></u> or <u><a href="https://www.sublimetext.com/">Sublime Text</a></u><a href="https://www.sublimetext.com/">.</a> In the Linux VM I have provided, pico works fine. As long as you get a plain text file out of it with valid C syntax, you can choose whatever you like.

How you <em>compile</em> the code is another matter. The xv6 OS is set up to be built using make, which uses the rules defined in Makefile to compile the various pieces of xv6, and to allow you to run the code. The simplest way to build and run it is to use this system. Trying to coerce an IDE such as XCode into building xv6 is far more trouble than it’s worth.

Part 2: Implementing the <sub>‘tail’</sub> command

Write a program that prints the last 10 lines of its input. If a filename is provided on the command line (i.e., tail FILE) then tail should open it, read and print the last 10 lines, and then close it. If no filename is provided, tail should read from standard input.

$ tail README

<table width="0">

 <tbody>

  <tr>

   <td width="628"> To build xv6 on an x86 ELF machine (like Linux or FreeBSD), run “make”.     On non-x86 or non-ELF machines (like OS X, even on x86), you will     need to install a cross-compiler gcc suite capable of producing x86 ELF     binaries.  See http://pdos.csail.mit.edu/6.828/2014/tools.html.Then run “make TOOLPREFIX=i386-jos-elf-“.To run xv6, install the QEMU PC simulators.  To run in QEMU, run “make qe mu”.To create a typeset version of the code, run “make xv6.pdf”.  This</td>

  </tr>

 </tbody>

</table>

requires the “mpage” utility.  See http://www.mesa.nl/pub/mpage/.

You should also be able to invoke it without a file, and have it read from standard input. For example, you can use a <em>pipe</em> to direct the output of another xv6 command into tail:

$ grep the README | tail




Version 6 (v6).  xv6 loosely follows the structure and style of v6,     xv6 borrows code from the following sources:

JOS (asm.h, elf.h, mmu.h, bootasm.S, ide.c, console.c, and others)

Plan 9 (entryother.S, mp.h, mp.c, lapic.c)

In addition, we are grateful for the bug reports and patches contributed by

The code in the files that constitute xv6 is

To run xv6, install the QEMU PC simulators.  To run in QEMU, run “make qe mu”.

To create a typeset version of the code, run “make xv6.pdf”.  This     requires the “mpage” utility.  See http://www.mesa.nl/pub/mpage/.

The above command searches for all instances of the word the in the file README, and then prints the last 10 matching lines.

<strong>Hints</strong>:

<ol>

 <li>Many aspects of this are similar to the wc program: both can read from standard input if no arguments are passed or read from a file if one is given on the command line. Reading its code will help you if you get stuck.</li>

 <li>Part 3: Extending <sub style="letter-spacing: -1px">tail</sub><span style="font-size: 2.61792em;letter-spacing: -1px"> </span></li>

</ol>

The traditional UNIX tail utility can print out a configurable number of lines from the end of a file. Implement this behavior in your version of tail. The number of lines to be printed should be specified via a command line argument as tail -NUM FILE, for example tail -2 README to print the last 2 lines of the file README. The expected output of that command is:

$ tail -2 README




To create a typeset version of the code, run “make xv6.pdf”.  This     requires the “mpage” utility.  See http://www.mesa.nl/pub/mpage/.

If the number of lines is not given (i.e., if the first argument does not start with -), the number of lines to be printed should default to 10 as in the previous part.

<strong>Hints</strong>:

<ol>

 <li>You can convert a string to an integer with the atoi</li>

 <li>You may want to use <em>pointer arithmetic</em> (discussed in class in Lecture 2) to get a string suitable for passing to atoi.</li>

</ol>


