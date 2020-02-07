---
section: 11
x-masysma-name: ma_sitecopy
title: SiteCopy Low-Level Wrapper Script
date: 2020/02/07 21:43:19
lang: en-US
author: ["Linux-Fan, Ma_Sys.ma (Ma_Sys.ma@web.de)"]
keywords: ["scripts", "d5man", "sitecopy", "linux", "ftp"]
x-masysma-version: 1.0.0
x-masysma-repository: https://www.github.com/m7a/lp-ma-sitecopy
x-masysma-website: https://masysma.lima-city.de/11/ma_sitecopy.xhtml
x-masysma-owned: 1
x-masysma-copyright: |
  Copyright (c) 2014, 2020 Ma_Sys.ma.
  For further info send an e-mail to Ma_Sys.ma@web.de.
---
Name
====

`ma_sitecopy` -- SiteCopy Low-Level Wrapper Script

Synopsis
========

	ma_sitecopy -mu USER -ms SERVER -md DIR [-mr REMOTE-DIR] [-mt STATE]
							[-so "K V"] [--] [SCO]

Description
===========

This script wraps around the `sitecopy` command in order to provide a
configuration-file-less interface to said command. The script generates a
temporary configuration file, invokes `sitecopy` and deletes the temporary
configuration afterwards.

As a low-level wrapper, it does not work around the differences of INIT and
UPDATE operations. To allow INITs, it provides a means to add user-specified
options directly to the `sitecopy` invocation s. t. an INIT operation can
be performed.

This was originally developed as part of
[d5man/legacy(32)](../32/d5man_legacy.xhtml) for uploading exported websites.
It still does this job, but for separation of concerns is not included in the
new [d5man2(32)](../32/d5man2.xhtml) repository.

`ma_sitecopy` is intended to be part of an interactive upload workflow and thus
asks for a password to be provided via stdin. For automation, the password can
of course also be supplied through a pipeline.

Options
=======

----- ----------  ------------------------------------------------
`-mu` USER        login username
`-ms` SERVER      server address
`-md` DIR         local source directory
`-mr` REMOTE-DIR  remote destination directory
`-mt` STATE       local state file
`-so` K V         any number of site rcfile options
`--`              marks end of options for this wrapper script
`SCO`             any number and format of direct sitecopy-options
----- ----------  ------------------------------------------------

Examples
========

## Example for first-time invocation (INIT)

	ma_sitecopy -mu masysma -ms masysma.lima-ftp.de -md ".../mawebsite5" \
		-mr html -mt ".../sitecopy_state.xml" -so "state checksum" -- -i

## Example for subsequent invocation (UPDATE)

	ma_sitecopy -mu masysma -ms masysma.lima-ftp.de -md ".../mawebsite5" \
		-mr html -mt ".../sitecopy_state.xml" -so "state checksum" -- -u

See Also
========

[sitecopy(1)](https://manpages.debian.org/buster/sitecopy/sitecopy.1.en.html)
