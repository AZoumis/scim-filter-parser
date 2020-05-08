# SCIM Filter Parser
> Parser for the SCIM ([IETF RFC 7644, System for Cross-domain Identity Management](https://tools.ietf.org/html/rfc7644)) filter syntax.

## Installation

This library is available as [composer](https://getcomposer.org/) package and this is the recommended way to install this library.

```sh
$ composer require cloudstek/scim-filter-parser
```

### Manual installation

If you don't use composer, you can install this library manually using the following steps:

1. Clone this repository or download the latest release from the [releases page](https://github.com/Cloudstek/scim-filter-parser/releases).
2. Require all files manually or use a PSR-4 autoloader (recommended).

## Usage

As code often says more than a thousand words, a little code to get you started.

```php
<?php

use Cloudstek\SCIM\FilterParser\FilterParser;

// Create the parser.
$parser = new FilterParser();

// Parse a filter string
$firstFilterAst = $parser->parse('userName eq "foobar"'); // Cloudstek\SCIM\FilterParser\AST\Comparison ...

// ... walk through the AST (abstract syntax tree) and do something with it.

// The parser is stateless so you can safely parse another filter if you like.
$secondFilterAst = $parser->parse('name[given eq "John" and family eq "Dough"]'); // Cloudstek\SCIM\FilterParser\AST\Conjunction ...
```

Documentation explaining the different AST nodes has yet to be written. For now, please see the unit tests in the [tests](./tests) directory for more examples or see the [IETF RFC 7644](https://tools.ietf.org/html/rfc7644#section-3.4.2.2) section 3.4.2.2 for more information about the filter syntax.

## Issues

Please report issues on the projects [GitHub issues page](https://github.com/Cloudstek/scim-filter-parser/issues) and be sure to include information about your PHP version, library version, filter string and resulting AST.

## Known limitations

At the moment there are a few limitations to be aware of, though in the future these may be addressed.

* Does not support SCIM v1.0 query filter syntax (only v2.0).
* Does not support parsing the `path` attribute for `PATCH` requests.
* Does not come with a "dumper" to provide a nice textual representation of the AST. Instead you can use [`var_dump`](https://www.php.net/manual/en/function.var-dump.php) or [`VarDumper`](https://symfony.com/doc/current/components/var_dumper.html).