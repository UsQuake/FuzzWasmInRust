**IMPORTANT**
1. You have verified that the issue to be present in the current `dev` branch.
2. Please supply the command line options and relevant environment variables,
   e.g., a copy-paste of the contents of `out/default/fuzzer_setup`.

Thank you for making AFL++ better!

**Describe the bug**
When I instrument static library with AFL_LLVM_ALLOWLIST, 
If AFL can't capture any bitmap in instrumented static library, afl-showmap emits error message not the message that "0 bitmaps captured". 
In case of building executable binary directly with afl-clang-fast, afl-showmap emits the message that "0 bitmaps captured", not like static library one's.

**To Reproduce**
Steps to reproduce the behavior:
1. Clone the AFLplusplus
2. Open AFLplusplus repository folder and build. ->`make', `make install`
3. In the repository folder, `ar rcus libafl-rt.a afl-compiler-rt.o`
4. Clone *tiny-js* git.
5. Set compiler with `export CC=afl-clang-fast` and `export CXX=afl-clang-fast++`.
6. Open cloned *tiny-js* repository folder and "cmake -S . -B build" to make a Makefile & build directory.
7. Open tiny-js/build folder and Instrument with `make tiny-js`
8. Copy libafl-rt.a from AFLplusplus repository folder to tiny-js/build folder.
9. 

**Expected behavior**
I want 0 bitmap not the error emission.

**Screen output/Screenshots**

In case of instrumenting static library and using instrumented library in another executable binary,
result is below..
<img width="1143" alt="tjs_static_1" src="https://github.com/AFLplusplus/AFLplusplus/assets/24998577/b3f173ec-3350-4d2b-83ca-5b417ea9cf83">
<img width="1143" alt="tjs_static_2" src="https://github.com/AFLplusplus/AFLplusplus/assets/24998577/4bd13d36-1dab-4790-abad-78e1926fb922">


**Additional context**
Add any other context about the problem here.
