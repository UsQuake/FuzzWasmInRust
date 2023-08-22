## Using instrumented javascript engines in container environment
    
 ### 1. Build an image with Docker
  
  - Belows are dockerfile of each js engine.
    + [AFL-JSC rust-FFI env](https://github.com/UsQuake/JSinRust/blob/main/jsc_container)
    + [AFL-SpiderMonkey rust-FFI env](https://github.com/UsQuake/JSinRust/blob/main/mozjs_container)
    + [AFL-V8 rust-FFI env](https://github.com/UsQuake/JSinRust/blob/main/v8_container)
      
  - Clone this git(https://github.com/UsQuake/FuzzWasmInRust.git).
       
    + `cd path_to_clone_this_git`
    + `git clone https://github.com/UsQuake/FuzzWasmInRust.git`
      
  - Build an image with each dockerfile in cloned repo.
       
    + `cd FuzzWasmInRust`
    + `docker build -t jsc_afl_inst_rust_ffi_image jsc_container`
    + `docker build -t v8_afl_inst_rust_ffi_image v8_container`
    + `docker build -t spider_monkey_afl_inst_rust_ffi_image mozjs_container`

 ### 2. Let's check whether environment setting is done.
  
  - Belows are built images.

  - Run v8 image with anonymous container by below commands.
     
     + `docker run -it v8_afl_inst_rust_ffi_image:latest`
     + `cd /home/root`
     + `git clone https://github.com/UsQuake/wasm_fuzz_driver.git` 
     +  Do authentication...
     + `cd wasm_fuzz_driver`
     + `cargo run ../v8_integ/target/release/v8_integ`
     +  See coverage raw data per byte. *v8_integ* is v8-afl-sample-runner.
     + `../v8_integ/target/release/v8_integ`

  - Run spider-monkey image with anonymous container by below commands.
     
     + `docker run -it spider_monkey_afl_inst_rust_ffi_image:latest`
     + `cd /home/root`
     + `git clone https://github.com/UsQuake/wasm_fuzz_driver.git` 
     +  Do authentication...
     + `cd wasm_fuzz_driver`
     + `cargo run ../mozjs_integ/target/release/mozjs_integ`
     +  See coverage raw data per byte. *mozjs_integ* is mozjs(spidermonkey rust ffi)-afl-sample-runner.
     + `../mozjs_integ/target/release/mozjs_integ`
       
  - Run jsc image with anonymous container by below commands.
     
     + `docker run -it jsc_afl_inst_rust_ffi_image:latest`
     + `cd /home/root`
     + `git clone https://github.com/UsQuake/wasm_fuzz_driver.git` 
     +  Do authentication...
     + `cd wasm_fuzz_driver`
     + `cargo run ../jsc_integ/target/release/jsc_integ`
     +  See coverage raw data per byte. *jsc_integ* is jsc-afl-sample-runner.
     + `../jsc_integ/target/release/jsc_integ`
