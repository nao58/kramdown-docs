kramdown Parser
===============

Introduction
------------

This is the main parser of the kramdown library (as the name suggests). It parses text in kramdown syntax which is based on Markdown, a very easy to write, easy to read markup for writing HTML documents in plain text. Since the basic Markdown syntax has some shortcomings, implementations (especially the [PHP Markdown Extra](http://michelf.com/projects/php-markdown/extra/) package) have tried to overcome this shortcomings with additional syntax. The kramdown parser supports all features of the original Markdown syntax (albeit with some minor corrections) as well as newer features implemented in the [PHP Markdown Extra](http://michelf.com/projects/php-markdown/extra/) package and [Maruku](http://maruku.rubyforge.org/).

For a complete description of the implemented syntax, have a look at the [syntax page][kramdown Syntax], the [quick reference] provides a short overview.

HTML parsing
------------

The kramdown parser uses the HTML parser for parsing HTML tags. However, HTML tags are not converted to a native element representation by default, in contrast to the HTML parser. You need to set the option html_to_native to true to achieve this.

Options
-------

The kramdown parser supports the following options:

parse_block_html
: Process kramdown syntax in block HTML tags
  If this option is true, the kramdown parser processes the content of block HTML tags as text containing block-level elements. Since this is not wanted normally, the default is false. It is normally better to selectively enable kramdown processing via the markdown attribute.

  Default: false

parse_span_html
: Process kramdown syntax in span HTML tags
  If this option is true, the kramdown parser processes the content of span HTML tags as text containing span-level elements.

  Default: true

html_to_native
: Convert HTML elements to native elements
  If this option is true, the parser converts HTML elements to native elements. For example, when parsing <em>hallo</em> the emphasis tag would normally be converted to an :html element with tag type :em. If html_to_native is true, then the emphasis would be converted to a native :em element.

  This is useful for converters that cannot deal with HTML elements.

  Default: false
