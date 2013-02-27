# DOCUMENTATION

# Usage

## Settings

### $fontSize

The base font size.

**Default:** `1em`
**Accepts:** `em` or `px`

### $lineLength

The line length or measure. If you want to measure in characters, I suggest you divide the amount of characters you want with 1,5 and turn that into `em`s. For example, 45 characters -> `(45/1,5) * 1em = 30em`.

**Default:** `35em`
**Accepts:** `em` or `px`

### $xHeight

Multiplier for the final line height. Use this to fine tune the baseline.

**Default:** `1`
**Accepts:** unitless value

### $ratio

Ratio for Modular Scale. You can find a list of ratios [here](https://github.com/scottkellum/modular-scale#ratios). You can also use your own ratio such as `10/9`.

**Default:** `fifth()`
**Accepts:** Modular Scale ratio function or a ratio

### $headingLinesBefore

Multiplier for headings' spacing above. The value to be multiplied is the calculated line height of the heading.

**Default:** `1`
**Accepts:** number

### $headingLinesAfter

Multiplier for headings' spacing below. The value to be multiplied is the calculated line height of the heading.

**Default:** `0`
**Accepts:** number

### $headingBaselineShift

The amount of baseline shift for all headings. Will be applied using `position: relative` and `top: -$headingBaselineShift`

**Default:** `0em`
**Accepts:** `em`

### $h[1-6]LinesBefore

Multiplier for a specific heading's spacing above. The value to be multiplied is the calculated line height of the heading.

**Default:** `$headingLinesBefore`
**Accepts:** number

### $h[1-6]LinesAfter

Multiplier for a specific heading's spacing below. The value to be multiplied is the calculated line height of the heading.

**Default:** `$headingLinesAfter`
**Accepts:** number

### $h[1-6]BaselineShift

The amount of baseline shift for a specific heading. Will be applied using `position: relative` and `top: -$headingBaselineShift`

**Default:** `$headingBaselineShift`
**Accepts:** `em`

### $pixelSnapBaseSize

A boolean deciding whether the $fontSize value you give TypeUp is pixel snapped.

**Default:** `true`
**Accepts:** `boolean`

### $baseFontSize

The browser base font size that TypeUp does its calculations from. You shouldn't have to change this.

**Default:** `16px`
**Accepts:** `px`

### $minimumLineHeight

The minimum line height that TypeUp sets for any element. Unless you're working with some funky typesetting, you don't need to change this.

**Default:** `0.7`
**Accepts:** `number`

### $doubleStrandedHeadingClasses

If true, will clone each headings styles into a corresponding .headingN cllass using @extend. This would get you classes like .heading2, .heading3 that you can use to style text without giving it a semantic heading element type.

**Default:** `false`
**Accepts:** `boolean`

### $startModularScaleAt

The modular scale number that is assigned to h1. Next one gets 3, next one gets 2, etc. The modular scale cuts off at 0, so with the default settings h5 and h6 get a modular scale number of 0.

**Default:** `4`
**Accepts:** `number`

## Mixins

### typeup-body()

	@include typeup-body($fontSize, $lineLength, $xHeight);

The typeup-body mixin should be included by itself, not under any selector. If you do not supply any arguments, they will be fetched from the settings variables.

### typeup-container()

	@include typeup-container($fontSize, $lineLength, $xHeight);

The typeup-container mixin should be used when you want the rules to apply only inside a specific element. It should be included inside a selector. This mixin also establishes the width of the element with $lineLength.

If you do not supply any arguments, they will be fetched from the settings variables.

### typeup-spacer()

	@include typeup-spacer(
	    $size-in-ems,
	    $before: $headingLinesBefore, // uses default value if not supplied
	    $after: $headingLinesAfter, // uses default value if not supplied
	    $baselineShift: $headingBaselineShift, // optional
	    $overrideSpacingWithBaseline: $overrideSpacingWithBaseline // uses default value if not supplied
    );

The spacer mixin is used to give vertical rhythm to headings inside TypeUp, but you can use it for other things.

This is how it works:

See how many baselines are needed to meet $size-in-ems, in half increments
Multiply by the global line height, pixel snap it
Multiply that number with before to get margin-top and after to get margin-bottom
Apply baseline shift if larger than 0 em with position:relative and top
If $overrideSpacingWithBaseline is true (default is false), the before and after values are multiplied by the global line height instead of the calculated one.

You could use the mixin to make simple paragraphs: @include typeup-spacer($fontSize, 0, 1, 0, false); which would apply a line-height and some margin to the bottom. Or any other element where you have a differing font size - line height will be adjusted correctly.