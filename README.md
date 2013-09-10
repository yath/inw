# NAME

inw -- inotifywait(1) wrapper

# SYNOPSIS

inw \[options and inotifywait arguments\]

# DESCRIPTION

_inw_ is a wrapper for _inotifywait_ (from [inotify-tools](https://github.com/rvoicilas/inotify-tools/wiki))
that waits for a given time after a file change for additional changes and returns if no changes
have been made for a specific amount of time.

This might be useful if you trigger e.g. [unison](http://www.cis.upenn.edu/~bcpierce/unison/) from a shell
script or incrond but don't want to synchronize on __every__ change but rather when nothing has been
written for like 5 seconds.

# OPTIONS

## NOTE

Options can't be be bundled, that is, you can't write _\-ABC 123_ for _\-A -B -C 123_. _\-ABC_ would
be recogized as _\-A BC_, that is _BC_ being an argument to _\-A_.

You can mix _inw_ options and _inotifywait_ arguments on the command line; everything unknown
to _inw_ will be passed to _inotifywait_.

- __\-T _NUM___

    Wait _NUM_ seconds after the last change to a file for other changes before returning.

- __\-M _NUM___

    Exit after _NUM_ seconds after the first change to a file, regardless of __\-T__. This is
    an overall timeout to prevent _inw_ from never returning if something changes a file
    continuously.

- __\-V__

    Be verbose.

- __\-N__

    Assume the first change to a file has already been done; just watch out for subsequent
    writes. Might be useful from within [incron](http://inotify.aiken.cz/?section=incron&page=about&lang=en).

# BUGS

Probably. Please report them to the [GitHub issue tracker](https://github.com/yath/inw/issues),
preferably with pull request :-).

# COPYRIGHT & LICENSE

Copyright 2013 Sebastian Schmidt <yath@yath.de>.

This program is free software; you can redistribute it and/or modify it under the terms of
the GNU General Public License version 2 (__not__ "any later" and __no__ different version) as
published by the Free Software Foundation.
