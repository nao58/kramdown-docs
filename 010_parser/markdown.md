Markdown Parser
===============

This parser parses text in [Markdown](http://daringfireball.net/projects/markdown/) format. It is based on the [kramdown parser] and just removes the functionality for parsing the additional markup that the kramdown syntax supports. Since some things are handled differently by the kramdown parser (like deciding when a list item contains just text), this parser differs from real Markdown parsers in some minor respects.

Note, though, that the parser basically fails just one of the Markdown test cases (some others also fail but those failures are negligible).
