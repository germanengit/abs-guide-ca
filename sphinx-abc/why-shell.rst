.. XXX TODO: translate me

####################################
Capítol 1. Perquè programar en Shell
####################################

    *No programming language is perfect. There is not even a single best
    language; there are only languages well suited or perhaps poorly suited
    for particular purposes.*

    -- Herbert Mayer

A working knowledge of shell scripting is essential to anyone wishing to
become reasonably proficient at system administration, even if they do
not anticipate ever having to actually write a script. Consider that as
a Linux machine boots up, it executes the shell scripts in ``/etc/rc.d``
to restore the system configuration and set up services. A detailed
understanding of these startup scripts is important for analyzing the
behavior of a system, and possibly modifying it.

The craft of scripting is not hard to master, since the scripts can be
built in bite-sized sections and there is only a fairly small set of
shell-specific operators and options [#why-shell]_ `[1] <why-shell.html#FTN.AEN60>`_
to learn. The syntax is simple -- even austere -- similar to that of
invoking and chaining together utilities at the command line, and there
are only a few "rules" governing their use. Most short scripts work
right the first time, and debugging even the longer ones is
straightforward.

    In the 1970s, the BASIC language enabled anyone reasonably
     computer proficient to write programs on an early generation of
     microcomputers. Decades later, the Bash scripting language enables
     anyone with a rudimentary knowledge of Linux or UNIX to do the same
     on much more powerful machines.

A shell script is a quick-and-dirty method of prototyping a complex
application. Getting even a limited subset of the functionality to work
in a script is often a useful first stage in project development. In
this way, the structure of the application can be tested and tinkered
with, and the major pitfalls found before proceeding to the final coding
in *C*, *C++*, *Java*, `Perl <wrapper.html#PERLREF>`_, or *Python*.

Shell scripting hearkens back to the classic UNIX philosophy of breaking
complex projects into simpler subtasks, of chaining together components
and utilities. Many consider this a better, or at least more
esthetically pleasing approach to problem solving than using one of the
new generation of high powered all-in-one languages, such as *Perl*,
which attempt to be all things to all people, but at the cost of forcing
you to alter your thinking processes to fit the tool.

According to `Herbert Mayer <biblio.html#MAYERREF>`_, "a useful language
needs arrays, pointers, and a generic mechanism for building data
structures." By these criteria, shell scripting falls somewhat short of
being "useful." Or, perhaps not. . . .

When not to use shell scripts

-  Resource-intensive tasks, especially where speed is a factor
   (sorting, hashing, recursion `[2] <why-shell.html#FTN.AEN84>`_ ...)

-  Procedures involving heavy-duty math operations, especially floating
   point arithmetic, arbitrary precision calculations, or complex
   numbers (use *C++* or *FORTRAN* instead)

-  Cross-platform portability required (use *C* or *Java* instead)

-  Complex applications, where structured programming is a necessity
   (type-checking of variables, function prototypes, etc.)

-  Mission-critical applications upon which you are betting the future
   of the company

-  Situations where *security* is important, where you need to guarantee
   the integrity of your system and protect against intrusion, cracking,
   and vandalism

-  Project consists of subcomponents with interlocking dependencies

-  Extensive file operations required (*Bash* is limited to serial file
   access, and that only in a particularly clumsy and inefficient
   line-by-line fashion.)

-  Need native support for multi-dimensional arrays

-  Need data structures, such as linked lists or trees

-  Need to generate / manipulate graphics or GUIs

-  Need direct access to system hardware or external peripherals

-  Need port or `socket <devref1.html#SOCKETREF>`_ I/O

-  Need to use libraries or interface with legacy code

-  Proprietary, closed-source applications (Shell scripts put the source
   code right out in the open for all the world to see.)

If any of the above applies, consider a more powerful scripting language
-- perhaps *Perl*, *Tcl*, *Python*, *Ruby* -- or possibly a compiled
language such as *C*, *C++*, or *Java*. Even then, prototyping the
application as a shell script might still be a useful development step.

We will be using Bash, an acronym `[3] <why-shell.html#FTN.AEN136>`_ for
"Bourne-Again shell" and a pun on Stephen Bourne's now classic *Bourne*
shell. Bash has become a *de facto* standard for shell scripting on most
flavors of UNIX. Most of the principles this book covers apply equally
well to scripting with other shells, such as the *Korn Shell*, from
which Bash derives some of its features,
`[4] <why-shell.html#FTN.AEN143>`_ and the *C Shell* and its variants.
(Note that *C Shell* programming is not recommended due to certain
inherent problems, as pointed out in an October, 1993 `Usenet
post <http://www.faqs.org/faqs/unix-faq/shell/csh-whynot/>`_ by Tom
Christiansen.)

What follows is a tutorial on shell scripting. It relies heavily on
examples to illustrate various features of the shell. The example
scripts work -- they've been tested, insofar as possible -- and some of
them are even useful in real life. The reader can play with the actual
working code of the examples in the source archive (``scriptname.sh`` or
``scriptname.bash``), `[5] <why-shell.html#FTN.AEN153>`_ give them
*execute* permission (``chmod u+rx scriptname``), then run them to see
what happens. Should the `source
archive <http://bash.deta.in/abs-guide-latest.tar.bz2>`_ not be
available, then cut-and-paste from the
`HTML <http://www.tldp.org/LDP/abs/abs-guide.html.tar.gz>`_ or
`pdf <http://bash.deta.in/abs-guide.pdf>`_ rendered versions. Be aware
that some of the scripts presented here introduce features before they
are explained, and this may require the reader to temporarily skip ahead
for enlightenment.

Unless otherwise noted, `the author <mailto:thegrendel.abs@gmail.com>`_
of this book wrote the example scripts that follow.

    *His countenance was bold and bashed not.*

    -- Edmund Spenser

Notes
=====

.. [#why-shell] These are referred to as builtins features internal to
   the shell.


`[2] <why-shell.html#AEN84>`_

Although `recursion *is* possible in a shell
script <localvar.html#RECURSIONREF0>`_, it tends to be slow and its
implementation is often an `ugly kludge <recurnolocvar.html#FIBOREF>`_.

`[3] <why-shell.html#AEN136>`_

An *acronym* is a word formed by pasting together the initial letters of
the words into a tongue-tripping phrase. This is a pernicious and
subversive practice that surely deserves appropriately severe
punishment.

`[4] <why-shell.html#AEN143>`_

Many of the features of *ksh88*, and even a few from the updated *ksh93*
have been merged into Bash.

`[5] <why-shell.html#AEN153>`_

By convention, user-written shell scripts that are Bourne shell
compliant generally take a name with a ``.sh`` extension. System
scripts, such as those found in ``/etc/rc.d``, do not necessarily
conform to this nomenclature.

