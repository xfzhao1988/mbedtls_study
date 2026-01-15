README for Mbed TLS
Mbed TLS 自述文件
===================
===================

Mbed TLS is a C library that implements cryptographic primitives (including the [PSA Cryptography API](#psa-cryptography-api)), X.509 certificate manipulation and the SSL/TLS and DTLS protocols. Its small code footprint makes it suitable for embedded systems.
Mbed TLS 是一个 C 语言库，实现了密码学原语（包括 [PSA 密码学 API](#psa-cryptography-api)）、X.509 证书处理以及 SSL/TLS 和 DTLS 协议。其代码占用小，适用于嵌入式系统。

Configuration
配置
-------------
-------------

Mbed TLS should build out of the box on most systems. Some platform specific options are available in the fully documented configuration file `include/mbedtls/mbedtls_config.h`, which is also the place where features can be selected. This file can be edited manually, or in a more programmatic way using the Python 3 script `scripts/config.py` (use `--help` for usage instructions).
Mbed TLS 在大多数系统上应当开箱即用即可构建。某些平台相关选项可在完整文档化的配置文件 `include/mbedtls/mbedtls_config.h` 中找到，这里也是选择功能特性的地方。该文件可以手动编辑，也可以使用 Python 3 脚本 `scripts/config.py` 以更程序化的方式编辑（使用 `--help` 查看用法说明）。

Compiler options can be set using conventional environment variables such as `CC` and `CFLAGS` when using the Make and CMake build system (see below).
在使用 Make 和 CMake 构建系统时（见下文），可通过常规环境变量如 `CC` 和 `CFLAGS` 来设置编译器选项。

We provide some non-standard configurations focused on specific use cases in the `configs/` directory. You can read more about those in `configs/README.txt`
我们在 `configs/` 目录提供了一些面向特定用例的非标准配置。更多内容请参见 `configs/README.txt`。

Documentation
文档
-------------
-------------

The main Mbed TLS documentation is available via [ReadTheDocs](https://mbed-tls.readthedocs.io/).
Mbed TLS 的主要文档可在 [ReadTheDocs](https://mbed-tls.readthedocs.io/) 获取。

Documentation for the PSA Cryptography API is available [on GitHub](https://arm-software.github.io/psa-api/crypto/).
PSA 密码学 API 的文档可在 [GitHub](https://arm-software.github.io/psa-api/crypto/) 获取。

To generate a local copy of the library documentation in HTML format, tailored to your compile-time configuration:
要生成与编译时配置相匹配的本地 HTML 格式库文档：

1. Make sure that [Doxygen](http://www.doxygen.nl/) is installed.
1. 确保已安装 [Doxygen](http://www.doxygen.nl/)。
1. Run `make apidoc`.
1. 运行 `make apidoc`。
1. Browse `apidoc/index.html` or `apidoc/modules.html`.
1. 浏览 `apidoc/index.html` 或 `apidoc/modules.html`。

For other sources of documentation, see the [SUPPORT](SUPPORT.md) document.
其他文档来源请参见 [SUPPORT](SUPPORT.md) 文档。

Compiling
编译
---------
---------

There are currently three active build systems used within Mbed TLS releases:
目前 Mbed TLS 发布版本中有三种在用的构建系统：

-   GNU Make
-   GNU Make
-   CMake
-   CMake
-   Microsoft Visual Studio
-   Microsoft Visual Studio

The main systems used for development are CMake and GNU Make. Those systems are always complete and up-to-date. The others should reflect all changes present in the CMake and Make build system, although features may not be ported there automatically.
开发主要使用的系统是 CMake 和 GNU Make。这些系统始终完整且保持最新。其他系统应当反映 CMake 与 Make 构建系统中的全部变更，但功能可能不会自动移植过去。

The Make and CMake build systems create three libraries: libmbedcrypto, libmbedx509, and libmbedtls. Note that libmbedtls depends on libmbedx509 and libmbedcrypto, and libmbedx509 depends on libmbedcrypto. As a result, some linkers will expect flags to be in a specific order, for example the GNU linker wants `-lmbedtls -lmbedx509 -lmbedcrypto`.
Make 和 CMake 构建系统会生成三个库：libmbedcrypto、libmbedx509 和 libmbedtls。请注意，libmbedtls 依赖 libmbedx509 和 libmbedcrypto，而 libmbedx509 依赖 libmbedcrypto。因此，某些链接器要求特定的链接顺序，例如 GNU 链接器要求 `-lmbedtls -lmbedx509 -lmbedcrypto`。

### Tool versions
### 工具版本

You need the following tools to build the library with the provided makefiles:
使用提供的 makefile 构建该库需要以下工具：

* GNU Make 3.82 or a build tool that CMake supports.
* GNU Make 3.82 或 CMake 支持的构建工具。
* A C99 toolchain (compiler, linker, archiver). We actively test with GCC 5.4, Clang 3.8, Arm Compiler 6, IAR 8 and Visual Studio 2017. More recent versions should work. Slightly older versions may work.
* C99 工具链（编译器、链接器、归档器）。我们经常测试 GCC 5.4、Clang 3.8、Arm Compiler 6、IAR 8 和 Visual Studio 2017。更新版本通常可用，稍旧版本也可能可用。
* Python 3.8 to generate the test code. Python is also needed to integrate PSA drivers and to build the development branch (see next section).
* Python 3.8 用于生成测试代码。Python 也用于集成 PSA 驱动并构建开发分支（见下一节）。
* Perl to run the tests, and to generate some source files in the development branch.
* Perl 用于运行测试，并在开发分支中生成部分源文件。
* CMake 3.10.2 or later (if using CMake).
* CMake 3.10.2 或更高版本（如果使用 CMake）。
* Microsoft Visual Studio 2017 or later (if using Visual Studio).
* Microsoft Visual Studio 2017 或更高版本（如果使用 Visual Studio）。
* Doxygen 1.8.11 or later (if building the documentation; slightly older versions should work).
* Doxygen 1.8.11 或更高版本（如需生成文档；稍旧版本也可能可用）。

### Git usage
### Git 用法

The `development` branch and the `mbedtls-3.6` long-term support branch of Mbed TLS use a [Git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules#_cloning_submodules) ([framework](https://github.com/Mbed-TLS/mbedtls-framework)). This is not needed to merely compile the library at a release tag. This is not needed to consume a release archive (zip or tar).
Mbed TLS 的 `development` 分支和 `mbedtls-3.6` 长期支持分支使用 [Git 子模块](https://git-scm.com/book/en/v2/Git-Tools-Submodules#_cloning_submodules)（[framework](https://github.com/Mbed-TLS/mbedtls-framework)）。仅在发布标签上编译库时不需要该子模块。使用发布版归档（zip 或 tar）时也不需要。

### Generated source files in the development branch
### 开发分支中的生成源文件

The source code of Mbed TLS includes some files that are automatically generated by scripts and whose content depends only on the Mbed TLS source, not on the platform or on the library configuration. These files are not included in the development branch of Mbed TLS, but the generated files are included in official releases. This section explains how to generate the missing files in the development branch.
Mbed TLS 源代码包含一些由脚本自动生成的文件，其内容只依赖 Mbed TLS 源码，不依赖平台或库配置。这些文件不包含在 Mbed TLS 的开发分支中，但生成后的文件包含在官方发布版本中。本节说明如何在开发分支中生成缺失的文件。

The following tools are required:
需要以下工具：

* Perl, for some library source files and for Visual Studio build files.
* Perl，用于部分库源文件以及 Visual Studio 构建文件。
* Python 3.8 and some Python packages, for some library source files, sample programs and test data. To install the necessary packages, run:
* Python 3.8 及一些 Python 包，用于部分库源文件、示例程序和测试数据。要安装所需包，请运行：
    ```
    ```
    python3 -m pip install --user -r scripts/basic.requirements.txt
    python3 -m pip install --user -r scripts/basic.requirements.txt
    ```
    ```
    Depending on your Python installation, you may need to invoke `python` instead of `python3`. To install the packages system-wide, omit the `--user` option.
    根据你的 Python 安装情况，可能需要使用 `python` 而不是 `python3`。如需系统范围安装，请省略 `--user` 选项。
* A C compiler for the host platform, for some test data.
* 用于主机平台的 C 编译器，用于生成部分测试数据。

The scripts that generate the configuration-independent files will look for a host C compiler in the following places (in order of preference):
生成与配置无关文件的脚本会在以下位置查找主机 C 编译器（按优先级顺序）：

1. The `HOSTCC` environment variable. This can be used if `CC` is pointing to a cross-compiler.
1. `HOSTCC` 环境变量。如果 `CC` 指向交叉编译器，可使用该变量。
2. The `CC` environment variable.
2. `CC` 环境变量。
3. An executable called `cc` in the current path.
3. 当前路径中的 `cc` 可执行文件。

Note: If you have multiple toolchains installed, it is recommended to set `CC` or `HOSTCC` to the intended host compiler before generating the files.
注意：如果安装了多个工具链，建议在生成文件前将 `CC` 或 `HOSTCC` 设置为目标主机编译器。

Any of the following methods are available to generate the configuration-independent files:
可以通过以下任一方法生成与配置无关的文件：

* If not cross-compiling, running `make` with any target, or just `make`, will automatically generate required files.
* 如果不是交叉编译，运行 `make` 的任意目标，或直接运行 `make`，会自动生成所需文件。
* On non-Windows systems, when not cross-compiling, CMake will generate the required files automatically.
* 在非 Windows 系统且不是交叉编译时，CMake 会自动生成所需文件。
* Run `make generated_files` to generate all the configuration-independent files.
* 运行 `make generated_files` 以生成所有与配置无关的文件。
* On Unix/POSIX systems, run `tests/scripts/check-generated-files.sh -u` to generate all the configuration-independent files.
* 在 Unix/POSIX 系统上，运行 `tests/scripts/check-generated-files.sh -u` 以生成所有与配置无关的文件。
* On Windows, run `scripts\make_generated_files.bat` to generate all the configuration-independent files.
* 在 Windows 上，运行 `scripts\make_generated_files.bat` 以生成所有与配置无关的文件。

### Make
### Make

We require GNU Make. To build the library and the sample programs, GNU Make and a C compiler are sufficient. Some of the more advanced build targets require some Unix/Linux tools.
我们要求使用 GNU Make。要构建库和示例程序，只需 GNU Make 和 C 编译器即可。某些更高级的构建目标需要一些 Unix/Linux 工具。

We intentionally only use a minimum of functionality in the makefiles in order to keep them as simple and independent of different toolchains as possible, to allow users to more easily move between different platforms. Users who need more features are recommended to use CMake.
我们刻意在 makefile 中只使用最少功能，以尽可能保持简单并独立于不同工具链，方便用户在不同平台之间迁移。需要更多特性的用户建议使用 CMake。

In order to build from the source code using GNU Make, just enter at the command line:
要使用 GNU Make 从源码构建，只需在命令行输入：

    make
    make

In order to run the tests, enter:
要运行测试，请输入：

    make check
    make check

The tests need Python to be built and Perl to be run. If you don't have one of them installed, you can skip building the tests with:
测试需要 Python 来构建、Perl 来运行。如果其中一个未安装，可以用以下命令跳过构建测试：

    make no_test
    make no_test

You'll still be able to run a much smaller set of tests with:
你仍然可以运行一小部分测试：

    programs/test/selftest
    programs/test/selftest

In order to build for a Windows platform, you should use `WINDOWS_BUILD=1` if the target is Windows but the build environment is Unix-like (for instance when cross-compiling, or compiling from an MSYS shell), and `WINDOWS=1` if the build environment is a Windows shell (for instance using mingw32-make) (in that case some targets will not be available).
如需构建 Windows 平台，如果目标是 Windows 但构建环境是类 Unix（例如交叉编译或从 MSYS shell 编译），应使用 `WINDOWS_BUILD=1`；如果构建环境是 Windows shell（例如使用 mingw32-make），应使用 `WINDOWS=1`（此时某些目标不可用）。

Setting the variable `SHARED` in your environment will build shared libraries in addition to the static libraries. Setting `DEBUG` gives you a debug build. You can override `CFLAGS` and `LDFLAGS` by setting them in your environment or on the make command line; compiler warning options may be overridden separately using `WARNING_CFLAGS`. Some directory-specific options (for example, `-I` directives) are still preserved.
在环境中设置变量 `SHARED` 将在静态库之外构建共享库。设置 `DEBUG` 将生成调试构建。你可以在环境中或在 make 命令行中设置 `CFLAGS` 和 `LDFLAGS` 来覆盖它们；编译器警告选项可通过 `WARNING_CFLAGS` 单独覆盖。某些目录特定选项（例如 `-I` 指令）仍会保留。

Please note that setting `CFLAGS` overrides its default value of `-O2` and setting `WARNING_CFLAGS` overrides its default value (starting with `-Wall -Wextra`), so if you just want to add some warning options to the default ones, you can do so by setting `CFLAGS=-O2 -Werror` for example. Setting `WARNING_CFLAGS` is useful when you want to get rid of its default content (for example because your compiler doesn't accept `-Wall` as an option). Directory-specific options cannot be overridden from the command line.
请注意，设置 `CFLAGS` 会覆盖其默认值 `-O2`，设置 `WARNING_CFLAGS` 会覆盖其默认值（以 `-Wall -Wextra` 开头），因此如果只是想在默认值上添加一些警告选项，可以例如设置 `CFLAGS=-O2 -Werror`。当你想去掉 `WARNING_CFLAGS` 的默认内容时（例如你的编译器不接受 `-Wall` 作为选项），设置 `WARNING_CFLAGS` 会很有用。目录特定选项无法在命令行中覆盖。

Depending on your platform, you might run into some issues. Please check the Makefiles in `library/`, `programs/` and `tests/` for options to manually add or remove for specific platforms. You can also check [the Mbed TLS Knowledge Base](https://mbed-tls.readthedocs.io/en/latest/kb/) for articles on your platform or issue.
根据你的平台，可能会遇到一些问题。请检查 `library/`、`programs/` 和 `tests/` 中的 Makefile，了解需要为特定平台手动添加或移除的选项。你也可以查看 [Mbed TLS Knowledge Base](https://mbed-tls.readthedocs.io/en/latest/kb/) 获取与你的平台或问题相关的文章。

In case you find that you need to do something else as well, please let us know what, so we can add it to the [Mbed TLS Knowledge Base](https://mbed-tls.readthedocs.io/en/latest/kb/).
如果你发现还需要做其他事情，请告诉我们，以便将其加入 [Mbed TLS Knowledge Base](https://mbed-tls.readthedocs.io/en/latest/kb/)。

### CMake
### CMake

In order to build the source using CMake in a separate directory (recommended), just enter at the command line:
要在单独目录中使用 CMake 构建源码（推荐），只需在命令行输入：

    mkdir /path/to/build_dir && cd /path/to/build_dir
    mkdir /path/to/build_dir && cd /path/to/build_dir
    cmake /path/to/mbedtls_source
    cmake /path/to/mbedtls_source
    cmake --build .
    cmake --build .

In order to run the tests, enter:
要运行测试，请输入：

    ctest
    ctest

The test suites need Python to be built and Perl to be executed. If you don't have one of these installed, you'll want to disable the test suites with:
测试套件需要 Python 来构建、Perl 来执行。如果你没有安装其中之一，请使用以下命令禁用测试套件：

    cmake -DENABLE_TESTING=Off /path/to/mbedtls_source
    cmake -DENABLE_TESTING=Off /path/to/mbedtls_source

If you disabled the test suites, but kept the programs enabled, you can still run a much smaller set of tests with:
如果你禁用了测试套件但保留了程序构建，仍可通过以下方式运行一小部分测试：

    programs/test/selftest
    programs/test/selftest

To configure CMake for building shared libraries, use:
要配置 CMake 以构建共享库，请使用：

    cmake -DUSE_SHARED_MBEDTLS_LIBRARY=On /path/to/mbedtls_source
    cmake -DUSE_SHARED_MBEDTLS_LIBRARY=On /path/to/mbedtls_source

There are many different build modes available within the CMake buildsystem. Most of them are available for gcc and clang, though some are compiler-specific:
CMake 构建系统提供了多种构建模式。大多数可用于 gcc 和 clang，但也有一些是编译器特定的：

-   `Release`. This generates the default code without any unnecessary information in the binary files.
-   `Release`。生成默认代码，二进制文件中不包含不必要的信息。
-   `Debug`. This generates debug information and disables optimization of the code.
-   `Debug`。生成调试信息并禁用优化。
-   `Coverage`. This generates code coverage information in addition to debug information.
-   `Coverage`。在生成调试信息的同时生成代码覆盖率信息。
-   `ASan`. This instruments the code with AddressSanitizer to check for memory errors. (This includes LeakSanitizer, with recent version of gcc and clang.) (With recent version of clang, this mode also instruments the code with UndefinedSanitizer to check for undefined behaviour.)
-   `ASan`。使用 AddressSanitizer 对代码进行插桩以检查内存错误。（这包括 LeakSanitizer，适用于较新版本的 gcc 和 clang。）（在较新版本的 clang 上，该模式还会使用 UndefinedSanitizer 检查未定义行为。）
-   `ASanDbg`. Same as ASan but slower, with debug information and better stack traces.
-   `ASanDbg`。与 ASan 类似但更慢，包含调试信息并提供更好的栈追踪。
-   `MemSan`. This instruments the code with MemorySanitizer to check for uninitialised memory reads. Experimental, needs recent clang on Linux/x86\_64.
-   `MemSan`。使用 MemorySanitizer 检查未初始化内存读取。实验性，需要较新的 clang 在 Linux/x86\_64 上。
-   `MemSanDbg`. Same as MemSan but slower, with debug information, better stack traces and origin tracking.
-   `MemSanDbg`。与 MemSan 类似但更慢，包含调试信息、更好的栈追踪和来源跟踪。
-   `Check`. This activates the compiler warnings that depend on optimization and treats all warnings as errors.
-   `Check`。启用依赖优化的编译器警告并将所有警告视为错误。

Switching build modes in CMake is simple. For debug mode, enter at the command line:
在 CMake 中切换构建模式很简单。要使用调试模式，在命令行输入：

    cmake -D CMAKE_BUILD_TYPE=Debug /path/to/mbedtls_source
    cmake -D CMAKE_BUILD_TYPE=Debug /path/to/mbedtls_source

To list other available CMake options, use:
要列出其他可用的 CMake 选项，请使用：

    cmake -LH
    cmake -LH

Note that, with CMake, you can't adjust the compiler or its flags after the
请注意，使用 CMake 时，在完成初次
initial invocation of cmake. This means that `CC=your_cc make` and `make
调用 cmake 后，你无法再调整编译器或其标志。这意味着 `CC=your_cc make` 和 `make
CC=your_cc` will *not* work (similarly with `CFLAGS` and other variables).
CC=your_cc` 将 *无法* 工作（`CFLAGS` 等变量同理）。
These variables need to be adjusted when invoking cmake for the first time,
这些变量需要在首次调用 cmake 时进行调整，
for example:
例如：

    CC=your_cc cmake /path/to/mbedtls_source
    CC=your_cc cmake /path/to/mbedtls_source

If you already invoked cmake and want to change those settings, you need to
如果你已经调用了 cmake 并想更改这些设置，就需要
remove the build directory and create it again.
删除构建目录并重新创建。

Note that it is possible to build in-place; this will however overwrite the
需要注意的是，可以进行就地构建；但这会覆盖
provided Makefiles (see `scripts/tmp_ignore_makefiles.sh` if you want to
提供的 Makefile（如果你想避免 `git status` 显示它们被修改，请参见
prevent `git status` from showing them as modified). In order to do so, from
 `scripts/tmp_ignore_makefiles.sh`）。为此，在
the Mbed TLS source directory, use:
Mbed TLS 源码目录中使用：

    cmake .
    cmake .
    make
    make

If you want to change `CC` or `CFLAGS` afterwards, you will need to remove the
如果你想在之后更改 `CC` 或 `CFLAGS`，需要删除
CMake cache. This can be done with the following command using GNU find:
CMake 缓存。可使用 GNU find 的以下命令完成：

    find . -iname '*cmake*' -not -name CMakeLists.txt -exec rm -rf {} +
    find . -iname '*cmake*' -not -name CMakeLists.txt -exec rm -rf {} +

You can now make the desired change:
你现在可以进行所需的更改：

    CC=your_cc cmake .
    CC=your_cc cmake .
    make
    make

Regarding variables, also note that if you set CFLAGS when invoking cmake,
关于变量还需注意，如果在调用 cmake 时设置了 CFLAGS，
your value of CFLAGS doesn't override the content provided by cmake (depending
你的 CFLAGS 值不会覆盖 cmake 提供的内容（取决于
on the build mode as seen above), it's merely prepended to it.
上述构建模式），而只是被前置到其前面。

#### Consuming Mbed TLS
#### 使用 Mbed TLS

Mbed TLS provides a package config file for consumption as a dependency in other
Mbed TLS 提供了一个包配置文件，可作为其他
CMake projects. You can include Mbed TLS's CMake targets yourself with:
CMake 项目的依赖使用。你可以通过以下方式自行引入 Mbed TLS 的 CMake 目标：

    find_package(MbedTLS)
    find_package(MbedTLS)

If prompted, set `MbedTLS_DIR` to `${YOUR_MBEDTLS_INSTALL_DIR}/cmake`. This
如果提示，将 `MbedTLS_DIR` 设置为 `${YOUR_MBEDTLS_INSTALL_DIR}/cmake`。这会
creates the following targets:
创建以下目标：

- `MbedTLS::mbedcrypto` (Crypto library)
- `MbedTLS::mbedcrypto`（加密库）
- `MbedTLS::mbedtls` (TLS library)
- `MbedTLS::mbedtls`（TLS 库）
- `MbedTLS::mbedx509` (X509 library)
- `MbedTLS::mbedx509`（X509 库）

You can then use these directly through `target_link_libraries()`:
随后可以通过 `target_link_libraries()` 直接使用这些目标：

    add_executable(xyz)
    add_executable(xyz)

    target_link_libraries(xyz
    target_link_libraries(xyz
        PUBLIC MbedTLS::mbedtls
        PUBLIC MbedTLS::mbedtls
               MbedTLS::mbedcrypto
               MbedTLS::mbedcrypto
               MbedTLS::mbedx509)
               MbedTLS::mbedx509)

This will link the Mbed TLS libraries to your library or application, and add
这会把 Mbed TLS 库链接到你的库或应用，并将
its include directories to your target (transitively, in the case of `PUBLIC` or
其包含目录添加到你的目标中（在 `PUBLIC` 或
`INTERFACE` link libraries).
`INTERFACE` 链接库的情况下是传递性的）。

#### Mbed TLS as a subproject
#### 将 Mbed TLS 作为子项目

Mbed TLS supports being built as a CMake subproject. One can
Mbed TLS 支持作为 CMake 子项目构建。可以
use `add_subdirectory()` from a parent CMake project to include Mbed TLS as a
在父 CMake 项目中使用 `add_subdirectory()` 将 Mbed TLS 作为
subproject.
子项目引入。

### Microsoft Visual Studio
### Microsoft Visual Studio

The build files for Microsoft Visual Studio are generated for Visual Studio 2017.
Microsoft Visual Studio 的构建文件是为 Visual Studio 2017 生成的。

The solution file `mbedTLS.sln` contains all the basic projects needed to build the library and all the programs. The files in tests are not generated and compiled, as these need Python and perl environments as well. However, the selftest program in `programs/test/` is still available.
解决方案文件 `mbedTLS.sln` 包含构建库和所有程序所需的全部基本项目。tests 中的文件未生成也未编译，因为它们还需要 Python 和 perl 环境。不过，`programs/test/` 中的 selftest 程序仍可用。

In the development branch of Mbed TLS, the Visual Studio solution files need to be generated first as described in [“Generated source files in the development branch”](#generated-source-files-in-the-development-branch).
在 Mbed TLS 的开发分支中，需要先按照 [“开发分支中的生成源文件”](#generated-source-files-in-the-development-branch) 的描述生成 Visual Studio 解决方案文件。

Example programs
示例程序
----------------
----------------

We've included example programs for a lot of different features and uses in [`programs/`](programs/README.md).
我们在 [`programs/`](programs/README.md) 中包含了大量不同功能和用途的示例程序。
Please note that the goal of these sample programs is to demonstrate specific features of the library, and the code may need to be adapted to build a real-world application.
请注意，这些示例程序的目标是演示库的特定功能，代码可能需要调整才能构建实际应用。

Tests
测试
-----
-----

Mbed TLS includes an elaborate test suite in `tests/` that initially requires Python to generate the tests files (e.g. `test\_suite\_mpi.c`). These files are generated from a `function file` (e.g. `suites/test\_suite\_mpi.function`) and a `data file` (e.g. `suites/test\_suite\_mpi.data`). The `function file` contains the test functions. The `data file` contains the test cases, specified as parameters that will be passed to the test function.
Mbed TLS 在 `tests/` 中包含一套完善的测试套件，初始需要 Python 来生成测试文件（例如 `test\_suite\_mpi.c`）。这些文件由一个 `function file`（例如 `suites/test\_suite\_mpi.function`）和一个 `data file`（例如 `suites/test\_suite\_mpi.data`）生成。`function file` 包含测试函数。`data file` 包含测试用例，以参数形式传给测试函数。

For machines with a Unix shell and OpenSSL (and optionally GnuTLS) installed, additional test scripts are available:
对于安装了 Unix shell 和 OpenSSL（可选 GnuTLS）的机器，还提供了额外的测试脚本：

-   `tests/ssl-opt.sh` runs integration tests for various TLS options (renegotiation, resumption, etc.) and tests interoperability of these options with other implementations.
-   `tests/ssl-opt.sh` 运行各种 TLS 选项（重新协商、恢复等）的集成测试，并测试这些选项与其他实现的互操作性。
-   `tests/compat.sh` tests interoperability of every ciphersuite with other implementations.
-   `tests/compat.sh` 测试每个密码套件与其他实现的互操作性。
-   `tests/scripts/test-ref-configs.pl` test builds in various reduced configurations.
-   `tests/scripts/test-ref-configs.pl` 在多种精简配置下进行构建测试。
-   `tests/scripts/depends.py` test builds in configurations with a single curve, key exchange, hash, cipher, or pkalg on.
-   `tests/scripts/depends.py` 在仅启用单一曲线、密钥交换、哈希、密码或 pkalg 的配置下进行构建测试。
-   `tests/scripts/all.sh` runs a combination of the above tests, plus some more, with various build options (such as ASan, full `mbedtls_config.h`, etc).
-   `tests/scripts/all.sh` 运行上述测试的组合，并加上一些其他测试，使用多种构建选项（例如 ASan、完整的 `mbedtls_config.h` 等）。

Instead of manually installing the required versions of all tools required for testing, it is possible to use the Docker images from our CI systems, as explained in [our testing infrastructure repository](https://github.com/Mbed-TLS/mbedtls-test/blob/main/README.md#quick-start).
无需手动安装测试所需的所有工具版本，也可以使用我们 CI 系统中的 Docker 镜像，详见 [我们的测试基础设施仓库](https://github.com/Mbed-TLS/mbedtls-test/blob/main/README.md#quick-start)。

Porting Mbed TLS
移植 Mbed TLS
----------------
----------------

Mbed TLS can be ported to many different architectures, OS's and platforms. Before starting a port, you may find the following Knowledge Base articles useful:
Mbed TLS 可以移植到多种不同架构、操作系统和平台。在开始移植之前，以下知识库文章可能会有帮助：

-   [Porting Mbed TLS to a new environment or OS](https://mbed-tls.readthedocs.io/en/latest/kb/how-to/how-do-i-port-mbed-tls-to-a-new-environment-OS/)
-   [将 Mbed TLS 移植到新的环境或操作系统](https://mbed-tls.readthedocs.io/en/latest/kb/how-to/how-do-i-port-mbed-tls-to-a-new-environment-OS/)
-   [What external dependencies does Mbed TLS rely on?](https://mbed-tls.readthedocs.io/en/latest/kb/development/what-external-dependencies-does-mbedtls-rely-on/)
-   [Mbed TLS 依赖哪些外部依赖项？](https://mbed-tls.readthedocs.io/en/latest/kb/development/what-external-dependencies-does-mbedtls-rely-on/)
-   [How do I configure Mbed TLS](https://mbed-tls.readthedocs.io/en/latest/kb/compiling-and-building/how-do-i-configure-mbedtls/)
-   [如何配置 Mbed TLS](https://mbed-tls.readthedocs.io/en/latest/kb/compiling-and-building/how-do-i-configure-mbedtls/)

Mbed TLS is mostly written in portable C99; however, it has a few platform requirements that go beyond the standard, but are met by most modern architectures:
Mbed TLS 主要使用可移植的 C99 编写；不过它对平台有一些超出标准的要求，但大多数现代架构都满足：

- Bytes must be 8 bits.
- 字节必须为 8 位。
- All-bits-zero must be a valid representation of a null pointer.
- 全 0 比特必须是空指针的有效表示。
- Signed integers must be represented using two's complement.
- 有符号整数必须使用二进制补码表示。
- `int` and `size_t` must be at least 32 bits wide.
- `int` 和 `size_t` 必须至少为 32 位宽。
- The types `uint8_t`, `uint16_t`, `uint32_t` and their signed equivalents must be available.
- 类型 `uint8_t`、`uint16_t`、`uint32_t` 及其有符号等价类型必须可用。
- Mixed-endian platforms are not supported.
- 不支持混合端序平台。
- SIZE_MAX must be at least as big as INT_MAX and UINT_MAX.
- SIZE_MAX 必须至少与 INT_MAX 和 UINT_MAX 一样大。

PSA cryptography API
PSA 密码学 API
--------------------
--------------------

### PSA API
### PSA API

Arm's [Platform Security Architecture (PSA)](https://developer.arm.com/architectures/security-architectures/platform-security-architecture) is a holistic set of threat models, security analyses, hardware and firmware architecture specifications, and an open source firmware reference implementation. PSA provides a recipe, based on industry best practice, that allows security to be consistently designed in, at both a hardware and firmware level.
Arm 的 [平台安全架构（PSA）](https://developer.arm.com/architectures/security-architectures/platform-security-architecture) 是一整套威胁模型、安全分析、硬件与固件架构规范，以及一个开源固件参考实现。PSA 基于行业最佳实践提供了一套配方，使安全能够在硬件与固件层面得到一致设计。

The [PSA cryptography API](https://arm-software.github.io/psa-api/crypto/) provides access to a set of cryptographic primitives. It has a dual purpose. First, it can be used in a PSA-compliant platform to build services, such as secure boot, secure storage and secure communication. Second, it can also be used independently of other PSA components on any platform.
[PSA 密码学 API](https://arm-software.github.io/psa-api/crypto/) 提供对一组密码学原语的访问。它具有双重目的。首先，它可用于 PSA 合规的平台中构建服务，例如安全启动、安全存储和安全通信。其次，它也可以在任何平台上独立于其他 PSA 组件使用。

The design goals of the PSA cryptography API include:
PSA 密码学 API 的设计目标包括：

* The API distinguishes caller memory from internal memory, which allows the library to be implemented in an isolated space for additional security. Library calls can be implemented as direct function calls if isolation is not desired, and as remote procedure calls if isolation is desired.
* API 区分调用方内存和内部内存，从而允许库在隔离空间中实现以增强安全性。如果不需要隔离，库调用可以实现为直接函数调用；若需要隔离，则可实现为远程过程调用。
* The structure of internal data is hidden to the application, which allows substituting alternative implementations at build time or run time, for example, in order to take advantage of hardware accelerators.
* 内部数据结构对应用隐藏，从而允许在构建时或运行时替换替代实现，例如利用硬件加速器。
* All access to the keys happens through key identifiers, which allows support for external cryptoprocessors that is transparent to applications.
* 对密钥的所有访问都通过密钥标识符进行，从而支持对应用透明的外部密码处理器。
* The interface to algorithms is generic, favoring algorithm agility.
* 算法接口是通用的，强调算法敏捷性。
* The interface is designed to be easy to use and hard to accidentally misuse.
* 接口设计为易于使用且不易被误用。

Arm welcomes feedback on the design of the API. If you think something could be improved, please open an issue on our Github repository. Alternatively, if you prefer to provide your feedback privately, please email us at [`mbed-crypto@arm.com`](mailto:mbed-crypto@arm.com). All feedback received by email is treated confidentially.
Arm 欢迎对 API 设计的反馈。如果你认为某些地方可以改进，请在我们的 Github 仓库提出 issue。或者，如果你希望私下提供反馈，请发送邮件至 [`mbed-crypto@arm.com`](mailto:mbed-crypto@arm.com)。通过邮件收到的所有反馈都会被保密处理。

### PSA implementation in Mbed TLS
### Mbed TLS 中的 PSA 实现

Mbed TLS includes an implementation of the PSA Cryptography API. It covers most, but not all algorithms.
Mbed TLS 包含 PSA 密码学 API 的实现。它覆盖了大多数（但不是全部）算法。

The X.509 and TLS code can use PSA cryptography for most operations. To enable this support, activate the compilation option `MBEDTLS_USE_PSA_CRYPTO` in `mbedtls_config.h`. Note that TLS 1.3 uses PSA cryptography for most operations regardless of this option. See `docs/use-psa-crypto.md` for details.
X.509 和 TLS 代码可以在大多数操作中使用 PSA 密码学。要启用该支持，请在 `mbedtls_config.h` 中激活编译选项 `MBEDTLS_USE_PSA_CRYPTO`。请注意，TLS 1.3 在大多数操作中无论该选项是否启用都会使用 PSA 密码学。详见 `docs/use-psa-crypto.md`。

### PSA drivers
### PSA 驱动

Mbed TLS supports drivers for cryptographic accelerators, secure elements and random generators. This is work in progress. Please note that the driver interfaces are not fully stable yet and may change without notice. We intend to preserve backward compatibility for application code (using the PSA Crypto API), but the code of the drivers may have to change in future minor releases of Mbed TLS.
Mbed TLS 支持加密加速器、安全元件和随机数生成器的驱动。这项工作仍在进行中。请注意，驱动接口尚未完全稳定，可能会在不另行通知的情况下更改。我们打算为应用代码（使用 PSA Crypto API）保持向后兼容性，但驱动代码可能需要在 Mbed TLS 的未来小版本中进行调整。

Please see the [PSA driver example and guide](docs/psa-driver-example-and-guide.md) for information on writing a driver.
有关编写驱动的信息，请参见 [PSA 驱动示例与指南](docs/psa-driver-example-and-guide.md)。

When using drivers, you will generally want to enable two compilation options (see the reference manual for more information):
使用驱动时，通常需要启用两个编译选项（更多信息请参阅参考手册）：

* `MBEDTLS_USE_PSA_CRYPTO` is necessary so that the X.509 and TLS code calls the PSA drivers rather than the built-in software implementation.
* `MBEDTLS_USE_PSA_CRYPTO` 是必要的，这样 X.509 和 TLS 代码才会调用 PSA 驱动而不是内置的软件实现。
* `MBEDTLS_PSA_CRYPTO_CONFIG` allows you to enable PSA cryptographic mechanisms without including the code of the corresponding software implementation. This is not yet supported for all mechanisms.
* `MBEDTLS_PSA_CRYPTO_CONFIG` 允许你在不包含相应软件实现代码的情况下启用 PSA 密码学机制。这一点尚未对所有机制支持。

License
许可证
-------
-------

Unless specifically indicated otherwise in a file, Mbed TLS files are provided under a dual [Apache-2.0](https://spdx.org/licenses/Apache-2.0.html) OR [GPL-2.0-or-later](https://spdx.org/licenses/GPL-2.0-or-later.html) license. See the [LICENSE](LICENSE) file for the full text of these licenses, and [the 'License and Copyright' section in the contributing guidelines](CONTRIBUTING.md#License-and-Copyright) for more information.
除非某个文件另有说明，Mbed TLS 文件在双重许可下提供：[Apache-2.0](https://spdx.org/licenses/Apache-2.0.html) 或 [GPL-2.0-or-later](https://spdx.org/licenses/GPL-2.0-or-later.html)。完整许可证文本请参见 [LICENSE](LICENSE) 文件，更多信息请参见贡献指南中的 [“License and Copyright”](CONTRIBUTING.md#License-and-Copyright) 一节。

### Third-party code included in Mbed TLS
### Mbed TLS 中包含的第三方代码

This project contains code from other projects. This code is located within the `3rdparty/` directory. The original license text is included within project subdirectories, where it differs from the normal Mbed TLS license, and/or in source files. The projects are listed below:
本项目包含来自其他项目的代码。这些代码位于 `3rdparty/` 目录中。原始许可文本包含在与 Mbed TLS 常规许可不同的项目子目录和/或源文件中。项目列表如下：

* `3rdparty/everest/`: Files stem from [Project Everest](https://project-everest.github.io/) and are distributed under the Apache 2.0 license.
* `3rdparty/everest/`：文件来自 [Project Everest](https://project-everest.github.io/)，按 Apache 2.0 许可分发。
* `3rdparty/p256-m/p256-m/`: Files have been taken from the [p256-m](https://github.com/mpg/p256-m) repository. The code in the original repository is distributed under the Apache 2.0 license. It is distributed in Mbed TLS under a dual Apache-2.0 OR GPL-2.0-or-later license with permission from the author.
* `3rdparty/p256-m/p256-m/`：文件取自 [p256-m](https://github.com/mpg/p256-m) 仓库。原始仓库中的代码按 Apache 2.0 许可分发。经作者许可，在 Mbed TLS 中以 Apache-2.0 或 GPL-2.0-or-later 的双重许可分发。

Contributing
贡献
------------
------------

We gratefully accept bug reports and contributions from the community. Please see the [contributing guidelines](CONTRIBUTING.md) for details on how to do this.
我们非常感谢社区的错误报告和贡献。详情请参见 [贡献指南](CONTRIBUTING.md)。

Contact
联系
-------
-------

* To report a security vulnerability in Mbed TLS, please email <mbed-tls-security@lists.trustedfirmware.org>. For more information, see [`SECURITY.md`](SECURITY.md).
* 报告 Mbed TLS 的安全漏洞，请发送邮件至 <mbed-tls-security@lists.trustedfirmware.org>。更多信息请参见 [`SECURITY.md`](SECURITY.md)。
* To report a bug or request a feature in Mbed TLS, please [file an issue on GitHub](https://github.com/Mbed-TLS/mbedtls/issues/new/choose).
* 报告 bug 或请求功能，请 [在 GitHub 上提交 issue](https://github.com/Mbed-TLS/mbedtls/issues/new/choose)。
* Please see [`SUPPORT.md`](SUPPORT.md) for other channels for discussion and support about Mbed TLS.
* 其他讨论与支持渠道请参见 [`SUPPORT.md`](SUPPORT.md)。
