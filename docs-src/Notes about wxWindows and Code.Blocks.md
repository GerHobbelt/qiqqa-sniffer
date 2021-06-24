# Notes about wxWidgets and [Code::Blocks](https://www.codeblocks.org/)

## Installing [Code::Blocks](https://www.codeblocks.org/)

- Install the regular 64bit setup version. 

- Don't bother to download and install the setup with MINGW/GCC included as that one doesn't fly -- at least it didn't on this dev box.

  When you start Code::Blocks, it'll yak in the bottom right corner with an Environment Message about its inability to locate GCC anywhere in your path. It'll keep doing that until you follow the next few steps, even when you had a MINGW/GCC install in the `C:\Program Files\CodeBlocks\...` directory tree already, thanks to that codeblocks+MingW setup you tried first!
   
- Instead, follow their own guidebook and go download and install the preferred MINGW/GCC toolchain at [TDM-GCC](https://jmeubank.github.io/tdm-gcc/)!

- Install that one in the default path: `C:\TDM-GCC-64\`

- Kick on a fresh `bash` or `cmd` shell (`bash` from your git-for-windows install) and check if `gcc` is reachable:

  ```
  gcc -v
  ```
  
  should dump several lines of version and build info, e.g.
  
  ```
  $ gcc -v
  Using built-in specs.
  COLLECT_GCC=C:\TDM-GCC-64\bin\gcc.exe
  COLLECT_LTO_WRAPPER=C:/TDM-GCC-64/bin/../libexec/gcc/x86_64-w64-mingw32/10.3.0/lto-wrapper.exe
  Target: x86_64-w64-mingw32
  Configured with: ../../../src/gcc-git-10.3.0/configure --build=x86_64-w64-mingw32 --enable-targets=all --enable-languages=ada,c,c++,fortran,jit,lto,objc,obj-c++
   --enable-libgomp --enable-lto --enable-graphite --enable-cxx-flags=-DWINPTHREAD_STATIC --disable-build-with-cxx --disable-build-poststage1-with-cxx 
   --enable-libstdcxx-debug --enable-threads=posix --enable-version-specific-runtime-libs --enable-fully-dynamic-string --enable-libstdcxx-filesystem-ts=yes 
   --disable-libstdcxx-pch --enable-libstdcxx-threads --enable-libstdcxx-time=yes --enable-mingw-wildcard --with-gnu-ld --disable-werror --enable-nls 
   --disable-win32-registry --enable-large-address-aware --disable-rpath --disable-symvers --prefix=/mingw64tdm --with-local-prefix=/mingw64tdm 
   --with-pkgversion=tdm64-1 --with-bugurl=https://github.com/jmeubank/tdm-gcc/issues
  Thread model: posix
  Supported LTO compression algorithms: zlib zstd
  gcc version 10.3.0 (tdm64-1)
  ```
  
- Now the magic trick to get Code::Blocks to shut up and **find** that GCC install:

  + Open Code::Blocks. Ignore that pesky Environment Error Message.
  
  + Go to Settings > Compiler
  
  + In that dialog, click on the "**Reset defaults**" button.
  
  + 🥳 Code::Blocks will show a quick message that it has auto-discovered GCC in `C:\TDM-GCC-64\` and is ready for use.
  
  + Check the Settings > Debugger config for good measure.
  
  + Have fun. 🍭
  
### Extra

[Code::Blocks](https://www.codeblocks.org/) also provides daily builds; when you feel a little adventurous, you can download those, depack the 7z archives in a temp directory and then copy them all into the `C:\Program Files\CodeBlocks\...` installation directory to have a bleeding edge build at your fingertips. Works for me. 🍭

(The bitchy bit was getting Code::Blocks to discover *any* GCC rig I have on this dev box. May have been due to having uninstalled an older Code::blocks version first, whatever, it didn't fly until I hit that "Reset defaults" button.)




