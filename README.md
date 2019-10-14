# nds_vscode_template
[![License: CC0-1.0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)](http://creativecommons.org/publicdomain/zero/1.0/)

Develop Nintendo DS homebrew in a modern Visual Studio Code development environment.

  * ARM [devkitPro](https://devkitpro.org) toolchain
  * Emulation and debugging with [DeSmuME](https://desmume.org/)
  * Working IntelliSense in [VS Code](https://code.visualstudio.com/)

## Getting Started

Before this template will work, we need to do some homework and install the compiler toolchian, the emulator, and the necessary extensions for our development environment.

**NOTE**: These instructions are for Windows!

### devkitPro

**devkitPro** provides a set of compilers and tools so that we can create programs that are compatible with the ARM 7 and ARM 9 processors in the Nintendo DS.

Follow the instructions on the [Getting Started](https://devkitpro.org/wiki/Getting_Started) page to download the Windows graphical installer.

When you run the installer, make sure to leave the default options as is so that the paths in this template point to the correct place.

You can verify that the installation completed successfully by making sure you can see **devkitPro**>**MYSYS** in your Start Menu.

### DeSmuME

**DeSmuME** is a very stable Nintendo DS emulator that also provides basic tools for debugging our homebrew programs. Per the [DeSmuME FAQ](http://wiki.desmume.org/index.php?title=Faq#Does_the_GDB_stub_still_work.3F), the debugging functions in DeSmuME aren't completely fleshed out, but it works well enough to set breakpoints, step through code, watch memory locations for read/write operations, and other basic operations.

For this template we are going to download 2 separate versions of DeSmuME: one for release builds and one for debugging.

  * [DeSmuME 0.9.11 x32](http://sourceforge.net/projects/desmume/files/desmume/0.9.11/desmume-0.9.11-win32.zip/download) (Release emulator)
  * [DeSmuME 0.9.11 x32 Dev](https://sourceforge.net/projects/desmume/files/desmume/0.9.11/desmume-0.9.11-win32-dev.zip/download) (Development emulator)

To install, unzip the release emulator to `C:\desmume`. When the unzip is complete, you should have the executable at `C:\desmume\DeSmuME_0.9.11_x86.exe`.

Now for the development emulator, extract it to the same path: `C:\desmume`. Click the "Replace files at the destination" button when it prompts you. When the unzip is complete, the executable should be at `C:\desmume\DeSmuME_0.9.11_x86_dev+.exe`.

Double-click both the release and development emulators to make sure they work correctly. If you get an error about missing `MSVCP100.DLL`, you probably also need to install the x86 version of the [Microsoft Visual C++ 2010 Redistributable Package](http://www.microsoft.com/en-in/download/details.aspx?id=5555).

### VS Code

Install a copy of [Visual Studio Code](https://code.visualstudio.com/) if you don't have it already, and also install the following extensions:

  * [ARM](https://marketplace.visualstudio.com/items?itemName=dan-c-underwood.arm)
  * [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)
  * [C++ Intellisense](https://marketplace.visualstudio.com/items?itemName=austin.code-gnu-global)
  * [Make](https://marketplace.visualstudio.com/items?itemName=technosophos.vscode-make)

## Using this template

The C++ source code for your Nintendo DS program will go into the `source` directory. The `main.cpp` file in this template is from the `nds/hello_world` example that comes with devkitPro. You can use this as a starting point for your own program.

The `include` directory has a `vscode_fix.h` file that is used to fix IntelliSense behavior in Visual Studio Code. At the moment IntelliSense isn't smart enough to detect the feature flags that would be set by the compiler, so we add any interfaces that IntelliSense doesn't understand to this file.

For example, the `main.cpp` example code uses the `iprintf` function to print text to the screen. The `iprintf` function is defined in `C:\devkitPro\devkitARM\arm-none-eabi\include\stdio.h`, but it is protected by the `__MISC_VISIBLE` compiler feature. Since IntelliSense doesn't know what features our compiler has, we have to help it along by copying the interface from the `stdio.h` file and into `vscode_fix.h`.

The `vscode_fix.h` file is _only_ used by IntelliSense and will not compile with your code!

The `.vscode` directory holds the settings that VS Code should use for the project. The `c_cpp_properties.json` file determines what directories IntelliSense searches in to find code for your project. The `tasks.json` file defines useful tasks like `make` and `make clean` so you don't have to switch to your terminal application to run them. The `launch.json` file defines the `(gdb) Launch` task for running the debugger.

Running the `make` build task will create an `.nds` file at the root of the project. You can run this file in the emulator by running the `run` task.

---
To the extent possible under law, [cuibonobo](https://github.com/cuibonobo/) has [waived all copyright](https://creativecommons.org/publicdomain/zero/1.0/) and related or neighboring rights to this work.