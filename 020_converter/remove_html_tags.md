RemoveHtmlTags Converter
========================

Introduction
------------

This converter modifies a kramdown element tree and conditionally removes all block and/or span HTML elements, XML processing instructions and style as well as script tags from it. The resulting element tree should in most cases only contain “native” kramdown elements and is therefore better suited for converters that do not output HTML (like the [kramdown converter] or the [latex converter]).

A sample usage may be the following to convert a full HTML document (i.e. one that includes the HTML doctype, the HTML head section, …) into a kramdown document:

~~~
kramdown -i html -o remove_html_tags,kramdown my_document.html
~~~

Options
-------

The RemoveHtmlTags converter supports the following options:

remove_block_html_tags
: Remove block HTML tags
  If this option is true, the RemoveHtmlTags converter removes block HTML tags.

  Default: true

remove_span_html_tags
: Remove span HTML tags
  If this option is true, the RemoveHtmlTags converter removes span HTML tags.

  Default: false
