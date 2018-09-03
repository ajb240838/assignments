![UiS](https://www.uis.no/getfile.php/13391907/Biblioteket/Logo%20og%20veiledninger/UiS_liggende_logo_liten.png)

# Lab 1: Unix, programming tools and C

| Lab 1:		| Unix, programming tools and C		|
| -------------------- 	| ------------------------------------- |
| Subject: 		| DAT320 Operating Systems 		|
| Deadline:		| Aug 31 2018 16:00			|
| Expected effort:	| 10-15 hours 				|
| Grading: 		| Pass/fail 				|
| Submission: 		| Individually				|

### Table of Contents

1. [Introduction](https://github.com/uis-dat320-fall18/assignments/blob/master/lab1/README.md#introduction)
2. [The Linux Lab](https://github.com/uis-dat320-fall18/assignments/blob/master/lab1/README.md#the-linux-lab)
3. [Remote Login with Secure SHell](https://github.com/uis-dat320-fall18/assignments/blob/master/lab1/README.md#remote-login-with-secure-shell)
4. [Basic Unix commands](https://github.com/uis-dat320-fall18/assignments/blob/master/lab1/README.md#basic-unix-commands)
5. [The vi / vim editor](https://github.com/uis-dat320-fall18/assignments/blob/master/lab1/README.md#the-vi--vim-editor)
6. [Git and GitHub](https://github.com/uis-dat320-fall18/assignments/blob/master/lab1/README.md#git-and-github)
7. [The C language](https://github.com/uis-dat320-fall18/assignments/blob/master/lab1/README.md#the-c-language)
8. [Submitting the lab](https://github.com/uis-dat320-fall18/assignments/blob/master/lab1/README.md#submitting-the-lab)
9. [Lab Approval](https://github.com/uis-dat320-fall18/assignments/blob/master/lab1/README.md#lab-approval)

## Introduction

The overall aim of the labs in this course is to learn how to develop systems,
where some degree of low-level tuning is necessary to obtain the desired
performance. We will do this through a series of lab exercises that will expose
you to developing an application in the Go programming language, and some of
the tools that people frequently use to tune such applications. Specifically,
you will learn about a performance (CPU/memory) profiler and race detector.

## The Linux Lab

Previously lab sessions was held in the Linux lab in E353, where the machines
are named: `pitter1` - `pitter40`. This year we are trying something new.
Instead of being physically in the Linux lab, you will access these and other
Linux machines remotely; see below for more information about this.

All necessary software should be installed on these machines. Also, the lab
project will include a networking part, requiring you to run your code on
several machines, or at least from different ports on `localhost`. This can be
conveniently done using the machines in E353. To be able to log into the
machines in E353 you will need an account on the Unix system.

**Task - registration:**

Many of you have already done this one: You will need an Unix account to access
machines in the GNU/Linux lab. Get an account for UiS’ Unix system by following
the instructions [here](http://user.ux.uis.no).

## Remote Login with Secure SHell (SSH)

*Skip this part if you haven't got a Unix account password yet. If so, come back and do it later, because it is important for later labs.*

You can use `ssh` to log on to another machine without physically going to that
machine and login there. This makes it easy to run and test the example code
and your project later. To log onto a machine using ssh, open a terminal window
and type a command according to this template, and make sure to replace
username and hostname:

`ssh username@hostname`

For example to log on to one of the machines in the Linux lab, run:

`ssh username@pitter18.ux.uis.no`

This will prompt for your password. Enter your account password and you will be
logged into that machine remotely.

*The following may be skipped if you can login from one pitter machine to another without typing a password. Then your account was created with the appropriate ssh keys in your authorized keys file. (The following text is left in here for your information in case you want to configure your own machines logins.)*

You can avoid having to type the password each time by generating a
public-private key-pair using the `ssh-keygen` command (see the man pages for
`ssh-keygen`). Type

`man ssh-keygen`

and read the instructions. Then try running this command to generate your
key-pair; make sure that once asked to give a password, just press enter at the
password prompt. Once the key-pair have been generated, copy the public-key
file (ends with .pub) to a file named authorized keys.

If you have multiple keys in the latter file, make sure not to overwrite those
keys, and instead paste the new public-key at the end of your current file.
After having completed this process, try ssh to another machine and see whether
you have to type the password again.

Note that the security of this passphrase-less method of authenticating towards
a remote machine hinges on the protection of the private key file stored on
your client machine. Thus, it is actually recommended to create a key with a
passphrase, and instead use the `ssh-agent` command at startup, along with
`ssh-add` to add your key to this agent. Then, the `ssh`, `scp`, and other
ssh-based client commands can talk locally with the `ssh-agent`, and you as the
user only needs to type your password once. Please consult the `ssh-agent` and
`ssh-add` manual pages for additional details.

Another tip: If you are running from a laptop and wish to remain connected even
if you close the laptop-lid, you can check out the [mosh
command](http://mosh.mit.edu/).

If you want to change your UNIX password login to johanna2.uis.no and use the 
command passwd to change the password. It may take a while to update the password
everywhere.

**External access to the Linux machines**

Due to firewall configurations you cannot access the machines in the Linux lab
from outside UiS's network. Information about how to do a remote login to the
Linux machines externally can be found
[here](http://wiki.ux.uis.no/foswiki/Info/WebHome) and 
[here](http://wiki.ux.uis.no/foswiki/Info/HvordanLoggeInnP%E5Unix-anlegget).

## Basic Unix commands

To get a feeling for how to work with the Unix shell, we are going to try out
several different commands. We will use the online tutorials one to eight found
[here](http://www.ee.surrey.ac.uk/Teaching/Unix/).

Note: This lab was designed with the `bash` Unix shell. If you have trouble
with some commands, it may be caused by running by a different shell. To check
which shell you are using run the following command:
`/bin/ps -p $$`
which will give output similar to this:
```
  PID TTY          TIME CMD
10749 pts/23   00:00:00 bash
```

**Task: Do the exercises from tutorials one to eight.**

For later lookup, a more condensed tutorial can be found [here](https://csg.sph.umich.edu/docs/hints/learnUNIXin10minutes.html).

**Note: questions in the following should be answered in separate files for each topic; see the files available in the lab1 folder.**

**Shell questions**
```
1.) Which command lists the sizes of all the files and folders in top level of the current directory in human readable format? Note that if you are using max command line option for depth is -d.
	a. du -h -l .
	b. du -h -–max-depth=1 .
	c. du --max-depth=1
	d. du -h -a --max-depth=1 .

2.) Which command continously prints the contents of a file named file.txt in real time while its contents are being modified by some other process?
	a. cat file.txt
	b. cat -f file.txt
	c. tail -f file.txt
	d. head -f file.txt
	
3.) Which command removes a non-empty directory called temp_files?
	a. rm temp_files
	b. rm -r temp_files
	c. rmdir temp_files
	d. rem temp_files

4.) Which command prints the 10 recent kernel messages?
	a. dmesg -k 
	b. dmesg -k | tail
	c. dmesg | head
	d. dmesg

5.) Which command is used to display the manual pages for the command cat?
	a. man cat
	b. manual cat
	c. ? cat
	d. guide cat

6.) Which command will show the first 10 lines of readme.txt?
	a. cat -10 readme.txt
	b. less -10 readme.txt
	c. tail readme.txt
	d. head readme.txt

7.) Which command renames a file called file1.txt to file2.txt?
	a. mv file1.txt file2.txt
	b. cp file1.txt file2.txt
	c. ren file1.txt file2.txt
	d. ren file2.txt file1.txt

8.) Which command will show all symbolic links?
	a. ls -l
	b. ls -a
	c. find . -type l -ls
	d. find . -type f -ls

9.) Which command will display the contents of readme.txt with line numbers?
	a. cat readme.txt
	b. cat -l readme.txt
	c. cat -A readme.txt
	d. cat -n readme.txt

10.) Which command will count only the number of lines in readme.txt?
	a. wc readme.txt
	b. wc -l readme.txt
	c. wc -m readme.txt
	d. wc -n readme.txt

11.) Which command will display a list of the users who currently logged in in the system?
	a. whoami
	b. who
	c. top
	d. ps -al
	
12.) Which command will remove the trailing new line from echoing hello?
	a. echo -n hello
	b. echo \n hello
	c. echo n hello
	d. echo /n hello


13.) Which command do you use to change your password?
	a. password
	b. pwd
	c. passwd
	d. pswd

14.) The command "history" will show the commands previously run in the terminal. For example
 1052  ls -al
 1053  go test -v
 1054  pwd
 1055  cd ..
 1056  history
How can you repeat command "ls -al"?
	a. repeat 1052
	b. redo 1052
	c. !1052
	d. 1052

15.) What does the ”less” command do?
	a. Displays the contents of a file in a manner that allows users 
	   to move forwards or backwards through the file.
	b. Displays the contents of a file in a manner that allows users 
	   to move only forwards through the file.
	c. Displays the contents of a file in a manner that allows users 
	   to move only backwards through the file.
	d. Allows a user to edit a file.

16.) How can you exit the "less" command?
	a. Esc
	b. q
	c. z
	d. x

17.) What command will display the running processes of the current user?
	a. ps -u <your user ID or user name>
	b. ps -a
	c. ps -e
	d. ps

18.) What command can be used to find the process(es) consuming the most CPU?
	a. iostat
	b. netstat
	c. uptime
	d. top
	
19.) What does a screen command do?
	a. clears the screen
	b. starts a virtual terminal
	c. closes terminal
	d. prints screen

20.) Which command sorts the rows in the file according to descending numerical order?
	a. sort -r file.txt
	b. sort file.txt
	c. sort -n file.txt
	d. sort -r -n file.txt
```
## The vi / vim editor

In later labs we will be working in a constrained environment where you will
only have access to the `vi`-editor or the improved version `vim`. This editor
can be a bit hard to get used to, but it is quite useful to have some hands-on
experience with it, because it is almost always available on Unix systems. On
very stripped down Linux systems, e.g. on embedded systems like routers,
set-top boxes, typically the only editor available is `vi`. However, once you
get used to it, `vi` is actually quite powerful, and many people prefer it,
even over fully fledged IDEs for programming. Information about `vi` can be
found [here](https://csg.sph.umich.edu/docs/hints/learnUNIXin10minutes.html) and 
[here](http://www.washington.edu/computing/unix/vi.html).

**vi questions**
```
1.) Which command saves and exits a file in vi?
	a. :w
	b. :wq
	c. :q
	d. :q!

2.) Which command shows the line numbers in a file in vi?
	a. :n
	b. :nu
	c. n
	d. :set nu

3.) What command/key is used to start entering text?
	a. i
	b. x
	c. J
	d. p

4.) How many different modes the editor can be in?
	a. 1
	b. 2
	c. 3
	d. 4

5.) What command can be used to place the cursor at the beginning of line 4?
	a. $4
	b. :4
	c. l4
	d. ^4

6.) What will dd command do (in command-mode)?
	a. Pastes the contents of the buffer before the current line.
	b. Copies the current line into the buffer.
	c. Deletes the current line and stores it in the buffer.
	d. Pastes the contents of the buffer after the current line.

7.) Which command copies 10 lines from the cursor?
	a. 10yy
	b. yy10
	c. 10dd
	d. d10
	
8.) Which command undos recent changes?
	a. x
	b. u
	c. z
	d. y

9.) Which command moves forward one word?
	a. b
	b. w
	c. H
	d. M
	
10.) Which command takes you to the last line of the file?
	a. L
	b. :G
	c. :L
	d. G
```
## Git and GitHub

This course uses git and github for handins of lab exercises, and thus basic
knowledge of the these two tools are needed when working on the lab
assignments. The procedure used to submit your lab exercises is explained on
the front page of lab1 on github. This section only gives you a few pointers to
where you can find information to learn more about git and github.

#### Git

Git is a distributed revision control and source code management system. Basic
knowledge of Git is required for handing in the lab exercises. There are many
resources available online for learning Git. A good book is Pro Git by Scott
Chacon. The book is available for free [here](https://git-scm.com/book).
Chapter 2.1 and 2.2 should contain the necessary information for delivering the
lab exercises.

#### GitHub

GitHub is a web-based hosting service for software development projects that
use the Git revision control system. An introduction to Git and GitHub is
available in [this video](http://youtu.be/U8GBXvdmHT4). Students need to sign
up for a GitHub account to get access to the needed course material.

## The C language

In this lab we will first provide some basic introduction to the C language.
You will learn how to build a small program in C, how to compile and execute
it, and how to extend the program with libraries. You will also get to know the
make utility and learn how to automate the process of building an application
written in C. This is typically a little bit more difficult than doing the same
in Java, but since lots of legacy code out there rely on programmers with C
knowledge, by completing this course, you will have an edge over your peers who
don’t know these tools.

Even though the C language is almost 40 years old, it is still one of the most
important programming languages. This is mainly because it enables the
programmer to do low-level bit manipulation and access memory in a way that
most higher-level languages prevent users from doing. The C language is the
primary language for writing operating systems such as Windows, Linux, and
MacOS X. And for building embedded systems there is virtually no other viable
language.

#### Hello world

To get started with C, it is customary to implement the good old `Hello, world!`
program. **Task: Start a terminal window on a lab-machine and create the file
shown in Listing 1** using `vim`, and save it as `hello.c`

Listing 1: Hello, world! program.
```
#include <stdio.h>

int main(void)
{
	printf("Hello, world!\n");
	return 0;
}
```
Compile the program by using the following command:

`gcc hello.c -o hello`

The `-o` flag lets you specify the output (executable) file name, hello in this
case. Before continuing, inspect the current directory using the `ls` command to
confirm that the file has been compiled. Run the command by typing `./hello` in
the terminal window, which should give you:

`Hello, world!`

**Compiling C Questions:**
```
1.) Which gcc argument lets you name the output?
	a. -b
	b. -x
	c. -o
	d. -E

2.) Which gcc argument optimizes the code?
	a. -o
	b. -O
	c. -x
	d. -v

3.) Which gcc argument defines the DEBUG macro?
	a. -debug
	b. -ddebug
	c. -DEBUG
	d. -DDEBUG

4.) Which gcc argument produces assembly code?
	a. -asm
	b. -S
	c. -E
	d. -c
	
5.) Which gcc argument produces a map file called output.map?
	a. -M=output.map
	b. -Map=output.map
	c. -Wl,-Map=output.map
	d. -Wl=output.map


```

#### Arguments

It is important to know how to pass command line arguments to C programs. To
accept command line arguments, the main function is defined like this:
```
int main(int argc, char* argv[])
{
	// TODO: Implement program
	return 0;
}
```
`argc` is the number of arguments given to the program. There will always be at
least one argument, which is the program itself.

`argv` is an array of strings. The first one in the array is the program.

**Task: Implement arguments into hello world.**

Modify the hello world program to implement arguments to do the following:

If a user runs

`./hello`

the output should be

`Hello, world!`

If the user supplies an argument, for example Tom

`./hello Tom`

the output should be

`Hello, Tom!`

If the user supplies multiple arguments,

`./hello Tom Joe`

the output should be

`Hello, Tom!`

`Hello, Joe!`

There is also an intentional bug causing a test to fail. Find it.

## Setting up your Go environment

#### Checking Go Installation

The Go programming language will be used more in later labs. For this lab, it
is only used to help set up the environment. The latest version of Go should be
installed on all the machines in the GNU/Linux lab. You need to follow the
installation instructions found [here](http://golang.org/doc/install) if you
wish to use your own machine for Go programming.

**Task - check your Go installation:**

Set up a workspace, try to install and run simple packages, as explained on
[here](http://golang.org/doc/code.html). Don't forget to export your workspace
as `$GOPATH`.  Assuming that you have configured `$GOPATH` correctly,
you can run the go tool and its subcommands from any directory.

A good place to set the `GOPATH` is a workspace in your `HOME` directory.
```
$ mkdir $HOME/go
$ mkdir $HOME/go/bin
$ export GOPATH=$HOME/go
$ export PATH=$PATH:$GOPATH/bin
```

***It is very important that your Go installation and workspace setup is
verified working correctly before you proceed.***

Note: If you are using `bash` as your Unix shell, it is helpful to add the
`GOPATH` to the `.bashrc` file inside your $HOME directory. To do this, add
these lines
```
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
```
to the `.bashrc` file.

## Submitting the lab

#### The Autograder Tool

This course uses a new tool called Autograder. It is a tool for students and
teaching staff for submitting and validating lab assignments and is developed
at the University of Stavanger. All lab submissions from students are handled
using Git, a source code management system, and GitHub, a web-based hosting
service for Git source repositories.

**Task - Autograder registration:**

You will have to sign up for the lab project in Autograder if you have not
already done so. Instructions for this can be found
[here](https://github.com/uis-dat320-fall18/course-info/blob/master/autograder-registration.md).

#### Submission instructions

This section offers step-by-step instructions on how to hand in
Lab 1. Please refer to the workflow described below also for future labs unless
otherwise noted. 

1. You will have access to two repositories when you have signed up on
   Autograder. The first is the `labs` repository, which is where we will
   publish all lab assignments, skeleton code and additional information
   needed. You only have read access to this repository. The second repository
   is your own repository named `username-labs`, where `username` is your
   GitHub username. You have write access to this repository. Your answers to
   the assignments should be pushed here.

2. There are several ways to get the `labs` repo. Below we describe two options.

3. (Option 1) Using just the `git` command on the command line.
	1. `ls -la $GOPATH` (make sure that this is a real directory)
	2. `mkdir -p $GOPATH/src/github.com/uis-dat320-fall18`
	3. `cd $GOPATH/src/github.com/uis-dat320-fall18`
	4. `git clone https://github.com/uis-dat320-fall18/assignments.git`
	5. You will be asked for your GitHub user name and password
	6. Continue in Step 6 below
  
4. (Option 2) Using the `go get` command on the command line.
	1. `ls -la $GOPATH` (make sure that this is a real directory)
	2. `go get github.com/uis-dat320-fall18/assignments` 
	3. You will be asked for your GitHub user name and password
	4. (ignore the warning message about no buildable Go files)
	5. Continue in Step 6 below

5. (Advanced Option) Advanced users: Follow these [steps](https://github.com/uis-dat320-fall18/course-info/blob/master/github-ssh.md) if you want to use SSH for GitHub authentication. This will help avoid having to type your password every time.

6. (Information) Both Option 1 or 2 above will clone the original `labs` git 
   repo (not your copy of it.) This means that you don't need to
   change the import path in the source files to use your own repository's
   path. That is, when you make a commit and push to submit your handin, you 
   don't have to change this back to the original import path.

7. Now we need to set up your own remote so that you can make changes and push 
   those changes to your own copy of the repo. Follow these instructions:
	1. `cd $GOPATH/src/github.com/uis-dat320-fall18/assignments`.
	2. `git remote add labs https://github.com/uis-dat320-fall18/username-labs` 
     where `username` should be replaced with your own GitHub username.
	3. The above command adds your own `username-labs` repository as a remote
   repository on your local machine. This means that once you've modified some
   files and committed the changes locally, you can run: 
	4. `git push labs` to have them pushed up to your own `username-labs` repository on GitHub.

8. If you make changes to your own `username-labs` repository using the GitHub
   web interface, and want to pull those changes down to your own computer, you
   can run the command: 
	* `git pull labs master` 
	* In later labs, you will work in groups. This approach is also the way that you can download (pull) your group's code changes from GitHub, assuming that another group member has previously pushed it out to GitHub.

9. As time goes by we (the teaching staff) may publish updates to the
   original `labs` repo, e.g. new or updated lab assignments. To see these 
   updates, you will need to run the following command: 
	* `git pull origin master`.

10. For the first lab, you will submit the source code for the hello world
   application and the answers to the three sets of questions. The skeleton code
   for the application, `hello.c`, has been provided along with forms for the
   questions. Autograder will run a set of test cases to verify your
   implementation. Not all tests must pass to get a passing grade.

11. In the following, we will use `hello.c` as an example. Change directory to:
   `cd $GOPATH/src/github.com/uis-dat320-fall18/assignments/lab1` and confirm that the files
   for lab1 resides in that folder. They should, assuming that you ran the `go
   get` command earlier.

12. Implement the main function in `hello.c`.

13. When your application is working, you may push your code to GitHub. This will 
    trigger Autograder which will then run a test suite on your code.

14. Using `hello.c` as an example, use the following
    procedure to commit and push your changes to GitHub and Autograder:
    ```
    $ cd $GOPATH/src/github.com/uis-dat320-fall18/assignments/lab1
    $ git add hello.c
    $ git commit
    // This will open an editor for you to write a commit message
    // Use for example "Implemented Assignment 1"
    $ git push labs
    ```

15. Running the last command above will, due to an error on our part, result in
    Git printing an error message about a conflict between the `README.md` file
    in the `labs` repository and the `README.md` file in your `username-labs`
    repository. Here is how to fix it:

    ```
    $ git push labs
    ...
    ! [rejected]        master -> master (fetch first)
    error: failed to push some refs to 'git@github.com:uis-dat320-fall18/username-labs.git'
    ...
    $ git pull labs master
    ...
    Auto-merging README.md
    CONFLICT (add/add): Merge conflict in README.md
    Automatic merge failed; fix conflicts and then commit the result.
    ...
    $ cd $GOPATH/src/github.com/uis-dat320-fall18/assignments
    $ vi README.md
    // Remove everything in the file, then add for example "username-labs" to the file.
    // Save and exit.
    $ git add README.md
    $ git commit
    $ // Use the existing (merge) commit message. Save and exit.
    $ git push labs
    // Your push should now complete successfully.
    // You may check that your changes are reflected on GitHub through the GitHub web interface.
    //If you still get an error like "fatal: Exiting because of an unresolved conflict." use the following command
    $ git pull --allow-unrelated-histories labs master
    $ git add README.md
    $ git commit
    $ git push labs
    ```

16. Autograder will now build and run a test suite on the code you submitted.
    You can check the output by going the [Autograder web
    interface](http://ag3.ux.uis.no/). The results (build log) should be
    available under "Individual - lab1". Note that the results shows output
    for all the tests in current lab assignment. You will want to focus on the
    output for the specific test results related to the task you're working on.

17. Repeat step 15 for the three sets of answers.

18. If some of the autograder tests fail, you may make changes to your code/answers.

19. Push your changes using `git push labs`. You should be able to view your
    results in the Autograder web interface as described earlier.

## Lab Approval

To have your lab assignment approved, you must come to the lab during lab hours
and present your solution. This lets you present the thought process behind your
solution, and gives us a more information for grading purposes. When you are
ready to show your solution, reach out to a member of the teaching staff.
It is expected that you can explain your code and show how it works.
You may show your solution on a lab workstation or your own
computer. The results from Autograder will also be taken into consideration
when approving a lab. At least 60% of the Autograder tests should pass for the
lab to be approved. A lab needs to be approved before Autograder will provide
feedback on the next lab assignment.

Also see the [Grading and Collaboration
Policy](https://github.com/uis-dat320-fall18/course-info/blob/master/policy.md)
document for additional information.

