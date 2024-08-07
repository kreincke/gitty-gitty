<!--
Copyright (C) 2020 Karsten Reincke (Hohenahr, Germany), Deutsche Telekom AG
-------------------------------------------------------
This file is part of of the software-project GTGT.

GTGT is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

GTGT is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.
Please see the file COPYING for details.
-------------------------------------------------------
# file <change-release> version <#4.0.0#> of project <GTGT>
-->
![gitty-gitty logo](doc/gtgt.gif)

 ***gtgt*** - (pronounced ***gitty-gitty***) - stands for "General/Gnu Template Generation Tools": As three cooperating scripts, *gtgt* instantiates a set of sources which are readily prepared for being developed, compiled, and installed by the GNU 'autoconf/automake' development environment.

If one uses the *autotools*, one can hardly use the GNU development tools to create software licensed under the terms of a NON-GNU-license. *gtgt* closes this gap: It shall enable the developers to use the GNU tools even if the result is licensed under a NON-GNU-License.

The current release is [<#4.0.0#>](https://github.com/kreincke/gitty-gitty/tree/releases)

* [Getting *gitty-gitty*](#p10)
* [The Structure of *gitty-gitty*](#p20)
* Usage -> [FAQ](./FAQ.md)
* [The License of *gitty-gitty*](#p40)


## <a id="p10" />Getting *gitty-gitty*

### <a id="p11" />- Prerequisites
With the help of your operating system / Linux distribution install the following tools:
  - bash
  - gcc development tools
  - autoconf
  - automake
  - libtools
  - doxygen
  - graphviz

### <a id="p12" />- Sources

You have two options to get *gtgt*:
* you can either clone its GitHub repository by using the command ``git clone https://github.com/kreincke/gitty-gitty.git``
* or you can download the corresponding [gtgt-release-branch](https://github.com/kreincke/gitty-gitty/tree/releases)

### <a id="p13" />- Installation

1. **IF** you've downloaded the repository
  * **THEN** open a terminal, change into the repository directory and enter the command ``./reconf``.
  * **ELSE** open a terminal, extract the downloaded tarball and change into the *gtgt* directory
2. Insert the commands
  * ``./configure --prefix=YOUR_CHOICE``
  * ``make``
  * ``sudo make install``
3. Insert the command ``gptg --help``. If you do not get the help screen, check your PATH variable: "YOUR_CHOICE/bin" must be part of the paths

## <a id="p20" />Script-Structure

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


## <a id="p30" />Usage -> [FAQ](./FAQ.md)

## <a id="p40" />License

(c) 2020 Karsten Reincke, Deutsche Telekom: *gitty-gitty* is licensed under the GNU General Public License 3.0

Due to the fact, that *gtgt* is a code generator and that its sub scripts contain code (which is copied into the generated sources), one can conclude that the files generated by *gtgt* are a derivative work of *gtgt* itself and that the copyleft effect of the GPL-v3 is triggered. **That is not intended by** ***gitty-gitty***: We explicitly state that the code generated by *gtgt* and its components is not covered by the copyleft effect and can be published under any open or closed source license.
