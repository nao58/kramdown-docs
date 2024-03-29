GFM Parser
==========

Introduction
------------

This parser can parse ["Github Flavored Markdown"](https://help.github.com/articles/github-flavored-markdown). This is a format of Markdown that is used on Github.com for most places where textual input is required, such as issues and comments. Some of the extensions, notably the “backtick fenced code blocks” are also used on other sites, for example StackOverflow.

Conformance
-----------

At the moment this parser is identical to the kramdown parser, except that it adds support for fenced code blocks using three or more backticks and enforces hard line breaks in paragraphs.

Options
-------

The GFM parser supports the following options:

hard_wrap
: Interprets line breaks literally
  Insert HTML <br /> tags inside paragraphs where the original Markdown document had newlines (by default, Markdown ignores these newlines).

  Default: true
