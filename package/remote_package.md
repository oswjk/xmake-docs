
This has been initially supported after the 2.2.2 version, the usage is much simpler, just set the corresponding dependency package, for example:

```lua
add_requires("tbox 1.6.*", "libpng ~1.16", "zlib")

target("test")
    set_kind("binary")
    add_files("src/*.c")
    add_packages("tbox", "libpng", "zlib")
```

The above `add_requires` is used to describe the dependencies required by the current project, and `add_packages` is used to apply dependencies to the test target. Only settings will automatically add links, linkdirs, includedirs, etc.

Then directly compile:

```console
$ xmake
```

xmake will remotely pull the relevant source package, then automatically compile and install, finally compile the project, and link the dependency package. The specific effect is shown in the following figure:

<img src="/assets/img/index/package_manage.png" width="80%" />

For more information and progress on package dependency management see the related issues: [Remote package management](https://github.com/xmake-io/xmake/issues/69)

## Currently Supported Features

* Semantic version support, for example: ">= 1.1.0 < 1.2", "~1.6", "1.2.x", "1.*"
* Provide multi-repository management support such as official package repository, self-built private repository, project built-in repository, etc.
* Cross-platform package compilation integration support (packages of different platforms and different architectures can be installed at the same time, fast switching use)
* Debug dependency package support, source code debugging

## Dependency Package Processing Mechanism

Here we briefly introduce the processing mechanism of the entire dependency package:

<div align="center">
<img src="/assets/img/index/package_arch.png" width="80%" />
</div>

1. Priority check for the current system directory, whether there is a specified package under the third-party package management, if there is a matching package, then you do not need to download and install (of course you can also set the system package)
2. Retrieve the package matching the corresponding version, then download, compile, and install (Note: installed in a specific xmake directory, will not interfere with the system library environment)
3. Compile the project, and finally automatically link the enabled dependencies

## Semantic Version Settings

Xmake's dependency package management fully supports semantic version selection, for example: "~1.6.1". For a detailed description of the semantic version, see: [https://semver.org/](https://semver.org/)

Some semantic versions are written:

```lua
add_requires("tbox 1.6.*", "pcre 1.3.x", "libpng ^1.18")
add_requires("libpng ~1.16", "zlib 1.1.2 || >=1.2.11 <1.3.0")
```

The semantic version parser currently used by xmake is the [sv](https://github.com/uael/sv) library contributed by [uael](https://github.com/uael), which also has a description of the version. For detailed instructions, please refer to the following: [Version Description](https://github.com/uael/sv#versions)

Of course, if we have no special requirements for the current version of the dependency package, then we can write directly:

```lua
add_requires("tbox", "libpng", "zlib")
```

This will use the latest version of the package known, or the source code compiled by the master branch. If the current package has a git repo address, we can also specify a specific branch version:

```lua
add_requires("tbox master")
add_requires("tbox dev")
```

## Extra Package Information Settings

### Optional Package Settings

If the specified dependency package is not supported by the current platform, or if the compilation and installation fails, then xmake will compile the error, which is reasonable for some projects that must rely on certain packages to work.
However, if some packages are optional dependencies, they can be set to optional packages even if they are not compiled properly.

```lua
add_requires("tbox", {optional = true})
```

### Disable System Library

With the default settings, xmake will first check to see if the system library exists (if no version is required). If the user does not want to use the system library and the library provided by the third-party package management, then you can set:

```lua
add_requires("tbox", {system = false})
```

### Using the debug version of the package

If we want to debug the dependencies at the same time, we can set them to use the debug version of the package (provided that this package supports debug compilation):

```lua
add_requires("tbox", {debug = true})
```

If the current package does not support debug compilation, you can submit the modified compilation rules in the repository to support the debug, for example:

```lua
package("openssl")
    on_install("linux", "macosx", function (package)
        os.vrun("./config %s --prefix=\"%s\"", package:debug() and "--debug" or "", package:installdir())
        os.vrun("make -j4")
        os.vrun("make install")
    end)
```

### Passing additional compilation information to the package

Some packages have various compile options at compile time, and we can pass them in. Of course, the package itself supports:

```lua
add_requires("tbox", {configs = {small=true}})
```

Pass `--small=true` to the tbox package so that compiling the installed tbox package is enabled.

## Install third-party packages

After version 2.2.5, xmake supports support for dependency libraries in third-party package managers, such as: conan, brew, vcpkg, clib and etc.

### Add a homebrew dependency package

```lua
add_requires("brew::zlib", {alias = "zlib"}})
add_requires("brew::pcre2/libpcre2-8", {alias = "pcre2"}})

target("test")
    set_kind("binary")
    add_files("src/*.c") 
    add_packages("pcre2", "zlib")
```

### Add a vcpkg dependency package

```lua
add_requires("vcpkg::zlib", "vcpkg::pcre2")

target("test")
    set_kind("binary")
    add_files("src/*.c") 
    add_packages("vcpkg::zlib", "vcpkg::pcre2")
```

We can also add a package alias name to simplify the use of `add_packages`:

```lua
add_requires("vcpkg::zlib", {alias = "zlib"})
add_requires("vcpkg::pcre2", {alias = "pcre2"})

target("test")
    set_kind("binary")
    add_files("src/*.c") 
    add_packages("zlib", "pcre2")
```

### Add a conan dependency package

```lua
add_requires("CONAN::zlib/1.2.11@conan/stable", {alias = "zlib", debug = true})
add_requires("CONAN::OpenSSL/1.0.2n@conan/stable", {alias = "openssl", 
    configs = {options = "OpenSSL:shared=True"}})

target("test")
    set_kind("binary")
    add_files("src/*.c") 
    add_packages("openssl", "zlib")
```

After executing xmake to compile:

```console
ruki:test_package ruki$ xmake
checking for the architecture ... x86_64
checking for the Xcode directory ... /Applications/Xcode.app
checking for the SDK version of Xcode ... 10.14
note: try installing these packages (pass -y to skip confirm)?
  -> CONAN::zlib/1.2.11@conan/stable  (debug)
  -> CONAN::OpenSSL/1.0.2n@conan/stable  
please input: y (y/n)

  => installing CONAN::zlib/1.2.11@conan/stable .. ok
  => installing CONAN::OpenSSL/1.0.2n@conan/stable .. ok

[  0%]: ccache compiling.release src/main.c
[100%]: linking.release test
```

### Add a clib dependency package

Clib is a source-based dependency package manager. The dependent package is downloaded directly to the corresponding library source code, integrated into the project to compile, rather than binary library dependencies.

It is also very convenient to integrate in xmake. The only thing to note is that you need to add the source code of the corresponding library to xmake.lua, for example:

```lua
add_requires("clib::clibs/bytes@0.0.4", {alias = "bytes"})

target("test")
    set_kind("binary")
    add_files("clib/bytes/*.c")
    add_files("src/*.c")
    add_packages("bytes")
```

## Using self-built private package repository

If the required package is not in the official repository [xmake-repo](https://github.com/xmake-io/xmake-repo), we can submit the contribution code to the repository for support.
But if some packages are only for personal or private projects, we can create a private repository repo. The repository organization structure can be found at: [xmake-repo](https://github.com/xmake-io/xmake-repo)

For example, now we have a private repository repo:`git@github.com:myrepo/xmake-repo.git`

We can add the repository with the following command:

```console
$ xmake repo --add myrepo git@github.com:myrepo/xmake-repo.git
```

Starting with v2.2.3, support for adding repos for specified branches, for example:

```console
$ xmake repo --add myrepo git@github.com:myrepo/xmake-repo.git dev
```

Or we write directly in xmake.lua:

```lua
add_repositories("my-repo git@github.com:myrepo/xmake-repo.git")
```

If we just want to add one or two private packages, this time to build a git repo is too big, we can directly put the package repository into the project, for example:

```
projectdir
  - myrepo
    - packages
      - t/tbox/xmake.lua
      - z/zlib/xmake.lua
  - src
    - main.c
  - xmake.lua
```

The above myrepo directory is your own private package repository, built into your own project, and then add this repository location in xmake.lua:

```lua
add_repositories("my-repo myrepo")
```

This can be referred to [benchbox](https://github.com/tboox/benchbox) project, which has a built-in private repository.

We can even build a package without directly building a package description into the project xmake.lua, which is useful for relying on one or two packages, for example:

```lua
package("libjpeg")

    set_urls("http://www.ijg.org/files/jpegsrc.$(version).tar.gz")

    add_versions("v9c", "650250979303a649e21f87b5ccd02672af1ea6954b911342ea491f351ceb7122")

    on_install("windows", function (package)
        os.mv("jconfig.vc", "jconfig.h")
        os.vrun("nmake -f makefile.vc")
        os.cp("*.h", package:installdir("include"))
        os.cp("libjpeg.lib", package:installdir("lib"))
    end)

    on_install("macosx", "linux", function (package)
        import("package.tools.autoconf").install(package)
    end)

package_end()

add_requires("libjpeg")

target("test")
    set_kind("binary")
    add_files("src/*.c")
    add_packages("libjpeg")
```

## Package Management Command 

The package management command `$ xmake require` can be used to manually display the download, install, uninstall, retrieve, and view package information.

### Install the specified package

```console
$ xmake require tbox
```

Install the specified version package:

```console
$ xmake require tbox "~1.6"
```

Force a re-download of the installation and display detailed installation information:

```console
$ xmake require -f -v tbox "1.5.x"
```

Pass additional setup information:

```console
$ xmake require --extra="debug=true,config={small=true}" tbox
```

Install the debug package and pass the compilation configuration information of `small=true` to the package.

### Uninstall the specified package

```console
$ xmake require --uninstall tbox
```

This will completely uninstall the removal package file.

### Show package information

```console
$ xmake require --info tbox
```

### Search for packages in the current repository

```console
$ xmake require --search tbox
```

This is to support fuzzy search and lua pattern matching search:

```console
$ xmake require --search pcr
```

Will also search for pcre, pcre2 and other packages.

### List the currently installed packages

```console
$ xmake require --list
```

## Repository Management Command 

As mentioned above, adding a private repository is available (supporting local path addition):

```console
$ xmake repo --add myrepo git@github.com:myrepo/xmake-repo.git
```

We can also remove a repository that has already been installed:

```console
$ xmake repo --remove myrepo
```

Or view all the added repositories:

```console
$ xmake repo --list
```

If the remote repository has updates, you can manually perform a repository update to get more and the latest packages:

```console
$ xmake repo -u
```

## Submit packages to the official repository

### Package structure in repository

Before making our own package, we need to understand the structure of the next package repository, whether it is the official package repository or the self-built private package repository, the structure is the same:

```
xmake-repo
   - packages
     - t/tbox/xmake.lua
     - z/zlib/xmake.lua
```

Through the above structure, you can see that each package will have a xmake.lua to describe its installation rules, and according to the `z/zlib` two-level sub-category storage, convenient for quick retrieval.

### Package Description

The description rules for the package are basically done in its xmake.lua, which is similar to the xmake.lua description in the project project. The difference is that the description field only supports `package()`.

However, in the project xmake.lua, you can also directly add `package()` to the built-in package description, and even the package warehouse is saved, sometimes it will be more convenient.

First, let's take a look at zlib's description rules first. This rule can be found at [xmake-repo/z/zlib/xmake.lua](https://github.com/xmake-io/xmake-repo/blob Found under /master/packages/z/zlib/xmake.lua).

```
package("zlib")

    set_homepage("http://www.zlib.net")
    set_description("A Massively Spiffy Yet Delicately Unobtrusive Compression Library")

    set_urls("http://zlib.net/zlib-$(version).tar.gz",
             "https://downloads.sourceforge.net/project/libpng/zlib/$(version)/zlib-$(version).tar.gz")

    add_versions("1.2.10", "8d7e9f698ce48787b6e1c67e6bff79e487303e66077e25cb9784ac8835978017")
    add_versions("1.2.11", "c3e5e9fdd5004dcb542feda5ee4f0ff0744628baf8ed2dd5d66f8ca1197cb1a1")

    on_install("windows", function (package)
        io.gsub("win32/Makefile.msc", "%-MD", "-" .. package:config("vs_runtime"))
        os.vrun("nmake -f win32\\Makefile.msc zlib.lib")
        os.cp("zlib.lib", package:installdir("lib"))
        os.cp("*.h", package:installdir("include"))
    end)

    on_install("linux", "macosx", function (package)
        import("package.tools.autoconf").install(package, {"--static"})
    end)
 
    on_install("iphoneos", "android@linux,macosx", "mingw@linux,macosx", function (package)
        import("package.tools.autoconf").configure(package, {host = "", "--static"})
        io.gsub("Makefile", "\nAR=.-\n",      "\nAR=" .. (package:build_getenv("ar") or "") .. "\n")
        io.gsub("Makefile", "\nARFLAGS=.-\n", "\nARFLAGS=cr\n")
        io.gsub("Makefile", "\nRANLIB=.-\n",  "\nRANLIB=\n")
        os.vrun("make install -j4")
    end)

    on_test(function (package)
        assert(package:has_cfuncs("inflate", {includes = "zlib.h"}))
    end)
```

This package rule adds installation rules to windows, linux, macosx, iphoneos, mingw and other platforms. Basically, it has achieved full platform coverage, and even some cross-compilation platforms, which is a typical example.

Of course, some packages rely on source code implementation and are not completely cross-platform, so you only need to set the installation rules for the platforms it supports.

#### set_homepage

Set the official page address of the project where the package is located.

#### set_description

Set the package description information, generally see the relevant package information through `xmake require --info zlib`.

#### set_kind

Set the package type. For the dependent library, you don't need to set it. If it is an executable package, you need to set it to binary.

```
package("cmake")

    set_kind("binary")
    set_homepage("https://cmake.org")
    set_description("A cross-platform family of tool designed to build, test and package software")
```

#### set_urls

Set the source package or git repository address of the package. Unlike add_urls, this interface is the override setting, and add_urls is the additional setting. Other usage methods are similar. This is chosen according to different needs.

#### add_urls

Add the source package of the package or the git repository address. This interface is generally paired with add_version to set the version of each source package and the corresponding sha256 value.

!> You can add multiple urls as the mirror source, xmake will automatically detect the fastest url for download, and if the download fails, try other urls.

```lua
add_urls("https://github.com/protobuf-c/protobuf-c/releases/download/v$(version)/protobuf-c-$(version).tar.gz")
add_versions("1.3.1", "51472d3a191d6d7b425e32b612e477c06f73fe23e07f6a6a839b11808e9d2267")
```

The `$(version)` built-in variable in urls will be adapted according to the version selected during the actual installation, and the version number is selected from the list of versions specified in `add_versions`.

If there is a more complicated version string for urls and there is no direct correspondence with add_versions, you need to customize the conversion in the following way:

```lua
add_urls("https://sqlite.org/2018/sqlite-autoconf-$(version)000.tar.gz",
         {version = function (version) return version:gsub("%.", "") end})

add_versions("3.24.0", "d9d14e88c6fb6d68de9ca0d1f9797477d82fc3aed613558f87ffbdbbc5ceb74a")
add_versions("3.23.0", "b7711a1800a071674c2bf76898ae8584fc6c9643cfe933cfc1bc54361e3a6e49")
```

Of course, we can only add the git source address:

```lua
add_urls("https://gitlab.gnome.org/GNOME/libxml2.git")
```

If the source code package sha256 corresponding to multiple mirror addresses is different, we can set them separately by means of alias:

```lua
add_urls("https://ffmpeg.org/releases/ffmpeg-$(version).tar.bz2", {alias = "home"})
add_urls("https://github.com/FFmpeg/FFmpeg/archive/n$(version).zip", {alias = "github"})
add_versions("home:4.0.2", "346c51735f42c37e0712e0b3d2f6476c86ac15863e4445d9e823fe396420d056")
add_versions("github:4.0.2", "4df1ef0bf73b7148caea1270539ef7bd06607e0ea8aa2fbf1bb34062a097f026")
```

#### add_versions

Used to set the version of each source package and the corresponding sha256 value, as described in [add_urls](#add_urls)

#### add_patches

This interface is used for the source code package. Before compiling and installing, firstly set the corresponding patch package, compile it, and support multiple patches at the same time.

```lua
if is_plat("macosx") then
    add_patches("1.15", "https://raw.githubusercontent.com/Homebrew/patches/9be2793af/libiconv/patch-utf8mac.diff",
                        "e8128732f22f63b5c656659786d2cf76f1450008f36bcf541285268c66cabeab")
end
```

For example, the above code, when compiled for macosx, is marked with the corresponding patch-utf8mac.diff patch, and each patch is also set to the value of sha256 to ensure integrity.

#### add_links

By default, xmake will automatically detect the installed libraries and set the link relationship, but sometimes it is not very accurate. If you want to manually adjust the link order and the link name, you can set it through this interface.

```lua
add_links("mbedtls", "mbedx509", "mbedcrypto")
```

#### add_syslinks

Add some system library links. When some packages integrate links, you also need to rely on some system libraries to link them. This time you can attach them to the package description.

```
if is_plat("macosx") then
    add_frameworks("CoreGraphics", "CoreFoundation", "Foundation")
elseif is_plat("windows") then
    add_defines("CAIRO_WIN32_STATIC_BUILD=1")
    add_syslinks("gdi32", "msimg32", "user32")
else
    add_syslinks("pthread")
end
```

#### add_frameworks

Add a dependent system frameworks link.

See for example: [add_syslinks](#add_syslinks)

#### add_linkdirs

The package's link library search directory can also be adjusted, but it is usually not needed, unless some libraries are not installed under prefix/lib, but in the lib subdirectory, the default search is not available.

#### add_includedirs

Add another header file search directory.

#### add_defines

Some specific definition options can be exported to the integrated package.

#### add_configs

We can add the external output configuration parameters of each package through this interface:

```lua
package("pcre2")

    set_homepage("https://www.pcre.org/")
    set_description("A Perl Compatible Regular Expressions Library")

    add_configs("bitwidth", {description = "Set the code unit width.", default = "8", values = {"8", "16", "32"}})

    on_load(function (package)
        local bitwidth = package:config("bitwidth") or "8"
        package:add("links", "pcre2-" .. bitwidth)
        package:add("defines", "PCRE2_CODE_UNIT_WIDTH=" .. bitwidth)
    end)
```

In the engineering project, we can also view a list of configurable parameters and values for a particular package:

```bash
$ xmake require --info pcre2
The package info of project:
    require(pcre2): 
      -> description: A Perl Compatible Regular Expressions Library
      -> version: 10.31
      ...
      -> configs:
         -> bitwidth:
            -> description: Set the code unit width.
            -> values: {"8","16","32"}
            -> default: 8
```

Then in the project, enable these configurations and compile the package with the specific configuration:

```lua
add_requires("pcre2", {configs = {bitwidth = 16}})
```

#### on_load

This is an optional interface. If you want to be more flexible and dynamically judge various platform architectures, you can do it in this way, for example:

```lua
on_load(function (package)
    Local bitwidth = package:config("bitwidth") or "8"
    package:add("links", "pcre" .. (bitwidth ~= "8" and bitwidth or ""))
    If not package:config("shared") then
        package:add("defines", "PCRE_STATIC")
    end
end)
```

The pcre package needs to do some judgment on the bitwidth to determine the name of the link library for external output. It also needs to add some defines to the dynamic library. This time, it is more flexible when set in on_load.

#### on_install

This interface is mainly used to add installation scripts. The preceding string parameters are used to set up supported platforms. Other script fields like `on_load`, `on_test` are also supported.

##### Platform Filtering

The complete filtering syntax is as follows: `plat|arch1,arch2@host|arch1,arch2`

It looks very complicated, but it is very simple. Each stage is optional and can be partially omitted. Corresponding: `Compile Platform|Compile Architecture@Host Platform|Host Architecture

If you do not set any platform filtering conditions, then the default full platform support, the script inside is effective for all platforms, for example:

```lua
on_install(function (package)
    -- TODO
end)
```

If the installation script is valid for a specific platform, then directly specify the corresponding compilation platform, you can specify more than one at the same time:

```lua
on_install("linux", "macosx", function (package)
    -- TODO
end)
```

If you want to break down to the specified architecture to take effect, you can write:


```lua
on_install("linux|x86_64", "iphoneos|arm64", function (package)
    -- TODO
end)
```

If you want to limit the execution of the host environment platform and architecture, you can append `@host|arch` to the end, for example:

```lua
on_install("mingw@windows", function (package)
    -- TODO
end)
```

This means that only the mingw platform is valid for Windows.

We can also specify the host platform and architecture without specifying a platform and architecture. This is usually used to describe some dependencies related to the build tool and can only be run in the host environment.

For example, the package we compiled depends on cmake, we need to add the package description of cmake, then the compiler installation environment can only be the host platform:

```lua
on_install("@windows", "@linux", "@macosx", function (package)
    -- TODO
end)
```

Some other examples:

```lua
-- `@linux`
-- `@linux|x86_64`
-- `@macosx,linux`
-- `android@macosx, linux`
-- `android|armv7-a@macosx,linux`
-- `android|armv7-a@macosx,linux|x86_64`
-- `android|armv7-a@linux|x86_64`
```

##### Compilation Tools

We have built-in scripts for installing common build tools for convenient build support for different source code-dependent build toolchains, such as autoconf, cmake, meson, etc.

###### xmake

If it is a xmake-based dependency package, then the integration is very simple, xmake has very good built-in integration support, you can directly support it for cross-platform compilation, generally only need to:

```lua
on_install(function (package)
    import("package.tools.xmake").install(package)
end)
```

If you want to pass some unique build configuration parameters:

```lua
on_install(function (package)
    import("package.tools.xmake").install(package, {"--xxx=y"})
end)
```

###### cmake

If it is a cmake-based package, the integration is also very short-answered. Usually you only need to set some configuration parameters, but you need to add the cmake dependency first:

```lua
add_deps("cmake")
on_install(function (package)
    import("package.tools.cmake").install(package, {"-Dxxx=ON"})
end)
```

###### autoconf

If it is based on autoconf package, the integration method is similar to cmake, but the configuration parameters are different. However, under normal circumstances, the Unix system has built-in autoconf series tools, so it is fine without any dependencies.

```lua
on_install(function (package)
    import("package.tools.autoconf").install(package, {"--enable-shared=no"})
end)
```

However, some source packages may not be fully satisfied with the system's built-in autoconf, so you can add autoconf family dependencies and build them:

```lua
add_deps("autoconf", "automake", "libtool", "pkg-config")
on_install(function (package)
    import("package.tools.autoconf").install(package, {"--enable-shared=no"})
end)
```

###### meson

If it is meson, you need to add ninja's dependencies to perform the build.

```lua
add_deps("meson", "ninja")
on_install(function (package)
    import("package.tools.meson").install(package, {"-Dxxx=ON"})
end)
```

#### on_test

After installation, you need to set the corresponding test script, perform some tests to ensure the reliability of the installation package, if the test does not pass, the entire installation package will be revoked.

```lua
on_test(function (package)
    assert(package:has_cfuncs("inflate", {includes = "zlib.h"}))
end)
```

The above script calls the built-in `has_cfuncs` interface to detect whether the zlib.h header file exists in the installed package, and whether the interface function `inflate` exists in the library and header files.

Xmake will try to compile the link for testing, `has_cfuncs` for detecting c functions, and `has_cxxfuncs` for detecting c++ library functions.

And include multiple header files in include, for example: `includes = {"xxx.h", "yyy.h"}`

We can also pass some of our own compilation parameters into the detection, for example:

```lua
on_test(function (package)
    assert(package:has_cxxfuncs("func1", {includes = "xxx.h", configs = {defines = "c++14", cxflags = "-Dxxx"}}))
end)
```

We can also detect a code snippet with `check_csnippets` and `check_cxxsnippets`:

```lua
on_test(function (package)
    assert(package:check_cxxsnippets({test = [[
        #include <boost/algorithm/string.hpp>
        #include <string>
        #include <vector>
        #include <assert.h>
        using namespace boost::algorithm;
        using namespace std;
        static void test() {
            string str("a,b");
            vector<string> strVec;
            split(strVec, str, is_any_of(","));
            assert(strVec.size()==2);
            assert(strVec[0]=="a");
            assert(strVec[1]=="b");
        }
    ]]}, {configs = {languages = "c++14"}}))
end)
```

if it is an executable package, it can also be detected by trying to run:

```lua
on_test(function (package)
    os.run("xxx --help")
end)
```

if the run fails, the test will not pass.

### Extended configuration parameters

See: [add_configs](#add_configs) for details.

### Built-in configuration parameters

In addition to setting some extended configuration parameters via [add_configs](#add_configs), xmake also provides some built-in configuration parameters that can be used.

#### Enable debug package

```lua
add_requires("xxx", {debug = true})
```

There must be relevant processing in the package description to support:

```lua
on_install(function (package)
    Local configs = {}
    if package:debug() then
        Table.insert(configs, "--enable-debug")
    end
    import("package.tools.autoconf").install(package)
end)
```

#### Setting up the msvc runtime library

```lua
add_requires("xxx", {configs = {vs_runtime = "MT"}})
```

Normally, packages installed by built-in tool scripts such as `import("package.tools.autoconf").install` are automatically processed internally by vs_runtime.

But if it is a special source package, the build rules are special, then you need to handle it yourself:

```lua
on_install(function (package)
    io.gsub("build/Makefile.win32.common", "%-MD", "-" .. package:config("vs_runtime"))
end)
```

### Adding environment variables

For some libraries, there are also executable tools. if you need to use these tools in the integration package, you can also set the corresponding PATH environment variable:

```lua
package("luajit")
    on_load(function (package)
        if is_plat("windows") then
            Package:addenv("PATH", "lib")
        end
        Package:addenv("PATH", "bin")
    end)
```

In the project project, the corresponding environment variables will only take effect after the corresponding package is integrated by `add_packages`.

```lua
add_requires("luajit")
target("test")
    set_kind("binary")
    add_packages("luajit")
    after_run(function (package)
        os.exec("luajit --version")
    end)
```

### Installing binary packages

Xmake also supports direct reference to the binary version package, which is used directly for installation, for example:

```lua
if is_plat("windows") then
    set_urls("https://www.libsdl.org/release/SDL2-devel-$(version)-VC.zip")
    add_versions("2.0.8", "68505e1f7c16d8538e116405411205355a029dcf2df738dbbc768b2fe95d20fd")
end

on_install("windows", function (package)
    os.cp("include", package:installdir())
    os.cp("lib/$(arch)/*.lib", package:installdir("lib"))
    os.cp("lib/$(arch)/*.dll", package:installdir("lib"))
end)
```

### Local test

If you have added and created a new package in the local xmake-repo repository, you can run the test locally and pass it. If the test passes, you can submit the pr to the official repository and request the merge.

We can execute the following script to test the specified package:

```bash
cd xmake-repo
xmake l scripts/test.lua -v -D zlib
```

The above command will force the download and installation of the zlib package to test whether the entire installation process is ok, plus `-v -D` is to see the complete detailed log information and error information, which is convenient for debugging analysis.

If the network environment is not good, do not want to re-download all dependencies every time, you can add the `--shallow` parameter to execute, this parameter tells the script, just re-decompress the local cached zlib source package, re-execute the installation command, but Will not download various dependencies.

```bash
cd xmake-repo
xmake l scripts/test.lua -v -D --shallow zlib
```

If we want to test the package rules of other platforms, such as: android, iphoneos and other platforms, you can specify by `-p/--plat` or `-a/--arch`.

```bash
cd xmake-repo
xmake l scripts/test.lua -v -D --shallow -p iphoneos -a arm64 zlib
xmake l scripts/test.lua -v -D --shallow -p android --ndk=/xxxx zlib
```

## Submit package to the official repository

If you need a package that is not supported by the current official repository, you can commit it to the official repository after local tuning: [xmake-repo](https://github.com/xmake-io/xmake-repo)

For detailed contribution descriptions, see: [CONTRIBUTING.md](https://github.com/xmake-io/xmake-repo/blob/master/CONTRIBUTING.md)

For how to make your own package, you can look at the above: [Adding packages to the official repository](#Adding-packages-to-the-official-repository).
