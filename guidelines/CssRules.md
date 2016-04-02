---
title: Document Center
---

# SODA Styling Cheat Sheet

# SASS Rules

## CSS Class Names

SODA class names should be pre-fixed with `hde-` to avoid naming conflicts with
other frameworks or plugins. Besides it's more clear which styles have been
written by us.

```scss
.hde-my-class {}
```

Furthermore class names should describe the case or functionality without having information about the element.

```scss
button.hde-primary {
  background: $hde-primary-color;
  color: complement($hde-primary-color);
}

a.hde-primary {
  color: $hde-primary-color;
}
```

```html
<button class="hde-primary">Book</button>

<a href="#" class="hde-primary">Foo Bar</a>
```

## Reduce Complexity

Split complex CSS values to separate properties. This makes it easier to read instead of using complex CSS statements.

```scss
.hde-my-class {

  border: {
    top: 1px solid red;
    bottom: 1px dotted green;
  }
}
```

## Declaring Variables

SASS variables should be prefixed with `$hde-` as well. Whether we embed a CSS framework or third party libs, it will be quite impossible to have conflicting names.

```scss
$hde-primary-color: orange;
$hde-secondary-color: #111;
$hde-complementary-color: blue;
```

## Do Not Alter Variables

Don't change variable values without the `variables.scss`. This might break the compilation process. If you have to alter the value use a copy instead.

```scss
$hde-component-color: $hde-primary-color;

$hde-component-color-transparent: rgba($hde-component-color, 0.5);
```

## Comments

In SASS we can use comments without affecting our styles. We should use this feature to make components, or CSS hacks more clear. And there are always some strange CSS hacks for any bad device out there ;)

```scss
// This affects a bug in firefox
// Bug: http://any.bug.com/issue?id=123456
#meh,  x:-moz-any-link  { color: red }
```

# Global Styling

## Style Reset

Base styles, or `reset styles` are small libs which overwrites all predefined styles from the browser.

```scss
// base.scss
* { padding: 0; margin: 0; /* ... etc. */ }
```

## Variables

Define variables which can be used in any part of the page (components).

```scss
// variables.scss

// Color stack
$hde-background: #eee;
$hde-primary-color: orange;
$hde-secondary-color: blue;

// Fonts
$hde-font-url: "https://fonts.googleapis.com/css?family=Open+Sans";
$hde-font-stack: 'Open Sans', sans-serif;
$hde-font-color: #222;
$hde-font-color-light: #999;

/*
  Responsive break points.
  Simply use ...
  @media {$hde-media-small} {
    my: definition;
  }
*/
$hde-media-xs: "screen and (max-width: 320)";
$hde-media-small: "screen and (max-width: 480px)";
$hde-media-medium: "screen and (max-width: 640px)";
$hde-media-large: "screen and (max-width: 768px)";
$hde-media-xlarge: "screen and (min-width: 169px)";

// ... and more ...
```

## Skeleton

In this file we define the basics like grid layout and the page structure
(aside, navbar, header, footer, offcanvas, etc.)

```scss
// skeleton.scss

/*
  The page skeleton
*/
.container {
  margin: auto;
  padding: $hde-content-space;
  max-width: $hde-app-max-width;
}

header {
  padding: {
    bottom: $hde-content-space;
  }
  border: {
    bottom: 1px solid #000;
  }
}

main {
  padding: $hde-content-space 0;
}

footer {
  padding: $hde-content-space 0;
  border: {
    top: 1px solid #000;
  }
}
```

## Theming

In SODA we have just one 'theme' however it's always a good idea to separate theming styles.

```scss
// theme.scss

@import url($hde-font-url);

* {
  outline: none;
}

html,
body {

  color: $hde-font-color;
  background: $hde-background;
  font: {
    family: $hde-font-stack;
  }
}

a {
  color: $hde-link-color;
  background: $hde-link-background;
  text-decoration: none;
}

// ... and so on ...
```

# Components

A component is completely independent from any other component, but it can use any global variable.

Since we want to build SODA the angular way which comes which modules (components / directives), we declare a component using HTML attributes, prefixed with `hde-` as well.

```scss
[hde-hotel-thumb] {

}
```

```html
<div hde-hotel-thumb></div>
```

Hence we want to encapsulate our styles to re-use the component without any conflicts, we should declare every style within our HTML attribute.

```scss
[hde-hotel-thumb] {

  overflow: hidden;

  img {

    max-width: 200px;
    max-height: 200px;
    width: 100%;
    float: left;
    margin: {
      top: 0;
      right: $content-space;
      bottom: $content-space;
      left: 0;
    }
  }

}

```

```html
<div hde-hotel-thumb>
  <img
    src="hotel-thumbnail.jpg"
    alt="Hotel Image"
    title="Hotel Image" />
  <h3>Super Superior</h3>
  <p>
    Bacon ipsum dolor amet shoulder pig brisket...
  </p>
  <button>Book</button>
</div>
```

## Nested Components

In case of a responsive hotel list, we define a new component which can contain one or more hotels.

```scss
[hde-hotel-teaser-list] {

  overflow: hidden;

  [hde-hotel-thumb] {

    float: left;
    margin: {
      bottom: $content-space;
    }

    @media #{$media-xlarge} {
      width: 25%;
    }

    @media #{$media-large} {
      width: 33.333333%;
    }

    @media #{$media-medium} {
      width: 50%;
    }

    @media #{$media-small} {
      width: 100%;
    }

  }

}
```

# Main File

Use the `main.scss` to include all global styles and components.

```scss
// main.scss

/*
  This section defines everything which is needed globally
*/
@import 'global/base'; // style reset
@import 'global/variables';
@import 'global/skeleton';
@import 'global/theme';

/*
  Modules which can be used independently in the HDE ecosystem
*/
@import 'article/article';
@import 'hotel/hotel-thumb';
@import 'hotel/hotel-teaser-list';
```

# In Case of Angular

Everything which belongs to one module should stored at the same directory. Even SCSS files :)

```
/hde
  /hotel
    module.js                // definition of the module
    hotel.html               // hotel template
    hotel.scss               // styles for [hde-hotel] {}
    hotel-directive.js       // hotel directive for "hde-hotel"
    hotel-directive.spec.js  // a test :) => later
    hotel-controller.js      // hotel controller
    hotel-controller.spec.js // another test :) => later
```

```js
// module.js
angular.module('hde.hotel', []);
```

```js
// hotel-directive.js
angular.module('hde.hotel')
  .directive('hdeHotel', function () {
    return {
      template: 'hotel.html',
      controller: 'HotelCtrl',
      controllerAs: 'hotel'
    };
  });
```

```js
// hotel-controller.js
angular.module('hde.hotel')
  .controller('HotelCtrl', function () {});
```

```html
<!-- hotel.html -->
<img ng-src="{{::hotel.src}}" alt="{{::hotel.name}}" />
<h2>{{::hotel.name}}</h2>
<p>{{::hotel.description}}</p>
```

```scss
// hotel.scss
[hde-hotel] {

  img {
    max-width: 200px;
    max-height: 200px;
    width: 100%;
  }

  p {
    line-height: 1.5em;
  }
}
```

```html
<!-- somewhere at the page -->
<div hde-hotel="hotel-x"></div>
<div hde-hotel="hotel-y"></div>
<div hde-hotel="hotel-z"></div>
```

# Demo

First, checkout the `Samples` repository at VSO.

```shell
git clone https://hdetfs.visualstudio.com/DefaultCollection/SODA/_git/Samples
```

Open your shell and switch to the `sass` project.

Now install all needed dependencies (NPM is required)

```shell
npm install -g gulp node-static && npm install
```

Run the `static` command to start a static server.

```shell
static
```

Now your app is serving at `localhost:8080`.

If you want to play with SASS, start the gulp task `gulp sass:watch`.
