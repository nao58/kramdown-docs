HTML Parser
===========

Introduction
------------

This parser assumes that the input document is an HTML document. It automatically converts HTML tags that have a native element representation to their native representation – all other tags as well as processing instructions and HTML comments are parsed as is.

Conversion of HTML tags to native kramdown elements
---------------------------------------------------

Here is a description of the HTML tags that have native representations and how they are converted:

em strong blockquote hr br a img p thead tbody tfoot tr td th ul ol dl li dl dt dd
: These HTML tags are just transformed into their native representation and don’t need any further processing.

b i
: The HTML <b> tag is converted to the strong element and the <i> tag to the em element.

h1 h2 h3 h4 h5 h6
: These six header tags are all mapped to the single header element with different header levels.

code pre
: The code tag is converted to a codespan element and the pre tag to a codeblock element. All child tags are removed and only the contained text is used.

table
: The table tag is converted to its native element counterpart if its cells contain only span level elements - otherwise it is not converted.

The following general transformations are also applied:

* Direct text children of the following HTML tags are removed:

  ~~~
  html head hgroup ol ul dl table colgroup tbody thead tfoot tr select optgroup
  ~~~

* Text elements containing only whitespace and appearing either directly after the start tag, directly before the end tag or between block-level child elements are removed from the following HTML tags:

  ~~~
  body section nav article aside header footer address div li dd blockquote figure figcaption td th fieldset form
  ~~~

* Leading and trailing whitespace in the content of the following HTML tags is removed:

  ~~~
  address article aside blockquote body caption dd div dl dt fieldset figcaption form footer header h1 h2 h3 h4 h5 h6 legend li nav p section td th
  ~~~

Options
-------

The HTML parser doesn’t have any options.
