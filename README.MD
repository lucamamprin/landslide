# Landslide CSS grid system

**Superclean, powerful, responsive, Sass-based, BEM-syntax CSS grid system forked from Avalanche.**

## Why use Landslide?

- No bloat. Only create the selectors you'll actually use.
- No duplication: `.col-1-2` is the same as `.col-2-4`, so why create two selectors?
- No floats. No clears. No .last
- Flexible, configurable naming conventions.
- Nesting to infinity and beyond.
- Real-world breakpoint naming. 'thumb', 'handheld' and 'desk'; not 'xs', 'md' and 'xl'.
- Integrated media query mixin. Connect your media queries to your grid breakpoints.

## What are the differences from Avalanche?
- This fork implements a Flexbox grid by using the `@supports` CSS at-rule on top of the original `inline-block` based grid from Avalanche.
- Added `rtl` support for better localization. (Yes, even the reverse grid works!)
- Removed the `fraction` option from the code, to avoid issues in compilation with dart-sass and some other compilers.
- Tired of manually setting margins and paddings? Now you can set `$ls-enable-grid-spacers` to `true` to compile tons of customizable utilities.
- Want to add `display: none` or `block`, but only for specific elements and media queries? Set `$ls-enable-displays` to `true` and avoid code repetition by using the Displays pluggable classes.

## Installation
1. Type `yarn add lucamamprin/landslide` if you use yarn or `npm install lucamamprin/landslide --save` if you use NPM
2. Import `~/landslide/src/_landslide.scss` in your SCSS or grab the compiled file;
3. Override settings to fit your requirements or use the defaults;
4. Compile and enjoy!

## Usage

Example of a two column, responsive, centered grid. All grid layout classes and responsive width classes are modifiers.

```
<div class="grid grid--center">
  <div class=".col-3-4 .col-1-2--thumb grid__cell"></div>
  <div class=".col-1-4 .col-1-2--thumb grid__cell"></div>
</div>
```

## Settings

**`$ls-namespace`**
Global prefix for layout and cell class names. Default: `grid`.

**`$ls-element-name`**
Element (in a BEM context) or grid cell name. Default: `cell`.

**`$ls-element-class-chain`**
Chain characters/separator between BEM block and element. Default: `__`.

**`$ls-modifier-class-chain`**
Chain characters/separator between BEM block and modifier. Default: `--`.

**`$ls-breakpoint-class-chain`**
Chain characters/separator between width class and breakpoint. Default: `--`.

**`$ls-gutter`**
Gutter width between cells. Default: `20px`.

**`$ls-width-class-namespace`**
Prefix for width class names. Default: `''`.

**`$ls-width-class-style`**
Naming style of width classes. Default: `'fragment'`. Options: `percentage` (25, 50 etc), `fragment` (1-of-3, 4-of-5 etc).

*N.B. If using percentage then `$ls-width-class-namespace` (Default: `$ls-element-name + '-'`) above cannot be null. Landslide escapes leading integers for fraction and fragment naming styles but this isn't possible with percentage style as Sass attempts to escape the whole number (e.g. 50 instead of just 5 or 30 instead of just 3) so fails*.

**`$ls-widths`**
Sass list of width denominator values (when expressed as a fraction). For example, 2 produces 1/2 width class, 3 produces 1/3 and 2/3 width classes etc. Default: `( 2, 3, 4 )`.

*N.B. This setting has a large impact on the size of your compiled CSS. Avoid bloat by inputting just the numbers you'll use.*

**`$ls-enable-responsive`**
Enable/disable the inclusion of responsive width classes. With this enabled, class names (for denominators set above) will be created for each of your breakpoint aliases (set below). Default: `true`.

**`$ls-breakpoints`**
Sass map of responsive breakpoint aliases and associated media queries (in key-value pairs).

*N.B. This setting has a large impact on the size of your compiled CSS. Avoid bloat by inputting just the breakpoints you'll use.*
Default:
```
(
  "thumb":            "screen and (max-width: 499px)",
  "handheld":         "screen and (min-width: 500px) and (max-width: 800px)",
  "handheld-and-up":  "screen and (min-width: 500px)",
  "pocket":           "screen and (max-width: 800px)",
  "lap":              "screen and (min-width: 801px) and (max-width: 1024px)",
  "lap-and-up":       "screen and (min-width: 801px)",
  "portable":         "screen and (max-width: 1024px)",
  "desk":             "screen and (min-width: 1025px)",
  "widescreen":       "screen and (min-width: 1160px)",
  "retina":           "screen and (-webkit-min-device-pixel-ratio: 2), screen and (min-resolution: 192dpi), screen and (min-resolution: 2dppx)"
)
```

**`$ls-base-spacer`**
Pixel or rem value for the margin and padding utilities. Default: `$ls-gutter`.

**`$ls-enable-grid-spacers-breakpoints`**
Enable responsive spacers (example: margin bottom only above or below a certain breakpoint). Default: `$ls-enable-responsive`
*N.B. This setting has a huge impact on the size of your compiled CSS. Avoid bloat by using PostCSS to remove the utilities you don't use.*

**`$ls-spacers`**
Sass map of sizes for the margin and padding utilities. Default:

```
  (
    0: 0,
    1: $ls-base-spacer * 0.25,
    2: $ls-base-spacer * 0.5,
    3: $ls-base-spacer,
    4: $ls-base-spacer * 1.5,
    5: $ls-base-spacer * 2,
  )
```

**`$ls-enable-displays-breakpoints`**
Enable responsive display utilities (example: element is a flex container above or below a certain media query). Default: `$ls-enable-responsive`
*N.B. This setting has a minimal impact on the size of your compiled CSS.*

**`$ls-displays`**
Sass map of display values that will generate the Displays utilities. Default:

```
  (
    none,
    block,
    inline-block,
    flex,
  );
```

## Grid layouts

Apply as modifier classes to your base `grid` element. For example; `<div class="grid grid--center">`.

All optionable grid layouts listed below are switched off by default. Set to `true` to enable.

**`$ls-enable-grid-center`**
All cells are horizontally centered within the container.

**`$ls-enable-grid-cell-center`**
Center an individual grid cell within the container.
*N.B. Class should be applied to an individual cell, not the grid container. For example; `<div class="grid__cell grid__cell--center">`.*

**`$ls-enable-grid-right`**
All cells are horizontally aligned to the right within the container.

**`$ls-enable-grid-middle`**
All cells are vertically centered within in the container.

**`$ls-enable-grid-bottom`**
All cells are vertically aligned to the bottom of the container.

**`$ls-enable-grid-flush`**
Gutters removed between cells.

**`$ls-enable-grid-tiny`**
Gutters between cells set to a quarter of the global gutter value. Default: `5px`.

**`$ls-enable-grid-small`**
Gutters between cells set to half of the global gutter value. Default: `10px`.

**`$ls-enable-grid-medium`**
Gutters between cells set to the global gutter value. Default: `20px`.

**`$ls-enable-grid-large`**
Gutters between cells set to double the global gutter value. Default: `40px`.

**`$ls-enable-grid-huge`**
Gutters between cells set to quadruple the global gutter value. Default: `80px`.

**`$ls-enable-grid-auto`**
All cells take up an unspecified width set by their content.

**`$ls-enable-grid-rev`**
Grid cells are displayed in the opposite of their source order.

**`$ls-enable-flex`**
Enable flexbox functionalities in the grid. Set to `false` to debug the `inline-block` grid, or if you don't want flexbox.  Default: `true`.

**`$ls-enable-rtl`**
Enable RTL layout support. Default: `true`.

**`$ls-enable-grid-spacers`**
Enable margin and padding utilities. Default: `false`.

**`$ls-enable-displays`**
Enable displays utilities. Default: `false`.

**`$ls-grids-sizes`**
Sass map that will be used to loop the grids.
The first value corresponds to the boolean that enables/disables the grid size (see "Grid Layouts"); the second value is the name of the size; third value is true if the loop will have to divide or multiply by the fourth value.
 Default:
```
(
    ($ls-enable-grid-tiny, 'tiny', true, 4),
    ($ls-enable-grid-small, 'small', true, 2),
    ($ls-enable-grid-medium, 'medium', false, 1),
    ($ls-enable-grid-large, 'large', false, 2),
    ($ls-enable-grid-huge, 'huge', false, 4),
);
```


## Media query

Landslide includes a media query mixin that makes use of the breakpoint aliases you set. This enables better coupling between your grid and other responsive content items. Usage as follows.

```
@include ls-mq(pocket){
  .content-item{
    /* responsive CSS */
  }
}
```

## Browser support

All modern browsers are supported and Internet Explorer from IE9 upwards. If IE8 support is required then all that is needed is a pixel-value to be set for `font-size` on `.grid__cell`. This is due to IE8 not supporting rem units. Use of a 'rem-to-px' check during build is recommended.

## Contributing

When issuing a pull request to improve this project, please:

1. Rigourously comment your code, particularly where new variables are introduced or manipulated
2. Be as descriptive as possible in your commit message

## F.A.Q.

### Why implement Flexbox on top of Avalanche?
In short, progressive enhancement. Avalanche is excellent to support older or less used browsers around the world, however `inline-block` can only get so far - for example, you can't have equal-width columns (see `grid--auto`).
Users with more modern browsers and devices should be able to enjoy the feature Flexbox provides.

### Why was @supports used instead of just writing Flexbox code?
The at-rule was used to avoid IE11 and older versions that do support flexbox, but with a [plethora of bugs](https://github.com/philipwalton/flexbugs).

[These old browsers](https://caniuse.com/#feat=css-featurequeries) just won't parse the CSS written inside of @supports, and will use the `inline-block` based grid instead.

### IE 11 doesn't look the same as [insert modern browser here], how come?
You will find a situation like this, like when using `grid--auto`. This is because these IE is not using Flexbox, while the modern browser is - *they're not supposed to act or look the same!*

IE (especially 11) just has too many bugs while trying to use Flexbox, and the solutions to "fix" these bugs don't look nice. As an example, `align-items: center` won't work unless you set a fixed height, either through JS or CSS.

In short, it's just not worth it to write bloat. IE users won't see the same exact layout as Chrome or Firefox - **because the alternative is much worse**.

### Why no CSS Grid?
CSS Grid is way too different from the more "traditional" approach to Avalanche/Landslide to be implemented in a sensible way.

## Questions

If you have any questions or need some help then feel free to [open an issue](https://github.com/lucamamprin/landslide/issues/new).
