# fontpath

[![experimental](http://badges.github.io/stability-badges/dist/experimental.svg)](http://github.com/badges/stability-badges)

A tool which generates paths and kerning data from a TTF/OTF/WOFF/etc font. The paths can then be decomposed into points, or rendered to a canvas, or triangulated.

The project is similar to [typeface.js](http://typeface.neocracy.org/) and [cufon](http://cufon.shoqolate.com/generate/). Both of those tools are very old, and were made before @font-face gained widespread support. This project has a few different goals in mind:

- Stronger focus on WebGL/animations/effects rather than trying to replace DOM text rendering
- NPM/node tooling, eventual integration with build tools
- decoupled modules, e.g. outline generator doesn't depend on rendering utils, glyph layout doesn't depend on canvas rendering
- rendering engine isn't tied to Canvas (or even the browser; e.g. you could use node-canvas)
- eventually, these tools could be used by a server to generate paths or hinted bitmap data for the client
- TTF, OTF, WOFF, and most other formats supported (FreeType2)
- font converter is an offline tool and fairly easy to modify (i.e. for a custom JSON/binary exporter)
- you can specify any charsets with the API (e.g. foreign and icon fonts)
- other stuff: hit detection on paths, advanced glyph/face metrics

# example

```fontpath myfont.ttf -o mfont.json --size 128```

The default size is 12 pt, but exporting with a higher font size will give you better resolution when rendering the path at large sizes. It's best to match the exported size to the final rendered size, as it will produce better rounding when scaled down.

Please note to use this package, you'll need to load an older version of Node, e.g. with [nvm](https://github.com/creationix/nvm):

```
nvm install 0.10.48
nvm use 0.10.48
```

# roadmap

This project is a heavy WIP. Some things I want to explore:

- Bitmap font rendering and atlas packing for Canvas/WebGL
- Basic support for styled/attributed text (italics, bold, color, etc)
- Maybe some tools for SDF rendering
- Better Node/CLI integration

New modules will be added to [text-modules](https://github.com/mattdesl/text-modules).

# demos

- [Triangulated text effect](http://mattdesl.github.io/fontpath-renderer/demo/tris.html) - a custom renderer using triangles
- [Custom steiner points](http://mattdesl.github.io/shape2d-triangulate/demo/glyph.html) - finer control over triangulation for creative effects
- [WebGL Path Rendering](http://mattdesl.github.io/fontpath-gl/demo/)
- [WebGL Triangulated Rendering](http://mattdesl.github.io/fontpath-gl/demo/wireframe.html)
- [Bitmap Fonts](http://mattdesl.github.io/gl-sprite-text/demo/demo.html)
- [Signed-Distance Field Bitmap Fonts](http://mattdesl.github.io/gl-sprite-text/demo/demo-sdf.html)

# modules

*Note:* New modules will be more generic and not specifically tied to "fontpath." See [text-modules](https://github.com/mattdesl/text-modules).

The framework is split into many small modules. Some of them aren't specific to fontpath, but are useful alongside it. You generally won't need to use all of them together; but instead, you'll pick and choose based on your particular application.

Most commonly, you might want to use a "renderer" which gives you a basic word-wrapper and glyph layout tools.

- [fontpath-canvas](https://github.com/mattdesl/fontpath-canvas) - a renderer using 2D Canvas and paths for fill/stroke
- [fontpath-gl](https://github.com/mattdesl/fontpath-gl) - a WebGL renderer using stackgl modules
- [gl-sprite-text](https://github.com/mattdesl/gl-sprite-text) - a WebGL renderer for [BMFont](http://www.angelcode.com/products/bmfont/) files that can also be used for signed-distance field text

Some other utilities that make up the ecosystem:

- [fontpath-simple-renderer](https://github.com/mattdesl/fontpath-simple-renderer) a generic renderer, useful if you need something more optimized
- [fontpath-wordwrap](https://github.com/mattdesl/fontpath-wordwrap) a basic word wrapper that supports `pre` and `nowrap` (for parity with CSS)
- [fontpath-util](https://github.com/mattdesl/fontpath-util) - point to pixel utilities
- [shape2d](https://github.com/mattdesl/shape2d) - Converts bezier/quadratic curves into points, with HTML5CanvasContext-like API
- [shape2d-triangulate](https://github.com/mattdesl/shape2d-triangulate) - triangulates a list of Shapes from shape2d, ideal for triangulating fontpath glyphs. uses poly2tri
- [fontpath-shape2d](https://github.com/mattdesl/fontpath-shape2d) - decomposes a fontpath JSON/JS glyph into points with shape2d
- [fontpath-test-fonts](https://github.com/mattdesl/fontpath-test-fonts) - some fonts that have already been exported to JSON, so you can easily pull them in with NPM
- [fontpath-vecmath](https://github.com/mattdesl/fontpath-vecmath) - vector/matrix utilities for font and glyph faces, built on [vecmath](https://github.com/mattdesl/vecmath)
- [point-util](https://github.com/mattdesl/point-util) - used by shape2d-triangulate, but includes a couple of handy features like `pointInPoly`


# license

MIT
