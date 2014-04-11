HTML Converter
==============

Introduction
------------

This converter converts a kramdown element tree into an HTML fragment and supports all available element types. Below is a list of additional features of the HTML converter as well as some additional information.

Automatic Generation of Header IDs
----------------------------------

kramdown supports the automatic generation of header IDs if the option auto_ids is set to true (which is the default). This is done by converting the untransformed, i.e. plain, header text (or, if the option auto_id_stripping is set, only the text from real text elements) via the following steps:

* All characters except letters, numbers, spaces and dashes are removed.
* All characters from the start of the line until the first letter are removed.
* Everything except letters and numbers is converted to dashes.
* Everything is lowercased.
* If nothing is left, the identifier section is used.
* If a such created identifier already exists, a dash and a sequential number is added (first -1, then -2 and so on).

Note that the option auto_id_stripping will be removed in version 2.0 because this will be the default behaviour!

Following are some examples of header texts and their respective generated IDs:

|---------------------------+--------------------+-------------------------------------|
| Sample header             | generated ID       | generated ID with auto_id_stripping |
|---------------------------+--------------------+-------------------------------------|
| # This is a header        | this-is-a-header   | this-is-a-header                    |
| ## 12. Another one 1 here | another-one-1-here | another-one-1-here                  |
| ### Do ^& it now          | do–it-now          | do–it-now                           |
| # Hallo                   | hallo              | hallo                               |
| # Hallo                   | hallo-1            | hallo-1                             |
| # 123456789               | section            | section                             |
| # <i>test</i>             | itesti             | test                                |
|---------------------------+--------------------+-------------------------------------|


The automatic creation of header IDs is not part of standard Markdown. The rules on how header text is converted to an identifier are based on the rules specified by Pandoc.
{: .diff-standard-markdown}

Such generated IDs are only used if no ID has been set manually before.

Code Blocks
-----------

A code block is wrapped in both <pre> and <code> tags.

### Showing Whitespace in a Code Block

It is sometimes useful to visualize whitespace within a code block. This can be achieved by adding the class show-whitespaces to a code block (using a [block IAL][kramdown Syntax - Block Inline Attribute Lists]).

Here is an example where the whitespaces are shown:

~~~
  ⋅⋅leading⋅tab and⋅space
trailing⋅⋅⋅tab⋅and⋅space⋅⋅⋅⋅  
~~~

When showing whitespace in a code block, all spaces are replaced with the entity &sdot; and additionally spaces and tabs in the code block are marked up using HTML span tags and the following CSS classes:

* ws-space-l, ws-tab-l: leading spaces/tabs
* ws-space-r, ws-tab-r: trailing spaces/tabs
* ws-space, ws-tab: spaces/tabs in between

Automatic Syntax Highlighting
-----------------------------

kramdown supports setting a code language for code blocks and code spans, see [Language of Code Blocks][kramdown Syntax - Language of Code Blocks]. This language will be used for highlighting code blocks and spans.

Syntax highlighting for text is done using the [CodeRay](http://coderay.rubychan.de/) library which can be installed, for example, via Rubygems (the gem name is coderay). Have a look at the CodeRay homepage to see all supported languages.

Note that syntax highlighting won’t work unless the CodeRay library is installed!
{: .notes}

Here is an example on how Ruby code is highlighted:

~~~ruby
require 'kramdown'

Kramdown::Document.new('* something').to_html
puts 1 + 1
~~~

You can set the option enable_coderay to false to completely disable this feature, leaving a clean source.

Math Support
------------

If you want math formulas to be correctly displayed, you have to include the [MathJax](http://www.mathjax.org/) javascript library in the HTML file (see the [MathJax homepage](http://www.mathjax.org/) for details). Note that kramdown does not ship with the MathJax library and that therefore the default template does not include a link to it!

Why MathJax? Because I think that it is simply the best way to display LaTeX math formulas on the Web. It is easy to install and use and works on all modern browsers.

Emphasis
--------

kramdown uses the HTML element em to style light and the element strong to style strong emphasized text parts.

Automatic “Table of Contents” Generation
----------------------------------------

kramdown supports the automatic generation of the table of contents of all headers that have an ID set. Just assign the reference name “toc” to an ordered or unordered list by using an IAL and the list will be replaced with the actual table of contents, rendered as nested unordered lists if “toc” was applied to an unordered list or else as nested ordered lists. All attributes applied to the original list will also be applied to the generated TOC list and it will get an ID of markdown-toc if no ID was set.

When the auto_ids option is set, all headers will appear in the table of contents as they all will have an ID. Assign the class name “no_toc” to a header to exclude it from the table of contents.

Here is an example:

~~~
# Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

# H1 header

## H2 header
~~~

Options
-------

The HTML converter supports the following options:

auto_ids
: Use automatic header ID generation
  If this option is true, ID values for all headers are automatically generated if no ID is explicitly specified.

  Default: true

auto_id_prefix
: Prefix used for automatically generated header IDs
  This option can be used to set a prefix for the automatically generated header IDs so that there is no conflict when rendering multiple kramdown documents into one output file separately. The prefix should only contain characters that are valid in an ID!

  Default: ‘’

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

template
: The name of an ERB template file that should be used to wrap the output or the ERB template itself.
  This is used to wrap the output in an environment so that the output can be used as a stand-alone document. For example, an HTML template would provide the needed header and body tags so that the whole output is a valid HTML file. If no template is specified, the output will be just the converted text.

  When resolving the template file, the given template name is used first. If such a file is not found, the converter extension (the same as the converter name) is appended. If the file still cannot be found, the templates name is interpreted as a template name that is provided by kramdown (without the converter extension). If the file is still not found, the template name is checked if it starts with ‘string://’ and if it does, this prefix is removed and the rest is used as template content.

  kramdown provides a default template named ‘document’ for each converter.

  Default: ‘’

footnote_nr
: The number of the first footnote
  This option can be used to specify the number that is used for the first footnote.

  Default: 1

entity_output
: Defines how entities are output
  The possible values are :as_input (entities are output in the same form as found in the input), :numeric (entities are output in numeric form), :symbolic (entities are output in symbolic form if possible) or :as_char (entities are output as characters if possible, only available on Ruby 1.9).

  Default: :as_char

smart_quotes
: Defines the HTML entity names or code points for smart quote output
  The entities identified by entity name or code point that should be used for, in order, a left single quote, a right single quote, a left double and a right double quote are specified by separating them with commas.

  Default: lsquo,rsquo,ldquo,rdquo

toc_levels
: Defines the levels that are used for the table of contents
  The individual levels can be specified by separating them with commas (e.g. 1,2,3) or by using the range syntax (e.g. 1..3). Only the specified levels are used for the table of contents.

  Default: 1..6

enable_coderay
: Use coderay for syntax highlighting
  If this option is true, coderay is used by the HTML converter for syntax highlighting the content of code spans and code blocks.

  Default: true

coderay_wrap
: Defines how the highlighted code should be wrapped
  The possible values are :span, :div or nil.

  Default: :div

coderay_line_numbers
: Defines how and if line numbers should be shown
  The possible values are :table, :inline or nil. If this option is nil, no line numbers are shown.

  Default: :inline

coderay_line_number_start
: The start value for the line numbers

  Default: 1

coderay_tab_width
: The tab width used in highlighted code

coderay_bold_every
: Defines how often a line number should be made bold
  Can either be an integer or false (to turn off bold line numbers completely).

  Default: 10

coderay_css
: Defines how the highlighted code gets styled
  Possible values are :class (CSS classes are applied to the code elements, one must supply the needed CSS file) or :style (default CSS styles are directly applied to the code elements).

  Default: style

coderay_default_lang
: Sets the default language for highlighting code blocks
  If no language is set for a code block, the default language is used instead. The value has to be one of the languages supported by coderay or nil if no default language should be used.

  Default: nil
