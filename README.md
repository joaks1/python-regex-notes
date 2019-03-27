Using regular expressions (regex) in Python is very similar to how we have been
using them in Bash.
The main difference is that we will be creating and using regex-crunching
objects (instances of a class designed for dealing with regular expression
patterns).
Other than that, the syntax for how we describe the pattern we want to find is
very similar.

# A note about backslashes and raw strings

tl;dr always use raw strings when writing regex patterns in Python.

In Python, the backslash (`'\'`) has special meanings within literal strings.
For example, you can use it to **escape** or "deactivate" a character that
would normally have a special meaning, like:

    >>> 'I\'m cold'

Conversely, it can also be used to activate a special character like a tab:

    >>> 'I\'m\tcold'

The problem is that the backslash also has special meanings in regular
expressions.
So, if we compose a string that we want to be used to desribe a regular
expression pattern, we have to think 2 steps ahead: (1) How will Python
interpret this string, and then (2) pass it along to a regular expression
function or argument.

For example, if we want to write a regex that matches the literal string
`\section`, the regex pattern needs to escape the backslash. So, the
regular expression pattern needs to be `\\section`. To write a literal
string in Python that will be `\\section` *after* Python interprets it,
we would need to write `'\\\\section'`; what a pain!

The solution is Python's **raw** string notation!

In Python, if we prefix a string with an `r`, we are telling Python
that we mean exactly what we are typing.
For example, `'\t'` is a string string with one tab character, whereas
`r'\t'` is a string with two characters, `\` and `t`.

**Long story short:** To make our lives easier, when we are writing a regex
pattern in Python, we will always use **raw** strings.


# Using the `re` module


# Acknowledgments

## Support
This work was made possible by funding provided to [Jamie
Oaks](http://phyletica.org) from the National Science Foundation (DEB 1656004).


# License

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/deed.en_US"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/deed.en_US">Creative Commons Attribution 4.0 International License</a>.
