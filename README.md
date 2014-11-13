# Color Palette

## Docs

You can view the docs online [here](http://undistraction.github.io/palette/docs/) or locally in Chrome by running:

```
$ grunt docs
```

There is also a Grunt task to build the docs:

```
$ grunt sassdoc
```

## Tests

Tests are available [Bootcamp](https://github.com/thejameskyle/bootcamp) and can
be run using:

```
$ grunt test
```

## API

Color Palette is a very simple way to manage colour. It does not handle automatic colour calculations as I've always found I've needed more control. You can use any colour names you like, but this is not a themer, so they should describe the colour, not its usage.

So `midnight-blue` is perfect, but 'alert' is not.

Personally I break colours down into different hues, so I might have a `midnight-blue` an `aqua-blue` and an `ultramarine`. I then break each of these down using some keywords. You can set a key to a single value if you like, or you can set it to map with variations of the colour. If you include a key of `base` in this map, you can still refer to the colour using just its name (see examples). By breaking up colours into named hues, you reduce the need for so many variations, then you can use simple varient names for each colour.

```
$color-palette-map: (
  blood-red: #FC0000,
  midnight-blue: (
    lightest: #095ED8,
    lighter: #08409B,
    light: #052972,
    base: #03184C,
    dark: #000D26
  )
)
```

To look up the colours, you can use either the `color-palette` function or the short version `cp`:

```
# Root color
color: cp(blood-red);

# These two are equivalent
color: cp(midnight-blue);
color: cp(midnight-blue, base);

# Variant
color: cp(midnight-blue, lightest);
```

You might find it simpler to store your colours as variables and manipulate their variants with colour functions. That's OK too:

```
$color-palette-map: (
  blood-red: $color-blood-red,
  midnight-blue: (
    lightest: lighten($midnight-blue, 30),
    lighter: lighten($midnight-blue, 20),
    light: lighten($midnight-blue, 9),
    base: $color-midnight-blue,
    dark: darken($midnight-blue, 8)
  )
)
```

In many cases it's useful to reference colours semantically, for example you might have a warning colour and a success colour or you might have a set of categories which each have an associated colour. Resist the urge to use semantic names in the palette map. Instead, store these either in their own map or as variables containing lists to look up the colours.

```
$danger-color: blood-red;
$success-color: emerald lighter;
```

Then look them up by passing these variables to the palette function:

```
color: cp($success-color);
```

Note: The palette function is clever enough to see if you are passing a list, so you don't need to unpack it using `...`.
