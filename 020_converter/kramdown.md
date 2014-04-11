kramdown Converter
==================

Introduction
------------

This converter converts a kramdown element tree into a kramdown document and supports all available element types. This converter, together with the [HTML parser], can be used to convert HTML documents to kramdown documents.

Another use would be to format a badly styled kramdown document (i.e. one with wrapped lines, multiple different indentations used in one list, …).

Options
-------

The kramdown converter supports the following options:

entity_output
: Defines how entities are output
  The possible values are :as_input (entities are output in the same form as found in the input), :numeric (entities are output in numeric form), :symbolic (entities are output in symbolic form if possible) or :as_char (entities are output as characters if possible, only available on Ruby 1.9).

  Default: :as_char

template
: The name of an ERB template file that should be used to wrap the output or the ERB template itself.
  This is used to wrap the output in an environment so that the output can be used as a stand-alone document. For example, an HTML template would provide the needed header and body tags so that the whole output is a valid HTML file. If no template is specified, the output will be just the converted text.

  When resolving the template file, the given template name is used first. If such a file is not found, the converter extension (the same as the converter name) is appended. If the file still cannot be found, the templates name is interpreted as a template name that is provided by kramdown (without the converter extension). If the file is still not found, the template name is checked if it starts with 'string://' and if it does, this prefix is removed and the rest is used as template content.

  kramdown provides a default template named 'document' for each converter.

  Default: ''
