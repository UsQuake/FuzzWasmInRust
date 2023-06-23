
  # JSEngine을 Rust 코드에 (나만 볼꺼얌 >~<)
  ## V8
  - rusty_v8 모듈을 사용하세요!
  - 구글에서 C++로 작성된 v8 미리 빌드한 단일 라이브러리를 Rust로 FFI해서 쓸 수 있게 해놨습니다.(a.k.a v8monolith.a, v8_monolith.lib)
  - 여담으로, 이 프로젝트가 인기가 많고 유지가 잘 되는 이유는 Node.js의 차기작인 Deno 프로젝트가 Rust로 작성되서
  - V8 엔진을 Rust 코드에서 불러와야 했기에 관리가 잘 되어 있습니다.(외쳐! 구글갓!)

  ## SpiderMonkey
  - Rust는 원래 모질라 재단에서 Servo 브라우저를 만들기 위해 나왔습니다.
  - 그래서 Rust 기반으로 작성된 Servo에 C++로 만든 JSEngine인 SpiderMonkey를 추가하기 위해
  - C++ JS Engine인 SpiderMonkey를 Rust코드와 통합할 수 있도록 자체적으로 MozJS라는 프로젝트를 통해 관리하고 있습니다.
  - 근데 Servo 프로젝트가 중간에 망했다가 부활하면서 MozJS 프로젝트도 관리가 잘 안 되어 왔습니다.
  - 그래서 [여기 Readme파일](https://github.com/servo/mozjs)에 빌드 옵션 팁이 나와 있는데 좀 안맞습니다.
  - 리눅스 빌드의 경우에 clang은 요새 14버전이 나오고 있고,
  - export LIBCLANG_PATH=/usr/lib/clang/4.0/lib 보다는 X86 우분투22 기준으로 export LIBCLANG_PATH=/usr/lib/x86_64-linux-gnu/ 가 맞습니다.
  - 또한 llvm도 같이 설치 되어 있어야 하는 거 같습니다.
  
  ## JavascriptCore
  - JavascriptCore는 WebKit/Safari,
  - 그리고 최근에 핫한 Bun.JS 런타임에 내장된 JS Engine입니다.
  - WebKit 안에 내장 되어 있어 있기에 WebKit 라이브러리가 있다면사용할 수 있습니다. 
  - 저는 그래서 GLib, GTK에 FFI하는 [javascriptcore-rs](https://github.com/tauri-apps/javascriptcore-rs)를 이용하고 있습니다.
  - 우분투의 경우는 apt-get install libjavascriptcoregtk-4.1-dev gir1.2-webkit2-4.1가 필요합니다.
