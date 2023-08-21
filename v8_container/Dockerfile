#For V8 AFL instrumentaed Rust-FFI
FROM ubuntu:22.04
RUN \
      apt-get update && \
      apt-get install -y llvm-15 llvm-15-tools clang-15 lld-15\
      build-essential libglib2.0-dev python3 curl git cargo
WORKDIR /home/root/
RUN git clone https://github.com/AFLplusplus/AFLplusplus.git
WORKDIR /home/root/AFLplusplus
ENV AFL_PATH "/home/root/AFLplusplus"
ENV AFL_LLVM_INSTRUMENT "CLASSIC"
ENV RUSTFLAGS "-Ccodegen-units=1 -Clink-arg=-fuse-ld=gold -lafl-rt -L/home/root/AFLplusplus" 
ENV CLANG_BASE_PATH "/usr/local" 
ENV V8_FROM_SOURCE 1 
ENV PYTHON "/usr/bin/python3"
ENV LLVM_CONFIG "llvm-config-15"
RUN make
RUN make install
RUN ar rcus libafl-rt.a afl-compiler-rt.o
WORKDIR /usr/local/bin
RUN ln -s afl-clang-fast clang
RUN ln -s afl-clang-fast++ clang++
WORKDIR /usr/bin
RUN cp llvm-ar-15 /usr/local/bin/llvm-ar
WORKDIR /home/root
RUN git clone https://github.com/denoland/rusty_v8.git
WORKDIR /home/root/rusty_v8
RUN git submodule update --init --recursive
WORKDIR /home/root
RUN git clone https://UsQuake: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@github.com/UsQuake/v8_integ.git
WORKDIR /home/root/v8_integ
RUN cargo build --release
