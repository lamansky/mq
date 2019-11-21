# mq

A library of media query mixins for [Sass](https://sass-lang.com/).

## Installation and Usage

If you have [Node.js](https://nodejs.org/en/) installed, you can add this module to your project using npm:

```bash
npm i @lamansky/mq
```

Assuming you’re using [webpack](https://webpack.js.org/) for your project, include the module into your own Sass/SCSS stylesheet like so:

```scss
@use "~@lamansky/mq";
```

## Functions

The `mq` library includes three functions.

### dark

Tests for a [dark-mode media query](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme).

```scss
@use "~@lamansky/mq";

body {
  background: white;
  color: black;

  @include mq.dark {
    background: black;
    color: white;
  }
}
```

This function also adds the classes necessary for a manual JavaScript-powered dark-mode/light-mode toggle. The default settings are:

```scss
@use "~@lamansky/mq" with (
  $color-scheme-override-root: 'html',
  $dark-class: 'dark-mode',
  $default-color-class: 'default-color-mode',
  $light-class: 'light-mode',
);
```

With these defaults, your dark-mode styles can be triggered by adding a `dark-mode` class to the `html` element.

If the dark-mode styles are already active as a result of the media query, the dark-mode styles can be manually disabled by adding a `light-mode` or `default-color-mode` class to the `html` element.

### light

Tests for a [light-mode media query](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme) (useful for stylesheets that go with a dark default).

```scss
@use "~@lamansky/mq";

body {
  background: black;
  color: white;

  @include mq.light {
    background: white;
    color: black;
  }
}
```

This function also adds the classes necessary for a manual JavaScript-powered light-mode/dark-mode toggle. The default settings for this are:

```scss
@use "~@lamansky/mq" with (
  $color-scheme-override-root: 'html',
  $dark-class: 'dark-mode',
  $default-color-class: 'default-color-mode',
  $light-class: 'light-mode',
);
```

With these defaults, your light-mode styles can be triggered by adding a `light-mode` class to the `html` element.

If the light-mode styles are already active as a result of the media query, the light-mode styles can be manually disabled by adding a `dark-mode` or `default-color-mode` class to the `html` element.

### width

Creates a media query that tests whether the viewport width is between two given multiples of a certain measurement. By default, this multiple is `160px`.

```scss
@use "~@lamansky/mq";

body {
  font-size: 14px;

  @include mq.width(6) { // Viewport is at least 160px * 6 = 960px
    font-size: 16px;
  }
}

.sidebar {
  float: right;

  @include mq.width(0, 4) { // Viewport is less than 160px * 4 = 640px
    float: none;
  }
}

.menu {
  li {
    padding-left: .5em;
    padding-right: .5em;

    @include mq.width(4, 6) {
      padding-left: 1em;
      padding-right: 1em;
    }

    @include mq.width(6) {
      padding-left: 1.5em;
      padding-right: 1.5em;
    }
  }
}
```

For a "greater than" query, omit the second argument. For a "less than" query, set the first argument to zero.

You can customize the settings for this function using the `with` keyword:

```scss
@use "~@lamansky/mq" with (
  $scrollbar-padding: 0px,
  $width-step: 160px,
);
```

If you set a `$scrollbar-padding`, it will be subtracted from all viewport width measurements in the resulting media queries.

## Related

* [styles](https://github.com/lamansky/styles): A small library of commonly-used stylesheet rules, packaged as a Sass module.
