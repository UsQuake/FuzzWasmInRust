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
2. Open *AFLplusplus repository folder* and build. ->`make` , `make install`
3. In *the repository folder*, `ar rcus libafl-rt.a afl-compiler-rt.o`
4. Clone *tiny-js* git **outside** of *the AFLplusplus repository folder*.
5. Set compiler with `export CC=afl-clang-fast` and `export CXX=afl-clang-fast++`.
6. Open cloned *tiny-js* repository folder and `cmake -S . -B build` to make a Makefile & build directory.
7. Open tiny-js/build folder and Instrument static library with `make tiny-js`
8. Copy libafl-rt.a from AFLplusplus repository folder to tiny-js/build folder.
9. Make dummy cpp file to make executable binary to test instrumented static library.
Code is
    ``` C++
      #include "TinyJS.h"
      #include "TinyJS_Functions.h"
      #include <assert.h>
      #include <stdio.h>
      #include <memory>

      void js_print(CScriptVar *v, void *userdata) {
          printf("> %s\n", v->getParameter("text")->getString().c_str());
      }

      void js_dump(CScriptVar *v, void *userdata) {
          CTinyJS *js = (CTinyJS*)userdata;
          js->root->trace(">  ");
      }


      int main(int argc, char **argv)
      {
        std::shared_ptr<CTinyJS> js = std::make_shared<CTinyJS>();
        /* add the functions from TinyJS_Functions.cpp */
        registerFunctions(js.get());
        /* Add a native function */
        js->addNative("function print(text)", &js_print, 0);
        js->addNative("function dump()", &js_dump, js.get());

        FILE* input_js = fopen("tests/test004.js", "r");
  
        fseek(input_js, 0, SEEK_END);
        const int js_file_size = ftell(input_js);
        rewind(input_js);

        char* code = new char[js_file_size + 1];
        fread(code, 1, js_file_size, input_js);
  
          try {
            js->execute(code);
          } catch (CScriptException *e) {
            printf("ERROR: %s\n", e->text.c_str());
          }
        fclose(input_js);
        delete[] code;
         #ifdef _WIN32
         #ifdef _DEBUG
           _CrtDumpMemoryLeaks();
         #endif
         #endif
        return 0;
      }
   ```

**Expected behavior**
I expect the message that "0 bitmaps captured" not error message.

**Screen output/Screenshots**

In case of instrumenting static library and using instrumented library in another executable binary,
result is below..
<img width="1143" alt="tjs_static_1" src="https://github.com/AFLplusplus/AFLplusplus/assets/24998577/b3f173ec-3350-4d2b-83ca-5b417ea9cf83">
<img width="1143" alt="tjs_static_2" src="https://github.com/AFLplusplus/AFLplusplus/assets/24998577/4bd13d36-1dab-4790-abad-78e1926fb922">


**Additional context**

You can say that "Why don't you instrument executable binary source code directly?".
Yes, I know, But I want to instrument only static library, not with shell executable like *d8, jsc,..etc*
Also, I should use partial instrumentation for testing specific features on javascript engines..
Plz.. Plz.. help me..
