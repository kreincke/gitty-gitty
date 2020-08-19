# gtgt FAQ:


* [.) ](#)


## <a id="q001" /> **What's the purpose of 'gtgt'?**

**gtgt** - pronounced: ***gitty-gitty*** - stands for "General/Gnu Template Generation Tools": As three cooperating scripts *gtgt* instantiates a set of sources which are readily prepared for being developed, compiled, and installed by the GNU 'autoconf / automake' development environment.

If one uses the *autotools* then one can hardly use the GNU development tools for developing sources licensed under the terms of a NON-GNU-license. *gtgt* closes this gap: It shall enable the developers to use the GNU tools even if the result is licnsed under a NON-GNU-License.

## <a id="q002" /> **Which components requires 'gtgt'?**

For using *gtgt* you must have installed:
  - bash
  - gcc development tools
  - autoconf
  - automake
  - libtools

## <a id="q003" /> **Where can I get 'gtgt'?**

There are two options to get *gtgt*:
* You can either clone the respective GitHub repository using the command [https://github.com/kreincke/gitty-gitty.git](https://github.com/kreincke/gitty-gitty.git)
* Or you can download a tarball from [gtgt-tarball](https://github.com/kreincke/gitty-gitty)

## <a id="q004" /> **How can I install 'gtgt'?**

1. **IF** you've downloaded the repository
  * **THEN** open a terminal, change into the repository directory and enter the command ``./reconf``.
  * **ELSE** open a terminal, extract the downloaded tarball and change into the *gtgt* directory
2. Insert the commands
  * ``./configure --prefix=YOUR_CHOICE``
  * ``make``
  * ``sudo make install``
3. Insert the command ``gptg --help``. If you do not get the help screen, check your PATH variable: "YOUR_CHOICE/bin" must be part of the paths

## <a id="q005" /> **Which sub-tools offers 'gtgt'?**

*gtgt* is a set of three bash scripts, each with a specific task:

* ***gcng (= General Copyright Note Generator)*** generates files, which are instantiated by a copyright header.

* ***gscg (=General Source Code Generator)*** generates already compilable software modules, particularly the respective header file and the corresponding source file: You can select c or c++ as the programming-language. Think of gscg as a program, which is able to create very sophisticated "hello world" modules.

* ***gptg (=General Project Template Generator***) generates the whole set of files for an already compilable and installable software project: Using gscg + gcng, gptg instantiates and fills a project directory with the artifacts required by *autoconf* and *automake*. Think of gptg as a program which generates a quite sophisticated "hello world" program - being built upon two modules and one static library  and one shared library.

## <a id="q006" /> **How do I configure 'gtgt'?**

The three *gtgt*-scripts operate on a configuration file named ``gcng.conf`` which contains the following elements;

- The author-name
- The email address of the author
- The year of publishing the program (will be inserted automatically)
- The name of the company licensing the sources
- The absolute path to a short version of the company's license
- The absolute path to a long version of the company's license

If this file doesn't exist, you will be asked for the respective data and it will be created. If your company is GNU, you won't be asked for licenses, because they are known. If not, you have to create such licenses. They will be automatically used for generating the source code headers. Examples for those company licenses can be found in the *gtgt* documentation directory installed under ``$PREFIX/share/doc/gtgt``.


## <a id="q007" /> **How do I create my first project?**

1. Create a short project name like 'mypo', which does not contain blanks or other separators. Think of it as a name, not as a double name or sentence or anything else. Following the c/c++-coding-standard this name will automatically be changed in some cases: he can be capitalized or written in lower or upper cases.
2. Decide, whether you want to use C or C++ as a programming-language. (If you only want to write shell scripts, you may choose any of these.)
3. Decide with which main release number you want to begin. Usually you start with zero (select an integer like 1,2,3, not any real or float number like 1.2 and so on)
4. Decide with which revision number you want to begin. Usually you start with one (select an integer like 1,2,3, not any real or float number like 1.2 and so on)
5.  Type ``gptg --help`` to see in which way these decisions can be inserted into gptg:
```
OPTIONS  :-
   -h, --help       This message
   -v, --version    Version information
   -cpp             Language C++, uses the LF macros
   -c               Language C, uses traditional *autoconf* macros
PROJECT  :-         projectname [myproject]
RELEASE  :-         start-release-number [0]
REVISION :-         start-release-branch-number [1]
```

6. Create the *gcng.conf* cobfiguration files in xour working-directory. It ontains 6 lines:
- The author name
- The email address of the author
- The year of publishing the program (will be inserted automatically)
- The name of the company licensing the sources
- The absolute path to a short version of the company's license
- The absolute path to a long version of the company's license

If this file doesn't exist, you will be asked for the respective data and it will be created. If your company is GNU, you won't be asked for licenses, because they are known. If not, you have to create such licenses. They will be automatically used for generating the source code headers. Examples for those company licenses can be found in the gtgt documentation directory installed under $PREFIX/share/doc/gtgt.

7.  Insert the command ``user@computer> gptg -cpp mypo 0 1`` for getting a project named *mypo*, positioned in a directory *mypo-0.1*

8. Note: After having changed into your project directory, you can already type ``./configure``, ``make``, ``make distcheck``, or ``make install``. You get a project which
- at first installs one application named like your project and made of two modules and which
- at second installs two libraries, a static and a shared one.

You now have to adopt these options to your wishes and you can use this automatically generated project as a teaching example to handle *autoconf* and *configure.in*, *automake* and *Makefile.am* and *configure.in*. Because the sources are following the c/c++ coding standard and are already commented in the doxygen style, you can take them as teaching examples for these aspects, too.

## <a id="q008" /> **How do I license my project?**

GNU and its GPL is good. Very good, indeed. But sometimes it's not all. Therefore, for example, the LGPL has been created. Well, you should be able to create applications following the GNU methods and GNU recommendations and using the GNU tools - without publishing your results under the GPL. In these cases you might want to distribute your sources under a special 'company' license. And this license should be referred by all your files.

GNU uses the following way to mark the GNU sources as GNU sources:

1.  As part of the project directory, the GNU license is handed over to the recipient of the tarball. This license can be found in the file COPYING.
2.  Each source file contains a short version of this license by listing up the main points of the whole license and referring to file COPYING or the GPL
3.  Sometimes it's necessary to publish special parts of the tarball under a weaker license than the other parts. For example remember the LGPL: In these cases such (library-)sources contain a special hint.

Think of the company license as a special "GNU license" of your company. And therefore you should have two versions: The long version is that one, which shall be put into the file COPYING, and the short is that one, which will be used inside of the the files and which should refer to the long version.

The last question could be this: How can I determine, to create a template for my company or for the GNU world? the answer is very simple:

* If you insert the word GNU in the fourth line of the gcng.conf file, line 5 and 6 will be ignored and the normal GNU licenses will be inserted for case (1) and (2) of the above mentioned list.
* If you insert a different word than GNU in the fourth line of
gcng.conf, line 5 and 6 will be evaluated as absolute paths of your company license files: line 5 as path of the abbreviated version, line 6 as path of the long version.

The gtgt-tarball offers two license examples inside the doc-directory: the file "company-license.long" and the file "company-license.short". Note: They haven't been legally checked! They exist for demonstrating the technical possibilities.

## <a id="q009" /> **What if I want to build my tarball with more or other source files than instantiated by the *gptg* script?**

Very simple, in the first part of the following chapters, we explain what you should do, if you don't want to use the full set of files. And in the second part we explain, what you need to do, if you want to expand set files.

## <a id="q010" /> **What if I don't want to write libraries?**<a id="dellib" />

Read ${YOURPRJ} as a name of your project:

1. Change into the top-directory of your project
2. Delete the sub-string 'lib/Makefile' as parameter of the macro AC_OUTPUT in the file 'configure.in'
3. Delete the directory 'lib'
4. Delete the sub-string 'lib' as parameter of the macro SUBDIRS in the file 'Makefile.am'
5. Change into the sub directory src of your project directory
  * Delete the sub-string '-l ${YOURPRJ}_stli' as parameter of the macro ${YOURPRJ}_LDADD in the file 'Makefile.am'
  * Delete the sub-string '-L$(topbuilddir)/lib' as parameter of the macro ${YOURPRJ}_LDFLAGS in the file 'Makefile.am'
6. Delete all lines containing the sub-string '_stli' in the source-files ${YOURPRJ}.c(pp)
7. Change back into the top-directory and call *autoconf* and *automake* or call the *reconf*-script

## <a id="q011" /> **What if I don't want to work with deeply embedded daughter modules?**

1. Change into the top-directory of your project
2. Delete the sub-string 'src/damo/Makefile' as parameter of the macro AC_OUTPUT in the file 'configure.in'
3. Change into the sub-directory src of your project-directory
4. Delete the sub-string 'damo' as parameter of the macro SUBDIRS in the file 'Makefile.am'
5. Delete all lines containing the sub-string 'damo' in the source-files ${YOURPRJ}.c(pp)
6. Delete the directory 'damo' in your src-directory
7. Change back into the top-directory and call *autoconf* and *automake* or call the *reconf*-script

## <a id="q011" /> **What if I only want to offer a set of scripts?**

1. [Delete the libraries](#dellib) like described above.
2. Change into the top-directory of your project
3. Delete the sub-string 'src/Makefile' and 'src/damo/Makefile' as parameter of the macro AC_OUTPUT in the file 'configure.in'
4. Delete sub-directory 'src' of your project directory
5. Delete the sub-string 'src' as parameter of the macro SUBDIRS in the file 'Makefile.am'
6. Change back into the top-directory and call *autoconf* and *automake* or call the *reconf*-script

## <a id="q012" /> **What if I want to add a new sister module or class?**

Sister modules are sources with a declaring *header-file* and a defining *source-file* and lay in the same directory as the main *source-file*. For generating such a module do this:

1.  Change into the sub directory *src* of your project directory
2.  Call *gscg* and insert the parameters in accordance to this help extract:

```
gscg <-c|-cpp|-h|-v> [-i|-s|-is] [MODULE] [PROJECT] [RELEASE]

 -c             module will be written in C
 -cpp           module will be written in C++
 --help -h      this screen
 --version -v   version and license

 -i             write include-code for the module
 -s             write source-code for the module
 -is            write both, the include- + source-code as file

MODULE          should be a short module-identifier without
                brackets, underlines, points etc. etc.

PROJECT         should be a short project-identifier without
                brackets, underlines, points etc. etc.

RELEASE         release-number
```
example: ** ***gscg -cpp -is modu mypo 1.0*** creates mypo.h and mypo.cpp

3. Include ${MODULENAME}.cpp and ${MODULENAME}.h in Makefile.am as arguments of ${YOURPROJECT}_SOURCES

4. Change back into the top-directory and call *autoconf* and *automake* or call the *reconf*-script

5.  Then write and include your module / class

## <a id="q013" /> **(What, if I want to add a new module or class for libraries?**

Nearly the same as for adding a new sister module. But act in the
library directory instead of the source directory.

## <a id="q014" /> **What, if I want to create a new library ?**

Nearly the same as for adding a new sister module. After having determined the library name (=module name) you need to insert the following information into the Makefile.am of your lib-directory:
* lib_LIBRARIES=lib${modulename}.a
* lib${modulename}_a_sources= $your-sources
* Don't forget to insert the new library name in src/Makefile under ${YOURPROJECT}_LDADD as a string starting with -L

## <a id="q015" /> **What, if I want to add doc files or scripts ?**

* Move the scripts and documentation files into the director doc respectively scripts
* Change into the sub-directory doc resp. scripts of your project directory
* Add the filenames of the new scripts to the variable EXTRA_DIST of Makefile.am . In case of shell-scripts, add the name also to the variable bin_SCRIPTS and to CLEANFILES and insert any makefile target for those scripts.

## <a id="q016" /> **What, if I want use VPATH ?**

The VPATH variable allows us to use other directories whose content is able to fulfill the dependencies although it's not directly integrated into the 'make' procedure. Using this variable, one can split the object-files and its sources:

1. Change into the top of your project directory
2. Rename the sub-directory src into vpdir (or anything else)
3. Rename all those sub-strings 'src' into vpdir, which arise as
    contents of the variable SUBDIRS in the main Makefile.am
4. Insert a new sub-string src into the content of the variable SUBDIRS in the main Makefile.am
5.  Create a new sub-directory src
6.  Move all sources *.cpp \*.c \*.h from vpdir into the new directory src
7.  Change into the new src directory
8.  Edit a new src/Makefile.am
9.  Insert into this src/Makefile.am the only variable EXTRA_DIST=$all-names-of-your-moved-sources
10. Insert into each Makefile.am arising in any directory under vpdir or lib the string VPATH=$(top\_srcdir)/src.

The main point of this procedure is this: make recursively follows the structure of vpdir. There make meets its targets. And it seeks the sources, named inside of the Makefile and not really being in the make directory. But make finds them none-the-less, because it looks for them in all directories named by the variable VPATH which in this case is indicating the directory source as an add-on

##  <a id="q017" /> **What about the coding and documentation style?**

Last but not least, we have added the doxygen documentation style into the automatically generated source-files of your project initially created by the gitty-gitty-tools. This includes that

* the corresponding default doxygen configuration file (named Doxyconf) will automatically be generated inside of the project-directory
* all pieces of sourcecode are already be commented in the doxygen style
* the initial version of corresponding doxygen sourcecode documentation will be automatically generated while creating the initial version of your project
* the whole sourcecode doxygen documentation of the initial-version of your project can be found under doc/doxygen/

For being generally acceptable, we have adopted the c++ and c coding standard. But note: There doesn't exist "**the** coding standard"; you can find more than one which differ in more or less details. Therefore we give only one hint for a [C++ Coding
Standard](http://www.possibility.com/Cpp/CppCodingStandard.html) while recommending to have a look at the others, being found with some search engine.

## <a id="q018" /> **What if I want to change the numbers of the release or the revision?**

Last but not least we have integrated a script into the GNU-source-tree which allows the change of the release- and the revision-number.

Remember, if you let create the template of your project you have to name integers for the release and the revision on the command-line. these numbers will be merged into many places: for example into the short copyright line of each piece of source-code where the name of the file and that of the project is also announced.

But there exist more important places where these numbers are inserted. There they will be evaluated for generating the tarball-number or the library-version. For updating all these case with one command **gptg** writes a script into your project-directory. This script named ***change-release*** does what its name announces: it should be called with one or more file- or directory-names (or with \*) as parameter. and for all these entities it recursively changes all relevant release/revision numbers.

For using this script you have to respect the following points:

1.  You shouldn't change the release/revision-strings manually. or at least you have to respect the given syntactically structure.
2.  If you want to increment (decrement ?-) ) the revison/release-number you have to edit the script ***change-release***: insert the correct old versions of the numbers and the wished new versions at the beginning of the script and then call *./change-release*
3.  Note, ***change-release*** isn't backward compatible. if you want to use it in an existing project (made by GTGT release 1.1 or earlier) you have to recreate it. and if you merge older pieces of source-code into that new tree you have at least to replace the short-copy-right line which signals filename, project and version-number

Note: In the string "-version-info xc:xr:xa" , which arises in the *Makefile.am* and is updated by the script *changerelease*, the integer at the position *xc* means *current release*, the integer at the position *xr* *revision* and the integer at the position *xa* the *age* of the library. And the age of a library denotes the row of elder releases, which interfaces all only are expanded by the newer ones.

But this row of integers "xc:xr:xa" arises not directly in the version of a shared library. You have to read such version-numbers like the scheme *libxxx-so.xc.xa.xr*: the first integer of a library-version number denotes the current release, the second the age(\!) and the third the the revision number.

## <a id="q019" /> **What if I want to add debugging and profiling information during the compilation?**

In each Makefile.am *gtgt* offers four different lines with compiler flags:

* In a Makefile.am for c++-programs
  1. CXXFLAGS = -DLinux -Wall -ansi -pedantic
  2. \#CXXFLAGS = -DLinux -Wall -ansi -pedantic -g
  3. \#CXXFLAGS = -DLinux -Wall -ansi -pedantic -O3
  4. \#CXXFLAGS = -DLinux -Wall -ansi -pedantic -g -pg

* In a Makefile.am for c-programs
  1. CFLAGS = -DLinux -Wall -ansi -pedantic
  2. \#CFLAGS = -DLinux -Wall -ansi -pedantic -g
  3. \#CFLAGS = -DLinux -Wall -ansi -pedantic -O3
  4. \#CFLAGS = -DLinux -Wall -ansi -pedantic -g -pg

So, if you want to add debug info, uncomment line 2 after having
commented line 1. If you want to add debug and profiling info,
uncomment line 4 after having commented line 1. And if you want to use optimized code, uncomment line 3 after having commented line 1.

## <a id="q020" /> **What if I want to import my newly generated project into a repository or to use wildcards to commit and/or add files?**

If you import a more or less elaborated project into a repository, you should not import binary files and not files, which can be derived from other files by using any program. *gtgt* supports the clearing of your working directory by gathering the necessary commands in a specific script *prepClearRepCommit.sh*:

* By using the command``make distclean`` , *prepClearRepCommit.sh* deletes all libs, object-files and applications generated by ``make``
* Additionally it deletes all files and links which can be regenerated by calling ``./reconf`` , ``autoconf``, ``automake`` and ``./configure``.
* Finally it gathers the names of all reclaimable files and links and patterns for all libraries and object-files in all directories of the tarball into a respective *.gitignore* file.

After having called *prepClearRepCommit.sh* you can therefore import, commit or add files with wildcards without having to reflect which of themselves files should not be committed. For getting back the files erased by *prepClearRepCommit.sh* insert the commands ``reconf``, ``configure`` and ``make``


## <a id="q020" /> **What if I want to build a rpm-package on the base of my tarball?**

Beginning with release 2.0.0 gtgt automatically generates a specfile named ``prj.spec``. Using the command ``rpm -bb prj.spec`` you will get the rpm-package containing the same files like the tarball generated by the commands
* ``make distcheck``
* ``configure  --prefix=/usr/local && make && install``

For changing the spec-file see <http://www.rpm.org/>.

## <a id="q021" /> **Under which conditions gtgt is licensed?**

## <a id="q022" /> **How can I give feedback?**

Feel free to use the GitHub methods or directly to write to  [k.reincke@fodina.de](mailto://k.reincke@fodina.de]). You are strongly encouraged to correct, to suggest, to wish ... For further information have a look at [www.fodina.de](http://www.fodina.de)
