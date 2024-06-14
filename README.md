# ced-wasm

> Detect the character encoding using Google’s [compact_enc_det](https://github.com/google/compact_enc_det) library with wasm

## Usage

Feel free to include the bin/ced.js in your pages, then use it like:
```js
<script type="text/javascript">
Module.onRuntimeInitialized = async () => {
  let encoding = Module.DetectEncoding(buffer);
  console.log("Detected Encoding: ", encoding);
}
</script>
```

Or you can get your own one by:

## Using Docker (recommend)

```console
$ git clone https://github.com/neichen/ced-wasm.git
$ cd compact_enc_det
$ docker run --rm -v $(pwd):/src trzeci/emscripten emcc compact_enc_det/compact_enc_det.cc compact_enc_det/compact_enc_det_hint_code.cc util/encodings/encodings.cc util/languages/languages.cc -o output.js -O3 --bind -s WASM=1 -s "EXPORTED_RUNTIME_METHODS=['ccall','cwrap']" -I. -I./util -I./util/encodings -I./util/languages
```

Or

## Manual build

```console
$ git clone https://github.com/google/compact_enc_det.git
$ git clone https://github.com/emscripten-core/emsdk.git
$ cd emsdk
$ ./emsdk install latest
$ ./emsdk activate latest
$ source ./emsdk_env.sh
$ cd compact_enc_det
$ emcc compact_enc_det/compact_enc_det.cc compact_enc_det/compact_enc_det_hint_code.cc util/encodings/encodings.cc util/languages/languages.cc -o output.js -O3 --bind -s WASM=1 -s "EXPORTED_RUNTIME_METHODS=['ccall','cwrap']" -I. -I./util -I./util/encodings -I./util/languages
```

then you will get the output.js and output.wasm, which can be used anywhere you like.

## Thanks to

 - [compact_enc_det](https://github.com/google/compact_enc_det) by Google
 - [ced](https://github.com/sonicdoe/ced) by sonicdoe
 - [A quick and dirty C++ WebAssembly demo](https://github.com/alexnoz/wasm-class-sample) by alexnoz
 - [Monica](https://monica.im/) by Butterfly Effect
 - [GPT4](https://chatgpt.com) by OpenAI