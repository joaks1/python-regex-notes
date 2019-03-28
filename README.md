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
So, if we compose a string that we want to be used to describe a regular
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

Python has a really nice module for dealing with regular expressions; all we
have to do is import it:

    >>> import re

Using the `re` module generally follows three steps:

1.  Write a wrong string for your regex pattern

        >>> dna_pattern_str = r'[ACGT]+'

2.  Create a regex object from your pattern

        >>> dna_pattern = re.compile(dna_pattern_str)

3.  Use one of the object's methods (it has several) to search target strings

        >>> match_object = dna_pattern.search('Drosophila\tACCCTGGCTTCAATGTC\n')


# Arguments that can be passed to `re.compile` method

There are several flags accepted by the `compile` method that allow you to
adjust how the regex pattern behaves. For example:

        >>> dna_pattern = re.compile(dna_pattern_str, re.IGNORECASE)

will cause the regex object to be case-insensitive when it looks for matches in
the target string.

Others flags include:
<dl>
    <dt><code>re.IGNORECASE</code></dt>
    <dd>Perform case-insensitive matching.</dd>
    <dt><code>re.MULTILINE</code></dt>
    <dd>Allow <code>'^'</code> to match at the beginning of the string and at
    the beginning of each line.  Allow <code>'$'</code> to match at the end of
    the string and at the end of each line.</dd>
    <dt><code>re.DOTALL</code></dt>
    <dd>Make <code>'.'</code> match any character, including a newline
    character.</dd>
</dl>


# Regex object methods

<dl>
    <dt><code>re_object.match(target_str)</code></dt>
    <dd>Look for a match only at the beginning of the target string. Returns a
    match object if found, None if not.</dd>
    <dt><code>re_object.search(target_str)</code></dt>
    <dd>Look for the first match anywhere in the target string. Returns a match
    object if found, None if not.</dd>
    <dt><code>re_object.findall(target_str)</code></dt>
    <dd>Look for all non-overlapping matches in the target string. Returns a
    list of the matches that were found.</dd>
    <dt><code>re_object.finditer(target_str)</code></dt>
    <dd>Similar to <code>findall</code>, but returns an iterator yielding match objects.</dd>
</dl>

# Character classes

<dl>
    <dt><code>\d</code></dt>
    <dd>Any digit; equivalent to character set <code>[0-9]</code>.</dd>
    <dt><code>\D</code></dt>
    <dd>Any nondigit; <code>[^0-9]</code>.</dd>
    <dt><code>\s</code></dt>
    <dd>Any whitespace character <code>[ \t\n\r\f\v]</code>.</dd>
    <dt><code>\S</code></dt>
    <dd>Any nonwhitespace character <code>[^ \t\n\r\f\v]</code>.</dd>
    <dt><code>\w</code></dt>
    <dd>Any alphanumeric character <code>[a-zA-Z0-9_]</code>.</dd>
    <dt><code>\W</code></dt>
    <dd>Any non-alphanumeric character <code>[^a-zA-Z0-9_]</code>.</dd>
    <dt><code>\b</code></dt>
    <dd>Match at the boundary between a word and nonword character.</dd>
    <dt><code>\B</code></dt>
    <dd>Match anywhere *except* at the boundary between a word and nonword
    character.</dd>
</dl>


# Acknowledgments

## Support
This work was made possible by funding provided to [Jamie
Oaks](http://phyletica.org) from the National Science Foundation (DEB 1656004).


# License

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/deed.en_US"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/deed.en_US">Creative Commons Attribution 4.0 International License</a>.
