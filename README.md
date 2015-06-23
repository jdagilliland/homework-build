This is a skeleton homework project using:
- [LaTeX](http://www.latex-project.org)
  - tikz (coming soon)
- [python](http://www.python.org)
  - [numpy](http://www.numpy.org)
  - [matplotlib](http://matplotlib.org)
- [pygments](http://pygments.org)
- [SCons](http://www.scons.org)

It incorporates a [LaTeX style file](jdaghw.sty) that provides many of the
useful packages
and some custom macros that one might frequently use as well as a nice style
for homework which I adapted from a source on Github.
Besides that, it uses [custom SCons builders](SConstruct) to create figures
using python
and matplotlib, it also uses pygments to create lovely source code
listings.
There is also a [SCons builder](SConstruct) for an archive that includes all
of the
compiled images and pygmentized source code listings, for the benefit of
anyone not using SCons to build the homework you so put together who still
wants to see or modify the source.

The [gitignore](.gitignore) has most of the general file types listed that
you would want
to ignore, including the cruft from LaTeX, python, SCons, and LibreOffice
(in case you are using it to view compiled csv tables).

The general idea is to put any kind of source that is not the main
LaTeX source in the `src/` directory, and then in the
[SConstruct](SConstruct) put the
built images, etc. (anything you do not want git to see) in the `build/`
directory.
