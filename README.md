# Fuzzing WASM based on semantic preservation.

## Instrument each JS engine in named browsers.

  - [Rust FFI tip](https://github.com/UsQuake/JSinRust/blob/main/embed_inst_js.md)
  - Environment dockerfiles.
    + [AFL-JSC rust-FFI env](https://github.com/UsQuake/JSinRust/blob/main/jsc_container)
    + [AFL-SpiderMonkey rust-FFI env](https://github.com/UsQuake/JSinRust/blob/main/mozjs_container)
    + [AFL-V8 rust-FFI env](https://github.com/UsQuake/JSinRust/blob/main/v8_container)
      
## Reference for design fuzzing algorithm

  - [Analysis of chromium wasm vulnerability](https://kiss.kstudy.com/Detail/Ar?key=3921110)
  - [DIE framework for fuzzing JS](https://taesoo.kim/pubs/2020/park:die.pdf)
  - [Fuzzing wasi & browsers](https://i.blackhat.com/USA-22/Wednesday/US-22-Ventuzelo-A-Journey-Into-Fuzzing-WebAssembly-Virtual-Machines.pdf)
  - [Fuzzing wasi](https://i.blackhat.com/USA-22/Wednesday/US-22-Hai-Is-WebAssembly-Really-Safe-wp.pdf)

