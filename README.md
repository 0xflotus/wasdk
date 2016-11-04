[![Build Status](https://travis-ci.org/yurydelendik/wasdk.svg?branch=master)](https://travis-ci.org/yurydelendik/wasdk)

# WebAssembly SDK
A toolkit for creating WebAssembly modules.

## Installing Wasdk

### Installing from NPM

```
npm install wasdk
```

### Installing from GitHub
This is recommended if you want to contribute to the wasdk project.

Clone this repository and run:
```
npm run installdeps
```

and to build sources:
```
npm run build
```

To download all necessary pre-compiled binaries for your operating system, which includes: Emscripten, Binaryen, SpiderMonkey, LLVM and Clang:
```
wasdk sdk --install
```

And clean up (built sourced and download binaries):
```
npm run clean
```

## Usage

Wasdk includes a variety of tools which accessible through the `wasdk` command:

### Compiling Modules

```
wasdk ez test/malloc.json -o malloc.js
```

This producs several files:
  - `malloc.asm.js`: asm.js code
  - `malloc.wasm`: WebAssembly Binary
  - `malloc.wast` WebAssembly Text
  - `malloc.js`: Node / Browser runtime environment.

### Running Modules

```
wasdk js dist/wasm-shell.js malloc.wasm
```

This creates a lightweight WebAssembly environemnt and runs the `malloc.wasm` file. At the moment,
this only works with the `malloc.wasm` file.

### Viewing WebAssembly Compiled Machine Code

Use the `disassemble` command to view the compiled machine code for a WebAssembly program.
This code is generated by the ION compiler (used in the Firefox Web Browser). It should be
fairly similar to the code produced by other browser engines.

```
wasdk disassemble test/universe.wast
```

```
(module
  (export "answer" (func $answer))
  (func $answer (result i32)
    (return (i32.const 42))
  )
)
```

Compiled x86/AMD64 Code:

```
Total Code Size: 5.00 Bytes
100.00%    5          Func 0:
Func 0:
  sub rsp, 8                                        ; 0x000050 48 83 ec 08
  mov eax, 0x2a                                     ; 0x000054 b8 2a 00 00 00
  nop                                               ; 0x000059 66 90
  add rsp, 8                                        ; 0x00005b 48 83 c4 08
  ret                                               ; 0x00005f c3
```

### SDK Management

```
wasdk sdk --install
```


```
wasdk sdk --clean
```

## Testing
```
npm test
```
