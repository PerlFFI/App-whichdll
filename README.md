# whichdll ![linux](https://github.com/PerlFFI/App-whichdll/workflows/linux/badge.svg)

Find dynamic libraries in the appropriate path

# SYNOPSIS

```
$ whichdll xml2
$ whichdll -a xml2  # print all matches
$ whichdll -a \*    # print all DLLs
$ whichdll -s xml2  # silent mode
```

# DESCRIPTION

`whichdll` is a command line interface to [FFI::CheckLib](https://metacpan.org/pod/FFI::CheckLib).  It can be helpful in determining the location of
dynamic libraries installed on your system.  Its primary purpose is to be used in debugging issues related to
[FFI::CheckLib](https://metacpan.org/pod/FFI::CheckLib), or [FFI::Platypus](https://metacpan.org/pod/FFI::Platypus).  The command takes one or more arguments, which are treated as library
names.  The `whichdll` script will find the platform specific names in the appropriate places if they can
be found in the system path.  Thus when you search for `foo` you will get a result like `libfoo.so.1.2.3` on
Linux, `foo.dll` on Windows, `libfoo.dylib` or `foo.bundle` on OS X, `cygfoo-1.0.dll` on Cygwin, etc., with
the appropriate full path.

By default duplicates due to duplicate paths or symlinks will be removed.  You can see them using the `-x`
option.  For example on Debian:

```perl
$ ./bin/whichdll -a xml2
/usr/lib/x86_64-linux-gnu/libxml2.so.2.9.4
$ ./bin/whichdll -a -x xml2
/usr/lib/x86_64-linux-gnu/libxml2.so.2.9.4
/usr/lib/x86_64-linux-gnu/libxml2.so => /usr/lib/x86_64-linux-gnu/libxml2.so.2.9.4
/usr/lib/x86_64-linux-gnu/libxml2.so.2 => /usr/lib/x86_64-linux-gnu/libxml2.so.2.9.4
```

You can use the wildcard `*` to print all libraries.  This implies the `-a` option.

# OPTIONS

## -a

Print all matches instead of just the first one.

## -s

No output, just return 0 if any of the DLLs are found, or 1 if none are found.

## -v

Prints version and copyright notice and exits.

## -x

Do not prune duplicates.

# AUTHOR

Graham Ollis <plicease@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2018-2022 by Graham Ollis.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
