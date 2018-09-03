[![Linux Build Status](https://img.shields.io/travis/com/smudgelang/smudge.svg?label=Linux%20build)](https://travis-ci.com/smudgelang/smudge)
[![Windows Build Status](https://img.shields.io/appveyor/ci/smudgelang/smudge.svg?label=Windows%20build)](https://ci.appveyor.com/project/smudgelang/smudge)

# The Smudge Programming Language

Smudge is a domain specific language for implementing state
machines. The compiler generates standard C code as well as graphical
state diagrams. Its output is optimized for use on very limited
embedded systems, but designed to be used anywhere state machines are
appropriate. Here's a simple example to show you what the language
looks like:

## first.smudge

    SM_NAME
    {
        *FIRST_STATE (@enterFirst)
        [
            event --> SECOND_STATE,
            altEvent -(@sideEffect)-,
            reenter --> FIRST_STATE
        ] (@exitFirst),
    
        SECOND_STATE
        [
            _ -(@sideEffect)-> FIRST_STATE
        ]
    }

## Getting Smudge

### Binaries

There are binary releases available for Windows and Linux available on
the
[Smudge releases page](https://github.com/smudgelang/smudge/releases). The
latest release includes a pdf of the tutorial, which is a great place
to start learning Smudge.

### Building From Source

First, make sure you have `ghc` installed, along with
`haskell-stack`. In order to build the documentation, you'll also need
`rst2pdf` and `pdflatex`.

Then, in your shell of choice, run:

    $ make

The first time you build, it might tell you to run

    $ stack setup

This may take a bit, as stack will have to download and configure the
build environment.

This should work on Windows under Cygwin, as well as reasonably recent
versions of Debian (with [issues](https://github.com/commercialhaskell/stack/blob/master/doc/faq.md#i-get-strange-ld-errors-about-recompiling-with--fpic)) and Ubuntu. It has worked on other distros and
MacOS, and if you have trouble getting it to build we encourage you to
ask for help on [gitter](https://gitter.im/smudge-sm/Lobby). It
generates an executable called `smudge` (or `smudge.exe` on Windows) that
you can use to compile Smudge code by running `stack exec smudge`.

## How to Use Smudge

Once you have Smudge installed, either because you built it from
source or downloaded a release, the best way to learn how to use it is
to look at the tutorial. It's in the release tarball and it's built as
part of the normal build process in
`docs/tutorial/tutorial.pdf`. Here's the quick version for the
impatient though.

### Prerequisites

First, make sure you have `graphviz` installed. It should be available
through your package manager on Linux, through
[homebrew](https://brew.sh/) on MacOS, or within
[cygwin](https://www.cygwin.com/) on Windows. If you're running on
Windows, we strongly suggest that you use Cygwin.

### Running

    $ smudge --dot-fmt=Svg first.smudge
    Wrote file "first.svg"
    Wrote file "first.h"
    Wrote file "first.c"
    Wrote file "first_ext.h"

This generates 4 files. The `.svg` file is just an image with a
diagram of your state machine. The `.h` file is the interface to the
code generated by Smudge, and the `_ext.h` file contains generated
prototypes for functions you must provide.

## There's more!

Further example state machines can be found in the examples
directory. In particular, first.smudge is the state machine shown
above but with extensive comments to describe what it's doing.

There's also a [gitter](https://gitter.im/smudge-sm/Lobby) if you need
help or want to communicate with the contributors.

## License

Smudge is released under a standard BSD 3-clause license, found in
LICENSE file.
