<div data-align="center">

## **gtgt**

## *gitty-gitty*

### **The General/GNU Template Generation Tools**

### *version \<\#3.2.0\#\>*

</div>

### *(0) Content of this Explanation*

  - (1) [General Purpose](#gp)
  - (2) [Involved Applications](#ia)
  - (3) [Installation Conditions](#ic)
  - (4) [Special Hints For The Usage (handbook)](#sh)
  - (4.01) [How do I create my first project?](#sh401)
  - (4.02) [The configuration file gcng.conf and what the hell does
    "company license" mean?](#sh402)
  - (4.03) [What if I want to build my tarball with more or other
    sourcefiles than given by the gptg-script?](#sh403)
  - (4.04) [What if I don't want to write libraries?](#sh404)
  - (4.05) [What if I don't want to work with deep embedded daughter
    modules?](#sh405)
  - (4.06) [What if I only want to offer a set of scripts?](#sh406)
  - (4.07) [What if I want to add a new sister module or class?](#sh407)
  - (4.08) [What if I want to add a new module or class for
    libraries?](#sh408)
  - (4.09) [What if I want create a new library ?](#sh409)
  - (4.10) [What if I want to add doc files or scripts ?](#sh410)
  - (4.11) [What if I want to use the VPATH ?](#sh411)
  - (4.12) [What about the coding and documentation style?](#sh412)
  - (4.13) [What if I want to change the numbers of the release or the
    revision?](#sh413)
  - (4.14) [What if I want to add debugging and profiling informations
    during the compilation?](#sh414)
  - (4.15) [What if I want to import my newly generated project into a
    cvs or subversion repository or to use wildcards to commit and/or
    add files?](#sh415)
  - (4.16) [What if I want to build a rpm-package on the base of my
    tarball?](#sh416)
  - (5.A) [What if I need more informations?](#c5A)
  - (5.B) [What if I want to add some remarks?](#c5B)
  - (6) [Thanks](#c6)

copyright (c) 2000/2001/2002/2003/2004/2005/2006/2007 karsten reincke
(<karsten.reincke@fodina.de>)

### *(1) <span id="gp">General Purpose</span>*

The **(general | GNU) template generation tools** are a set of scripts
for creating a whole set of sources, which may already be compiled and
installed by using the GNU development tools. Think of ***gtgt*** as a
program which is able to create an already compilable, very
sophisticated "hello world" program, written in C or C++ and constituted
by a main program, two internal modules (classes), one static and one
shared library. Using gitty-gitty you will get a template of sources for
the main cases you might meet, and which you can also use as examples
for automake, autoconf and so on.

For understanding the general purpose of the **(general |
GNU)-template-generation-tools**, we should have a look at an
abbreviated version of the history of programming with gcc:

1.  At the beginning we have nothing but ***gcc***: we have to order
    each act of compilation with regards to name the right versions of
    sourcecodes on the command-line. **(practical, but not
    comfortable)**
2.  The next step in evolution is "MAKE", now we are not only able to
    create scripts for compiling more than one set of sources, but now
    we can demand to respect dependencies. **(comfortable, but not the
    end of the world)**
3.  Then there has been the problem to compile for more than one
    specific hardware environment. And this problem leads to the
    solution by using ***autoconf***: We are setting up two scripts,
    configure.in and Makefile.in. In the first one we determine in a
    declarative way those aspects, which we want to have tested. Then we
    call the tool 'autoconf' which takes the ***configure.in*** scripts
    and creates the well known ***configure*** script. This script
    itself takes the ***makefile.in***, tests the environment and
    replaces variables in the makefile.in by the test-results and
    creates the normal makefiles, which are now very sophisticated. But
    at this point of history, we only have to create the
    ***configure.in*** and the ***makefile.in***, and we can use
    informations about the hardware used for the compilation, by writing
    variables into our makefile.in **(a bit better, but still
    optimizable)**
4.  "Why" - so the next question - "shouldn't it be possible to use a
    high-level declarative language for saying what we want to compile
    instead of using the old makefile-language?" The answer has been
    ***automake***. This script takes ***Makefile.am*** and
    ***configure.in*** and creates ***Makefile.in***. and as
    software-developpers we now only have to write our intentions into
    Makefile.am and configure.in. **(the world seems to be good, but not
    the best of all possible ones)**
5.  The GNU development tools demand a lot more files than
    ***Makefile.am*** and ***configure.in***: One has to touch at least
    NEWS, Changelog, Install, README ..., and you have to create a
    directory structure. For automating this procedure, ***autotools***
    have been offered: Here you may create a whole but empty environment
    for the GNU development tools and you have a tool to generate files
    containing a copyright-note. (This major step has been done by
    [Eleftherios
    Gkioulekas](http://www.amath.washington.edu/~lf/tutorials/autoconf/))
    **(yoop, yoop, but then ...)**
6.  There are two demands, which can't be fullfilled by autotools. If
    you want to have your own licenses in your sources, you can't use
    autotools because they only offer GNU files and -conditions. Ok, GNU
    is quite fine, but it's not everything. And although you are using
    autotools you still have to declare and define all functions inside
    of your sources and you need to setup the correct Makefile.am and
    configure.in in a corresponding way. That can be automised too - at
    least for a starting version. And that's the task of the ***(general
    | GNU) template generation tools***. They are able to replace the
    autotools and contain three scripts: ***gcng***, ***gscg*** and
    ***gptg***.

### *(2) <span id="ia">The Constituting Tools</span>*

  - ***gcng = General Copyright Note Generator***  
    Script of generating files, which already contain the correct
    copyright header, regardless of which copyright and which
    programming language shall be used

  - ***gscg = General Source Code Generator***  
    Script for generating all already compilable source files of a
    software module, namely the header file as a module declaration and
    the source file as a module defintion.
    
    You can select c or c++ as the programming-language, which is used
    for writing these functions. Think of gscg as a program, which is
    able to create very sophisticated "hello world" modules.

  - ***gptg = General Project Template Generator***  
    Script for generating the whole set of files for an already
    compilable and installable software project: Using gscg + gcng too,
    gptg will offer a project directory, which is completely prepared
    for utilisation of autoconf and automake and which contains a quite
    sophisticated "hello world" program - being built upon two modules
    and one static library - and which already offers a shared library.

Using these tools (which are using themselves too), you get a template,
which only needs to be adopted to what you want to have.

### *(3) <span id="ic">Installation Conditions</span>*

For being able to install and **use** the gtgt you need

  - Normal gcc development tools (normally you are already having them)
  - autoconf
  - automake
  - libtools

For installing the gtgt you do the following:

  - gunzip gtgt-xxx.tgz
  - tar -xvf gtgt-xxx.tar
  - cd gtgt-xxx
  - ./configure --prefix=/whereever/youwant/tohave/thetools
  - make
  - su
  - make install

Note: It's not nescessary to have autoconf and automake for installing
gtgt but for using it, because adding a new piece of sourcecode includes
modification of Makefile.am (and configure.in). And in all those cases
you need to call automake and autoconf at least one time, before being
able to call configure for the set.

### *(4) <span id="sh">Special Hints For Usage (Handbook)</span>*

### **(4.1) <span id="sh401">How do I create my first project?</span>**

1.  Create a short project name like 'mypo', which should not contain
    blanks or other seperators. Think of it as a name, not as a double
    name or sentence or anything else. Following the
    c/c++-coding-standard this name will automatically be changed in
    some cases: he can be capitalized or written in lower or upper
    cases.

2.  Decide, whether you want to use C or C++ as a programming-language.
    (If you only want to write shell scripts, you may choose any of
    these.)

3.  Decide with which main release number you want to begin. Usually you
    start with zero (select an integer like 1,2,3, not any real or float
    number like 1.2 and so on)

4.  Decide with which revision number you want to begin. Usually you
    start with one (select an integer like 1,2,3, not any real or float
    number like 1.2 and so on)

5.  Type 'gptg --help' to see in which way these decisions can be
    inserted into gptg:
    
    |      |                                                                  |             |                      |                             |
    | ---- | ---------------------------------------------------------------- | ----------- | -------------------- | --------------------------- |
    | gptg | OPTIONS                                                          | \[PROJECT\] | \[RELEASE\]          | \[REVISION\]                |
    |      | \-h, --help, -v, --version, -cpp (Language C++), -c (Language C) | projectname | start release number | start release branch number |
    

6.  gptg uses gscg and gscg uses gcng. gcng itself needs a file
    gcng.conf in the working-directory. This file contains 6 lines:
    
    1.  The authorname
    2.  The email adress of the author
    3.  The year of publishing the program (will be inserted
        automatically)
    4.  The name of the company licensing the sources
    5.  The absolute path to a short version of the company's license
    6.  the absolute path to a long version of the company's license
    
    If this file doesn't exist, you will be asked for the informations
    and it will be created. If your company is GNU, you won't be asked
    for licenses, because they are known. If not, you have to create
    such licenses. They will be used automatically for generating
    sourcecode headers. Examples for those company licenses can be found
    in the documentation directory of the gtgt, which will be installed
    under $PREFIX/share/doc/gtgt.

7.  ``` 
    user@computer> gptg -cpp mypo 0 1
    ```
    
    will generate a project named mypo, positioned in a directory
    mypo-0.1

8.  Note: After changing into your project directory, you can already
    type ./configure, make, make distcheck, or make install. You have a
    project which at first installs one application named like your
    project and made to modules and which installs two libraries as a
    second step, a static and a shared one. You now have to adopt these
    possibilities to your whishes and you can use this automatically
    generated project as a teaching example to handle autoconf and
    configure.in, automake and Makefile.am and configure.in while
    working at your own specific project. Because the sources are
    following the c/c++ coding standard and are already commented in the
    doxygen style, you can take them as teaching examples for these
    aspects, too.

### **<span id="sh402">(4.02)</span> The configuration file gcng.conf and what the hell does "company license" mean?**

Ok, GNU is good. Very good, indeed. But \[ in very rare cases ;-) \]
it's not evrything. Therefore, for example, the LGPL has been created.
Well, you should be able to create applications following the GNU
methods and GNU recommendations and using the GNU tools - without
publishing your results under the GPL. In these cases you might want to
distribute your sources under a special company license. And this
license should be referred to by all your files.

GNU uses the following way to mark the GNU sources as GNU sources:

1.  Inside of the project directory, there the whole GNU license is
    given to the user who gets a source tarball for creating an
    application from the sources. This license can be found in the file
    COPYING.
2.  Each sourcefile contains a short version of this license by listing
    up the main points of the whole license and refering to file COPYING
    or the GPL
3.  Sometimes it's necessary to publish special parts of the tarball
    under a weaker license than the other parts. For example remember
    the LGPL: In these cases such (library-)sources contain a special
    hint.

Think of the company license as a special "GNU license" of your company
;-). And therefore you should have two versions: The long version is
that one, which shall be put into the file COPYING, and the short is
that one, which will be used inside of the the files and which should
refer to the long version.

The last question could be this: How can I determine, to create a
template for my company or for the GNU world? the answer is very simple:

  - If you insert the word GNU in the fourth line of the gcng.conf file,
    line 5 and 6 will be ignored and the normal GNU licenses will be
    inserted for case (1) and (2) of the above mentioned list.
  - If you insert a different word than GNU in the fourth line of
    gcng.conf, line 5 and 6 will be evaluated as absolute pathnames of
    your company license files: line 5 as pathname of the abbreviated
    version, line 6 as pathname of the long version.

The gtgt-tarball offers two license examples inside the doc-directory:
the file "company-license.long" and the file "company-license.short".
Note: They haven't been juristically checked\! They exist for
demonstrating the technical possibilities.

### **<span id="sh403">(4.03)</span> What if I want to build my tarball with more or other sourcefiles than given by the gptg script?**

Very simple, in the first part of the following chapters, we explain
what you should do, if you don't want to use the full set of files. And
in the second part we explain, what you need to do, if you want to
expand set files.

### **<span id="sh404">(4.04)</span> <span id="dellib">What if I don't want to write libraries?</span>**

Read ${YOURPRJ} as a name of your project:

1.  Change into the toplevel of your project directory
2.  Delete the substring 'lib/Makefile' as parameter of the macro
    AC\_OUTPUT in the file 'configure.in'
3.  Delete the directory 'lib'
4.  Delete the substring 'lib' as parameter of the macro SUBDIRS in the
    file 'Makefile.am'
5.  Change into the subdirectory src of your project directory
6.  Delete the substring '-l ${YOURPRJ}\_stli' as parameter of the macro
    ${YOURPRJ}\_LDADD in the file 'Makefile.am'
7.  Delete the substring '-L$(topbuilddir)/lib' as parameter of the
    macro ${YOURPRJ}\_LDFLAGS in the file 'Makefile.am'
8.  Delete all lines containing the substring '\_stli' in the
    source-files ${YOURPRJ}.c(pp)
9.  Call autoconf and automake or your reconf script

### **(4.05) <span id="sh405">What if I don't want to work with deep embedded daughter modules?</span>**

1.  change into the toplevel of your project directory
2.  Delete the substring 'src/damo/Makefile' as parameter of the macro
    AC\_OUTPUT in the file 'configure.in'
3.  Change into the subdirectory src of your project-directory
4.  Delete the substring 'damo' as parameter of the macro SUBDIRS in the
    file 'Makefile.am'
5.  Delete all lines containing the substring 'damo' in the source-files
    ${YOURPRJ}.c(pp)
6.  Delete the directory 'damo' in your src-directory
7.  Call autoconf and automake or your reconf script

### **(4.06) <span id="sh406">What if I only want to offer a set of scripts?</span>**

1.  [Delete the libraries](#dellib) like described above
2.  Change back into the toplevel of your project directory
3.  Delete the substring 'src/Makefile' and 'src/damo/Makefile' as
    parameter of the macro AC\_OUTPUT in the file 'configure.in'
4.  Delete subdirectory src of your project directory
5.  Delete the substring 'src' as parameter of the macro SUBDIRS in the
    file 'Makefile.am'
6.  Call autoconf and automake or your reconf-script

### **(4.07) <span id="sh407">What if I want to add a new sister module or class?</span>**

Sister modules are sources with a declaring headerfile and a defining
sourcefile physically lying in the same directory of the main sourcefile
and being included. For generating such a module you may do this:

1.  Change into the subdirectory src of your project directory

2.  Call gscg and insert the parameters:
    
    <table style="width:100%;">
    <colgroup>
    <col style="width: 16%" />
    <col style="width: 16%" />
    <col style="width: 16%" />
    <col style="width: 16%" />
    <col style="width: 16%" />
    <col style="width: 16%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td>gscg</td>
    <td>[-c|-cpp|-h|-v]</td>
    <td>[-i|-s|-is]</td>
    <td>[MODULE]</td>
    <td>[PROJECT]</td>
    <td>[RELEASE]</td>
    </tr>
    <tr class="even">
    <td> </td>
    <td>Select your programming language or 'help' or 'version'</td>
    <td><ul>
    <li>-i echos the corresponding headerfile</li>
    <li>-s echos sourcecode for the module</li>
    <li>-is writes include- + sourcecode as file</li>
    </ul></td>
    <td>should be a short module identifier without brackets, underlines, points etc. etc.</td>
    <td>should be a short project identifier without brackets, underlines, points etc. etc.</td>
    <td>release number (must be a float with two digits like 1.0 !!!)</td>
    </tr>
    </tbody>
    </table>
    
    **user@mashine \>** ***gscg -cpp -is modu mypo 1.0*** creates mypo.h
    and mypo.cpp

3.  Include ${MODULENAME}.cpp and ${MODULENAME}.h in Makefile.am as
    arguments of ${YOURPROJECT}\_SOURCES

4.  Change back to the top of your project directory and call autoconf
    and automake or your reconf script

5.  Then write and include your module / class

### **(4.08) <span id="sh408">What, if I want to add a new module or class for libraries?</span>**

Nearly the same as for adding a new sister module. But act in the
library directory instead of the source directory.

### **(4.09) <span id="sh409">What, if I want to create a new library ?</span>**

Nearly the same as for adding a new sister module. After having
determined the library name (=module name) you need to insert the
following into the Makefile.am of your lib-directory:

  - lib\_LIBRARIES=lib${modulename}.a
  - lib${modulename}\_a\_sources= $your-sources
  - Don't forget to insert the new library name in src/Makefile under
    ${YOURPROJECT}\_LDADD as a string starting with -L

### **(4.10) <span id="sh410">What, if I want to add doc files or scripts ?</span>**

  - Move the scripts and documentation files into the director doc
    respectively scripts
  - Change into the subdirectory doc resp. scripts of your project
    directory
  - Add the filenames of the new scripts to the variable EXTRA\_DIST of
    Makefile.am . In case of shell-scripts, add the name also to the
    variable bin\_SCRIPTS and to CLEANFILES and insert any makefile
    target for those scripts.

### **(4.11) <span id="sh411">What, if I want use VPATH ?</span>**

The VPATH variable allows us to use other directories whose content is
able to fulfill the dependencies although it's not directly integrated
into the 'make' procedure. Using this variable, one can split the
objectfiles and its sources. From make's point of view, it's a hack. But
not all hacks are bad, aren't they?. Ok, do this (and write me, if you
are sucessful ;-) ):

1.  Change into the top of your project directory
2.  Rename the subdirectory src into vpdir (or anything else)
3.  Rename all those substrings 'src' into vpdir, which arise as
    contents of the variable SUBDIRS in the main Makefile.am
4.  Insert a new substring src into the content of the variable SUBDIRS
    in the main Makefile.am
5.  Create a new subdirectory src
6.  mv all sources vpdir/\*.cpp \*.c \*.h from vpdir into the new
    directory src
7.  Change into the new src directory
8.  Edit a new src/Makefile.am
9.  Insert into this src/Makefile.am the only variable EXTRA\_DIST=
    $all-names-of-your-moved-sources
10. Insert into each Makefile.am arising in any directory under vpdir or
    lib the string VPATH=$(top\_srcdir)/src.

The main point of this procedure is this: make recursively follows the
structure of vpdir. There maket meets its targets. And it seeks the
sources, named inside of the Makefile and not really being in the make
directory. But make finds them none-the-less, because it looks for them
in all directories named by the variable VPATH which in this case is
indicating the directory source as an add-on

### **(4.12) <span id="sh412">What about the coding and documentation style?</span>**

Last but not least, we have added the doxygen documentation style into
the automatically generated sourcefiles of your project initially
created by the gitty-gitty-tools. This includes that

  - the correspondig default doxygen configuration file (named Doxyconf)
    will automatically be generated inside of the project-directory
  - all pieces of sourcecode are already be commented in the doxygen
    style
  - the initial version of corresponding doxygen sourcecode
    documentation will be automatically generated while creating the
    initial version of your project
  - the whole sourcecode doxygen documentation of the initial-version of
    your project can be found under doc/doxygen/

For being generally acceptable, we have adopted the c++ and c coding
standard. But note: There doesn't exist "**the** coding standard"; you
can find more than one which differ in more or less details. Therefore
we give only one hint for a [C++ Coding
Standard](http://www.possibility.com/Cpp/CppCodingStandard.html) while
recommending to have a look at the others, being found with some search
engine.

### **(4.13) <span id="sh413">What if I want to change the numbers of the release or the revision?</span>**

Last but not least we have integrated a script into the GNU-sourcetree
which allows the change of the release- and the revisionnumber.

Remember, if you let create the template of your project you have to
name integers for the release and the revision on the commandline. these
numbers will be merged into many places: for example into the short
copyright line of each piece of sourcecode where the name of the file
and that of the project is also announced.

But there exist more important places where these numbers are inserted.
There they will be evaluated for generating the tarball-number or the
library-version. For updating all these case with one command **gptg**
writes a script into your project-direcgtory. This script named
***change-release*** does what its name announces: it should be called
with one or more file- or directorynames (or with \*) as parameter. and
for all these entities it recursively changes all relevant
release/revision numbers.

For using this script you have to respect the following points:

1.  You shouldn't change the release/revision-strings manually. or at
    least you have to respect the given syntactically structure.
2.  If you want to increment (decrement ?-) ) the revison/release-number
    you have to edit the script ***change-release***: insert the correct
    old versions of the numbers and the wished new versions at the
    beginning of the script and then call *./change-release*
3.  Note, ***change-release*** isn't backward compatible. if you want to
    use it in an existing project (made by GTGT release 1.1 or earlier)
    you have to recreate it. and if you merge older pieces of sourcecode
    into that new tree you have at least to replace the short-copy-right
    line which signals filename, project and version-number

Note: In the string "-version-info xc:xr:xa" , which arises in the
�Makefile.am� and is updated by the script �changerelease�, the
integer at the position �xc� means �current release�, the integer at the
position �xr� �revision� and the integer at the postion �xa� the �age�
of the library. And the age of a library denotes the row of elder
releases, which interfaces all only are expanded by the newer ones.

But this row of integers "xc:xr:xa" arises not directly in the version
of a shared library. You have to read such versionnumbers like the
scheme �libxxx-so.xc.xa.xr�: the first integer of a library-version
number denotes the current release, the second the age(\!) and the third
the the revision number.

### **(4.14) <span id="sh414">What if I want to add debugging and profiling informations during the compilation?</span>**

In each Makefile.am GTGT offers now four different lines with compiler
flags:

  - In a Makefile.am for c++-programs
    
    1.  CXXFLAGS = -DLinux -Wall -ansi -pedantic
    2.  \#CXXFLAGS = -DLinux -Wall -ansi -pedantic -g
    3.  \#CXXFLAGS = -DLinux -Wall -ansi -pedantic -O3
    4.  \#CXXFLAGS = -DLinux -Wall -ansi -pedantic -g -pg

  - In a Makefile.am for c-programs
    
    1.  CFLAGS = -DLinux -Wall -ansi -pedantic
    2.  \#CFLAGS = -DLinux -Wall -ansi -pedantic -g
    3.  \#CFLAGS = -DLinux -Wall -ansi -pedantic -O3
    4.  \#CFLAGS = -DLinux -Wall -ansi -pedantic -g -pg

So, if you want to add debug infos, uncomment line 2 after having
commented line 1. If you want to add debug and profiling infos,
uncomment line 4 after having commented line 1. And if you want to use
optimized code, uncomment line 3 after having commented line 1.

### **(4.15) <span id="sh415">What if I want to import my newly generated project into a cvs or subversion repository or to use wildcards to commit and/or add files?</span>**

If you import a more or less elaborated project into a cvs repository,
you must pay attention not to import binary files as text and not to
import those files, which can be derivated from other files by using any
program. For CVS-repositories you should have a file �.cvsignore� in
each directory by which you can evoke cvs to ignore those derivatable
files. For Subversion-repositories you should have expanded the
svn:ignore-feature by those file-names and/or patterns which shall be
ignored. With gtgt it is not nescessary to do this by yourself:

Beginning with release 3.0.0 gtgt offers a shell script
�prepClearRepCommit.sh� which realizes the following aspects:

  - Using the command �make distclean� all libs, object-files and
    applications will be deleted (because they can be regenerated by the
    pair �./configure make�)
  - All files and links will be deleted which can be regenerated by
    calling �./reconf , autoconf, automake and ./configure�.
  - In all directories of the tarball the names of all regeneratable
    files and links and patterns for all libraries and object-files will
    be inserted into a file �.cvsignore�
  - In all directories which contain a subdirectory .svn (= which
    already are managed by subversion) the content of the generated
    .cvsignore-file will be inserted as content of the property
    �svn:ignore� (by using the command �svn propset svn:ignore -F
    .cvsignore .;�)

After having called �prepClearRepCommit.sh� you can therefore import,
commit or add files with wildcards without having to reflect which of
the files normally have to be ignored.

If you have generated a tarball being cleared by �prepClearRepCommit.sh�
you must type

  - �reconf�
  - �configure�
  - �make�

for getting back the erased files.

### **(4.16) <span id="sh416">What if I want to build a rpm-package on the base of my tarball?</span>**

Beginning with release 2.0.0 gtgt automatically generates a specfile
named �prj.spec�. Using the command �rpm -bb prj.spec� you will get that
rpm-package which contains the same files like the tarball generated
with �make distcheck� and extracted and installed with the commands
�configure --prefix=/usr/local && make && install�

For changing the spec-file see <http://www.rpm.org/>.

### **(5.A) <span id="c5A">What, if I need more informations?</span>**

you can find more hints inside of the tarball.

### **(5.B) <span id="c5B">What, if I want to add some remarks?</span>**

Feel free to contact <reincke@icdm.de> or at <karsten@fodina.de>. you
are strongly encoraged to correct, to suggest, to wish ...

For general informations have a look at <http://www.icdm.de/> and
<http://www.fodina.de/karsten/> too.

### **(6) <span id="c6">Thanks</span>**

It's a great pleasure for me to thank some people:

  - [Christian
    Heissing](mailto:christian.heissing@cl-ki.uni-osnabrueck.de) as
    first user and tester of the gitty-gitty-tools who has good eyes for
    finding improvable aspects
  - [Guido Sassmannshausen](mailto:sassi@sedan.uni-osnabrueck.de) as
    first reader of the documentation who worked hard to correct my
    english. (For any still existing fault I am responsible not he
    \!\!\!)
  - [Eleftherios
    Gkioulekas](http://www.amath.washington.edu/~lf/tutorials/autoconf/)
    as developper of the autotools which have been the basis of the
    gitty-gitty-tools.
  - [Ralph
    Schunk](http://gtgt.sourceforge.net/schunk@opal.biophys.uni-duesseldorf.de),
    who has pointed to the correct use of some new libtool macros.
  - My company [ICDM](http://www.icdm.de/) which formerly has used gtgt
    and has evoked some improvements
