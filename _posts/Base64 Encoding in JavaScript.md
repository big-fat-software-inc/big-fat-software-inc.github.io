



# Usage

*Base64* encoding is a useful format to represent binary data in text form for storage or for transfer.

For example, if you want to turn a complex webpage consisting of images into single html file we can use `base64` in the `src `of `<img>`.





In JavaScript strings are represented in `UTF-16` character encoding format. ASCII characters can easily fit into a byte. But in `UTF-16` strings are occupy `16-bits` of memory i.e. `2 bytes` .` Base64`, by design, expects *binary data* as its input. In the context of JavaScript strings this refers to byte-length-strings. So, `16-bit` encoded `UTF-16` strings that occupy `2 byte` are incompatible with `btoa()`.

```js
const a = "✓"
const b = "✓"
console.log(btoa(a));    // YQ==
console.log(btoa(b)); // error



console.log(a.codePointAt(0).toString(16)); // 2713: occupies > 1 byte

```



## How to encode/decode a string to/from base64 without a library

### Quick Summary

```js
str = "The quick brown fox jumps over the lazy dog";
b64 = btoa(unescape(encodeURIComponent(str)));
str = decodeURIComponent(escape(window.atob(b64)));
```

 `btoa` and `atob` - Needless to say that these built-in functions will perform lightning fast in comparison to raw `base64` decoding using a custom JavaScript function.

### Explanation





With Unicode `atob` and `btoa` can not be used directly. 

Almost all websites have a `utf-8` or `utf-16` text-encoding format these days. It's Unicode everywhere, no ASCII no more. 

Please note that this is not suitable for raw Unicode strings! See Unicode section [here](https://developer.mozilla.org/en-US/docs/DOM/window.btoa).

Syntax for encoding

`window.btoa(str);` returns an ASCII string containing the `Base64` representation of `str`.

Syntax for decoding

```javascript
var decodedData = window.atob(encodedData);
```





```js
function b64EncodeUnicode(str) {
    return btoa(encodeURIComponent(str).replace(/%([0-9A-F]{2})/g, function(match, p1) {
        return String.fromCharCode('0x' + p1);
    }));
}

b64EncodeUnicode('✓ à la mode'); // "4pyTIMOgIGxhIG1vZGU="
b64EncodeUnicode('\n'); // "Cg=="



function b64DecodeUnicode(str) {
    return decodeURIComponent(Array.prototype.map.call(atob(str), function(c) {
        return '%' + ('00' + c.charCodeAt(0).toString(16)).slice(-2);
    }).join(''));
}

b64DecodeUnicode('4pyTIMOgIGxhIG1vZGU='); // "✓ à la mode"
b64DecodeUnicode('Cg=='); // "\n"
```



## Demo

For newer browsers to encode Uint8Array to string, and decode string to Uint8Array.

```js
const base64 = {
    decode: s => Uint8Array.from(atob(s), c => c.charCodeAt(0)),
    encode: b => btoa(String.fromCharCode(...new Uint8Array(b)))
};
```

For Node.js you can use the following to encode string, Buffer, or Uint8Array to string, and decode from string, Buffer, or Uint8Array to Buffer.

```js
const base64 = {
    decode: s => Buffer.from(s, 'base64'),
    encode: b => Buffer.from(b).toString('base64')
};
```













##  Base64 encode an `HTMLImageElement`

To encode HTML image object (`HTMLImageElement`):

```js
function getBase64Image(img) {  
  var canvas = document.createElement("canvas");  
  canvas.width = img.width;  
  canvas.height = img.height;  
  var ctx = canvas.getContext("2d");  
  ctx.drawImage(img, 0, 0);  
  var dataURL = canvas.toDataURL("image/png");  
  // escape data:image prefix
  return dataURL.replace(/^data:image\/(png|jpg);base64,/, "");  
  // or just return dataURL
  // return dataURL
}

getBase64Image(document.querySelector('img'));
```



more [here](http://drcreazy.com/art/61/base64-javascript.aspx)