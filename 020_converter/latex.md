LaTeX Converter
===============

Introduction
------------

This converter converts a kramdown element tree into LaTeX. It supports all available element types except the HTML specific ones. The LaTeX document can, for example, further be converted to a PDF file to produce a high quality, printable version.

Since the LaTeX converter outputs just the converted element tree and not a whole LaTeX document by default, one should always use the template option (see below) to include the necessary “framework”. There are also some [other options][LaTeX Converter - Options] that can be used to customize the generated LaTeX output.

Needed Packages
---------------

Some packages are always required (when using the provided document template):

* inputenc and fontenc
* listings (see Code Blocks)
* ucs (when using Ruby 1.8)
* hyperref

The following LaTeX packages are needed to support certain features and are only included if such a feature is actually used:

* amssymb, amsmath, amsthm, amsfonts (for math support)
* graphicx (for image support)
* wasysym, amssymb, mathabx, textcomp, mathcomp, eurosym (for special entity character support)
* fancyvrb (see Footnotes)
* acronym (for acronym support)

Hyper Targets and Links
-----------------------

All elements which have an ID set (if the option auto_ids is set to true, an ID is automatically generated for header elements – for details on how the ID is generated see the corresponding section of the HTML converter documentation) are available as hyper targets within the LaTeX document. All links (the in-document links starting with # and absolute links) are transformed automatically into hyper links. This means that when a PDF is generated from the LaTeX document, in-document as well as general links will work correctly.

Code Blocks
-----------

The LaTeX converter supports the visualisation of whitespace and syntax highlighting as specified in the [HTML converter documentation][HTML Converter - Code Blocks]. Syntax highlighting and visualizing whitespace in a code block is done using the listings package. So all languages supported by the listings package can be highlighted.

Emphasis
--------

The latex command emph is used for light and the command textbf for strong emphasis.

Footnotes
---------

The fancyvrb package is used to support code blocks (i.e. verbatim environments) inside footnotes.

Automatic "Table of Contents" Generation
----------------------------------------

If you add a "toc" reference to a list as described on the [HTML converter page][HTML Converter], the list is replaced by the table of contents using the \tableofcontents command.

Standalone Images
-----------------

The LaTeX converter handles images that are the only child of a paragraph specially. Such images are not shown inline but rather in a figure environment, using the alternative text as caption.

Element Attributes
------------------

Since the element attributes cannot be used directly by the LaTeX converter in most cases, the converter outputs them as LaTeX comment when possible so that a post-processor can make use of them. The attributes are output as key value pairs (like XHTML attributes) and sorted by the key.

Here is an example input and output:

~~~
> This is a quote.
{: #my-id .cls}
~~~

will be converted by the LaTeX converter to:

~~~
\begin{quote}   % class="cls" id="my-id"
This is a quote.
\end{quote}
~~~

The attributes are output for the following elements: blockquotes; ordered, unordered and definition lists; code blocks that use the listings environment; tables; and math blocks.

Options
-------

The LaTeX converter supports the following options:

auto_ids
: Use automatic header ID generation
  If this option is true, ID values for all headers are automatically generated if no ID is explicitly specified.

  Default: true

auto_id_prefix
: Prefix used for automatically generated header IDs
  This option can be used to set a prefix for the automatically generated header IDs so that there is no conflict when rendering multiple kramdown documents into one output file separately. The prefix should only contain characters that are valid in an ID!

  Default: ''

auto_id_stripping
: Strip all formatting from header text for automatic ID generation
  If this option is true, only the text elements of a header are used for generating the ID later (in contrast to just using the raw header text line).

  This option will be removed in version 2.0 because this will be the default then.

  Default: false

transliterated_header_ids
: Transliterate the header text before generating the ID
  Only ASCII characters are used in headers IDs. This is not good for languages with many non-ASCII characters. By enabling this option the header text is transliterated to ASCII as good as possible so that the resulting header ID is more useful.

  The stringex library needs to be installed for this feature to work!

  Default: false

toc_levels
: Defines the levels that are used for the table of contents
  The individual levels can be specified by separating them with commas (e.g. 1,2,3) or by using the range syntax (e.g. 1..3). Only the specified levels are used for the table of contents.

  Default: 1..6

latex_headers
: Defines the LaTeX commands for different header levels
  The commands for the header levels one to six can be specified by separating them with commas.

  Default: section,subsection,subsubsection,paragraph,subparagraph,subparagraph

smart_quotes
: Defines the HTML entity names or code points for smart quote output
  The entities identified by entity name or code point that should be used for, in order, a left single quote, a right single quote, a left double and a right double quote are specified by separating them with commas.

  Default: lsquo,rsquo,ldquo,rdquo

template
: The name of an ERB template file that should be used to wrap the output or the ERB template itself.
  This is used to wrap the output in an environment so that the output can be used as a stand-alone document. For example, an HTML template would provide the needed header and body tags so that the whole output is a valid HTML file. If no template is specified, the output will be just the converted text.

  When resolving the template file, the given template name is used first. If such a file is not found, the converter extension (the same as the converter name) is appended. If the file still cannot be found, the templates name is interpreted as a template name that is provided by kramdown (without the converter extension). If the file is still not found, the template name is checked if it starts with ‘string://’ and if it does, this prefix is removed and the rest is used as template content.

  kramdown provides a default template named ‘document’ for each converter.

  Default: ''
