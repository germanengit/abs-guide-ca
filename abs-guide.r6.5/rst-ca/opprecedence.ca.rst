+----------------------------------+--------------------------------------------+------------------------+
| Advanced Bash-Scripting Guide:   |
+==================================+============================================+========================+
| `Prev <dblparens.html>`_         | Chapter 8. Operations and Related Topics   | `Next <part3.html>`_   |
+----------------------------------+--------------------------------------------+------------------------+

--------------

8.4. Operator Precedence
========================

In a script, operations execute in order of *precedence*: the higher
precedence operations execute *before* the lower precedence ones.
`[1] <opprecedence.html#FTN.AEN4262>`_

**Table 8-1. Operator Precedence**

+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| Operator                        | Meaning                                              | Comments                                                    |
+=================================+======================================================+=============================================================+
| ````                            |                                                      | **HIGHEST PRECEDENCE**                                      |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``var++ var--``                 | post-increment, post-decrement                       | `C-style <assortedtips.html#CSTYLE>`_ operators             |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``++var --var``                 | pre-increment, pre-decrement                         |                                                             |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``! ~``                         | `negation <special-chars.html#NOTREF>`_              | logical / bitwise, inverts sense of following operator      |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``**``                          | `exponentiation <ops.html#EXPONENTIATIONREF>`_       | `arithmetic operation <ops.html#AROPS1>`_                   |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``* / %``                       | multiplication, division, modulo                     | arithmetic operation                                        |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``+ -``                         | addition, subtraction                                | arithmetic operation                                        |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``<< >>``                       | left, right shift                                    | `bitwise <ops.html#BITWSOPS1>`_                             |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``-z -n``                       | *unary* comparison                                   | string is/is-not `null <comparison-ops.html#STRINGNULL>`_   |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``-e -f -t -x, etc.``           | *unary* comparison                                   | `file-test <fto.html>`_                                     |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``< -lt > -gt <= -le >= -ge``   | *compound* comparison                                | string and integer                                          |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``-nt -ot -ef``                 | *compound* comparison                                | file-test                                                   |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``== -eq !=            -ne``    | equality / inequality                                | test operators, string and integer                          |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``&``                           | AND                                                  | bitwise                                                     |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``^``                           | XOR                                                  | *exclusive* OR, bitwise                                     |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``|``                           | OR                                                   | bitwise                                                     |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``&& -a``                       | AND                                                  | `logical <ops.html#LOGOPS1>`_, *compound* comparison        |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``|| -o``                       | OR                                                   | logical, *compound* comparison                              |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``?:``                          | `trinary operator <special-chars.html#CSTRINARY>`_   | C-style                                                     |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``=``                           | `assignment <varassignment.html#EQREF>`_             | (do not confuse with equality *test*)                       |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``*= /= %= += -= <<= >>= &=``   | `combination assignment <ops.html#ARITHOPSCOMB>`_    | times-equal, divide-equal, mod-equal, etc.                  |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ``,``                           | `comma <ops.html#COMMAOP>`_                          | links a sequence of operations                              |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+
| ````                            |                                                      | **LOWEST PRECEDENCE**                                       |
+---------------------------------+------------------------------------------------------+-------------------------------------------------------------+

In practice, all you really need to remember is the following:

-  The "My Dear Aunt Sally" mantra (*multiply, divide, add, subtract*)
   for the familiar `arithmetic operations <ops.html#AROPS1>`_.

-  The *compound* logical operators, **&&**, **\|\|**, **-a**, and
   **-o** have low precedence.

-  The order of evaluation of equal-precedence operators is usually
   *left-to-right*.

Now, let's utilize our knowledge of operator precedence to analyze a
couple of lines from the ``/etc/init.d/functions file``, as found in the
*Fedora Core* Linux distro.

::

    while [ -n "$remaining" -a "$retry" -gt 0 ]; do

    # This looks rather daunting at first glance.


    # Separate the conditions:
    while [ -n "$remaining" -a "$retry" -gt 0 ]; do
    #       --condition 1-- ^^ --condition 2-

    #  If variable "$remaining" is not zero length
    #+      AND (-a)
    #+ variable "$retry" is greater-than zero
    #+ then
    #+ the [ expresion-within-condition-brackets ] returns success (0)
    #+ and the while-loop executes an iteration.
    #  ==============================================================
    #  Evaluate "condition 1" and "condition 2" ***before***
    #+ ANDing them. Why? Because the AND (-a) has a lower precedence
    #+ than the -n and -gt operators,
    #+ and therefore gets evaluated *last*.

    #################################################################

    if [ -f /etc/sysconfig/i18n -a -z "${NOLOCALE:-}" ] ; then


    # Again, separate the conditions:
    if [ -f /etc/sysconfig/i18n -a -z "${NOLOCALE:-}" ] ; then
    #    --condition 1--------- ^^ --condition 2-----

    #  If file "/etc/sysconfig/i18n" exists
    #+      AND (-a)
    #+ variable $NOLOCALE is zero length
    #+ then
    #+ the [ test-expresion-within-condition-brackets ] returns success (0)
    #+ and the commands following execute.
    #
    #  As before, the AND (-a) gets evaluated *last*
    #+ because it has the lowest precedence of the operators within
    #+ the test brackets.
    #  ==============================================================
    #  Note:
    #  ${NOLOCALE:-} is a parameter expansion that seems redundant.
    #  But, if $NOLOCALE has not been declared, it gets set to *null*,
    #+ in effect declaring it.
    #  This makes a difference in some contexts.

.. figure:: http://tldp.org/LDP/abs/images/tip.gif
   :align: center
   :alt: Tip

   Tip
To avoid confusion or error in a complex sequence of test operators,
break up the sequence into bracketed sections.

::

    if [ "$v1" -gt "$v2"  -o  "$v1" -lt "$v2"  -a  -e "$filename" ]
    # Unclear what's going on here...

    if [[ "$v1" -gt "$v2" ]] || [[ "$v1" -lt "$v2" ]] && [[ -e "$filename" ]]
    # Much better -- the condition tests are grouped in logical sections.

Notes
~~~~~

`[1] <opprecedence.html#AEN4262>`_

*Precedence*, in this context, has approximately the same meaning as
*priority*

--------------

+------------------------------------+---------------------------+------------------------+
| `Prev <dblparens.html>`_           | `Home <index.html>`_      | `Next <part3.html>`_   |
+------------------------------------+---------------------------+------------------------+
| The Double-Parentheses Construct   | `Up <operations.html>`_   | Beyond the Basics      |
+------------------------------------+---------------------------+------------------------+

