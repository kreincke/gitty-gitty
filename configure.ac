#!/bin/sh
#
# Copyright (C) 2001-2009 karsten reincke <karsten.reincke@fodina.de>
#  
# This file is part of of the software-project GTGT.
# 
# GTGT is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
# 
# GTGT is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# 
# file <configure.in> version <#3.2.0#> of project <GTGT>

dnl process this file with autoconf to produce a configure script
dnl (1) -------- general startmacros
AC_INIT([gtgt],[4.0.0], reconf)
AM_INIT_AUTOMAKE([foreign])
AM_CONFIG_HEADER(config.h)
AC_PREFIX_DEFAULT(/usr/local/)
AC_PROG_MAKE_SET

dnl (2) -------- set of available languages

dnl (3) -------- checks for programs

AC_PROG_CC
AC_PROG_CPP
AC_AIX
AC_ISC_POSIX
AC_MINIX
AC_HEADER_STDC
AC_PROG_CXX
AC_PROG_CXXCPP

dnl (4) -------- checks for libraries
AC_PROG_LIBTOOL

dnl (5) -------- checks for header files
dnl (6) -------- checks for library-functions

dnl (7) -------- les autres petis choses
AC_PATH_PROGS(BASH, bash sh)

dnl (8) -------- determine whole directory-structure
AC_OUTPUT(Makefile doc/Makefile scripts/Makefile)
