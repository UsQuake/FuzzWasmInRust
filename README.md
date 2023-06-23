# English
  ## V8
  - use rusty_v8, which use prebuilt v8 monolithic static library(a.k.a v8monolith.a, v8_monolith.lib)
  -  And if you need latest snapshot, you can use your custom-build of V8.
    
# Korean
  ## V8
  - rusty_v8 모듈을 사용하세요!
  - 구글에서 C++로 작성된 v8 미리 빌드한 단일 라이브러리를 Rust로 FFI해서 쓸 수 있게 해놨습니다.(a.k.a v8monolith.a, v8_monolith.lib)
  - 여담으로, 이 프로젝트가 인기가 많고 유지가 잘 되는 이유는 Node.js의 차기작인 Deno 프로젝트가 Rust로 작성되서
  - V8 엔진을 Rust 코드에서 불러와야 했기에 관리가 겁나 잘 되있습니다.(외쳐! 구글갓!)

  ## "V8을 내 손으로 직접 FFI하겠다. 난 상남자다" 
  - 라면 MSVC의 디버거로 작업할 수 있습니다.
  - V8 정적 라이브러리를 직접 빌드해서 C++ 코드에서 Rust로 FFI해서 쓰고 싶은 싶은 용자가 있다면,
  - [다음 옵션](https://github.com/newkjs/v8-monolith-builds)을 통해 v8을 빌드하면 정신 건강에 이롭습니다.
  - 아무런 설정도 하지 않으면, 경고가 오류로 지정되서 경고만 떠도 빌드 막힙니다.
  - 윈도우에서 빌드할 경우 VS2022로 세팅하고, VS2022 Installer에서 자동으로 다운로드 해준 WindowsSDK 제거/추가/관리에서 디버거를 추가하세요.
  - 또한, VS2022안에서 정적 라이브러리를 호출할 경우 MT_Debug와 MT(멀티스레드, 디버그 모드, 릴리즈 모드) 지정해주지 않으면 에러를 뿜습니다.
  

  ## SpiderMonkey
  - Rust는 원래 모질라 재단에서 Servo브라우저를 만들려다가 나왔으나,
  - Rust만 남고 Servo 브라우저는 망했다가 2023년이 되어서야 부활합니다.
  - 아무튼 그렇기에 모질라 재단의 Rust 기반으로 작성된 Servo에 SpiderMonkey를 추가하기 위해
  - MozJS라는 프로젝트를 통해 C++ JS Engine을 Rust코드와 통합할 수 있도록 만들었습니다.

