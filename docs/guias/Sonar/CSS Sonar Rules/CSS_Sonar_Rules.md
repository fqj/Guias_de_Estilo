<style>
h1 {
    color:white;
    background:#7ab6df;
    width:100%;
    padding-left:0.5em;
    padding:auto;
    font-size:3em;
    font-weight:bold;
    letter-spacing:0.01em
 }
h2 {
    color:#7ab6df;
    background:#ffffff;
    font-weight:bold;
    width:100%;
    padding:5px;
    font-size:30px;
    letter-spacing:0.01em;
    border-bottom:1px solid #7ab6df!important;
    margin-top: 40px;
    margin-bottom:40px;
}
h3 {
    color:#7ab6df;
    background:#ffffff;
    width:100%;
    padding:3px;
    font-size:20px;
    font-weight:bold;
    border-bottom:1px solid #7ab6df!important;
    letter-spacing:0.01em;
}
pre {
    background:#e1f0fa!important;
    border: 1px solid #8ac6ef
}
code {
    color:#222;
    font-size:1em;
    font-weight:300;
}

blockquote {
    padding: 1em!important;
    color: #000!important;
    border-left: 0.25em solid #ce7206!important;
    background:#fbebc0;
}
ul {margin:1em}
li{margin:0.5em}
</style>

# CSS Sonar Rules 

## Parsing errors should be fixed

> The most important rule, as far as CSS Lint is concerned, is to ensure there are no parsing errors in the CSS. Parsing errors usually mean you mistyped a character and caused the code to become invalid CSS. These errors may cause the browser to drop a property or an entire rule. Parsing errors are always presented as errors by CSSLint, the most important issues to fix. 

## Possible Errors

> The following rules point out potential errors in your CSS.

1. [box-model](docs/box-model.md): Beware of box model size.
1. [display-property-grouping](docs/display-property-grouping.md): Require properties appropriate for display.
1. [duplicate-properties](docs/duplicate-properties.md): Disallow duplicate properties.
1. [empty-rules](docs/empty-rules.md): Disallow empty rules.
1. [known-properties](docs/known-properties.md): Require use of known properties.

## Compatibility

> The following rules flag for compatibility problems across browsers and browser settings.

1. [adjoining-classes](docs/adjoining-classes.md)[link](adjoining-classes.md) : Disallow adjoining classes.
1. [box-sizing](docs/box-sizing.md): Disallow box-sizing.
1. [compatible-vendor-prefixes](docs/compatible-vendor-prefixes.md): Require compatible vendor prefixes.
1. [gradients](docs/gradients.md): Require all gradient definitions.
1. [text-indent](docs/text-indent.md): Disallow negative text-indent.
1. [vendor-prefix](docs/vendor-prefix.md): Require standard property with vendor prefix.
1. [fallback-colors](docs/fallback-colors.md): Require fallback colors.
1. [star-property-hack](docs/star-property-hack.md): Disallow star hack.
1. [underscore-property-hack](docs/underscore-property-hack.md): Disallow underscore hack.
1. [bulletproof-font-face](docs/bulletproof-font-face.md): Bulletproof font-face. (new in v0.9.10)

<br><br>

## Performance

> The following rules are aimed at improving CSS performance, including runtime performance and overall code size.

1. [font-faces](docs/font-faces.md): Don't use too many web fonts.
1. [import](docs/import.md): Disallow @import.
1. [regex-selectors](docs/regex-selectors.md): Disallow selectors that look like regular expressions.
1. [universal-selector](docs/universal-selector.md): Disallow universal selector.
1. [unqualified-attributes](docs/unqualified-attributes.md): Disallow unqualified attribute selectors.
1. [zero-units](docs/zero-units.md): Disallow units for zero values.
1. [overqualified-elements](docs/overqualified-elements.md): Disallow overqualified elements.
1. [shorthand](docs/shorthand.md): Require shorthand properties.
1. [duplicate-background-images](docs/duplicate-background-images.md): Disallow duplicate background images.

## Maintainability & Duplication

> These rules help to ensure your code is readable and maintainable by others.

1. [floats](docs/floats.md): Disallow too many floats.
1. [font-sizes](docs/font-sizes.md): Don't use too many font-size declarations.
1. [ids](docs/ids.md): Disallow IDs in selectors.
1. [important](docs/important.md): Disallow !important.
1. [order-alphabetical](docs/order-alphabetical.md): Disallow non alphabetical.

## Accessibility

> These rules are designed to pick out possible accessibility issues.

1. [outline-none](docs/outline-none.md): Disallow outline:none.

## OOCSS

> These rules are based on the principles of OOCSS.

1. [qualified-headings](docs/qualified-headings.md): Disallow qualified headings.
1. [unique-headings](docs/unique-headings.md): Headings should only be defined once.

