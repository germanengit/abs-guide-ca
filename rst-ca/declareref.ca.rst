+------------------------------------+----------------------------------------+----------------------------+
| Advanced Bash-Scripting Guide:     |
+====================================+========================================+============================+
| `Prev <internalvariables.html>`_   | Chapter 9. Another Look at Variables   | `Next <randomvar.html>`_   |
+------------------------------------+----------------------------------------+----------------------------+

--------------

9.2. Typing variables: **declare** or **typeset**
=================================================

The *declare* or *typeset* `builtins <internal.html#BUILTINREF>`_, which
are exact synonyms, permit modifying the properties of variables. This
is a very weak form of the *typing* `[1] <declareref.html#FTN.AEN5648>`_
available in certain programming languages. The *declare* command is
specific to version 2 or later of Bash. The *typeset* command also works
in ksh scripts.

**declare/typeset options**

-r ``readonly``
    (``declare -r var1`` works the same as ``readonly var1``)

    This is the rough equivalent of the **C** *const* type qualifier. An
    attempt to change the value of a *readonly* variable fails with an
    error message.

    ::

        declare -r var1=1
        echo "var1 = $var1"   # var1 = 1

        (( var1++ ))          # x.sh: line 4: var1: readonly variable

-i ``integer``

    ::

        declare -i number
        # The script will treat subsequent occurrences of "number" as an integer.       

        number=3
        echo "Number = $number"     # Number = 3

        number=three
        echo "Number = $number"     # Number = 0
        # Tries to evaluate the string "three" as an integer.

    Certain arithmetic operations are permitted for declared integer
    variables without the need for `expr <moreadv.html#EXPRREF>`_ or
    `let <internal.html#LETREF>`_.

    ::

        n=6/3
        echo "n = $n"       # n = 6/3

        declare -i n
        n=6/3
        echo "n = $n"       # n = 2

-a ``array``

    ::

        declare -a indices

    The variable ``indices`` will be treated as an
    `array <arrays.html#ARRAYREF>`_.

-f ``function(s)``

    ::

        declare -f

    A ``declare -f`` line with no arguments in a script causes a listing
    of all the `functions <functions.html#FUNCTIONREF>`_ previously
    defined in that script.

    ::

        declare -f function_name

    A ``declare -f function_name`` in a script lists just the function
    named.

-x `export <internal.html#EXPORTREF>`_

    ::

        declare -x var3

    This declares a variable as available for exporting outside the
    environment of the script itself.

-x var=$value

    ::

        declare -x var3=373

    The **declare** command permits assigning a value to a variable in
    the same statement as setting its properties.

**Example 9-10. Using *declare* to type variables**

::

    #!/bin/bash

    func1 ()
    {
      echo This is a function.
    }

    declare -f        # Lists the function above.

    echo

    declare -i var1   # var1 is an integer.
    var1=2367
    echo "var1 declared as $var1"
    var1=var1+1       # Integer declaration eliminates the need for 'let'.
    echo "var1 incremented by 1 is $var1."
    # Attempt to change variable declared as integer.
    echo "Attempting to change var1 to floating point value, 2367.1."
    var1=2367.1       # Results in error message, with no change to variable.
    echo "var1 is still $var1"

    echo

    declare -r var2=13.36         # 'declare' permits setting a variable property
                                  #+ and simultaneously assigning it a value.
    echo "var2 declared as $var2" # Attempt to change readonly variable.
    var2=13.37                    # Generates error message, and exit from script.

    echo "var2 is still $var2"    # This line will not execute.

    exit 0                        # Script will not exit here.

.. figure:: http://tldp.org/LDP/abs/images/caution.gif
   :align: center
   :alt: Caution

   Caution
Using the *declare* builtin restricts the
`scope <subshells.html#SCOPEREF>`_ of a variable.

::

    foo ()
    {
    FOO="bar"
    }

    bar ()
    {
    foo
    echo $FOO
    }

    bar   # Prints bar.

However . . .

::

    foo (){
    declare FOO="bar"
    }

    bar ()
    {
    foo
    echo $FOO
    }

    bar  # Prints nothing.


    # Thank you, Michael Iatrou, for pointing this out.

9.2.1. Another use for *declare*
--------------------------------

The *declare* command can be helpful in identifying variables,
`environmental <othertypesv.html#ENVREF>`_ or otherwise. This can be
especially useful with `arrays <arrays.html#ARRAYREF>`_.

::

    bash$ declare | grep HOME
    HOME=/home/bozo


    bash$ zzy=68
    bash$ declare | grep zzy
    zzy=68


    bash$ Colors=([0]="purple" [1]="reddish-orange" [2]="light green")
    bash$ echo ${Colors[@]}
    purple reddish-orange light green
    bash$ declare | grep Colors
    Colors=([0]="purple" [1]="reddish-orange" [2]="light green")
             

Notes
~~~~~

`[1] <declareref.html#AEN5648>`_

In this context, *typing* a variable means to classify it and restrict
its properties. For example, a variable *declared* or *typed* as an
integer is no longer available for `string
operations <refcards.html#STRINGOPSTAB>`_.

::

    declare -i intvar

    intvar=23
    echo "$intvar"   # 23
    intvar=stringval
    echo "$intvar"   # 0

--------------

+------------------------------------+---------------------------+------------------------------------+
| `Prev <internalvariables.html>`_   | `Home <index.html>`_      | `Next <randomvar.html>`_           |
+------------------------------------+---------------------------+------------------------------------+
| Internal Variables                 | `Up <variables2.html>`_   | $RANDOM: generate random integer   |
+------------------------------------+---------------------------+------------------------------------+

