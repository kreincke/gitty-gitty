# gtgt

- pronounced: ***gitty-gitty*** - stands for "General/Gnu Template Generation Tools": As three cooperating scripts *gtgt* instantiates a set of sources which are readily prepared for being developed, compiled, and installed by the GNU 'autoconf/automake' development environment.

If one uses the *autotools* then one can hardly use the GNU development tools for developing sources licensed under the terms of a NON-GNU-license. *gtgt* closes this gap: It shall enable the developers to use the GNU tools even if the result is licnsed under a NON-GNU-License.

## <a id="sh10" /> (1) Getting *gitty-gitty*

### <a id="sh11 /> 1.1. Prerequisites
With the help of your operating system / Linux distribution install the following tools:
  - bash
  - gcc development tools
  - autoconf
  - automake
  - libtools

### <a id="sh12" /> 1.2 Sources

There are two options to get *gtgt*: you can either clone the respective GItHub repository or you can download the corresponding [gtgt-tarball](https://github.com/kreincke/gitty-gitty)

### <a id="sh13" /> 1.3 Installation

1. **IF** you've downloaded the repository
  * **THEN** open a terminal, change into the repository directory and enter the command ``./reconf``.
  * **ELSE** open a terminal, extract the downloaded tarball and change into the *gtgt* directory
2. Insert the commands
  * ``./configure --prefix=YOUR_CHOICE``
  * ``make``
  * ``sudo make install``
3. Insert the command ``gptg --help``. If you do not get the help screen, check your PATH variable: "YOUR_CHOICE/bin" must be part of the paths

## <a id="sh2" />(2) Structure

*gtgt* is a set of three bash scripts, each with a specific task:

* ***gcng (= General Copyright Note Generator)*** generates files, which are instantiated by a copyright header.

* ***gscg (=General Source Code Generator)*** generates already compilable software modules, particularly the respective header file and the corresponding source file: You can select c or c++ as the programming-language. Think of gscg as a program, which is able to create very sophisticated "hello world" modules.

* ***gptg (=General Project Template Generator***) generates the whole set of files for an already compilable and installable software project: Using gscg + gcng, gptg instantiates and fills a project directory with the artifacts required by *autoconf* and *automake*. Think of gptg as a program which generates a quite sophisticated "hello world" program - being built upon two modules and one static library  and one shared library.

These three programs operate on a configuration file named ``gcng.conf`` which contains the following elements;

- The author-name
- The email address of the author
- The year of publishing the program (will be inserted automatically)
- The name of the company licensing the sources
- The absolute path to a short version of the company's license
- The absolute path to a long version of the company's license

If this file doesn't exist, you will be asked for the respective data and it will be created. If your company is GNU, you won't be asked for licenses, because they are known. If not, you have to create such licenses. They will be automatically used for generating the source code headers. Examples for those company licenses can be found in the *gtgt* documentation directory installed under ``$PREFIX/share/doc/gtgt``.


## <a id="sh30" /> (3) Usage

We think that use of *gitty-gitty* should preferably be described in form of a [FAQ](./FAQ.md).
