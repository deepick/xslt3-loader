# xslt3-loader for Webpack

This Web loader can load XSLT stylesheets using [Saxon-JS
2](https://www.saxonica.com/saxon-js/documentation/index.html).  The
compiler is called to convert the stylesheet into the SEF format.  The
result will be a module exporting a single variable, `stylesheet`,
which can then be imported into the frontend application and used by
Saxon-JS 2.  At this point, only the free (XX) compiler is supported.
The name of the exported variable cannot be changed, as it can be
changed during import.

## Installation

Before using this loader, the xslt3 command line utility needs to be
installed on the local system using

    npm install -g xslt3

## Usage

In your `module.rules` section of `webpack.config.js`, add a rule like
so:

    {
        test: /\.xsl$/,
        use: [ 'xslt3-loader' ]
    }

In your application source, you can then import a stylesheet like so:

    import { stylesheet as myStylesheet } from './my-stylesheet.xsl';

The stylesheet can then be used in invokations to Saxon-JS 2 like so:

    import { stylesheet as example } from '../example.xsl';

    console.log(SaxonJS.transform({ stylesheetInternal: example,
                                    sourceText: '<foo>bar</foo>',
                                    destination: 'serialized' }).principalResult);
