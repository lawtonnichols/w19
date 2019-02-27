---
layout: lab
num: lab03
ready: true
desc: "Counting ducks: File I/O and flow control"
assigned: 2019-02-05 09:00:00.00-7
due: 2019-02-12 09:00:00.00-7
---


# Introduction

By the time you have completed this lab, you should be able to:

* Use for loops to count up and count down
* Check command-line argument for input filename, and open that input file for reading
* Read every line of text in an input file and process it, using a while loop
* Use if-else statements to select blocks of code
* Count how many times a value occurs in a file
* Use Unix commands to create directories, navigate to directories, list files, and copy files
* Use the "make" command to compile simple stand-alone C++ programs (i.e. single source code file)
* Run simple C++ programs both with and without a single command-line parametera
* Practice git/GitHub workflow of committing your changes

This is an **individual** lab.

# Step by Step Instructions

* [Log on to CSIL and bring up a terminal window](#step1)
* [Create a new repo, and clone it to your local directory](#step2)
* [Get the starter code from a local directory](#step3)
* [Compile and run the first program for this assignment](#step4)
* [Copy sample01.cpp to myProg01.cpp and make changes](#step5)
* [Read from input files and count ducks](#step6)
* [A more detailed counting program](#step7)
* [Commit your code on GitHub](#step8)
* [Turn in your code ](#step9)


## Step 1: Log on to CSIL and bring up a terminal window. <a name="step1"></a>

I hope I can safely assume that you have all gotten a CoE account.
 If your account is not working, refer to Lab00 on how to fix it. 

Log into your account to make sure it works.
As a reminder to get to the terminal go to <strong>Application</strong> Menu, then <strong>System Tools</strong>, then <strong>Terminal Window</strong>.

In the steps below, and in most future labs, you will create files on your own
account.

## Step 2: Create a new repo, and clone it to your local directory <a name="step2"></a>

In lab02, we have done the same thing. So if you don't know to how to do that, please refer to lab02 for details. The basic steps are as follows:

* Create a git repo on github following the correct naming convention. Don't forget to make it 'PRIVATE'.

* Go to your CS16 directory and clone the repo locally.


## Step 3: Get the starter code from a local directory <a name="step3"></a>


Copy the skeleton to your local lab03 repo using the following command, <strong>REMEMBER</strong> to change the directory name in the commands below to your own directory's name, in this lab we would use `lab03_agaucho` instead of `<your_repo>` as a example for your local git directory:

```
  cp /cs/faculty/ykk/cs16/labs/lab03/* ~/cs16/<your_repo>/
```

After doing this command, if you `cd` into ~/cs16/lab03_agaucho/ and use the `ls` command, you should see several .cpp files:

```
-bash-4.2$ ls
animals01.txt  animals02.txt  countDucks.cpp  sample01.cpp
-bash-4.2$
```

If you don't see those files, go back through the instructions and make sure you didn't miss a step. If you still have trouble, ask for assistance.


Let's add and commit these files to your git repository.

```
git add .

git commit -m "Adding starter files for Lab 3"

git push

```

Let the staff know if you got any errors.



## Step 4: Compile and run the first program for this assignment <a name="step4"></a>

The first program we are going to compile and run is one that demonstrates a `for` loop in C++.   

In your lab03 directory, you should have a program called sample01.cpp that we copied in the previous step. 
Below is a reminder of how you can "move" yourself in that directory (though you should already be there):

```
-bash-4.2$ cd ~/cs16/lab03_agaucho/
-bash-4.2$ pwd
/cs/student/<your_username>/cs16/<your_repo>/
-bash-4.2$
```

Then you can list out your files with the <code>ls</code> command:

```
-bash-4.2$ ls
animals01.txt  animals02.txt  countDucks.cpp  sample01.cpp
-bash-4.2$
```

Finally, use the Unix <code>cat</code> command to list the contents of the file sample01.cpp.  (The reason this command is called "cat" has nothing to do with the animal that goes "meow".  The name is derived from its ability to concatenate files.)

```
-bash-4.2$ cat sample01.cpp
// sample01.cpp
#include <iostream>
using namespace std;
 
int main() {
    // Simple for loop that counts from 1 up to n
 
    int n=5;
 
    for (int i=1; i<=n; i++) {
       cout << "i=" << i << endl;
    }
 
    return 0;
}
-bash-4.2$
```

We are going to create a simple `Makefile`, which will allow us to compile the programs in modules.

Create a new file called **`Makefile`** (note that **the name has to be exact**: capital M and no file extension).
```
-bash-4.2$ vim Makefile
```

Inside of that file, add the following TWO lines (making sure you remember to include the colon **`:`** and **add a TAB before `g++`**, there should be **no spaces before `g++`**):
```
sample01: sample01.cpp
	g++ sample01.cpp -o sample01
```

You are ready to compile your `sample01.cpp` program using this `Makefile`.

Compile this with the command <code>make sample01</code> and run it with the command <code>./sample01</code>.  It looks like this:

```
-bash-4.2$ make sample01
g++     sample01.cpp   -o sample01
-bash-4.2$ ./sample01
i=1
i=2
i=3
i=4
i=5
-bash-4.2$
```


If you get that output, you are ready for the next step.

**Troubleshooting**

If you got the following error:
```
$ make sample01
Makefile:2: *** missing separator.  Stop.
```
it means you ignored our warning and *did not include just the TAB before `g++`*.


If you got a different error, let the TA or tutors know.


**Read and follow the instructions carefully.**


## Step 5: Copy sample01.cpp to myProg01.cpp and make changes <a name="step5"></a>

Use the the Unix command <code>cp </code><em>oldfile newfile</em> which copies files, to copy from sample01.cpp to a new file called myProg01.cpp, as shown here:

```
-bash-4.2$ cp sample01.cpp myProg01.cpp
-bash-4.2$ ls
animals01.txt  countDucks.cpp  sample01
animals02.txt  myProg01.cpp    sample01.cpp
-bash-4.2$
```

Now you have a new file called myProg01.cpp that is a copy of sample01.cpp. This is your change to practice the [basic Vim commands](/ucsb-cs16.github.io/topics/vim_basic_eight/).   
Open `myProg01.cpp` in a text editor and make the following changes:

1. Change the comment at the top of the file so that it says `// myProg01.cpp`
2. Add a new line and make the second line of the file to be of the format "`// Author: your name`"
3. Change the comment within the code to "`Simple program that counts down from n to 1`"

4. Change the `for` loop as follows:

  * Instead of initializing to 1, initialize to `n`
  * Instead of testing <code>i&lt;=n</code>, test whether <code>i&gt;0</code>
  * Instead of changing i by incrementing with <code>i++</code>, change it to decrementing with <code>i--</code>
  * Remove the printing of "i=" each time.  Instead just print the number.  
  * Instead of printing a newline after each number, just print one space.  We do that by changing <code>cout &lt;&lt; "i=" &lt;&lt; i &lt;&lt; endl;</code> to <code> cout &lt;&lt; i &lt;&lt; " ";</code>
  * Add a line that prints a newline at the very end, just after the for loop is over, but BEFORE the <code>return 0;</code> statement. *Note: As a reminder, you get out of vim or gvim with ESC:x or ESC:wq.*

Compile and run myProg01.cpp with these changes. The output should look like this:

<pre>
5 4 3 2 1
</pre>

To compile the code using the makefile, add `myProg01` as another target in your Makefile: open the Makefile file again (`vim Makefile`) and add the following TWO lines (making sure you remember to include the colon **`:`** and **add a TAB before `g++`**, there should be **no spaces before `g++`**):

```
myProg01: myProg01.cpp
	g++ myProg01.cpp -o myProg01
```

Save the file and exit it.

Now, to acually compile, run `make myProg01`. To run your code, use `./myProg01`.

You are now ready to move to the next step.   


**Troubleshooting**
Tip: *If you make a mistake that results in an "infinite loop", i.e. the window is just scrolling by without stopping, you can use CTRL+C (hold down Control and type C) to stop the program.*
To fix the program, verify that your loop conditions are correct (see the instructions above).


## Step 6: Reading from input files and counting ducks <a name="step6"></a>
The next files we are going to look at are not C++ code, but rather data files.

Use the `cat` command to look at the contents of animals01.txt and animals02.txt. You should get results like these:

```
-bash-4.2$ cat animals01.txt
duck
duck
goose
-bash-4.2$ cat animals02.txt
duck
duck
goose
duck
duck
cow
duck
duck
dog
-bash-4.2$
```

The next program we are going to look at will read input from files such as these.    It is called <code>countDucks.cpp</code> and it will simply count the number of ducks in each file.

Before you look at the code, try compiling the program and running it, because this will help you understand what the program is trying to do.  

Add `countDucks` as another target in your Makefile: open the Makefile file again (`vim Makefile`) and add the following TWO lines (making sure you remember to include the colon **`:`** and **add a TAB before `g++`**, there should be **no spaces before `g++`**):

```
countDucks: countDucks.cpp
	g++ countDucks.cpp -o countDucks
```

Hopefully, you are starting to see the pattern!



Compile with:

```
-bash-4.2$ make countDucks
g++     countDucks.cpp   -o countDucks
-bash-4.2$
```

Then try running it with just <code>./countDucks</code>.  You'll see that you get a "Usage" message.  This is telling us that the program expects a "command-line argument", which is the name of the file to read:

```
-bash-4.2$ ./countDucks
Usage: ./countDucks inputFile
-bash-4.2$
```

IMPLEMENT THE COUNTDUCKS PROGRAM in countDucks.cpp so that when you run the program with argument animals01.txt as the filename, it produces the following output:

```
-bash-4.2$ ./countDucks animals01.txt
There were 2 ducks in animals01.txt

```

Alternatively if you give animals02.txt as the argument it should produce the following output.
```
-bash-4.2$ ./countDucks animals02.txt
There were 6 ducks in animals02.txt
-bash-4.2$
```

You will need to use `ifstream` and the `getline()` functions (see examples of `ifstream` [here](http://www.cplusplus.com/reference/fstream/ifstream/ifstream/) and [here](http://www.physics.utah.edu/~detar/lessons/c++/canned_classes/node9.html), and examples of `getline` [here](http://www.cplusplus.com/reference/string/string/getline/) and [here](https://stackoverflow.com/questions/12133379/c-using-ifstream-with-getline)).
You can check if a `string` variable contains a specific string, e.g., "animal" by using `if ( ... == "animal")`.

Once you've done that, you are ready for the next step.


## Step 7: A more detailed counting program <a name="step7"></a>

Your job is now to copy `countDucks.cpp` to a file `myProg02.cpp` and make some changes.

First, let's stipulate that you may assume that everything in the input file is an animal, one per line&mdash;if someone adds "potato" or "bicycle" to the file, you can just assume that potato and bicycle are now to be considered types of animals.

1. Add a variable that will count ALL animals in the file.    Give it an appropriate name and initialize it to zero.
2. Add a variable that will count ALL animals in the file that are NOT ducks.   Give it an appropriate name and initialize it to zero.
3. Add code that will increment those counts when appropriate.  It may help to know that C++ has an else clause for an if that looks like this:

```
   if (condition) {
     // lines of code here are
     // executed when condition is true
   } else {
     // lines of code here are
     // executed when condition is false
   }
```

Note that it is NOT required for every `if` to have an `else` clause.

Also note that the braces <code>{ } </code> are:

* OPTIONAL when there is a **SINGLE** statement inside a particular if or else block (still recommended though!)
* REQUIRED when there is more than one statement inside a particular if or else block

After making these changes, one more thing: change the lines that give the output so they look like the ones shown below.


<pre>
Report for animals01.txt:
   Animal count:    3
   Duck count:      2
   Non duck count:  1
</pre>

<pre>
Report for animals02.txt:
   Animal count:    9
   Duck count:      6
   Non duck count:  3
</pre>

It is IMPORTANT to be EXACT since the autograder system will compare your output with the expected output character-by-character.   The spacing MATTERS!   You can add extra spaces at the beginning and end of the string literals for <code>"   Animal count:   "</code>  and <code>"   Duck count:   "</code> so that the spacing comes out right and matches the expected output.  I'm not going to tell you how many; you'll have to figure that out.

Note that we will also test your program on other input files, so you should too.  Use the `cp` command to copy animals02.txt to animals03.txt and add some ducks and some other animals (note that you can use Vim's `yy` and `p` or `P` commands to copy/yank and paste lines).  Count by hand, and make sure that the count when you run your program matches what is expected.

When you are satisfied that the count is correct and that format of the output is precise, you are ready to submit your code for grading.



## Step 8: Commit your files to GitHub <a name="step8"></a>

Hopefully, you've been working inside of the directory that you cloned from GitHub.

You can check the status of your files by running the `git status` command.
git will show you the files that have been added or changed.

Let's add and commit these files to your git repository.

```
git status

git add .

git commit -m "Adding Lab 3 files"

git push

```


## Step 9: Turn in your code on gradescope <a name="step9"></a>


* Navigate to your ~/cs16/lab03_agaucho directory, the one containing your code for this week's lab.
<pre>
-bash-4.2$ cd ~/cs16/lab03_agaucho
</pre>

* Use the <code>ls</code> command to list your files and to be sure that you have the myProg01.cpp and myProg02.cpp files in your directory.  It is ok if there are other files (countDucks.cpp, animals01.txt, etc.) along with the executables.  You only have to submit myProg01.cpp and myProg02.cpp.

```
-bash-4.2$ cd ~/cs16/lab03_agaucho
-bash-4.2$ ls
animals01.txt  countDucks.cpp  myProg02      sample01
animals02.txt  myProg01.cpp    myProg02.cpp  sample01.cpp
-bash-4.2$
```

Submit all the cpp files to lab03 assignment on gradescope. Then visit gradescope and check that you have a correct score.

* You must check that you have followed these style guidelines:

1. Indentation is neat, consistent and follows good practice. Your code should be indented neatly.  Code that is inside braces should be indented, and code that is at the same "level" of nesting inside braces should be indented in a consistent way.    Follow the examples from lecture, the sample code, and from the textbook. 
2. Variable name choice: variables should have sensible names.

* Your submission should be on-time. If you miss the deadline, you are subject to getting a zero.



