# stb\_image\_js

[stb_image.h](https://github.com/nothings/stb) wrapper for a Web Browser. Or any JavaScript environment that supports [WebAssembly](https://webassembly.org/) and [fetch()](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)

What we did is basically compiled [stb_image.h](https://github.com/nothings/stb) to a self-contained WASM module and wrote a simple js wrapper that takes the bytes of image files, feeds them into the WASM module, receives the parsed pixels and constructs [ImageData](https://developer.mozilla.org/en-US/docs/Web/API/ImageData) out of them. So you can download an image and get its ImageData in one go if you ever wanted to do it this way.

## Quick Start

1. Copy [js/stb_image.js](./js/stb_image.js) and [wasm/stb_image.wasm](./wasm/stb_image.wasm) file to your website to `js` and `wasm` folder correspondingly.
1. Modify `STB_IMAGE_WASM_PATH` in [js/stb_image.js](./js/stb_image.js) if you want a different path to [wasm/stb_image.wasm](./wasm/stb_image.wasm).
1. `<script src='./js/stb_image.js'></script>`
1.

```javascript
const canvas = document.getElementById("canvas-id");
const ctx = canvas.getContext("2d");
stbi_load_from_url("image.png").then((image) => ctx.putImageData(image, 0, 0));
```

*I'll eventually turn this into a proper npm package. Just copy the files for now. It's simple and straightforward. You have everything you need in here. See Demo for more info. The whole codebase is dead simple. You can learn it in less than an hour. I believe in you.*

## Demo

The demo consists of two files: [index.html](./index.html) and [js/demo.js](./js/demo.js) compiled from [ts/demo.ts](./ts/demo.ts) (that's probably the one you wanna read). It loads up images from [./img/](./img/) folder using [js/stb_image.js](./js/stb_image.js) and puts them into the canvas.

If you want to run it locally just run something like

```console
$ python3 -m http.server 6969 # or any other lightweight HTTP server of your choice
$ browser http://localhost:6969/
```

You can also find it deployed at https://tsoding.github.io/stb_image_js/

## Rebuilding `stb_image.wasm`

You will need clang 13.0.0+:

```console
$ node build-wasm.js
```

## Rebuilding the JS files

```console
$ npm install
$ ./node_modules/.bin/tsc
```
