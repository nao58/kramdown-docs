Available Options
=================

The behaviour of kramdown can be adjusted via the available options. Below is a list of all currently available options. Have a look at the documentation of a converter or parser to see directly which options they support!

auto_id_prefix
: Prefix used for automatically generated header IDs
  This option can be used to set a prefix for the automatically generated header IDs so that there is no conflict when rendering multiple kramdown documents into one output file separately. The prefix should only contain characters that are valid in an ID!

  Default: ''

auto_id_stripping
: Strip all formatting from header text for automatic ID generation
  If this option is true, only the text elements of a header are used for generating the ID later (in contrast to just using the raw header text line).

  This option will be removed in version 2.0 because this will be the default then.

  Default: false

auto_ids
: Use automatic header ID generation
  If this option is true, ID values for all headers are automatically generated if no ID is explicitly specified.

  Default: true

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

coderay_line_number_start
: The start value for the line numbers

  Default: 1

coderay_line_numbers
: Defines how and if line numbers should be shown
  The possible values are :table, :inline or nil. If this option is nil, no line numbers are shown.

  Default: :inline

coderay_tab_width
: The tab width used in highlighted code

coderay_wrap
: Defines how the highlighted code should be wrapped
  The possible values are :span, :div or nil.

  Default: :div

enable_coderay
: Use coderay for syntax highlighting
  If this option is true, coderay is used by the HTML converter for syntax highlighting the content of code spans and code blocks.

  Default: true

entity_output
: Defines how entities are output
  The possible values are :as_input (entities are output in the same form as found in the input), :numeric (entities are output in numeric form), :symbolic (entities are output in symbolic form if possible) or :as_char (entities are output as characters if possible, only available on Ruby 1.9).

  Default: :as_char

footnote_nr
: The number of the first footnote
  This option can be used to specify the number that is used for the first footnote.

  Default: 1

hard_wrap
: Interprets line breaks literally
  Insert HTML <br /> tags inside paragraphs where the original Markdown document had newlines (by default, Markdown ignores these newlines).

  Default: true

header_offset
: Sets the output offset for headers
  If this option is c (may also be negative) then a header with level n will be output as a header with level c+n. If c+n is lower than 1, level 1 will be used. If c+n is greater than 6, level 6 will be used.

  Default: 0

html_to_native
: Convert HTML elements to native elements
  If this option is true, the parser converts HTML elements to native elements. For example, when parsing <em>hallo</em> the emphasis tag would normally be converted to an :html element with tag type :em. If html_to_native is true, then the emphasis would be converted to a native :em element.

  This is useful for converters that cannot deal with HTML elements.

  Default: false

latex_headers
: Defines the LaTeX commands for different header levels
  The commands for the header levels one to six can be specified by separating them with commas.

  Default: section,subsection,subsubsection,paragraph,subparagraph,subparagraph

line_width
: Defines the line width to be used when outputting a document

  Default: 72

link_defs
: Pre-defines link definitions
  This option can be used to pre-define link definitions. The value needs to be a Hash where the keys are the link identifiers and the values are two element Arrays with the link URL and the link title.

  If the value is a String, it has to contain a valid YAML hash and the hash has to follow the above guidelines.

  Default: {}

parse_block_html
: Process kramdown syntax in block HTML tags
  If this option is true, the kramdown parser processes the content of block HTML tags as text containing block-level elements. Since this is not wanted normally, the default is false. It is normally better to selectively enable kramdown processing via the markdown attribute.

  Default: false

parse_span_html
: Process kramdown syntax in span HTML tags
  If this option is true, the kramdown parser processes the content of span HTML tags as text containing span-level elements.

  Default: true

remove_block_html_tags
: Remove block HTML tags
  If this option is true, the RemoveHtmlTags converter removes block HTML tags.

  Default: true

remove_span_html_tags
: Remove span HTML tags
  If this option is true, the RemoveHtmlTags converter removes span HTML tags.

  Default: false

smart_quotes
: Defines the HTML entity names or code points for smart quote output
  The entities identified by entity name or code point that should be used for, in order, a left single quote, a right single quote, a left double and a right double quote are specified by separating them with commas.

  Default: lsquo,rsquo,ldquo,rdquo

template
: The name of an ERB template file that should be used to wrap the output or the ERB template itself.
  This is used to wrap the output in an environment so that the output can be used as a stand-alone document. For example, an HTML template would provide the needed header and body tags so that the whole output is a valid HTML file. If no template is specified, the output will be just the converted text.

  When resolving the template file, the given template name is used first. If such a file is not found, the converter extension (the same as the converter name) is appended. If the file still cannot be found, the templates name is interpreted as a template name that is provided by kramdown (without the converter extension). If the file is still not found, the template name is checked if it starts with ‘string://’ and if it does, this prefix is removed and the rest is used as template content.

  kramdown provides a default template named 'document' for each converter.

  Default: ''

toc_levels
: Defines the levels that are used for the table of contents
  The individual levels can be specified by separating them with commas (e.g. 1,2,3) or by using the range syntax (e.g. 1..3). Only the specified levels are used for the table of contents.

  Default: 1..6

transliterated_header_ids
: Transliterate the header text before generating the ID
  Only ASCII characters are used in headers IDs. This is not good for languages with many non-ASCII characters. By enabling this option the header text is transliterated to ASCII as good as possible so that the resulting header ID is more useful.

  The stringex library needs to be installed for this feature to work!

  Default: false
