######################################
XXX  16.5. File and Archiving Commands
######################################


** Archiving**

 **tar**
    The standard UNIX archiving utility. ` [1]
     <filearchiv.html#FTN.AEN11885>`__ Originally a *Tape ARchiving*
    program, it has developed into a general purpose package that can
    handle all manner of archiving with all types of destination
    devices, ranging from tape drives to regular files to even
    ``         stdout        `` (see `Example
    3-4 <special-chars.html#EX58>`__ ). GNU *tar* has been patched to
    accept various compression filters, for example: **tar czvf
    archive\_name.tar.gz \*** , which recursively archives and
    `gzips <filearchiv.html#GZIPREF>`__ all files in a directory tree
    except `dotfiles <basic.html#DOTFILESREF>`__ in the current working
    directory ( `$PWD <internalvariables.html#PWDREF>`__ ). ` [2]
     <filearchiv.html#FTN.AEN11896>`__

    Some useful **tar** options:

    #. ``           -c          `` create (a new archive)

    #. ``           -x          `` extract (files from existing archive)

    #. ``           --delete          `` delete (files from existing
       archive)

       .. raw:: html

          <div class="CAUTION">

       .. raw:: html

          <div>

       |Caution|

       This option will not work on magnetic tape devices.

       .. raw:: html

          </p>

       .. raw:: html

          </div>

       .. raw:: html

          </div>

    #. ``           -r          `` append (files to existing archive)

    #. ``           -A          `` append ( *tar* files to existing
       archive)

    #. ``           -t          `` list (contents of existing archive)

    #. ``           -u          `` update archive

    #. ``           -d          `` compare archive with specified
       filesystem

    #. ``           --after-date          `` only process files with a
       date stamp *after* specified date

    #. ``           -z          `` `gzip <filearchiv.html#GZIPREF>`__
       the archive

       (compress or uncompress, depending on whether combined with the
       ``           -c          `` or ``           -x          `` )
       option

    #. ``           -j          `` `bzip2 <filearchiv.html#BZIPREF>`__
       the archive

    .. raw:: html

       <div class="CAUTION">

    .. raw:: html

       <div>

    |Caution|

    It may be difficult to recover data from a corrupted *gzipped* tar
    archive. When archiving important files, make multiple backups.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

 **shar**
    *Shell archiving* utility. The text and/or binary files in a shell
    archive are concatenated without compression, and the resultant
    archive is essentially a shell script, complete with #!/bin/sh
    header, containing all the necessary unarchiving commands, as well
    as the files themselves. Unprintable binary characters in the target
    file(s) are converted to printable ASCII characters in the output
    *shar* file. *Shar archives* still show up in Usenet newsgroups, but
    otherwise **shar** has been replaced by **tar** / **gzip** . The
    **unshar** command unpacks *shar* archives.

    The **mailshar** command is a Bash script that uses **shar** to
    concatenate multiple files into a single one for e-mailing. This
    script supports compression and
    `uuencoding <filearchiv.html#UUENCODEREF>`__ .

 **ar**
    Creation and manipulation utility for archives, mainly used for
    binary object file libraries.

 **rpm**
    The *Red Hat Package Manager* , or **rpm** utility provides a
    wrapper for source or binary archives. It includes commands for
    installing and checking the integrity of packages, among other
    things.

    A simple **rpm -i package\_name.rpm** usually suffices to install a
    package, though there are many more options available.

    .. raw:: html

       <div class="TIP">

    .. raw:: html

       <div>

    |Tip|

    ``                         rpm -qf                       ``
    identifies which package a file originates from.

    | .. code:: SCREEN         |
    |                          |
    |     bash$ rpm -qf /bin/l |
    | s                        |
    |     coreutils-5.2.1-31   |
    |                          |
                              

    .. raw:: html

       </p>

    .. code:: SCREEN

        bash$ rpm -qf /bin/ls
        coreutils-5.2.1-31
                  

    .. raw:: html

       </p>

    .. code:: SCREEN

        bash$ rpm -qf /bin/ls
        coreutils-5.2.1-31
                  

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

    .. raw:: html

       <div class="TIP">

    .. raw:: html

       <div>

    |Tip|

    ``                         rpm -qa                       `` gives a
    complete list of all installed *rpm* packages on a given system. An
    ``                         rpm -qa package_name                       ``
    lists only the package(s) corresponding to
    ``            package_name           `` .

    | .. code:: SCREEN         |
    |                          |
    |     bash$ rpm -qa        |
    |     redhat-logos-1.1.3-1 |
    |      glibc-2.2.4-13      |
    |      cracklib-2.7-12     |
    |      dosfstools-2.7-1    |
    |      gdbm-1.8.0-10       |
    |      ksymoops-2.4.1-1    |
    |      mktemp-1.5-11       |
    |      perl-5.6.0-17       |
    |      reiserfs-utils-3.x. |
    | 0j-2                     |
    |      ...                 |
    |                          |
    |                          |
    |     bash$ rpm -qa docboo |
    | k-utils                  |
    |     docbook-utils-0.6.9- |
    | 2                        |
    |                          |
    |                          |
    |     bash$ rpm -qa docboo |
    | k | grep docbook         |
    |     docbook-dtd31-sgml-1 |
    | .0-10                    |
    |      docbook-style-dsssl |
    | -1.64-3                  |
    |      docbook-dtd30-sgml- |
    | 1.0-10                   |
    |      docbook-dtd40-sgml- |
    | 1.0-11                   |
    |      docbook-utils-pdf-0 |
    | .6.9-2                   |
    |      docbook-dtd41-sgml- |
    | 1.0-10                   |
    |      docbook-utils-0.6.9 |
    | -2                       |
    |                          |
                              

    .. raw:: html

       </p>

    .. code:: SCREEN

        bash$ rpm -qa
        redhat-logos-1.1.3-1
         glibc-2.2.4-13
         cracklib-2.7-12
         dosfstools-2.7-1
         gdbm-1.8.0-10
         ksymoops-2.4.1-1
         mktemp-1.5-11
         perl-5.6.0-17
         reiserfs-utils-3.x.0j-2
         ...


        bash$ rpm -qa docbook-utils
        docbook-utils-0.6.9-2


        bash$ rpm -qa docbook | grep docbook
        docbook-dtd31-sgml-1.0-10
         docbook-style-dsssl-1.64-3
         docbook-dtd30-sgml-1.0-10
         docbook-dtd40-sgml-1.0-11
         docbook-utils-pdf-0.6.9-2
         docbook-dtd41-sgml-1.0-10
         docbook-utils-0.6.9-2
                  

    .. raw:: html

       </p>

    .. code:: SCREEN

        bash$ rpm -qa
        redhat-logos-1.1.3-1
         glibc-2.2.4-13
         cracklib-2.7-12
         dosfstools-2.7-1
         gdbm-1.8.0-10
         ksymoops-2.4.1-1
         mktemp-1.5-11
         perl-5.6.0-17
         reiserfs-utils-3.x.0j-2
         ...


        bash$ rpm -qa docbook-utils
        docbook-utils-0.6.9-2


        bash$ rpm -qa docbook | grep docbook
        docbook-dtd31-sgml-1.0-10
         docbook-style-dsssl-1.64-3
         docbook-dtd30-sgml-1.0-10
         docbook-dtd40-sgml-1.0-11
         docbook-utils-pdf-0.6.9-2
         docbook-dtd41-sgml-1.0-10
         docbook-utils-0.6.9-2
                  

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

 **cpio**
    This specialized archiving copy command ( **c** o **p** y **i** nput
    and **o** utput) is rarely seen any more, having been supplanted by
    **tar** / **gzip** . It still has its uses, such as moving a
    directory tree. With an appropriate block size (for copying)
    specified, it can be appreciably faster than **tar** .

    .. raw:: html

       <div class="EXAMPLE">

    **Example 16-30. Using *cpio* to move a directory tree**

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        #!/bin/bash

        # Copying a directory tree using cpio.

        # Advantages of using 'cpio':
        #   Speed of copying. It's faster than 'tar' with pipes.
        #   Well suited for copying special files (named pipes, etc.)
        #+  that 'cp' may choke on.

        ARGS=2
        E_BADARGS=65

        if [ $# -ne "$ARGS" ]
        then
          echo "Usage: `basename $0` source destination"
          exit $E_BADARGS
        fi  

        source="$1"
        destination="$2"

        ###################################################################
        find "$source" -depth | cpio -admvp "$destination"
        #               ^^^^^         ^^^^^
        #  Read the 'find' and 'cpio' info pages to decipher these options.
        #  The above works only relative to $PWD (current directory) . . .
        #+ full pathnames are specified.
        ###################################################################


        # Exercise:
        # --------

        #  Add code to check the exit status ($?) of the 'find | cpio' pipe
        #+ and output appropriate error messages if anything went wrong.

        exit $?

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

 **rpm2cpio**
    This command extracts a **cpio** archive from an
    `rpm <filearchiv.html#RPMREF>`__ one.

    .. raw:: html

       <div class="EXAMPLE">

    **Example 16-31. Unpacking an *rpm* archive**

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        #!/bin/bash
        # de-rpm.sh: Unpack an 'rpm' archive

        : ${1?"Usage: `basename $0` target-file"}
        # Must specify 'rpm' archive name as an argument.


        TEMPFILE=$$.cpio                         #  Tempfile with "unique" name.
                                                 #  $$ is process ID of script.

        rpm2cpio < $1 > $TEMPFILE                #  Converts rpm archive into
                                                 #+ cpio archive.
        cpio --make-directories -F $TEMPFILE -i  #  Unpacks cpio archive.
        rm -f $TEMPFILE                          #  Deletes cpio archive.

        exit 0

        #  Exercise:
        #  Add check for whether 1) "target-file" exists and
        #+                       2) it is an rpm archive.
        #  Hint:                    Parse output of 'file' command.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

 **pax**
    The *pax* **p** ortable **a** rchive e **x** change toolkit
    facilitates periodic file backups and is designed to be
    cross-compatible between various flavors of UNIX. It was designed to
    replace `tar <filearchiv.html#TARREF>`__ and
    `cpio <filearchiv.html#CPIOREF>`__ .

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        pax -wf daily_backup.pax ~/linux-server/files 
        #  Creates a tar archive of all files in the target directory.
        #  Note that the options to pax must be in the correct order --
        #+ pax -fw     has an entirely different effect.

        pax -f daily_backup.pax
        #  Lists the files in the archive.

        pax -rf daily_backup.pax ~/bsd-server/files
        #  Restores the backed-up files from the Linux machine
        #+ onto a BSD one.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    Note that *pax* handles many of the standard archiving and
    compression commands.

.. raw:: html

   </div>

.. raw:: html

   <div class="VARIABLELIST">

** Compression**

 **gzip**
    The standard GNU/UNIX compression utility, replacing the inferior
    and proprietary **compress** . The corresponding decompression
    command is **gunzip** , which is the equivalent of **gzip -d** .

    .. raw:: html

       <div class="NOTE">

    .. raw:: html

       <div>

    |Note|

    The ``            -c           `` option sends the output of
    **gzip** to ``            stdout           `` . This is useful when
    `piping <special-chars.html#PIPEREF>`__ to other commands.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

    The **zcat** filter decompresses a *gzipped* file to
    ``         stdout        `` , as possible input to a pipe or
    redirection. This is, in effect, a **cat** command that works on
    compressed files (including files processed with the older
    `compress <filearchiv.html#COMPRESSREF>`__ utility). The **zcat**
    command is equivalent to **gzip -dc** .

    .. raw:: html

       <div class="CAUTION">

    .. raw:: html

       <div>

    |Caution|

    On some commercial UNIX systems, **zcat** is a synonym for
    **uncompress -c** , and will not work on *gzipped* files.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

    See also `Example 7-7 <comparison-ops.html#EX14>`__ .

 **bzip2**
    An alternate compression utility, usually more efficient (but
    slower) than **gzip** , especially on large files. The corresponding
    decompression command is **bunzip2** .

    Similar to the **zcat** command, **bzcat** decompresses a
    *bzipped2-ed* file to ``         stdout        `` .

    .. raw:: html

       <div class="NOTE">

    .. raw:: html

       <div>

    |Note|

    Newer versions of `tar <filearchiv.html#TARREF>`__ have been patched
    with **bzip2** support.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

 **compress** , **uncompress**
    This is an older, proprietary compression utility found in
    commercial UNIX distributions. The more efficient **gzip** has
    largely replaced it. Linux distributions generally include a
    **compress** workalike for compatibility, although **gunzip** can
    unarchive files treated with **compress** .

    .. raw:: html

       <div class="TIP">

    .. raw:: html

       <div>

    |Tip|

    The **znew** command transforms *compressed* files into *gzipped*
    ones.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

 **sq**
    Yet another compression ( **sq** ueeze) utility, a filter that works
    only on sorted `ASCII <special-chars.html#ASCIIDEF>`__ word lists.
    It uses the standard invocation syntax for a filter, **sq <
    input-file > output-file** . Fast, but not nearly as efficient as
    `gzip <filearchiv.html#GZIPREF>`__ . The corresponding uncompression
    filter is **unsq** , invoked like **sq** .

    .. raw:: html

       <div class="TIP">

    .. raw:: html

       <div>

    |Tip|

    The output of **sq** may be piped to **gzip** for further
    compression.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

 **zip** , **unzip**
    Cross-platform file archiving and compression utility compatible
    with DOS *pkzip.exe* . "Zipped" archives seem to be a more common
    medium of file exchange on the Internet than "tarballs."

 **unarc** , **unarj** , **unrar**
    These Linux utilities permit unpacking archives compressed with the
    DOS *arc.exe* , *arj.exe* , and *rar.exe* programs.

 **lzma** , **unlzma** , **lzcat**
    Highly efficient Lempel-Ziv-Markov compression. The syntax of *lzma*
    is similar to that of *gzip* . The `7-zip
    Website <http://www.7-zip.org/sdk.html>`__ has more information.

 **xz** , **unxz** , **xzcat**
    A new high-efficiency compression tool, backward compatible with
    *lzma* , and with an invocation syntax similar to *gzip* . For more
    information, see the `Wikipedia
    entry <http://en.wikipedia.org/wiki/Xz>`__ .

.. raw:: html

   </div>

.. raw:: html

   <div class="VARIABLELIST">

** File Information**

 **file**
    A utility for identifying file types. The command
    ``                   file file-name                 `` will return a
    file specification for ``         file-name        `` , such as
    ``         ascii text        `` or ``         data        `` . It
    references the `magic numbers <sha-bang.html#MAGNUMREF>`__ found in
    ``         /usr/share/magic        `` ,
    ``         /etc/magic        `` , or
    ``         /usr/lib/magic        `` , depending on the Linux/UNIX
    distribution.

    The ``         -f        `` option causes **file** to run in
    `batch <timedate.html#BATCHPROCREF>`__ mode, to read from a
    designated file a list of filenames to analyze. The
    ``         -z        `` option, when used on a compressed target
    file, forces an attempt to analyze the uncompressed file type.

    .. raw:: html

       <div>

    .. code:: SCREEN

        bash$ file test.tar.gz
        test.tar.gz: gzip compressed data, deflated,
         last modified: Sun Sep 16 13:34:51 2001, os: Unix

        bash file -z test.tar.gz
        test.tar.gz: GNU tar archive (gzip compressed data, deflated,
         last modified: Sun Sep 16 13:34:51 2001, os: Unix)
                  

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        # Find sh and Bash scripts in a given directory:

        DIRECTORY=/usr/local/bin
        KEYWORD=Bourne
        # Bourne and Bourne-Again shell scripts

        file $DIRECTORY/* | fgrep $KEYWORD

        # Output:

        # /usr/local/bin/burn-cd:          Bourne-Again shell script text executable
        # /usr/local/bin/burnit:           Bourne-Again shell script text executable
        # /usr/local/bin/cassette.sh:      Bourne shell script text executable
        # /usr/local/bin/copy-cd:          Bourne-Again shell script text executable
        # . . .

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       <div class="EXAMPLE">

    **Example 16-32. Stripping comments from C program files**

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        #!/bin/bash
        # strip-comment.sh: Strips out the comments (/* COMMENT */) in a C program.

        E_NOARGS=0
        E_ARGERROR=66
        E_WRONG_FILE_TYPE=67

        if [ $# -eq "$E_NOARGS" ]
        then
          echo "Usage: `basename $0` C-program-file" >&2 # Error message to stderr.
          exit $E_ARGERROR
        fi  

        # Test for correct file type.
        type=`file $1 | awk '{ print $2, $3, $4, $5 }'`
        # "file $1" echoes file type . . .
        # Then awk removes the first field, the filename . . .
        # Then the result is fed into the variable "type."
        correct_type="ASCII C program text"

        if [ "$type" != "$correct_type" ]
        then
          echo
          echo "This script works on C program files only."
          echo
          exit $E_WRONG_FILE_TYPE
        fi  


        # Rather cryptic sed script:
        #--------
        sed '
        /^\/\*/d
        /.*\*\//d
        ' $1
        #--------
        # Easy to understand if you take several hours to learn sed fundamentals.


        #  Need to add one more line to the sed script to deal with
        #+ case where line of code has a comment following it on same line.
        #  This is left as a non-trivial exercise.

        #  Also, the above code deletes non-comment lines with a "*/" . . .
        #+ not a desirable result.

        exit 0


        # ----------------------------------------------------------------
        # Code below this line will not execute because of 'exit 0' above.

        # Stephane Chazelas suggests the following alternative:

        usage() {
          echo "Usage: `basename $0` C-program-file" >&2
          exit 1
        }

        WEIRD=`echo -n -e '\377'`   # or WEIRD=$'\377'
        [[ $# -eq 1 ]] || usage
        case `file "$1"` in
          *"C program text"*) sed -e "s%/\*%${WEIRD}%g;s%\*/%${WEIRD}%g" "$1" \
             | tr '\377\n' '\n\377' \
             | sed -ne 'p;n' \
             | tr -d '\n' | tr '\377' '\n';;
          *) usage;;
        esac

        #  This is still fooled by things like:
        #  printf("/*");
        #  or
        #  /*  /* buggy embedded comment */
        #
        #  To handle all special cases (comments in strings, comments in string
        #+ where there is a \", \\" ...),
        #+ the only way is to write a C parser (using lex or yacc perhaps?).

        exit 0

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

 **which**
    **which command** gives the full path to "command." This is useful
    for finding out whether a particular command or utility is installed
    on the system.

    ``                   $bash which rm                 ``

    .. raw:: html

       <div>

    .. code:: SCREEN

        /usr/bin/rm

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    For an interesting use of this command, see `Example
    36-16 <colorizing.html#HORSERACE>`__ .

 **whereis**
    Similar to **which** , above, **whereis command** gives the full
    path to "command," but also to its `manpage <basic.html#MANREF>`__ .

    ``                   $bash whereis rm                 ``

    .. raw:: html

       <div>

    .. code:: SCREEN

        rm: /bin/rm /usr/share/man/man1/rm.1.bz2

    .. raw:: html

       </p>

    .. raw:: html

       </div>

 **whatis**
    **whatis command** looks up "command" in the
    ``                   whatis                 `` database. This is
    useful for identifying system commands and important configuration
    files. Consider it a simplified **man** command.

    ``                   $bash whatis whatis                 ``

    .. raw:: html

       <div>

    .. code:: SCREEN

        whatis               (1)  - search the whatis database for complete words

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       <div class="EXAMPLE">

    **Example 16-33. Exploring ``           /usr/X11R6/bin          ``**

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        #!/bin/bash

        # What are all those mysterious binaries in /usr/X11R6/bin?

        DIRECTORY="/usr/X11R6/bin"
        # Try also "/bin", "/usr/bin", "/usr/local/bin", etc.

        for file in $DIRECTORY/*
        do
          whatis `basename $file`   # Echoes info about the binary.
        done

        exit 0

        #  Note: For this to work, you must create a "whatis" database
        #+ with /usr/sbin/makewhatis.
        #  You may wish to redirect output of this script, like so:
        #    ./what.sh >>whatis.db
        #  or view it a page at a time on stdout,
        #    ./what.sh | less

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

    See also `Example 11-3 <loops1.html#FILEINFO>`__ .

 **vdir**
    Show a detailed directory listing. The effect is similar to `ls
    -lb <basic.html#LSREF>`__ .

    This is one of the GNU *fileutils* .

    .. raw:: html

       <div>

    .. code:: SCREEN

        bash$ vdir
        total 10
         -rw-r--r--    1 bozo  bozo      4034 Jul 18 22:04 data1.xrolo
         -rw-r--r--    1 bozo  bozo      4602 May 25 13:58 data1.xrolo.bak
         -rw-r--r--    1 bozo  bozo       877 Dec 17  2000 employment.xrolo

        bash ls -l
        total 10
         -rw-r--r--    1 bozo  bozo      4034 Jul 18 22:04 data1.xrolo
         -rw-r--r--    1 bozo  bozo      4602 May 25 13:58 data1.xrolo.bak
         -rw-r--r--    1 bozo  bozo       877 Dec 17  2000 employment.xrolo
                  

    .. raw:: html

       </p>

    .. raw:: html

       </div>

 **locate** , **slocate**
    The **locate** command searches for files using a database stored
    for just that purpose. The **slocate** command is the secure version
    of **locate** (which may be aliased to **slocate** ).

    ``                   $bash locate hickson                 ``

    .. raw:: html

       <div>

    .. code:: SCREEN

        /usr/lib/xephem/catalogs/hickson.edb

    .. raw:: html

       </p>

    .. raw:: html

       </div>

 **getfacl** , **setfacl**
    These commands *retrieve* or *set* the **f** ile **a** ccess **c**
    ontrol **l** ist -- the *owner* , *group* , and file permissions.

    .. raw:: html

       <div>

    .. code:: SCREEN

        bash$ getfacl *
        # file: test1.txt
         # owner: bozo
         # group: bozgrp
         user::rw-
         group::rw-
         other::r--

         # file: test2.txt
         # owner: bozo
         # group: bozgrp
         user::rw-
         group::rw-
         other::r--
         

         
        bash$ setfacl -m u:bozo:rw yearly_budget.csv
        bash$ getfacl yearly_budget.csv
        # file: yearly_budget.csv
         # owner: accountant
         # group: budgetgrp
         user::rw-
         user:bozo:rw-
         user:accountant:rw-
         group::rw-
         mask::rw-
         other::r--
                  

    .. raw:: html

       </p>

    .. raw:: html

       </div>

 **readlink**
    Disclose the file that a symbolic link points to.

    .. raw:: html

       <div>

    .. code:: SCREEN

        bash$ readlink /usr/bin/awk
        ../../bin/gawk
                  

    .. raw:: html

       </p>

    .. raw:: html

       </div>

 **strings**
    Use the **strings** command to find printable strings in a binary or
    data file. It will list sequences of printable characters found in
    the target file. This might be handy for a quick 'n dirty
    examination of a core dump or for looking at an unknown graphic
    image file (
    ``                   strings image-file | more                 ``
    might show something like *JFIF* , which would identify the file as
    a *jpeg* graphic). In a script, you would probably parse the output
    of **strings** with `grep <textproc.html#GREPREF>`__ or
    `sed <sedawk.html#SEDREF>`__ . See `Example
    11-8 <loops1.html#BINGREP>`__ and `Example
    11-10 <loops1.html#FINDSTRING>`__ .

    .. raw:: html

       <div class="EXAMPLE">

    **Example 16-34. An "improved" *strings* command**

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        #!/bin/bash
        # wstrings.sh: "word-strings" (enhanced "strings" command)
        #
        #  This script filters the output of "strings" by checking it
        #+ against a standard word list file.
        #  This effectively eliminates gibberish and noise,
        #+ and outputs only recognized words.

        # ===========================================================
        #                 Standard Check for Script Argument(s)
        ARGS=1
        E_BADARGS=85
        E_NOFILE=86

        if [ $# -ne $ARGS ]
        then
          echo "Usage: `basename $0` filename"
          exit $E_BADARGS
        fi

        if [ ! -f "$1" ]                      # Check if file exists.
        then
            echo "File \"$1\" does not exist."
            exit $E_NOFILE
        fi
        # ===========================================================


        MINSTRLEN=3                           #  Minimum string length.
        WORDFILE=/usr/share/dict/linux.words  #  Dictionary file.
        #  May specify a different word list file
        #+ of one-word-per-line format.
        #  For example, the "yawl" word-list package,
        #  http://bash.deta.in/yawl-0.3.2.tar.gz


        wlist=`strings "$1" | tr A-Z a-z | tr '[:space:]' Z | \
               tr -cs '[:alpha:]' Z | tr -s '\173-\377' Z | tr Z ' '`

        # Translate output of 'strings' command with multiple passes of 'tr'.
        #  "tr A-Z a-z"  converts to lowercase.
        #  "tr '[:space:]'"  converts whitespace characters to Z's.
        #  "tr -cs '[:alpha:]' Z"  converts non-alphabetic characters to Z's,
        #+ and squeezes multiple consecutive Z's.
        #  "tr -s '\173-\377' Z"  converts all characters past 'z' to Z's
        #+ and squeezes multiple consecutive Z's,
        #+ which gets rid of all the weird characters that the previous
        #+ translation failed to deal with.
        #  Finally, "tr Z ' '" converts all those Z's to whitespace,
        #+ which will be seen as word separators in the loop below.

        #  ***********************************************************************
        #  Note the technique of feeding/piping the output of 'tr' back to itself,
        #+ but with different arguments and/or options on each successive pass.
        #  ***********************************************************************


        for word in $wlist                    #  Important:
                                              #  $wlist must not be quoted here.
                                              # "$wlist" does not work.
                                              #  Why not?
        do
          strlen=${#word}                     #  String length.
          if [ "$strlen" -lt "$MINSTRLEN" ]   #  Skip over short strings.
          then
            continue
          fi

          grep -Fw $word "$WORDFILE"          #   Match whole words only.
        #      ^^^                            #  "Fixed strings" and
                                              #+ "whole words" options. 
        done  

        exit $?

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="VARIABLELIST">

** Comparison**

 **diff** , **patch**
    **diff** : flexible file comparison utility. It compares the target
    files line-by-line sequentially. In some applications, such as
    comparing word dictionaries, it may be helpful to filter the files
    through `sort <textproc.html#SORTREF>`__ and **uniq** before piping
    them to **diff** .
    ``                   diff file-1           file-2                 ``
    outputs the lines in the files that differ, with carets showing
    which file each particular line belongs to.

    The ``         --side-by-side        `` option to **diff** outputs
    each compared file, line by line, in separate columns, with
    non-matching lines marked. The ``         -c        `` and
    ``         -u        `` options likewise make the output of the
    command easier to interpret.

    There are available various fancy frontends for **diff** , such as
    **sdiff** , **wdiff** , **xdiff** , and **mgdiff** .

    .. raw:: html

       <div class="TIP">

    .. raw:: html

       <div>

    |Tip|

     The **diff** command returns an exit status of 0 if the compared
    files are identical, and 1 if they differ (or 2 when *binary* files
    are being compared). This permits use of **diff** in a test
    construct within a shell script (see below).

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

    A common use for **diff** is generating difference files to be used
    with **patch** The ``         -e        `` option outputs files
    suitable for **ed** or **ex** scripts.

    **patch** : flexible versioning utility. Given a difference file
    generated by **diff** , **patch** can upgrade a previous version of
    a package to a newer version. It is much more convenient to
    distribute a relatively small "diff" file than the entire body of a
    newly revised package. Kernel "patches" have become the preferred
    method of distributing the frequent releases of the Linux kernel.

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        patch -p1 <patch-file
        # Takes all the changes listed in 'patch-file'
        # and applies them to the files referenced therein.
        # This upgrades to a newer version of the package.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    Patching the kernel:

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        cd /usr/src
        gzip -cd patchXX.gz | patch -p0
        # Upgrading kernel source using 'patch'.
        # From the Linux kernel docs "README",
        # by anonymous author (Alan Cox?).

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       <div class="NOTE">

    .. raw:: html

       <div>

    |Note|

    The **diff** command can also recursively compare directories (for
    the filenames present).

    | .. code:: SCREEN         |
    |                          |
    |     bash$ diff -r ~/note |
    | s1 ~/notes2              |
    |     Only in /home/bozo/n |
    | otes1: file02            |
    |      Only in /home/bozo/ |
    | notes1: file03           |
    |      Only in /home/bozo/ |
    | notes2: file04           |
    |                          |
                              

    .. raw:: html

       </p>

    .. code:: SCREEN

        bash$ diff -r ~/notes1 ~/notes2
        Only in /home/bozo/notes1: file02
         Only in /home/bozo/notes1: file03
         Only in /home/bozo/notes2: file04
                  

    .. raw:: html

       </p>

    .. code:: SCREEN

        bash$ diff -r ~/notes1 ~/notes2
        Only in /home/bozo/notes1: file02
         Only in /home/bozo/notes1: file03
         Only in /home/bozo/notes2: file04
                  

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

    .. raw:: html

       <div class="TIP">

    .. raw:: html

       <div>

    |Tip|

    Use **zdiff** to compare *gzipped* files.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

    .. raw:: html

       <div class="TIP">

    .. raw:: html

       <div>

    |Tip|

    Use **diffstat** to create a histogram (point-distribution graph) of
    output from **diff** .

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

 **diff3** , **merge**
    An extended version of **diff** that compares three files at a time.
    This command returns an exit value of 0 upon successful execution,
    but unfortunately this gives no information about the results of the
    comparison.

    .. raw:: html

       <div>

    .. code:: SCREEN

        bash$ diff3 file-1 file-2 file-3
        ====
         1:1c
           This is line 1 of "file-1".
         2:1c
           This is line 1 of "file-2".
         3:1c
           This is line 1 of "file-3"
                  

    .. raw:: html

       </p>

    .. raw:: html

       </div>

     The **merge** (3-way file merge) command is an interesting adjunct
    to *diff3* . Its syntax is
    ``                   merge Mergefile file1 file2                 ``
    . The result is to output to ``         Mergefile        `` the
    changes that lead from ``         file1        `` to
    ``         file2        `` . Consider this command a stripped-down
    version of *patch* .

 **sdiff**
    Compare and/or edit two files in order to merge them into an output
    file. Because of its interactive nature, this command would find
    little use in a script.

 **cmp**
    The **cmp** command is a simpler version of **diff** , above.
    Whereas **diff** reports the differences between two files, **cmp**
    merely shows at what point they differ.

    .. raw:: html

       <div class="NOTE">

    .. raw:: html

       <div>

    |Note|

    Like **diff** , **cmp** returns an exit status of 0 if the compared
    files are identical, and 1 if they differ. This permits use in a
    test construct within a shell script.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

    .. raw:: html

       <div class="EXAMPLE">

    **Example 16-35. Using *cmp* to compare two files within a script.**

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        #!/bin/bash
        # file-comparison.sh

        ARGS=2  # Two args to script expected.
        E_BADARGS=85
        E_UNREADABLE=86

        if [ $# -ne "$ARGS" ]
        then
          echo "Usage: `basename $0` file1 file2"
          exit $E_BADARGS
        fi

        if [[ ! -r "$1" || ! -r "$2" ]]
        then
          echo "Both files to be compared must exist and be readable."
          exit $E_UNREADABLE
        fi

        cmp $1 $2 &> /dev/null
        #   Redirection to /dev/null buries the output of the "cmp" command.
        #   cmp -s $1 $2  has same result ("-s" silent flag to "cmp")
        #   Thank you  Anders Gustavsson for pointing this out.
        #
        #  Also works with 'diff', i.e.,
        #+ diff $1 $2 &> /dev/null

        if [ $? -eq 0 ]         # Test exit status of "cmp" command.
        then
          echo "File \"$1\" is identical to file \"$2\"."
        else  
          echo "File \"$1\" differs from file \"$2\"."
        fi

        exit 0

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

    .. raw:: html

       <div class="TIP">

    .. raw:: html

       <div>

    |Tip|

    Use **zcmp** on *gzipped* files.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

 **comm**
    Versatile file comparison utility. The files must be sorted for this
    to be useful.

    **comm ``                     -options                   ``
    ``                     first-file                   ``
    ``                     second-file                   ``**

    ``                   comm file-1 file-2                 `` outputs
    three columns:

    -  column 1 = lines unique to ``           file-1          ``

    -  column 2 = lines unique to ``           file-2          ``

    -  column 3 = lines common to both.

    The options allow suppressing output of one or more columns.

    -  ``           -1          `` suppresses column
       ``           1          ``

    -  ``           -2          `` suppresses column
       ``           2          ``

    -  ``           -3          `` suppresses column
       ``           3          ``

    -  ``           -12          `` suppresses both columns
       ``           1          `` and ``           2          `` , etc.

    This command is useful for comparing "dictionaries" or *word lists*
    -- sorted text files with one word per line.

.. raw:: html

   </div>

.. raw:: html

   <div class="VARIABLELIST">

** Utilities**

 **basename**
    Strips the path information from a file name, printing only the file
    name. The construction
    ``                   basename         $0                 `` lets the
    script know its name, that is, the name it was invoked by. This can
    be used for "usage" messages if, for example a script is called with
    missing arguments:

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        echo "Usage: `basename $0` arg1 arg2 ... argn"

    .. raw:: html

       </p>

    .. raw:: html

       </div>

 **dirname**
    Strips the **basename** from a filename, printing only the path
    information.

    .. raw:: html

       <div class="NOTE">

    .. raw:: html

       <div>

    |Note|

    **basename** and **dirname** can operate on any arbitrary string.
    The argument does not need to refer to an existing file, or even be
    a filename for that matter (see `Example
    A-7 <contributed-scripts.html#DAYSBETWEEN>`__ ).

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

    .. raw:: html

       <div class="EXAMPLE">

    **Example 16-36. *basename* and *dirname***

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        #!/bin/bash

        address=/home/bozo/daily-journal.txt

        echo "Basename of /home/bozo/daily-journal.txt = `basename $address`"
        echo "Dirname of /home/bozo/daily-journal.txt = `dirname $address`"
        echo
        echo "My own home is `basename ~/`."         # `basename ~` also works.
        echo "The home of my home is `dirname ~/`."  # `dirname ~`  also works.

        exit 0

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

 **split** , **csplit**
    These are utilities for splitting a file into smaller chunks. Their
    usual use is for splitting up large files in order to back them up
    on floppies or preparatory to e-mailing or uploading them.

    The **csplit** command splits a file according to *context* , the
    split occuring where patterns are matched.

    .. raw:: html

       <div class="EXAMPLE">

    **Example 16-37. A script that copies itself in sections**

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        #!/bin/bash
        # splitcopy.sh

        #  A script that splits itself into chunks,
        #+ then reassembles the chunks into an exact copy
        #+ of the original script.

        CHUNKSIZE=4    #  Size of first chunk of split files.
        OUTPREFIX=xx   #  csplit prefixes, by default,
                       #+ files with "xx" ...

        csplit "$0" "$CHUNKSIZE"

        # Some comment lines for padding . . .
        # Line 15
        # Line 16
        # Line 17
        # Line 18
        # Line 19
        # Line 20

        cat "$OUTPREFIX"* > "$0.copy"  # Concatenate the chunks.
        rm "$OUTPREFIX"*               # Get rid of the chunks.

        exit $?

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="VARIABLELIST">

** Encoding and Encryption**

 **sum** , **cksum** , **md5sum** , **sha1sum**
     These are utilities for generating *checksums* . A *checksum* is a
    number ` [3]  <filearchiv.html#FTN.AEN12840>`__ mathematically
    calculated from the contents of a file, for the purpose of checking
    its integrity. A script might refer to a list of checksums for
    security purposes, such as ensuring that the contents of key system
    files have not been altered or corrupted. For security applications,
    use the **md5sum** ( **m** essage **d** igest **5** check **sum** )
    command, or better yet, the newer **sha1sum** (Secure Hash
    Algorithm). ` [4]  <filearchiv.html#FTN.AEN12849>`__

    .. raw:: html

       <div>

    .. code:: SCREEN

        bash$ cksum /boot/vmlinuz
        1670054224 804083 /boot/vmlinuz

        bash$ echo -n "Top Secret" | cksum
        3391003827 10



        bash$ md5sum /boot/vmlinuz
        0f43eccea8f09e0a0b2b5cf1dcf333ba  /boot/vmlinuz

        bash$ echo -n "Top Secret" | md5sum
        8babc97a6f62a4649716f4df8d61728f  -
                  

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       <div class="NOTE">

    .. raw:: html

       <div>

    |Note|

    The **cksum** command shows the size, in bytes, of its target,
    whether file or ``            stdout           `` .

    The **md5sum** and **sha1sum** commands display a
    `dash <special-chars.html#DASHREF2>`__ when they receive their input
    from ``            stdout           `` .

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

    .. raw:: html

       <div class="EXAMPLE">

    **Example 16-38. Checking file integrity**

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        #!/bin/bash
        # file-integrity.sh: Checking whether files in a given directory
        #                    have been tampered with.

        E_DIR_NOMATCH=80
        E_BAD_DBFILE=81

        dbfile=File_record.md5
        # Filename for storing records (database file).


        set_up_database ()
        {
          echo ""$directory"" > "$dbfile"
          # Write directory name to first line of file.
          md5sum "$directory"/* >> "$dbfile"
          # Append md5 checksums and filenames.
        }

        check_database ()
        {
          local n=0
          local filename
          local checksum

          # ------------------------------------------- #
          #  This file check should be unnecessary,
          #+ but better safe than sorry.

          if [ ! -r "$dbfile" ]
          then
            echo "Unable to read checksum database file!"
            exit $E_BAD_DBFILE
          fi
          # ------------------------------------------- #

          while read record[n]
          do

            directory_checked="${record[0]}"
            if [ "$directory_checked" != "$directory" ]
            then
              echo "Directories do not match up!"
              # Tried to use file for a different directory.
              exit $E_DIR_NOMATCH
            fi

            if [ "$n" -gt 0 ]   # Not directory name.
            then
              filename[n]=$( echo ${record[$n]} | awk '{ print $2 }' )
              #  md5sum writes records backwards,
              #+ checksum first, then filename.
              checksum[n]=$( md5sum "${filename[n]}" )


              if [ "${record[n]}" = "${checksum[n]}" ]
              then
                echo "${filename[n]} unchanged."

                elif [ "`basename ${filename[n]}`" != "$dbfile" ]
                       #  Skip over checksum database file,
                       #+ as it will change with each invocation of script.
                       #  ---
                       #  This unfortunately means that when running
                       #+ this script on $PWD, tampering with the
                       #+ checksum database file will not be detected.
                       #  Exercise: Fix this.
                then
                  echo "${filename[n]} : CHECKSUM ERROR!"
                # File has been changed since last checked.
                fi

              fi



            let "n+=1"
          done <"$dbfile"       # Read from checksum database file. 

        }  

        # =================================================== #
        # main ()

        if [ -z  "$1" ]
        then
          directory="$PWD"      #  If not specified,
        else                    #+ use current working directory.
          directory="$1"
        fi  

        clear                   # Clear screen.
        echo " Running file integrity check on $directory"
        echo

        # ------------------------------------------------------------------ #
          if [ ! -r "$dbfile" ] # Need to create database file?
          then
            echo "Setting up database file, \""$directory"/"$dbfile"\"."; echo
            set_up_database
          fi  
        # ------------------------------------------------------------------ #

        check_database          # Do the actual work.

        echo 

        #  You may wish to redirect the stdout of this script to a file,
        #+ especially if the directory checked has many files in it.

        exit 0

        #  For a much more thorough file integrity check,
        #+ consider the "Tripwire" package,
        #+ http://sourceforge.net/projects/tripwire/.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

    Also see `Example A-19 <contributed-scripts.html#DIRECTORYINFO>`__ ,
    `Example 36-16 <colorizing.html#HORSERACE>`__ , and `Example
    10-2 <string-manipulation.html#RANDSTRING>`__ for creative uses of
    the **md5sum** command.

    .. raw:: html

       <div class="NOTE">

    .. raw:: html

       <div>

    |Note|

    There have been reports that the 128-bit **md5sum** can be cracked,
    so the more secure 160-bit **sha1sum** is a welcome new addition to
    the checksum toolkit.

    | .. code:: SCREEN         |
    |                          |
    |     bash$ md5sum testfil |
    | e                        |
    |     e181e2c8720c60522c4c |
    | 4c981108e367  testfile   |
    |                          |
    |                          |
    |     bash$ sha1sum testfi |
    | le                       |
    |     5d7425a9c08a66c3177f |
    | 1e31286fa40986ffc996  te |
    | stfile                   |
    |                          |
                              

    .. raw:: html

       </p>

    .. code:: SCREEN

        bash$ md5sum testfile
        e181e2c8720c60522c4c4c981108e367  testfile


        bash$ sha1sum testfile
        5d7425a9c08a66c3177f1e31286fa40986ffc996  testfile
                  

    .. raw:: html

       </p>

    .. code:: SCREEN

        bash$ md5sum testfile
        e181e2c8720c60522c4c4c981108e367  testfile


        bash$ sha1sum testfile
        5d7425a9c08a66c3177f1e31286fa40986ffc996  testfile
                  

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

    Security consultants have demonstrated that even **sha1sum** can be
    compromised. Fortunately, newer Linux distros include longer
    bit-length **sha224sum** , **sha256sum** , **sha384sum** , and
    **sha512sum** commands.

 **uuencode**
    This utility encodes binary files (images, sound files, compressed
    files, etc.) into `ASCII <special-chars.html#ASCIIDEF>`__
    characters, making them suitable for transmission in the body of an
    e-mail message or in a newsgroup posting. This is especially useful
    where MIME (multimedia) encoding is not available.

 **uudecode**
    This reverses the encoding, decoding *uuencoded* files back into the
    original binaries.

    .. raw:: html

       <div class="EXAMPLE">

    **Example 16-39. Uudecoding encoded files**

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        #!/bin/bash
        # Uudecodes all uuencoded files in current working directory.

        lines=35        # Allow 35 lines for the header (very generous).

        for File in *   # Test all the files in $PWD.
        do
          search1=`head -n $lines $File | grep begin | wc -w`
          search2=`tail -n $lines $File | grep end | wc -w`
          #  Uuencoded files have a "begin" near the beginning,
          #+ and an "end" near the end.
          if [ "$search1" -gt 0 ]
          then
            if [ "$search2" -gt 0 ]
            then
              echo "uudecoding - $File -"
              uudecode $File
            fi  
          fi
        done  

        #  Note that running this script upon itself fools it
        #+ into thinking it is a uuencoded file,
        #+ because it contains both "begin" and "end".

        #  Exercise:
        #  --------
        #  Modify this script to check each file for a newsgroup header,
        #+ and skip to next if not found.

        exit 0

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

    .. raw:: html

       <div class="TIP">

    .. raw:: html

       <div>

    |Tip|

    The `fold -s <textproc.html#FOLDREF>`__ command may be useful
    (possibly in a pipe) to process long uudecoded text messages
    downloaded from Usenet newsgroups.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

 **mimencode** , **mmencode**
    The **mimencode** and **mmencode** commands process
    multimedia-encoded e-mail attachments. Although *mail user agents*
    (such as *pine* or *kmail* ) normally handle this automatically,
    these particular utilities permit manipulating such attachments
    manually from the command-line or in `batch processing
    mode <timedate.html#BATCHPROCREF>`__ by means of a shell script.

 **crypt**
    At one time, this was the standard UNIX file encryption utility. `
    [5]  <filearchiv.html#FTN.AEN12969>`__ Politically-motivated
    government regulations prohibiting the export of encryption software
    resulted in the disappearance of **crypt** from much of the UNIX
    world, and it is still missing from most Linux distributions.
    Fortunately, programmers have come up with a number of decent
    alternatives to it, among them the author's very own
    `cruft <ftp://metalab.unc.edu/pub/Linux/utils/file/cruft-0.2.tar.gz>`__
    (see `Example A-4 <contributed-scripts.html#ENCRYPTEDPW>`__ ).

 **openssl**
    This is an Open Source implementation of *Secure Sockets Layer*
    encryption.

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        # To encrypt a file:
        openssl aes-128-ecb -salt -in file.txt -out file.encrypted \
        -pass pass:my_password
        #          ^^^^^^^^^^^   User-selected password.
        #       aes-128-ecb      is the encryption method chosen.

        # To decrypt an openssl-encrypted file:
        openssl aes-128-ecb -d -salt -in file.encrypted -out file.txt \
        -pass pass:my_password
        #          ^^^^^^^^^^^   User-selected password.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    `Piping <special-chars.html#PIPEREF>`__ *openssl* to/from
    `tar <filearchiv.html#TARREF>`__ makes it possible to encrypt an
    entire directory tree.

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        # To encrypt a directory:

        sourcedir="/home/bozo/testfiles"
        encrfile="encr-dir.tar.gz"
        password=my_secret_password

        tar czvf - "$sourcedir" |
        openssl des3 -salt -out "$encrfile" -pass pass:"$password"
        #       ^^^^   Uses des3 encryption.
        # Writes encrypted file "encr-dir.tar.gz" in current working directory.

        # To decrypt the resulting tarball:
        openssl des3 -d -salt -in "$encrfile" -pass pass:"$password" |
        tar -xzv
        # Decrypts and unpacks into current working directory.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    Of course, *openssl* has many other uses, such as obtaining signed
    *certificates* for Web sites. See the `info <basic.html#INFOREF>`__
    page.

 **shred**
    Securely erase a file by overwriting it multiple times with random
    bit patterns before deleting it. This command has the same effect as
    `Example 16-61 <extmisc.html#BLOTOUT>`__ , but does it in a more
    thorough and elegant manner.

    This is one of the GNU *fileutils* .

    .. raw:: html

       <div class="CAUTION">

    .. raw:: html

       <div>

    |Caution|

    Advanced forensic technology may still be able to recover the
    contents of a file, even after application of **shred** .

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="VARIABLELIST">

** Miscellaneous**

 **mktemp**
    Create a *temporary file* ` [6]  <filearchiv.html#FTN.AEN13030>`__
    with a "unique" filename. When invoked from the command-line without
    additional arguments, it creates a zero-length file in the
    ``         /tmp        `` directory.

    .. raw:: html

       <div>

    .. code:: SCREEN

        bash$ mktemp
        /tmp/tmp.zzsvql3154
                  

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        PREFIX=filename
        tempfile=`mktemp $PREFIX.XXXXXX`
        #                        ^^^^^^ Need at least 6 placeholders
        #+                              in the filename template.
        #   If no filename template supplied,
        #+ "tmp.XXXXXXXXXX" is the default.

        echo "tempfile name = $tempfile"
        # tempfile name = filename.QA2ZpY
        #                 or something similar...

        #  Creates a file of that name in the current working directory
        #+ with 600 file permissions.
        #  A "umask 177" is therefore unnecessary,
        #+ but it's good programming practice nevertheless.

    .. raw:: html

       </p>

    .. raw:: html

       </div>

 **make**

    Utility for building and compiling binary packages. This can also be
    used for any set of operations triggered by incremental changes in
    source files.

    The *make* command checks a ``         Makefile        `` , a list
    of file dependencies and operations to be carried out.

    The *make* utility is, in effect, a powerful scripting language
    similar in many ways to *Bash* , but with the capability of
    recognizing *dependencies* . For in-depth coverage of this useful
    tool set, see the `GNU software documentation
    site <http://www.gnu.org/manual/manual.html>`__ .

 **install**
    Special purpose file copying command, similar to
    `cp <basic.html#CPREF>`__ , but capable of setting permissions and
    attributes of the copied files. This command seems tailormade for
    installing software packages, and as such it shows up frequently in
    ``         Makefiles        `` (in the
    ``                   make           install :                 ``
    section). It could likewise prove useful in installation scripts.

 **dos2unix**
    This utility, written by Benjamin Lin and collaborators, converts
    DOS-formatted text files (lines terminated by CR-LF) to UNIX format
    (lines terminated by LF only), and
    `vice-versa <gotchas.html#DOSNEWLINES>`__ .

 **ptx**
    The **ptx [targetfile]** command outputs a permuted index
    (cross-reference list) of the targetfile. This may be further
    filtered and formatted in a pipe, if necessary.

 **more** , **less**
    Pagers that display a text file or stream to
    ``         stdout        `` , one screenful at a time. These may be
    used to filter the output of ``         stdout        `` . . . or of
    a script.

    An interesting application of *more* is to "test drive" a command
    sequence, to forestall potentially unpleasant consequences.

    .. raw:: html

       <div>

    .. code:: PROGRAMLISTING

        ls /home/bozo | awk '{print "rm -rf " $1}' | more
        #                                            ^^^^
                 
        # Testing the effect of the following (disastrous) command-line:
        #      ls /home/bozo | awk '{print "rm -rf " $1}' | sh
        #      Hand off to the shell to execute . . .       ^^

    .. raw:: html

       </p>

    .. raw:: html

       </div>

    The *less* pager has the interesting property of doing a formatted
    display of *man page* source. See `Example
    A-39 <contributed-scripts.html#MANED>`__ .

.. raw:: html

   </div>

.. raw:: html

   </div>

Notes
~~~~~

.. raw:: html

   <div>

` [1]  <filearchiv.html#AEN11885>`__

An *archive* , in the sense discussed here, is simply a set of related
files stored in a single location.

.. raw:: html

   </p>

` [2]  <filearchiv.html#AEN11896>`__

A ``               tar czvf ArchiveName.tar.gz *             `` *will*
include dotfiles in subdirectories *below* the current working
directory. This is an undocumented GNU **tar** "feature."

.. raw:: html

   </p>

` [3]  <filearchiv.html#AEN12840>`__

The checksum may be expressed as a *hexadecimal* number, or to some
other base.

.. raw:: html

   </p>

` [4]  <filearchiv.html#AEN12849>`__

For even *better* security, use the *sha256sum* , *sha512* , and
*sha1pass* commands.

.. raw:: html

   </p>

` [5]  <filearchiv.html#AEN12969>`__

This is a symmetric block cipher, used to encrypt files on a single
system or local network, as opposed to the *public key* cipher class, of
which *pgp* is a well-known example.

.. raw:: html

   </p>

` [6]  <filearchiv.html#AEN13030>`__

Creates a temporary *directory* when invoked with the
``       -d      `` option.

.. raw:: html

   </p>

.. raw:: html

   </div>

.. |Caution| image:: ../images/caution.gif
.. |Tip| image:: ../images/tip.gif
.. |Note| image:: ../images/note.gif
