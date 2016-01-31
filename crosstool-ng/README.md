# crosstool-ng 

crosstool-NG aims at building toolchains. Toolchains are an essential component in a software development project. It will compile, assemble and link the code that is being developed. Some pieces of the toolchain will eventually end up in the resulting binary/ies: static libraries are but an example.

## Overview

This dockerfile is crafted especially to provide building environment for ```armeb-unknown-linux-uclibcgnueabi``` architecture. Texas Instruments Puma5 boards are based on this arch and you can find it used by some docsis cable modem/router vendors or ISPs. 

It's been successfully tested on UBEE EVW3226 cable router, compiling gdb just fine.

## Usage

1. Put sources in /usr/src directory
2. Run docker container with mounted /usr/src dir.

```
docker run -it --rm -v /usr/src:/usr/src srozb/crosstool-ng:armeb-unknown-linux-uclibcgnueabi-arm --entrypoint=/bin/bash
```

3. Compile as usual with proper --target --host and --build parameters.


