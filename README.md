# rewrite-png-pHYs-chunk

Adds (or rewrites) the pHYs chunk in PNG files which specifies the pixels-per-meter

Based on [https://github.com/hughsk/png-chunks-extract]
## Usage

### `data = rewrite_pHYs_chunk(data, ppmX, ppmY);`

Takes the raw image file `data` as a `Uint8Array`, and returns raw image file `data` as a `Uint8Array` with the pHYs chunk added or rewritten with ppmX, ppmY (pixels-per-meter):

``` javascript
        var base64 = "iVBORw0KGgoAAAANSU...";
        var img = new Image();

        // encode PNG as Uint8Array
        var binary_string = window.atob(base64);
        var len = binary_string.length;
        var bytes = new Uint8Array(len);
        for (var i = 0; i < len; i++) {
            bytes[i] = binary_string.charCodeAt(i);
        }

        // mess with pHYs chunk here

        // dots per inch
        var dpi = 150;
        // pixels per metre
        var ppm = Math.round(dpi / 2.54 * 100);
        console.log("bytes.length = " + bytes.length)
        bytes = rewrite_pHYs_chunk(bytes, ppm, ppm);
        console.log("bytes.length = " + bytes.length);

        // re-encode PNG (btoa method)
        var b64encoded = btoa(String.fromCharCode.apply(null, bytes));
        console.log(pngHeader + b64encoded);
        img.src = pngHeader + b64encoded;

        // draw it
        document.body.appendChild(img);
```

## License

MIT, see [LICENSE.md](https://github.com/murkle/rewrite-png-pHYs-chunk/blob/master/LICENSE.md) for details.
