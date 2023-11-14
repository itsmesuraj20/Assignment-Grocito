slick
-------

[1]: <https://github.com/kenwheeler/slick>

_the last carousel you'll ever need_

#### Demo

[http://kenwheeler.github.io/slick](http://kenwheeler.github.io/slick/)

#### CDN

To start working with Slick right away, there's a couple of CDN choices availabile
to serve the files as close, and fast as possible to your users:

- https://cdnjs.com/libraries/slick-carousel
- https://www.jsdelivr.com/projects/jquery.slick

##### Example using jsDelivr

Just add a link to the css file in your `<head>`:

```html
<!-- Add the slick-theme.css if you want default styling -->
<link rel="stylesheet" type="text/css" href="//cdn.jsdelivr.net/gh/kenwheeler/slick@1.8.0/slick/slick.css"/>
<!-- Add the slick-theme.css if you want default styling -->
<link rel="stylesheet" type="text/css" href="//cdn.jsdelivr.net/gh/kenwheeler/slick@1.8.0/slick/slick-theme.css"/>
```

Then, before your closing ```<body>``` tag add:

```html
<script type="text/javascript" src="//cdn.jsdelivr.net/gh/kenwheeler/slick@1.8.0/slick/slick.min.js"></script>
```

#### Package Managers

```sh
# Bower
bower install --save slick-carousel

# NPM
npm install slick-carousel
```

#### Contributing

PLEASE review CONTRIBUTING.markdown prior to requesting a feature, filing a pull request or filing an issue.

### Data Attribute Settings

In slick 1.5 you can now add settings using the data-slick attribute. You still need to call $(element).slick() to initialize slick on the element.

Example:

```html
<div data-slick='{"slidesToShow": 4, "slidesToScroll": 4}'>
  <div><h3>1</h3></div>
  <div><h3>2</h3></div>
  <div><h3>3</h3></div>
  <div><h3>4</h3></div>
  <div><h3>5</h3></div>
  <div><h3>6</h3></div>
</div>
```

### Settings


##### Responsive Option Example

```javascript
$(".slider").slick({

  // normal options...
  infinite: false,

  // the magic
  responsive: [{

      breakpoint: 1024,
      settings: {
        slidesToShow: 3,
        infinite: true
      }

    }, {

      breakpoint: 600,
      settings: {
        slidesToShow: 2,
        dots: true
      }

    }, {

      breakpoint: 300,
      settings: "unslick" // destroys slick

    }]
});
```




### Events

In slick 1.4, callback methods were deprecated and replaced with events. Use them before the initialization of slick as shown below:

```javascript
// On swipe event
$('.your-element').on('swipe', function(event, slick, direction){
  console.log(direction);
  // left
});

// On edge hit
$('.your-element').on('edge', function(event, slick, direction){
  console.log('edge was hit')
});

// On before slide change
$('.your-element').on('beforeChange', function(event, slick, currentSlide, nextSlide){
  console.log(nextSlide);
});
```

Event | Params | Description
------ | -------- | -----------
afterChange | event, slick, currentSlide | After slide change callback
beforeChange | event, slick, currentSlide, nextSlide | Before slide change callback
breakpoint | event, slick, breakpoint | Fires after a breakpoint is hit
destroy | event, slick | When slider is destroyed, or unslicked.
edge | event, slick, direction | Fires when an edge is overscrolled in non-infinite mode.
init | event, slick | When Slick initializes for the first time callback. Note that this event should be defined before initializing the slider.
reInit | event, slick | Every time Slick (re-)initializes callback
setPosition | event, slick | Every time Slick recalculates position
swipe | event, slick, direction | Fires after swipe/drag
lazyLoaded | event, slick, image, imageSource | Fires after image loads lazily
lazyLoadError | event, slick, image, imageSource | Fires after image fails to load


#### Methods

Methods are called on slick instances through the slick method itself in version 1.4, see below:

```javascript
// Add a slide
$('.your-element').slick('slickAdd',"<div></div>");

// Get the current slide
var currentSlide = $('.your-element').slick('slickCurrentSlide');
```

This new syntax allows you to call any internal slick method as well:

```javascript
// Manually refresh positioning of slick
$('.your-element').slick('setPosition');
```


Method | Argument | Description
------ | -------- | -----------
`slick` | options : object | Initializes Slick
`unslick` |  | Destroys Slick
`slickNext` |  |  Triggers next slide
`slickPrev` | | Triggers previous slide
`slickPause` | | Pause Autoplay
`slickPlay` | | Start Autoplay (_will also set `autoplay` option to `true`_)
`slickGoTo` | index : int, dontAnimate : bool | Goes to slide by index, skipping animation if second parameter is set to true
`slickCurrentSlide` |  |  Returns the current slide index
`slickAdd` | element : html or DOM object, index: int, addBefore: bool | Add a slide. If an index is provided, will add at that index, or before if addBefore is set. If no index is provided, add to the end or to the beginning if addBefore is set. Accepts HTML String || Object
`slickRemove` | index: int, removeBefore: bool | Remove slide by index. If removeBefore is set true, remove slide preceding index, or the first slide if no index is specified. If removeBefore is set to false, remove the slide following index, or the last slide if no index is set.
`slickFilter` | filter : selector or function | Filters slides using jQuery .filter syntax
`slickUnfilter` | | Removes applied filter
`slickGetOption` | option : string(option name) | Gets an option value.
`slickSetOption` | change an option, `refresh` is always `boolean` and will update UI changes...
 | `option, value, refresh` | change a [single `option`](https://github.com/kenwheeler/slick#settings) to given `value`; `refresh` is optional.
 | `"responsive", [{ breakpoint: n, settings: {} }, ... ], refresh` | change or add [whole sets of responsive options](#responsive-option-example)
 | `{ option: value, option: value, ... }, refresh` | change  [multiple `option`s](https://github.com/kenwheeler/slick#settings) to corresponding `value`s.


#### Example

Initialize with:

```javascript
$(element).slick({
  dots: true,
  speed: 500
});
 ```

Change the speed with:

```javascript
$(element).slick('slickSetOption', 'speed', 5000, true);
```

Destroy with:

```javascript
$(element).slick('unslick');
```


#### Sass Variables

Variable | Type | Default | Description
------ | ---- | ------- | -----------
$slick-font-path | string | "./fonts/" | Directory path for the slick icon font
$slick-font-family | string | "slick" | Font-family for slick icon font
$slick-loader-path | string | "./" | Directory path for the loader image
$slick-arrow-color | color | white | Color of the left/right arrow icons
$slick-dot-color | color | black | Color of the navigation dots
$slick-dot-color-active | color | $slick-dot-color | Color of the active navigation dot
$slick-prev-character | string | '\2190' | Unicode character code for the previous arrow icon
$slick-next-character | string | '\2192' | Unicode character code for the next arrow icon
$slick-dot-character | string | '\2022' | Unicode character code for the navigation dot icon
$slick-dot-size | pixels | 6px | Size of the navigation dots

#### Browser support

Slick works on IE8+ in addition to other modern browsers such as Chrome, Firefox, and Safari.

#### Dependencies

jQuery 1.7

#### License

Copyright (c) 2017 Ken Wheeler

Licensed under the MIT license.

Free as in Bacon.
