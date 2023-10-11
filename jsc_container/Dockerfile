#For JSC AFL instrumented Rust-FFI
FROM ubuntu:22.04
RUN \
      apt-get update && \
      apt-get install -y llvm-15 llvm-15-tools clang-15 lld-15 \
      build-essential libglib2.0-dev python3 ruby3.0 git cargo \
      cmake ninja-build python-is-python3
WORKDIR /home/root/
RUN git clone https://github.com/AFLplusplus/AFLplusplus.git
WORKDIR /home/root/AFLplusplus
ENV LLVM_CONFIG "llvm-config-15"
RUN make
RUN make install
RUN ar rcus libafl-rt.a afl-compiler-rt.o
WORKDIR /usr/local/bin
RUN ln -s afl-clang-fast clang
RUN ln -s afl-clang-fast++ clang++
WORKDIR /usr/bin
RUN cp llvm-ar-15 /usr/local/bin/llvm-ar
RUN cp llvm-readelf-15 /usr/local/bin/llvm-readelf
RUN cp llvm-nm-15 /usr/local/bin/llvm-nm
WORKDIR /home/root
RUN git clone https://github.com/UsQuake/jsc-sys.git
WORKDIR /home/root/jsc-sys
RUN patch -p0 < jsc_makefile.patch
RUN patch -p0 < jsc_build-script.patch
RUN git clone https://github.com/WebKit/WebKit.git
WORKDIR /home/root
RUN git clone https://UsQuake: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@github.com/UsQuake/jsc_integ.git
ENV AFL_PATH "/home/root/AFLplusplus"
ENV AFL_LLVM_INSTRUMENT "CLASSIC"
ENV RUSTFLAGS "-Ccodegen-units=1 -Clink-arg=-fuse-ld=gold -lafl-rt -L/home/root/AFLplusplus" 
WORKDIR /home/root/jsc_integ
RUN cargo build --release
