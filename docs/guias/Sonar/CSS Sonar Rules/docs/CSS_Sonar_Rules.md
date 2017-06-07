## Parsing errors should be fixed

The most important rule, as far as CSS Lint is concerned, is to ensure there are no parsing errors in the CSS. Parsing errors usually mean you mistyped a character and caused the code to become invalid CSS. These errors may cause the browser to drop a property or an entire rule. Parsing errors are always presented as errors by CSSLint, the most important issues to fix. 

## Possible Errors

The following rules point out potential errors in your CSS.

1. [box-model](box-model.md): Beware of box model size.
1. [display-property-grouping](display-property-grouping.md): Require properties appropriate for display.
1. [duplicate-properties](duplicate-properties.md): Disallow duplicate properties.
1. [empty-rules](empty-rules.md): Disallow empty rules.
1. [known-properties](known-properties.md): Require use of known properties.

## Compatibility

The following rules flag for compatibility problems across browsers and browser settings.

1. [adjoining-classes](adjoining-classes.md) : Disallow adjoining classes.
1. [box-sizing](box-sizing.md): Disallow box-sizing.
1. [compatible-vendor-prefixes](compatible-vendor-prefixes.md): Require compatible vendor prefixes.
1. [gradients](gradients.md): Require all gradient definitions.
1. [text-indent](text-indent.md): Disallow negative text-indent.
1. [vendor-prefix](vendor-prefix.md): Require standard property with vendor prefix.
1. [fallback-colors](fallback-colors.md): Require fallback colors.
1. [star-property-hack](star-property-hack.md): Disallow star hack.
1. [underscore-property-hack](underscore-property-hack.md): Disallow underscore hack.
1. [bulletproof-font-face](bulletproof-font-face.md): Bulletproof font-face. (new in v0.9.10)

## Performance

The following rules are aimed at improving CSS performance, including runtime performance and overall code size.

1. [font-faces](font-faces.md): Don't use too many web fonts.
1. [import](import.md): Disallow @import.
1. [regex-selectors](regex-selectors.md): Disallow selectors that look like regular expressions.
1. [universal-selector](universal-selector.md): Disallow universal selector.
1. [unqualified-attributes](unqualified-attributes.md): Disallow unqualified attribute selectors.
1. [zero-units](zero-units.md): Disallow units for zero values.
1. [overqualified-elements](overqualified-elements.md): Disallow overqualified elements.
1. [shorthand](shorthand.md): Require shorthand properties.
1. [duplicate-background-images](duplicate-background-images.md): Disallow duplicate background images.

## Maintainability & Duplication

These rules help to ensure your code is readable and maintainable by others.

1. [floats](floats.md): Disallow too many floats.
1. [font-sizes](font-sizes.md): Don't use too many font-size declarations.
1. [ids](ids.md): Disallow IDs in selectors.
1. [important](important.md): Disallow !important.
1. [order-alphabetical](order-alphabetical.md): Disallow non alphabetical.

## Accessibility

These rules are designed to pick out possible accessibility issues.

1. [outline-none](outline-none.md): Disallow outline:none.

## OOCSS

These rules are based on the principles of OOCSS.

1. [qualified-headings](qualified-headings.md): Disallow qualified headings.
1. [unique-headings](unique-headings.md): Headings should only be defined once.

