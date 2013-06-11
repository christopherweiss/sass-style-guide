SASS Style Guide
================

Best-practices and coding conventions for the [SASS](http://sass-lang.com) programming language.

This is a work-in-progress document which can be updated every time. You're welcome to improve this document.

# Table of Contents

* [The SASS Style Guide](#starting)
  * [Structure](#structure)
    * [directory](#directory)
    * [code](#code)
      * [logical paragraphs](#logical_paragraphs)
      * [class names](#class_names)
      * [variables](#variables)
      * [functions](#functions)
      * [extending](#extending)
      * [sprites](#sprites)
      * [comments](#comments)
      * [annotations](#annotations)
    * [Extensions](#extensions)
    * [Inspiration](#inspiration)

#Starting
* SASS is the prefered syntax
* Indentation is always 2 spaces
* Leave always the code better off than when you started
* Be consistent to yourself
* DRY
* If the code violates against the style guide, clean up it
 * it takes less than ~1h
 * only when you are not behind your task

#Structure
##directory
The files are in the ```$ASSETS_DIR/stylesheets``` and you have always a application.sass which controlls the includes.
The ```application``` directory contains all files which you are including in the ```application.sass```. The partials folder can contain folders like libs or something you want. Fundamental layouts and styles go in ```application/general```.

Example:

```
+-\stylesheets/
 +-\application/
   +-_base.css.sass
   +-_form.css.sass
   +-_generic.css.sass
   +-_grid.css.sass
   +-_helpers.css.sass
   +-_mixins.css.sass
   +-_sprites.css.sass
 
 +-application.css.sass
 +-ie.css.sass
 +-ie7.css.sass
 +-ie8.css.sass
 +-ie9.css.sass
 +-print.css.sass
```
##Code
###Logical Paragraphs
* Logical paragraphs should be grouped e.g.
```
.some-class
  @extend .bold

  +mixin_name()
  +second_mixin_name()

  font-size: 2em

  &.italic
    font-size: 2.4em

  div
    @extend .headline-space
```

###Class Names
* Classes are always hyphens ```.i-love-hyphens-class-names```

###Variables
* Variables are always underscore ```$grey_dark: #333333```
* Create partials which are for the main configurations e.g.
 * ```_grid``` which contains informations for the grid
 * ```_colors``` which contains all the colors
 * ```_sizes``` which contains all width, font sizes, etc.
* Add variables which will be repeated before the class names

```sass
$country_select_width: 180px
.wrapper
  > .country-select
    +font(medium)
    +uppercase()
    +navigation_shadow($black, 0, 0, 4px, 0px)
    width: $country_select_width
    position: relative
    cursor: pointer
    margin: 8px 10px 0 0
    border: 2px solid $white
    background: $white    
```

```sass
// Yes
$grey           : #666666
$grey_light     : #999999
$grey_dark      : #333333

// No
$grey: #666666
$grey_light: #999999
$grey_dark: #333333

```

###Functions
* Function names are always underscore
* use ```=``` instead of ```@mixin```
* use ```+``` instead of ```@include```

```sass
// Yes
=icons-sprite($name, $x: 0, $y: 0)
  +retina-sprite($name, $x, $y, $sprites, $sprites2x)

// No
@mixin icons-sprite($name, $x: 0, $y: 0)
  @include retina-sprite($name, $x, $y, $sprites, $sprites2x)
```
###Extending
* Never extend something that is already using an ```@extend```
* If using extend on selection deep on page or more than ```4 or 5``` times on the site, create a ```mixin```

###Sprites
* Use the [sprites](http://compass-style.org/reference/compass/utilities/sprites/) generator of compass

###Comments
* File header

```sass
// ****************************************************************
// *  @file helper
// *  @description css helper classes
// ****************************************************************
```
* Inline

```sass
// * Reset
header
  margin: 0
  max-width: inherit
  min-width: inherit
  height: 100%
```
* Functions description

```sass
/****************************************************************/
/* @description wrapper to get the image from the spritemap
/* @param {string} - image name
/* @param {integer} - x axis
/* @param {integer} - y axis
/****************************************************************/
=icons-sprite($name, $x: 0, $y: 0)
  +retina-sprite($name, $x, $y, $sprites, $sprites2x)
```
###Annotations
* TODO: describe missing functionality that should be added at a later date
* FIXME: describe broken code that must be fixed
* OPTIMIZE: describe code that is inefficient and may become a bottleneck
* HACK: describe the use of a questionable (or ingenious) coding practice
* REVIEW: describe code that should be reviewed to confirm implementation

#Extensions
* Feel free to use helper which makes your life easier
* [Compass](http://compass-style.org/)
* [Breakpoint](http://breakpoint-sass.com/)

#Inspiration
* [Sass doesn’t create bad code. Bad coders do.](http://thesassway.com/articles/sass-doesnt-create-bad-code-bad-coders-do)
* [idiomatic](https://github.com/rwldrn/idiomatic.js/) Styleguide
* [CoffeeScript](https://github.com/polarmobile/coffeescript-style-guide) Styleguide
