
We can use `target("test")` to define a project target named "test", each target generates an executable program, a static library, or a dynamic library.

<p class="tip">
All interfaces of target can be set in the global scope, which affects all sub-targets.
</p>

For example:

```lua
-- affects both test and test2 targets
add_defines("DEBUG")

target("test")
    add_files("*.c")

target("test2")
    add_files("*.c")
```

<p class="tip">
`target()' interface can be repeatedly invoked in different places to set the same target.
</p>

| Interfaces                                      | Description                                            | Support version             |
| ---------------------------------------------   | ------------------------------------------------------ | --------------------------- |
| [target](#target)                               | Define a project target                                | >= 1.0.1                    |
| [target_end](#target_end)                       | End target definition                                  | >= 2.1.1                    |
| [set_kind](#targetset_kind)                     | Set target kind                                        | >= 1.0.1                    |
| [set_strip](#targetset_strip)                   | Strip target symbols                                   | >= 1.0.1                    |
| [set_enabled](#targetset_enabled)               | Enable or disable target                               | >= 2.2.2                    |
| [set_default](#targetset_default)               | Mark as default target                                 | >= 2.1.3                    |
| [set_options](#targetset_options)               | Set configuartion options                              | >= 1.0.1                    |
| [set_symbols](#targetset_symbols)               | Set symbol info                                        | >= 1.0.1                    |
| [set_basename](#targetset_basename)             | Set the base name of target file                       | >= 2.1.2                    |
| [set_filename](#targetset_filename)             | Set the full name of target file                       | >= 2.1.2                    |
| [set_warnings](#targetset_warnings)             | Set compilation warning level                          | >= 1.0.1                    |
| [set_optimize](#targetset_optimize)             | Set compilation optimization level                     | >= 1.0.1                    |
| [set_languages](#targetset_languages)           | Set source code language standards                     | >= 1.0.1                    |
| [set_headerdir](#targetset_headerdir)           | Set output directories for header files                | >= 1.0.1 < 2.2.5 deprecated |
| [set_targetdir](#targetset_targetdir)           | Set output directories for target file                 | >= 1.0.1                    |
| [set_objectdir](#targetset_objectdir)           | Set output directories for object files                | >= 1.0.1                    |
| [set_dependir](#targetset_dependir)             | Set output directories for dependent files             | >= 2.2.2                    |
| [add_imports](#targetadd_imports)               | Add imported modules for the custom script             | >= 2.1.7                    |
| [add_rules](#targetadd_rules)                   | Add custom compilation rule to target                  | >= 2.1.9                    |
| [on_load](#targeton_load)                       | Run custom load target configuartion script            | >= 2.1.5                    |
| [on_link](#targeton_link)                       | Run custom link target script                          | >= 2.2.7                    |
| [on_build](#targeton_build)                     | Run custom build target script                         | >= 2.0.1                    |
| [on_build_file](#targeton_build_file)           | Run custom build single file script                    | >= 2.2.3                    |
| [on_build_files](#targeton_build_files)         | Run custom build files script                          | >= 2.2.3                    |
| [on_clean](#targeton_clean)                     | Run custom clean files script                          | >= 2.0.1                    |
| [on_package](#targeton_package)                 | Run custom package target script                       | >= 2.0.1                    |
| [on_install](#targeton_install)                 | Run custom install target file script                  | >= 2.0.1                    |
| [on_uninstall](#targeton_uninstall)             | Run custom uninstall target file script                | >= 2.0.1                    |
| [on_run](#targeton_run)                         | Run custom run target script                           | >= 2.0.1                    |
| [before_link](#targetbefore_link)               | Run custom script before linking target                | >= 2.2.7                    |
| [before_build](#targetbefore_build)             | Run custom script before building target               | >= 2.0.1                    |
| [before_build_file](#targetbefore_build_file)   | Run custom script before building single file          | >= 2.2.3                    |
| [before_build_files](#targetbefore_build_files) | Run custom script before building files                | >= 2.2.3                    |
| [before_clean](#targetbefore_clean)             | Run custom script before cleaning target               | >= 2.0.1                    |
| [before_package](#targetbefore_package)         | Run custom script before packaging target              | >= 2.0.1                    |
| [before_install](#targetbefore_install)         | Run custom script before installing target             | >= 2.0.1                    |
| [before_uninstall](#targetbefore_uninstall)     | Run custom script before uninstalling target           | >= 2.0.1                    |
| [before_run](#targetbefore_run)                 | Run custom script before running target                | >= 2.0.1                    |
| [after_link](#targetafter_link)                 | Run custom script after linking target                 | >= 2.2.7                    |
| [after_build](#targetafter_build)               | Run custom script after building target                | >= 2.0.1                    |
| [after_build_file](#targetafter_build_file)     | Run custom script after building single file           | >= 2.2.3                    |
| [after_build_files](#targetafter_build_files)   | Run custom script after building files                 | >= 2.2.3                    |
| [after_clean](#targetafter_clean)               | Run custom script after cleaning target                | >= 2.0.1                    |
| [after_package](#targetafter_package)           | Run custom script after packaging target               | >= 2.0.1                    |
| [after_install](#targetafter_install)           | Run custom script after installing target              | >= 2.0.1                    |
| [after_uninstall](#targetafter_uninstall)       | Run custom script after uninstalling target            | >= 2.0.1                    |
| [after_run](#targetafter_run)                   | Run custom script after running target                 | >= 2.0.1                    |
| [set_config_h](#targetset_config_h)             | Set auto-generated config header file                  | >= 1.0.1 < 2.1.5 deprecated |
| [set_config_h_prefix](#targetset_config_h)      | Set macro prefix in auto-generated config header       | >= 1.0.1 < 2.1.5 deprecated |
| [set_config_header](#targetset_config_header)   | Set auto-generated config header file                  | >= 2.1.5 < 2.2.5 deprecated |
| [set_pcheader](#targetset_pcheader)             | Set pre-compiled c header file                         | >= 2.1.5                    |
| [set_pcxxheader](#targetset_pcxxheader)         | Set pre-compiled c++ header file                       | >= 2.1.5                    |
| [add_deps](#targetadd_deps)                     | Add target dependencies                                | >= 1.0.1                    |
| [add_links](#targetadd_links)                   | Add link libraries                                     | >= 1.0.1                    |
| [add_syslinks](#targetadd_syslinks)             | Add system link libraries                              | >= 2.2.3                    |
| [add_files](#targetadd_files)                   | Add source files                                       | >= 1.0.1                    |
| [del_files](#targetdel_files)                   | Remove source files                                    | >= 2.1.9                    |
| [add_headers](#targetadd_headers)               | Add installed header files                             | >= 1.0.1 < 2.2.5 deprecated |
| [add_linkdirs](#targetadd_linkdirs)             | Add link search directories                            | >= 1.0.1                    |
| [add_rpathdirs](#targetadd_rpathdirs)           | Add load search directories for dynamic library        | >= 2.1.3                    |
| [add_includedirs](#targetadd_includedirs)       | Add include search directories                         | >= 1.0.1                    |
| [add_defines](#targetadd_defines)               | Add macro definition                                   | >= 1.0.1                    |
| [add_undefines](#targetadd_undefines)           | Add macro undefinition                                 | >= 1.0.1                    |
| [add_defines_h](#targetadd_defines_h)           | Add macro definition to auto-generated config header   | >= 1.0.1 < 2.1.5 deprecated |
| [add_undefines_h](#targetadd_undefines_h)       | Add macro undefinition to auto-generated config header | >= 1.0.1 < 2.1.5 deprecated |
| [add_cflags](#targetadd_cflags)                 | Add c compilation flags                                | >= 1.0.1                    |
| [add_cxflags](#targetadd_cxflags)               | Add c/c++ compilation flags                            | >= 1.0.1                    |
| [add_cxxflags](#targetadd_cxxflags)             | Add c++ compilation flags                              | >= 1.0.1                    |
| [add_mflags](#targetadd_mflags)                 | Add objc compilation flags                             | >= 1.0.1                    |
| [add_mxflags](#targetadd_mxflags)               | Add objc/objc++ compilation flags                      | >= 1.0.1                    |
| [add_mxxflags](#targetadd_mxxflags)             | Add objc++ compilation flags                           | >= 1.0.1                    |
| [add_scflags](#targetadd_scflags)               | Add swift compilation flags                            | >= 2.0.1                    |
| [add_asflags](#targetadd_asflags)               | Add asm compilation flags                              | >= 2.0.1                    |
| [add_gcflags](#targetadd_gcflags)               | Add go compilation flags                               | >= 2.1.1                    |
| [add_dcflags](#targetadd_dcflags)               | Add dlang compilation flags                            | >= 2.1.1                    |
| [add_rcflags](#targetadd_rcflags)               | Add rust compilation flags                             | >= 2.1.1                    |
| [add_cuflags](#targetadd_cuflags)               | Add cuda compilation flags                             | >= 2.1.1                    |
| [add_culdflags](#targetadd_culdflags)           | Add cuda device-link flags                             | >= 2.2.7                    |
| [add_ldflags](#targetadd_ldflags)               | Add static library link flags                          | >= 1.0.1                    |
| [add_arflags](#targetadd_arflags)               | Add archive library flags                              | >= 1.0.1                    |
| [add_shflags](#targetadd_shflags)               | Add dynamic library link flags                         | >= 1.0.1                    |
| [add_packages](#targetadd_packages)             | Add package dependencies                               | >= 2.0.1                    |
| [add_options](#targetadd_options)               | Add options dependencies                               | >= 2.0.1                    |
| [add_languages](#targetadd_languages)           | Add language standards                                 | >= 1.0.1                    |
| [add_vectorexts](#targetadd_vectorexts)         | Add vector extensions                                  | >= 1.0.1                    |
| [add_frameworks](#targetadd_frameworks)         | Add frameworks                                         | >= 2.1.1                    |
| [add_frameworkdirs](#targetadd_frameworkdirs)   | Add framework search directories                       | >= 2.1.5                    |
| [set_tools](#targetset_tools)                   | Set toolchains                                         | >= 2.2.1                    |
| [add_tools](#targetadd_tools)                   | Add toolchains                                         | >= 2.2.1                    |
| [set_values](#targetset_values)                 | Set custom configuartion values                        | >= 2.2.1                    |
| [add_values](#targetadd_values)                 | Add custom configuartion values                        | >= 2.2.1                    |
| [set_rundir](#targetset_rundir)                 | Set run directory                                      | >= 2.2.7                    |
| [add_runenvs](#targetadd_runenvs)               | Add run environments                                   | >= 2.2.7                    |
| [set_runenv](#targetset_runenv)                 | Set run environment                                    | >= 2.2.8                    |
| [set_installdir](#targetset_installdir)         | Set the installation directory                         | >= 2.2.5                    |
| [add_installfiles](#targetadd_installfiles)     | add installation files                                 | >= 2.2.5                    |
| [add_headerfiles](#targetadd_headerfiles)       | Add header files                                       | >= 2.2.5                    |
| [set_configdir](#targetset_configdir)           | Set the output directory of configuartion files        | >= 2.2.5                    |
| [set_configvar](#targetset_configvar)           | Set template configuartion variable                    | >= 2.2.5                    |
| [add_configfiles](#targetadd_configfiles)       | Add template configuartion files                       | >= 2.2.5                    |

### target

#### Define a project target

Defines a console target named `test` in project and the default target filename is `test`.

```lua
target("test")
    set_kind("binary")
    add_files("src/*.c")
```

And we can call `target("demo")` repeatly to enter the target scope for modifying it's configuartion.

```lua
-- defines target: demo and enter it's scope to set configuartion
target("demo")
    set_kind("binary")
    add_files("src/demo.c")

-- defines and set `other` target
target("other")
    ...

-- re-enter demo target scope and add file `test.c` to `demo`
target("demo")
    add_files("src/test.c")
```

<p class="tip">
All configuartion in root scope affects all targets, but does not affect the configuartion of `option()`.
</p>

For example:

```lua
add_defines("DEBUG")

target("demo")                   -- add -DDEBUG
    set_kind("binary")
    add_files("src/demo.c")

target("test")                   -- add -DDEBUG
    set_kind("binary")
    add_files("src/test.c")
```

### target_end

#### End target definition

This is an optional api. If not called, then all settings after
`target("xxx")` are made for that target, unless you enter other
`target`, `option` or `task` scope. If you want to leave the current
`target` and enter the root scope setting, then you can use this api. For example:

```lua
target("test")
    set_kind("static")
    add_files("src/*.c")
target_end()

-- Here we are in the root scope
-- ...
```

If you don't call this api:

```lua
target("test")
    set_kind("static")
    add_files("src/*.c")

-- Here we are in the target scope above, the subsequent settings are still
set for test
-- ...

-- Enter another target scope
target("test2")
    ...
```

### target:set_kind

#### Set target kind

Set the target type. Currently supported types are:

| Value | Description |
| ------ | -----------|
| binary | Binary Program |
| static | Static library program |
| shared | dynamic library program |

```lua
target("demo")
    set_kind("binary")
```

### target:set_strip

#### Strip target symbols

Set the current target strip mode, currently supports the mode:

| Value | Description |
| ------ | ----------------------------------------- |
| debug | When you link, strip off debugging symbols |
| all | When you link, strip all symbols, including debugging symbols |

This api is generally used in release mode and can generate smaller binary programs.

```lua
target("xxxx")
    set_strip("all")
```

<p class="tip">
This api does not have to be used after the target. If no target is specified, it will be set to global mode. .
</p>

### target:set_enabled

#### Enable or disable target

If `set_enabled(false)` is set, the corresponding target will be directly disabled, including target loading and information acquisition, while [set_default](#targetset_default) is just set to not compile by default, but the target can still get related information. , the default will also be loaded.

### target:set_default

#### Mark as default target

This interface is used to set whether the given project target is the default build. If this interface is not called for setting, then this target is built by default, for example:

```lua
target("test1")
    set_default(false)

target("test2")
    set_default(true)

target("test3")
    ...
```

The three goals of the above code, when executing the `xmake`, `xmake install`, `xmake package`, `xmake run` and other commands, if you do not specify the target name, then:

| Target Name | Behavior |
| ------ | -------------------------------- |
| test1 | will not be built, installed, packaged, and run by default |
| test2 | Default build, install, package, and run |
| test3 | Default build, install, package, and run |

Through the above example, you can see that the default target can be set more than one, and it will run in turn when running.

<p class="tip">
    Note that the `xmake uninstall` and `xmake clean` commands are not affected by this interface setting, as most users prefer to clean and unload all of them.
</p>

If you don't want to use the default target, you can manually specify which targets you need to build the installation:

```bash
$ xmake build targetname
$ xmake install targetname
```

If you want to force the build to install all targets, you can pass in the `[-a|--all]` parameter:

```bash
$ xmake build [-a|--all]
$ xmake install [-a|--all]
```

### target:set_options

#### Set configuartion options

Add option dependencies. If you have customized some options through the [option](#option) interface, you can add associations only if you specify this option under the target target field.

```lua
-- Define a hello option
option("hello")
    set_default(false)
    set_showmenu(true)
    add_defines("HELLO_ENABLE")

target("test")
    -- If the hello option is enabled, this time the -DHELLO_ENABLE macro will be applied to the test target.
    set_options("hello")
```

<p class="warn">
Some settings defined in [option](#option) will affect this `target` target only after calling `set_options` for the association to take effect, such as macro definitions, link libraries, compile options, etc.
</p>

### target:set_symbols

#### Set symbol info

Set the symbol mode of the target. If no target is currently defined, it will be set to the global state, affecting all subsequent targets.

At present, we mainly support several levels:

| Value | Description |
| ------ | ---------------------- |
| debug | Add debug symbols |
| hidden | set symbol not visible |

These two values ​​can also be set at the same time, for example:

```lua
-- Add debug symbols, set symbols are not visible
set_symbols("debug", "hidden")
```

If this api is not called, the debug symbol is disabled by default. .

### target:set_basename

#### Set the base name of target file

By default, the generated target file name is based on the value configured in `target("name")`, for example:

```lua
-- The target file name is: libxxx.a
target("xxx")
    set_kind("static")

-- The target file name is: libxxx2.so
target("xxx2")
    set_kind("shared")
```

The default naming method basically meets the needs of most situations, but if you want to customize the target file name sometimes

For example, to distinguish the target name by compile mode and architecture, this time you can use this interface to set:

```lua
target("xxx")
    set_kind("static")
    set_basename("xxx_$(mode)_$(arch)")
```

if this time, the build configuration is: `xmake f -m debug -a armv7`, then the generated file name is: `libxxx_debug_armv7.a`

If you want to further customize the directory name of the target file, refer to: [set_targetdir](#targetset_targetdir).

Or implement more advanced logic by writing custom scripts, see: [after_build](#targetafter_build) and [os.mv](/manual/builtin_modules?id=osmv).

### target:set_filename

#### Set the full name of target file

The difference between it and [set_basename](#targetset_basename) is that [set_basename](#targetset_basename) sets the name without a suffix and a prefix, for example: `libtest.a`, if the basename is changed to test2, it becomes `libtest2.a `.

The modification of filename is to modify the entire target file name, including the prefix and suffix. For example, you can directly change `libtest.a` to `test.dll`, which is not available for [set_basename](#targetset_basename).

### target:set_warnings

#### Set compilation warning level

Set the warning level of the compilation of the current target, generally supporting several levels:

| Value | Description | gcc/clang | msvc |
| ----- | ---------------------- | ---------- | ----------------------------- |
| none | disable all warnings | -w | -W0 |
| less | Enable fewer warnings | -W1 | -W1 |
| more | Enable more warnings | -W3 | -W3 |
| all | Enable all warnings | -Wall | -W3 (-Wall too more warnings) |
| everything | Enable all supported warnings | -Wall -Wextra -Weffc++ / -Weverything | -Wall |
| error | Use all warnings as compilation errors | -Werror | -WX |

The parameters of this api can be added in combination, for example:

```lua
-- Enable all warnings and handle them as compilation errors
set_warnings("all", "error")
```

If there is no target currently, calling this api will set it to global mode. .

### target:set_optimize

#### Set competition optimization level

Set the compile optimization level of the target. If no target is currently set, it will be set to the global state, affecting all subsequent targets.

At present, we mainly support several levels:

| Value | Description | gcc/clang | msvc |
| ---------- | ---------------------- | ---------- | ------------ |
| none | disable optimization | -O0 | -Od |
| fast | quick optimization | -O1 | default |
| faster | faster optimization | -O2 | -Ox |
| fastest | Optimization of the fastest running speed | -O3 | -Ox -fp:fast |
| smallest | Minimize code optimization | -Os | -O1 |
| aggressive | over-optimization | -Ofast | -Ox -fp:fast |

E.g:

```lua
-- Optimization of the fastest running speed
set_optimize("fastest")
```

### target:set_languages

#### Set source code language standards

Set the language standard for target code compilation. If no target exists, it will be set to global mode. . .

The supported language standards currently have the following main ones:

| Value | Description |
| ---------- | ---------------------- |
| ansi | c language standard: ansi |
| c89 | c language standard: c89 |
| gnu89 | c language standard: gnu89 |
| c99 | c language standard: c99 |
| gnu99 | c language standard: gnu99 |
| cxx98 | c++ language standard: `c++98` |
| gnuxx98 | c++ language standard: `gnu++98` |
| cxx11 | c++ language standard: `c++11` |
| gnuxx11 | c++ language standard: `gnu++11` |
| cxx14 | c++ language standard: `c++14` |
| gnuxx14 | c++ language standard: `gnu++14` |
| cxx1z | c++ language standard: `c++1z` |
| gnuxx1z | c++ language standard: `gnu++1z` |
| cxx17 | c++ language standard: `c++17` |
| gnuxx17 | c++ language standard: `gnu++17` |

The c standard and the c++ standard can be set at the same time, for example:

```lua
-- Set c code standard: c99, c++ code standard: c++11
set_languages("c99", "cxx11")
```

<p class="warn">
Instead of setting the specified standard, the compiler will compile according to this standard. After all, each compiler supports different strengths, but xmake will try to adapt the support standard of the current compiler tool to the greatest extent possible. . .
<br><br>
E.g:
<br>
Windows vs compiler does not support compiling c code according to c99 standard, can only support c89, but xmake in order to support it as much as possible, so after setting c99 standard, xmake will force to compile according to c++ code mode c code, to some extent solved the c code problem of compiling c99 under windows. .
Users do not need to make any additional modifications. .
</p>

### target:set_headerdir

#### Set output directories for header files

<p class="warn">
Note that this interface has been deprecated after version 2.2.5, please use [add_headerfiles](#targetadd_headerfiles) instead.
</p>

Set the output directory of the header file, and output it to the build directory by default.

```lua
target("test")
    set_headerdir("$(buildir)/include")
```

For the header files that need to be installed, refer to the [add_headers](#targetadd_headers) interface.

### target:set_targetdir

#### Set output directories for target files

Set the output directory of the target program file. Under normal circumstances, you do not need to set it. The default output will be in the build directory.

The build directory can be manually modified during project configuration:

```bash
Xmake f -o /tmp/build
```

After modifying to `/tmp/build`, the target file is output to `/tmp/build` by default.

And if you use this interface to set, you don't need to change the command every time, for example:

```lua
target("test")
    set_targetdir("/tmp/build")
```

<p class="tip">
If the display sets `set_targetdir`, then the directory specified by `set_targetdir` is preferred as the output directory of the target file.
</p>

### target:set_objectdir

#### Set output directories for object files

Set the output directory of the object file (`*.o/obj`) of the target target, for example:

```lua
target("test")
    set_objectdir("$(buildir)/.objs")
```

### target:set_dependir

#### Set output directories for dependent files

Set the output directory of the compile dependency file (`.deps`) of the target target, for example:

```lua
target("test")
    set_dependir("$(buildir)/.deps")
```

### target:add_imports

#### Add imports modules for the custom script

Usually, we can import extension modules via `import("core.base.task")` inside a custom script such as [on_build](#targeton_build).
However, in the case of a large number of custom scripts, each custom script is repeatedly imported again, which is very cumbersome. Then you can implement pre-import through this interface, for example:

```lua
target("test")
    on_load(function (target)
        import("core.base.task")
        import("core.project.project")

        task.run("xxxx")
    end)
    on_build(function (target)
        import("core.base.task")
        import("core.project.project")

        task.run("xxxx")
    end)
    on_install(function (target)
        import("core.base.task")
        import("core.project.project")

        task.run("xxxx")
    end)
```

This interface can be simplified to:

```lua
target("test")
    add_imports("core.base.task", "core.project.project")
    on_load(function (target)
        task.run("xxxx")
    end)
    on_build(function (target)
        task.run("xxxx")
    end)
    on_install(function (target)
        task.run("xxxx")
    end)
```

### target:add_rules

#### Add custom compilation rule to target

We can extend the build support for other files by pre-setting the file suffixes supported by the rules:

```lua
-- Define a build rule for a markdown file
rule("markdown")
    set_extensions(".md", ".markdown")
    on_build(function (target, sourcefile)
        os.cp(sourcefile, path.join(target:targetdir(), path.basename(sourcefile) .. ".html"))
    end)

target("test")
    set_kind("binary")

    -- Make the test target support the construction rules of the markdown file
    add_rules("markdown")

    -- Adding a markdown file to build
    add_files("src/*.md")
    add_files("src/*.markdown")
```

We can also specify the application of local files to the rules, see: [add_files](#targetadd_files).

### target:on_load

#### Run custom load target configuartion script

This script will be executed when the target is initialized and loaded, and some dynamic target configurations can be made to achieve more flexible target description definitions, for example:

```lua
target("test")
    on_load(function (target)
        target:add("defines", "DEBUG", "TEST=\"hello\"")
        target:add("linkdirs", "/usr/lib", "/usr/local/lib")
        target:add({includedirs = "/usr/include", "links" = "pthread"})
    end)
```

You can dynamically add various target attributes in `on_load` via `target:set`, `target:add`.

### target:on_link

#### Run custom link target script

This is a new interface after v2.2.7, which is used to customize the link process of the target.

```lua
target("test")
    on_link(function (target) 
        print("link it")
    end)
```

### target:on_build

#### Run custom build target script

Override the target build behavior of the target target, implement a custom compilation process, in general, do not need to do this, unless you really need to do some compiler operations that xmake does not provide by default.

You can override it by following the steps below to customize the compilation:

```lua
target("test")

    -- Set up custom build scripts
    on_build(function (target)
        print("build it")
    end)
```

Note: After version 2.1.5, all target custom scripts can be processed separately for different platforms and architectures, for example:

```lua
target("test")
    on_build("iphoneos|arm*", function (target)
        print("build for iphoneos and arm")
    end)
```

If the first parameter is a string, then it is specified in which platform_architecture the script needs to be executed, and mode matching is supported, for example, `arm*` matches all arm architectures.

Of course, you can also set the platform only, do not set the architecture, this is to match the specified platform, execute the script:

```lua
target("test")
    on_build("windows", function (target)
        print("build for windows")
    end)
```

<p class="tip">
Once the build process is set for this target target, the default build process for xmake will no longer be executed.
</p>

### target:on_build_file

#### Run custom build single file script

Through this interface, you can use hook to specify the built-in build process of the target, replacing each source file compilation process:

```lua
target("test")
    set_kind("binary")
    add_files("src/*.c")
    on_build_file(function (target, sourcefile, opt)
        opt.origin(target, sourcefile, opt)
    end)
```

The `opt.origin` in the above code has a built-in build script. If you want to call the built-in build script to compile the source file after hooking, just continue to call `opt.origin`.

If you don't want to rewrite the built-in build script, just add some of your own processing before and after compiling. Its utility: [target.before_build_file](#targetbefore_build_file) and [target.after_build_file](#targetafter_build_file) will be more convenient and you don't need to call it. Opt.origin`.

### target:on_build_files

#### Run custom build files script

Through this interface, you can use hook to specify the built-in build process of the target, and replace a batch of the same type of source file compilation process:

```lua
target("test")
    set_kind("binary")
    add_files("src/*.c")
    on_build_files(function (target, sourcebatch, opt)
        opt.origin(target, sourcebatch, opt)
    end)
```

After setting this interface, the corresponding file in the source file list will not appear in the custom [target.on_build_file](#targeton_build_file), because this is an inclusion relationship.

Where sourcebatch describes the same source files of the same type:

* `sourcebatch.sourcekind`: Get the type of this batch of source files, for example: cc, as, ..
* `sourcebatch.sourcefiles()`: get the list of source files
* `sourcebatch.objectfiles()`: get the list of object files
* `sourcebatch.dependfiles()`: Get the list of corresponding dependent files, compile dependency information in the stored source file, for example: xxx.d

The `opt.origin` in the above code has a built-in build script. If you want to call the built-in build script to compile the source file after hooking, just continue to call `opt.origin`.

### target:on_clean

#### Run custom clean files script

Override the cleanup operation of the target target's `xmake [c|clean}` to implement a custom cleanup process.

```lua
target("test")

    -- Set up a custom cleanup script
    on_clean(function (target)

        -- Delete only target files
        os.rm(target:targetfile())
    end)
```

Some target interfaces are described as follows:

| target interface                    | description                                  |
| ----------------------------------- | -------------------------------------------- |
| target:name()                       | Get the target name                          |
| target:targetfile()                 | Get the target file path                     |
| target:get("kind")                  | Get the build type of the target             |
| target:get("defines")               | Get the macro definition of the target       |
| target:get("xxx")                   | Other target information set by the `set_/add_` interface can be obtained through this interface |
| target:add("links", "pthread")      | Add target settings                          |
| target:set("links", "pthread", "z") | Override target settings                     |
| target:deps()                       | Get all dependent targets of the target      |
| target:dep("depname")               | Get the specified dependency target          |
| target:sourcebatches()              | Get a list of all source files for the target |

### target:on_package

#### Run custom package target script

Override the target object's `xmake [p|package}` package operation to implement the custom packaging process. If you want to package the specified target into the format you want, you can customize it through this interface.

This interface is quite practical. For example, after compiling jni, the generated so is packaged into the apk package.

```lua
-- Define a test demo for an android app
target("demo")

    -- Generate dynamic libraries: libdemo.so
    set_kind("shared")

    -- Set the output directory of the object, optional
    set_objectdir("$(buildir)/.objs")

    -- Every time you compile the build directory of libdemo.so, set it to app/libs/armeabi
    set_targetdir("libs/armeabi")

    -- Add jni code files
    add_files("jni/*.c")

    -- Set up a custom package script. After compiling libdemo.so with xmake, execute xmake p to package
    -- will automatically compile the app into an apk file using ant
    --
    on_package(function (target)

        -- Use ant to compile the app into an apk file, and redirect the output to a log file.
        os.run("ant debug")
    end)
```

### target:on_install

#### Run custom install target file script

Override the installation of `xmake [i|install}` of the target target to implement a custom installation process.

For example, the generated apk package will be installed.

```lua
target("test")

    -- Set up a custom installation script to automatically install apk files
    on_install(function (target)

        -- Use adb to install packaged apk files
        os.run("adb install -r ./bin/Demo-debug.apk")
    end)
```

### target:on_uninstall

#### Run custom uninstall target file script

Override the uninstallation of `xmake [u|uninstall}` of the target target to implement a custom uninstall process.

```lua
target("test")
    on_uninstall(function (target)
        ...
    end)
```

### target:on_run

#### Run custom run target script

Override the running operation of the target target's `xmake [r|run}` to implement a custom running process.

For example, run the installed apk program:

```lua
target("test")

    -- Set custom run scripts, automatically run the installed app, and automatically get device output information
    on_run(function (target)

        os.run("adb shell am start -n com.demo/com.demo.DemoTest")
        os.run("adb logcat")
    end)
```

### target:before_link

#### Run custom script before linking target

This is a new interface after v2.2.7 to add custom script before linking target.

```lua
target("test")
    before_link(function (target) 
        print("")
    end)
```

### target:before_build

#### Run custom script before building target

It does not override the default build operation, just add some custom actions before building.

```lua
target("test")
    before_build(function (target)
        print("")
    end)
```

### target:before_build_file

#### Run custom script before building single file

Through this interface, you can use hook to specify the built-in build process of the target, and execute some custom scripts before each source file compilation process:

```lua
target("test")
    set_kind("binary")
    add_files("src/*.c")
    before_build_file(function (target, sourcefile, opt)
    end)
```

### target:before_build_files

#### Run custom script before building files

Through this interface, you can use hook to specify the built-in build process of the target, and execute some custom scripts before a batch of source files of the same type:

```lua
target("test")
    set_kind("binary")
    add_files("src/*.c")
    before_build_files(function (target, sourcebatch, opt)
    end)
```


### target:before_clean

#### Run custom script before cleaning target

It does not override the default cleanup operation, just add some custom actions before cleaning.

```lua
target("test")
    before_clean(function (target)
        print("")
    end)
```

### target:before_package

#### Run custom script before packaging target

It does not override the default packaging operation, just add some custom operations before packaging.

```lua
target("test")
    before_package(function (target)
        print("")
    end)
```

### target:before_install

#### Run custom script before installing target

It does not override the default installation operation, just add some custom actions before installation.

```lua
target("test")
    before_install(function (target)
        print("")
    end)
```

### target:before_uninstall

#### Run custom script before uninstalling target

It does not override the default uninstall operation, just add some custom actions before uninstalling.

```lua
target("test")
    before_uninstall(function (target)
        print("")
    end)
```

### target:before_run

#### Run custom script before running target

It does not override the default run operation, just add some custom actions before running.

```lua
target("test")
    before_run(function (target)
        print("")
    end)
```

### target:after_link

#### Run custom script after linking target

This is a new interface after v2.2.7 to add custom script after linking target.

```lua
target("test")
    after_link(function (target) 
        print("")
    end)
```

### target:after_build

#### Run custom script after building target

It does not override the default build operation, just add some custom actions after the build.

For example, for jailbreak development of ios, after the program is built, you need to use `ldid` for signature operation.

```lua
target("test")
    after_build(function (target)
        os.run("ldid -S %s", target:targetfile())
    end)
```

### target:after_build_file

#### Run custom script after building single file

Through this interface, you can use hook to specify the built-in build process of the target, and execute some custom scripts after each source file compilation process:

```lua
target("test")
    set_kind("binary")
    add_files("src/*.c")
    after_build_file(function (target, sourcefile, opt)
    end)
```

### target:after_build_files

#### Run custom script after building files

Through this interface, you can use hook to specify the built-in build process of the target, and execute some custom scripts after a batch of source files of the same type:

```lua
target("test")
    set_kind("binary")
    add_files("src/*.c")
    after_build_files(function (target, sourcebatch, opt)
    end)
```

### target:after_clean

#### Run custom script after cleaning target

It does not override the default cleanup operation, just add some custom actions after cleanup.

Generally used to clean up some extra temporary files automatically generated by a target. The default cleanup rules of these files may not be cleaned up.
To, for example:

```lua
target("test")
    after_clean(function (target)
        os.rm("$(buildir)/otherfiles")
    end)
```

### target:after_package

#### Run custom script after packaging target

It does not override the default packaging operation, just add some custom operations after packaging.

```lua
target("test")
    after_package(function (target)
        print("")
    end)
```

### target:after_install

#### Run custom script after installing target

It does not override the default installation operation, just add some custom actions after installation.

```lua
target("test")
    after_install(function (target)
        print("")
    end)
```
### target:after_uninstall

#### Run custom script after uninstalling target

It does not override the default uninstall operation, just add some custom actions after uninstalling.

```lua
target("test")
    after_uninstall(function (target)
        print("")
    end)
```

### target:after_run

#### Run custom script after running target

It does not override the default run operation, just add some custom actions after the run.

```lua
target("test")
    after_run(function (target)
        print("")
    end)
```


### target:set_config_h

#### Set auto-generated config header file

<p class="warn">
After the 2.2.5 version, this interface has been deprecated, please use [add_configfiles](#targetadd_configfiles).
After the 2.1.5 version, this interface has been deprecated, please use [set_config_header](#targetset_config_header).
</p>

If you want to write the result of the test to the configuration header after the xmake configuration project succeeds, or automatically detect an option, you need to call this interface to enable automatic generation of the `config.h` file.

How to use, for example:

```lua
target("test")

    -- Enable and set the path to the config.h file that needs to be automatically generated
    set_config_h("$(buildir)/config.h")

    -- Set the name prefix of the macro switch generated by automatic detection
    set_config_h_prefix("TB_CONFIG")
```

When the target passes the following interfaces, the related option dependencies, package dependencies, and interface dependencies are added to the target. If a dependency is enabled, the corresponding macro definition configuration will be automatically written to the set `config. Go to the .h` file.

* [add_options](#targetadd_options)
* [add_packages](#targetadd_packages)
* [add_cfuncs](#targetadd_cfuncs)
* [add_cxxfuncs](#targetadd_cxxfuncs)

These interfaces, in fact, use some of the detection settings in the [option](#option) option, for example:

```lua
option("wchar")

    -- Add detection of wchar_t type
    add_ctypes("wchar_t")

    -- If the test passes, automatically generate a macro switch of TB_CONFIG_TYPE_HAVE_WCHAR to config.h
    add_defines_h("$(prefix)_TYPE_HAVE_WCHAR")

target("test")

    -- Enable automatic generation of header files
    set_config_h("$(buildir)/config.h")
    set_config_h_prefix("TB_CONFIG")

    -- Add dependency on the wchar option. Only with this association, the detection result of the wchar option will be written to the specified config.h.
    add_options("wchar")
```

### target:set_config_h_prefix

#### Set macro prefix in auto-generated config header

<p class="warn">
After the 2.2.5 version, this interface has been deprecated, please use [add_configfiles](#targetadd_configfiles).
After the 2.1.5 version, this interface has been deprecated, please use [set_config_header](#targetset_config_header).
</p>

For details, see: [set_config_h](#targetset_config_h)

If set:

```lua
target("test")
    set_config_h_prefix("TB_CONFIG")
```

Then, the $(prefix) of `add_defines_h("$(prefix)_TYPE_HAVE_WCHAR")` in the option is automatically replaced with the new prefix value.


### target:set_config_header

#### Set macro prefix in auto-generated config header and prefix

<p class="warn">
After the 2.2.5 version, this interface has been deprecated, please use [add_configfiles](#targetadd_configfiles).
After the 2.1.5 version, this interface has been deprecated, please use [set_config_header](#targetset_config_header).
</p>

This interface is an upgraded version of [set_config_h](#targetset_config_h) and [set_config_h_prefix](#targetset_config_h_prefix), supported after 2.1.5.

If you want to write the result of the test to the configuration header after the xmake configuration project succeeds, or automatically detect an option, you need to call this interface to enable automatic generation of the `config.h` file.

How to use, for example:

```lua
target("test")
    set_config_header("$(buildir)/config.h", {prefix = "TB_CONFIG"})
```

The above code, enable and set the path to the config.h file that needs to be automatically generated, and set the name prefix of the macro switch generated by the automatic detection: `TB_CONFIG`, of course, the setting of this prefix is ​​optional.

```lua
target("test")
    set_config_header("$(buildir)/config.h")
```

If you do not set a prefix, it will automatically generate a unique string based on the target name.

After version 2.1.8, the version number is set separately for each local configuration file, which takes precedence over the global [set_version](#set_version), for example:

```lua
    set_config_header("$(buildir)/config.h", {prefix = "TB_CONFIG", version = "2.1.8", build = "%Y%m%d%H%M"})
```

#### Generate configuration with built-in detection rules

When the target passes the following interfaces, the related option dependencies, package dependencies, and interface dependencies are added to the target. If a dependency is enabled, the corresponding macro definition configuration will be automatically written to the set `config. Go to the .h` file.

* [add_options](#targetadd_options)
* [add_packages](#targetadd_packages)
* [add_cfunc](#targetadd_cfunc)
* [add_cfuncs](#targetadd_cfuncs)
* [add_cxxfuncs](#targetadd_cxxfuncs)

#### Customize detection and generate configuration header files

These interfaces, in fact, use some of the detection settings in the [option](#option) option, for example:

```lua
option("wchar")

    -- Add detection of wchar_t type
    add_ctypes("wchar_t")

    -- If the test passes, automatically generate a macro switch of TB_CONFIG_TYPE_HAVE_WCHAR to config.h
    add_defines_h("$(prefix)_TYPE_HAVE_WCHAR")

target("test")

    -- Enable automatic generation of header files
    set_config_header("$(buildir)/config.h", {prefix = "TB_CONFIG"})

    -- Add dependency on the wchar option. Only with this association, the detection result of the wchar option will be written to the specified config.h.
    add_options("wchar")
```

Even we can define a function in `xmake.lua`, package the option, provide more customized detection and process of generating config.h.

For example: there is a requirement here, we want to batch check some header files, if there is a macro switch such as `HAVE_LIMITS_H` in config.h, we can write

```lua
function add_checking_to_config(...)

    -- Batch definition of option detection rules, only include include files
    local options = {}
    for _, header in ipairs({...}) do
        local define = header:upper():gsub("[%./]", "_")
        option(define)
            add_cincludes(header)
            add_defines_h("HAVE_" .. define) -- Generate a macro switch like HAVE_LIMITS_H ​​to config.h
        option_end()
        table.insert(options, define)
    end

    -- Define a built-in __config empty target, only for association settings automatedconfig.h, and corresponding options detection rules
    -- Because set_config_header is globally set, it will affect all targets, and each target will detect the generation of a macro switch.
    target("__config")
        set_kind("phony")
        set_cOnfig_header("includes/automatedconfig.h")
        add_options(options)
    target_end()
end

-- Add some header file detection
add_checking_to_config("arpa/inet.h", "limits.h", "fcntl.h", "xxxx.h")
```

### target:set_pcheader

#### Set pre-compiled c header file

Xmake supports accelerating c program compilation by precompiling header files. Currently supported compilers are: gcc, clang, and msvc.

The usage is as follows:

```lua
target("test")
    set_pcheader("header.h")
```

### target:set_pcxxheader

#### Set pre-compiled c++ header file

Xmake supports precompiled header files to speed up C++ program compilation. Currently supported compilers are: gcc, clang, and msvc.

The usage is as follows:

```lua
target("test")
    set_pcxxheader("header.h")
```

### target:add_deps

#### Add target dependencies



Add the dependency target of the current target. When compiling, it will first compile the target of the dependency and then compile the current target. . .

```lua
target("test1")
    set_kind("static")
    set_files("*.c")

target("test2")
    set_kind("static")
    set_files("*.c")

target("demo")
    add_deps("test1", "test2")
```

In the above example, when compiling the target demo, you need to compile the test1 and test2 targets first, because the demo will use them.

<p class="tip">
The target will automatically inherit the configuration and properties in the dependent target. You don't need to call the interfaces `add_links`, `add_linkdirs` and `add_rpathdirs` to associate the dependent targets.
</p>

And the inheritance relationship is to support cascading, for example:

```lua
target("library1")
    set_kind("static")
    add_files("*.c")
    add_includedirs("inc") -- The default private header file directory will not be inherited
    add_includedirs("inc1", {public = true}) -- The header file related directory here will also be inherited

target("library2")
    set_kind("static")
    add_deps("library1")
    add_files("*.c")

target("test")
    set_kind("binary")
    add_deps("library2")
```

If we don't want to inherit any configuration that depends on the target, what should we do?

```lua
add_deps("dep1", "dep2", {inherit = false})
```

By explicitly setting the inherit configuration, tell xmake whether the two dependent configurations need to be inherited. If not set, the default is to enable inheritance.

After version 2.2.5, you can set public to true by `add_includedirs("inc1", {public = true})`, and expose the settings of includers to other dependent child targets.

At present, for the target compilation link flags related interface settings, support for inheritance properties, you can artificially control whether you need to export to other targets to rely on inheritance, the currently supported properties are:

| Attribute | Description |
| ---- | ---- |
| private | The default setting, as the private configuration of the current target, will not be inherited by other targets that depend on |
Public | public configuration, current target, dependent child targets will be set |
Interface | interface settings, only inherited by the dependent child target, the current target does not participate |

For a detailed description of this, you can look at it: https://github.com/xmake-io/xmake/issues/368

### target:add_links

#### Add link libraries

Add a link library for the current target, which is usually paired with [add_linkdirs](#targetadd_linkdirs).

```lua
target("demo")

    -- Add a link to libtest.a, equivalent to -ltest
    add_links("test")

    -- Add link search directory
    add_linkdirs("$(buildir)/lib")
```

### target:add_syslinks

#### Add system link libraries

This interface is similar to [add_links](#targetadd_links). The only difference is that the link library added through this interface is in the order of all `add_links`.

Therefore, it is mainly used to add system library dependencies, because the link order of the system libraries is very backward, for example:

```lua
add_syslinks("pthread", "m", "dl")
target("demo")
    add_links("a", "b")
    add_linkdirs("$(buildir)/lib")
```

The above configuration, even if `add_syslinks` is set in advance, the final link order is still: `-la -lb -lpthread -lm -ldl`

### target:add_files

#### Add source files

Source files used to add target projects, even library files, some file types currently supported:

| Supported source file types | Description |
| ------------------ | ---------------------------------- |
| .c/.cpp/.cc/.cxx | c++ file |
| .s/.S/.asm | Assembly files |
| .m/.mm | objc file |
| .swift | swift file |
| .go | golang file |
| .o/.obj | Object File |
| .a/.lib | Static library files, will automatically merge the library to the target program |
| .rc | msvc resource file |

The wildcard `*` indicates that the file in the current directory is matched, and `**` matches the file in the multi-level directory.

E.g:

```lua
add_files("src/test_*.c")
add_files("src/xxx/**.cpp")
add_files("src/asm/*.S", "src/objc/**/hello.m")
```

The use of `add_files` is actually quite flexible and convenient. Its matching mode draws on the style of premake, but it has been improved and enhanced.

This makes it possible to not only match files, but also to filter out a batch of files in the specified mode while adding files.

E.g:

```lua
-- Recursively add all c files under src, but not all c files under src/impl/
add_files("src/**.c|impl/*.c")

-- Add all cpp files under src, but not including src/test.cpp, src/hello.cpp, and all cpp files with xx_ prefix under src
add_files("src/*.cpp|test.cpp|hello.cpp|xx_*.cpp")
```

The separators after the ``` are all files that need to be excluded. These files also support the matching mode, and you can add multiple filtering modes at the same time, as long as the middle is separated by `|`. .

One of the benefits of supporting the filtering of some files when adding files is that they provide the basis for subsequent file additions based on different switching logic.

<p class="tip">
In order to make the description more streamlined, the filter descriptions after `|` are based on a schema: the directory before `*` in `src/*.cpp`.
So the above example is filtered after the file under src, this is to pay attention to.
</p>

After version 2.1.6, `add_files` has been improved to support more fine-grained compilation option controls based on files, such as:

```lua
target("test")
    add_defines("TEST1")
    add_files("src/*.c")
    add_files("test/*.c", "test2/test2.c", {defines = "TEST2", languages ​​= "c99", includedirs = ".", cflags = "-O0"})
```

You can pass a configuration table in the last parameter of `add_files` to control the compilation options of the specified files. The configuration parameters are consistent with the target, and these files will also inherit the target's common configuration `-DTEST1`.

After version 2.1.9, support for adding unknown code files, by setting rule custom rules, to achieve custom build of these files, for example:

```lua
target("test")
    -- ...
    add_files("src/test/*.md", {rule = "markdown"})
```

For instructions on using custom build rules, see: [Building Rules](#Building Rules).

And after the 2.1.9 version, you can use the force parameter to force the automatic detection of cxflags, cflags and other compile options, directly into the compiler, even if the compiler may not support, it will also be set:

```lua
add_files("src/*.c", {force = {cxflags = "-DTEST", mflags = "-framework xxx"}})
```

### target:del_files

#### Remove source files

Through this interface, you can delete the specified file from the list of files added by the [add_files](targetadd_files) interface, for example:

```lua
target("test")
    add_files("src/*.c")
    del_files("src/test.c")
```

In the above example, you can add all files except `test.c` from the `src` directory. Of course, this can also be done by `add_files("src/*.c|test.c").To achieve the same purpose, but this way is more flexible.

For example, we can conditionally determine which files to delete, and this interface also supports the matching mode of [add_files](targetadd_files), filtering mode, and bulk removal.

```lua
target("test")
    add_files("src/**.c")
    del_files("src/test*.c")
    del_files("src/subdir/*.c|xxx.c")
    if is_plat("iphoneos") then
        add_files("xxx.m")
    end
```

Through the above example, we can see that `add_files` and `del_files` are added and deleted sequentially according to the calling sequence, and deleted by `del_files("src/subdir/*.c|xxx.c")` Batch file,
And exclude `src/subdir/xxx.c` (that is, don't delete this file).

### target:add_headers

#### Add installed header files

<p class="warn">
Note that this interface has been deprecated after version 2.2.5, please use [add_headerfiles](#targetadd_headerfiles) instead.
</p>

Install the specified header file into the build directory. If [set_headerdir](#targetset_headerdir) is set, it will be output to the specified directory.

The syntax of the installation rules is similar to [add_files](#targetadd_files), for example:

```lua
    -- Install all the header files in the tbox directory (ignore the files in the impl directory), and press () to specify the part as a relative path to install
    add_headers("../(tbox/**.h)|**/impl/**.h")
```

### target:add_linkdirs

#### Add link search directories

Set the search directory of the link library. This interface is used as follows:

```lua
target("test")
    add_linkdirs("$(buildir)/lib")
```

This interface is equivalent to gcc's `-Lxxx` link option.

Generally, it is used together with [add_links](#targetadd_links). Of course, it can also be added directly through the [add_ldflags](#targetadd_ldflags) or [add_shflags](#targetadd_shflags) interface. It is also possible.

<p class="tip">
If you don't want to write to death in the project, you can set it by: `xmake f --linkdirs=xxx` or `xmake f --ldflags="-L/xxx"`, of course, this manually set directory search priority. higher.
</p>

### target:add_rpathdirs

#### Add load search directories for dynamic libraries

After [add_linkdirs](#targetadd_linkdirs) sets the link search directory of the dynamic library, the program is normally linked, but in the Linux platform, if you want to run the compiled program normally, it will report that the dynamic library fails to be loaded.

Because the dynamic library's load directory is not found, if you want to run the program that depends on the dynamic library, you need to set the `LD_LIBRARY_PATH` environment variable to specify the dynamic library directory to be loaded.

However, this method is global, and the impact is too wide. The better way is to set the dynamic library search path to be loaded when the linker is set by the linker option of `-rpath=xxx`, and xmake does it. Encapsulation, better handling cross-platform issues with `add_rpathdirs`.

The specific use is as follows:

```lua
target("test")
    set_kind("binary")
    add_linkdirs("$(buildir)/lib")
    add_rpathdirs("$(buildir)/lib")
```

Just need to set the rpath directory when linking, although the same purpose can be achieved by `add_ldflags("-Wl,-rpath=xxx")`, but this interface is more general.

Internally, different platforms will be processed. For example, under macOS, the `-rpath` setting is not required, and the running program can be loaded normally. Therefore, for this platform, xmake internally ignores the setting directly to avoid link error.

When doing dynamic library linking for dlang programs, xmake will automatically process it into `-L-rpath=xxx` to pass in the linker of dlang, thus avoiding the need to directly use `add_ldflags` to determine and handle different platforms and compile. Problem.

The 2.1.7 version has improved this interface, supporting: `@loader_path`, `@executable_path` and `$ORIGIN` built-in variables to specify the program's load directory. Their effects are basically the same, mainly for Also compatible with macho, elf.

E.g:

```lua
target("test")
    set_kind("binary")
    add_linkdirs("$(buildir)/lib")
    add_rpathdirs("@loader_path/lib")
```

Specify the test program to load the dynamic library file of `lib/*.[so|dylib]` in the current execution directory, which will help to improve the portability of the program without writing dead absolute paths and relative paths, resulting in program and directory switching. Causes the program to load the dynamic library failed.

<p class="tip">
It should be noted that under macos, if the add_rpathdirs setting is in effect, you need to do some preprocessing on dylib and add the `@rpath/xxx` path setting:
`$install_name_tool -add_rpath @rpath/libxxx.dylib xxx/libxxx.dylib`
We can also check if there is a path with @rpath via `otool -L libxxx.dylib`
</p>

### target:add_includedirs

#### Add include search directories

Set the search directory for the header file. This interface is used as follows:

```lua
target("test")
    add_includedirs("$(buildir)/include")
```

Of course, it can also be set directly through interfaces such as [add_cxflags](#targetadd_cxflags) or [add_mxflags](#targetadd_mxflags), which is also possible.

After 2.2.5, includedirs can be exported to dependent child targets via the extra `{public|interface = true}` property setting, for example:

```lua
target("test")
    set_kind("static")
    add_includedirs("src/include") -- only for the current target
    add_includedirs("$(buildir)/include", {public = true}), the current target and child targets will be set

target("demo")
    set_kind("binary")
    add_deps("test")
```

For more on this block, see: [add_deps](#targetadd_deps)

<p class="tip">
If you don't want to write to death in the project, you can set it by: `xmake f --includedirs=xxx` or `xmake f --cxflags="-I/xxx"`, of course, this manually set directory search priority. higher.
</p>

### target:add_defines

#### Add macro definition

```lua
add_defines("DEBUG", "TEST=0", "TEST2=\"hello\"")
```

Equivalent to setting the compile option:

```
-DDEBUG -DTEST=0 -DTEST2=\"hello\"
```

### target:add_undefines

#### Add macro undefinition

```lua
add_undefines("DEBUG")
```

Equivalent to setting the compile option: `-UDEBUG`

In the code is equivalent to: `#undef DEBUG`

### target:add_defines_h

#### Add macro definition to auto-generated config header

<p class="warn">
After the 2.2.5 version, this interface has been deprecated, please use [add_configfiles](#targetadd_configfiles).
</p>

Add macro definitions to the `config.h` configuration file, `config.h` settings, refer to the [set_config_h](#targetset_config_h) interface.

### target:add_undefines_h

#### Add macro undefinition to auto-generated config header

<p class="warn">
After the 2.2.5 version, this interface has been deprecated, please use [add_configfiles](#targetadd_configfiles).
</p>

Disable the macro definition by `undef` in the `config.h` configuration file. For the setting of `config.h`, refer to the [set_config_h](#targetset_config_h) interface.

### target:add_cflags

#### Add c compilation flags

Add compilation options only for c code

```lua
add_cflags("-g", "-O2", "-DDEBUG")
```

<p class="warn">
All option values ​​are based on the definition of gcc as standard. If other compilers are not compatible (for example: vc), xmake will automatically convert it internally to the corresponding option values ​​supported by the compiler.
Users don't have to worry about compatibility. If other compilers don't have matching values, xmake will automatically ignore the settings.
</p>

After version 2.1.9, the force parameter can be used to force the automatic detection of flags to be disabled and passed directly to the compiler. Even if the compiler may not support it, it will be set:

```lua
add_cflags("-g", "-O2", {force = true})
```

### target:add_cxflags

#### Add c/c++ compilation flags

Add compilation options to c/c++ code at the same time

### target:add_cxxflags

#### Add c++ compilation flags

Add compilation options only to c++ code

### target:add_mflags

#### Add objc compilation flags

Add compilation options only to objc code

```lua
add_mflags("-g", "-O2", "-DDEBUG")
```

After version 2.1.9, the force parameter can be used to force the automatic detection of flags to be disabled and passed directly to the compiler. Even if the compiler may not support it, it will be set:

```lua
add_mflags("-g", "-O2", {force = true})
```

### target:add_mxflags

#### Add objc/objc++ compilation flags

Also add compile options to objc/objc++ code

```lua
add_mxflAgs("-framework CoreFoundation")
```

### target:add_mxxflags

#### Add objc++ compilation flags

Add compilation options only to objc++ code

```lua
add_mxxflags("-framework CoreFoundation")
```

### target:add_scflags

#### Add swift compilation flags

Add compilation options to swift code

```lua
add_scflags("xxx")
```

### target:add_asflags

#### Add asm compilation flags

Add compilation options to assembly code

```lua
add_asflags("xxx")
```

### target:add_gcflags

#### Add go compilation flags

Add compile options to golang code

```lua
add_gcflags("xxx")
```

### target:add_dcflags

#### Add dlang compilation flags

Add compilation options to dlang code

```lua
add_dcflags("xxx")
```

### target:add_rcflags

#### Add MASTER compilation flags

Add compilation options to the rust code

```lua
add_rcflags("xxx")
```

### target:add_cuflags

#### Add cuda compilation flags

Add compilation options to cuda code

```lua
add_cuflags("-gencode arch=compute_30,code=sm_30")
```

### target:add_culdflags

#### Add cuda device link flags

After v2.2.7, cuda default build will use device-link. If you want to set some link flags in this stage, you can set it through this interface.
The final program link will use ldflags, will not call nvcc, and directly link through c/c++ linker such as gcc/clang.

For a description of device-link, please refer to: https://devblogs.nvidia.com/separate-compilation-linking-cuda-device-code/

```lua
add_culdflags("-gencode arch=compute_30,code=sm_30")
```

### target:add_ldflags

#### Add static library link flags

Add static link option

```lua
add_ldflags("-L/xxx", "-lxxx")
```

### target:add_arflags

#### Add archive library flags

Affect the generation of static libraries

```lua
add_arflags("xxx")
```
### target:add_shflags

#### Add dynamic library link flags

Affect the generation of dynamic libraries

```lua
add_shflags("xxx")
```

### target:add_options

#### Add option dependencies

This interface is similar to [set_options](#targetset_options), the only difference is that this is an append option, and [set_options](#targetset_options) overrides the previous settings each time.

### target:add_packages

#### Add package dependencies

In the target scope, add integration package dependencies, for example:

```lua
target("test")
    add_packages("zlib", "polarssl", "pcre", "mysql")
```

In this way, when compiling the test target, if the package exists, the macro definition, the header file search path, and the link library directory in the package will be automatically appended, and all the libraries in the package will be automatically linked.

Users no longer need to call the [add_links](#targetadd_links), [add_includedirs](#targetadd_includedirs), [add_ldflags](#targetadd_ldflags) interfaces to configure the dependent library links.

For how to set up the package search directory, please refer to: [add_packagedirs](/manual/global_interfaces?id=add_packagedirs) interface

After v2.2.2, this interface also supports packages defined by [add_requires](/manual/global_interfaces?id=add_requires) in remote dependency management.

```lua
add_requires("zlib", "polarssl")
target("test")
    add_packages("zlib", "polarssl")
```

After v2.2.3, it also supports overwriting built-in links to control the actual linked libraries:


```lua
-- By default, there will be links to ncurses, panel, form, etc.
add_requires("ncurses")

target("test")

    -- Display specified, only use ncurses a link library
    add_packages("ncurses", {links = "ncurses"})
```

Or simply disable links and only use header files:

```lua
add_requires("lua")
target("test")
    add_packages("lua", {links = {}})
```

### target:add_languages

#### Add language standards

Similar to [set_languages](#targetset_languages), the only difference is that this interface will not overwrite the previous settings, but append settings.

### target:add_vectorexts

#### Add vector extensions

Add extended instruction optimization options, currently supports the following extended instruction sets:

```lua
add_vectorexts("mmx")
add_vectorexts("neon")
add_vectorexts("avx", "avx2")
add_vectorexts("sse", "sse2", "sse3", "ssse3")
```

<p class="tip">
If the currently set instruction set compiler does not support it, xmake will automatically ignore it, so you don't need the user to manually determine the maintenance. Just set all the instruction sets you need.
</p>

### target:add_frameworks

#### Add frameworks

Currently used for the `objc` and `swift` programs of the `ios` and `macosx` platforms, for example:

```lua
target("test")
    add_frameworks("Foundation", "CoreFoundation")
```

Of course, you can also use [add_mxflags](#targetadd_mxflags) and [add_ldflags](#targetadd_ldflags) to set them up, but it is cumbersome and is not recommended.

```lua
target("test")
    add_mxflags("-framework Foundation", "-framework CoreFoundation")
    add_ldflags("-framework Foundation", "-framework CoreFoundation")
```

If it is not for both platforms, these settings will be ignored.

### target:add_frameworkdirs

#### Add framework search directories

For some third-party frameworks, it is impossible to find them only through [add_frameworks](#targetadd_frameworks). You also need to add a search directory through this interface.

```lua
target("test")
    add_frameworks("MyFramework")
    add_frameworkdirs("/tmp/frameworkdir", "/tmp/frameworkdir2")
```

### target:set_tools

#### Set toolchains

For the source files added by `add_files("*.c")`, the default is to call the system's best matching compiler to compile, or manually modify it by `xmake f --cc=clang` command, but these are Globally affects all target targets.

If there are some special requirements, you need to specify a different compiler, linker or specific version of the compiler for a specific target target under the current project. At this time, the interface can be used for purposes. For example:

```lua
target("test1")
    add_files("*.c")

target("test2")
    add_files("*.c")
    set_tools("cc", "$(projectdir)/tools/bin/clang-5.0")
```

The above description only makes special settings for the compiler of the test2 target, compiling test2 with a specific clang-5.0 compiler, and test1 still uses the default settings.

For setting multiple compiler types at the same time, you can write:

```lua
set_tools {
    cc = path.join(os.projectdir(), "tools/bin/clang-5.0"),
    mm = path.join(os.projectdir(), "tools/bin/clang-5.0"),
}
```

<p class="tip">
Each setting will override the previous setting under the current target target. Different targets will not be overwritten and independent of each other. If set in the root domain, all child targets will be affected.
</p>

Or you can use [add_tools](#targetadd_tools) to set:

```lua
add_tools("cc", "$(projectdir)/tools/bin/clang-5.0")
add_tools("mm", "$(projectdir)/tools/bin/clang-5.0")
```

The previous parameter is key, which is used to specify the tool type. Currently supported (compiler, linker, archiver):

| Tool Type | Description |
| ------------ | ------------------------------------ |
| cc | c compiler |
| cxx | c++ compiler |
| mm | objc compiler |
| mxx | objc++ compiler |
| gc | go compiler |
| as | assembler |
| sc | swift compiler |
| rc | rust compiler |
| dc | dlang compiler |
| ld | Common executable program linker such as c/c++/asm/objc |
| sh | c/c++/asm/objc and other universal dynamic library linker |
| ar | general static library archiver such as c/c++/asm/objc |
| dc-ld | dlang executable linker, rc-ld/gc-ld, etc. |
Dc-sh | dlang dynamic library linker, rc-sh/gc-sh, etc. |

For some compiler file names that are irregular, causing xmake to fail to recognize the known compiler name, we can also add a tool name prompt, for example:

```lua
add_tools("cc", "gcc@$(projectdir)/tools/bin/Mipscc.exe")
```

The above description sets mipscc.exe as the c compiler, and prompts xmake to compile as a pass-through processing method for gcc.

### target:add_tools

#### Add toolchains

Similar to [set_tools](#targetset_tools), the difference is that this interface can be called multiple times to add multiple tools, and [set_tools](#targetset_tools) will overwrite the previous settings each time.

### target:set_values

#### Set custom configuration values

Set some extended configuration values ​​for the target. These configurations do not have a built-in api like `set_ldflags`. You can extend the configuration by passing in a configuration name with the first argument.
Generally used to pass configuration parameters to scripts in custom rules, for example:

```lua
rule("markdown")
    on_build_file(function (target, sourcefile)
        -- compile .markdown with flags
        local flags = target:values("markdown.flags")
        if flags then
            -- ..
        end
    end)

target("test")
    add_files("src/*.md", {rule = "markdown"})
    set_values("markdown.flags", "xxx", "xxx")
```

In the above code example, it can be seen that when the target applies the markdown rule, some flag values ​​are set by set_values ​​and provided to the markdown rule for processing.
In the rule script, you can get the extended flag value set in the target by `target:values("markdown.flags")`.

<p class="tip">
The specific extension configuration name will be different according to different rules. Currently, you can refer to the description of related rules: [built-in rules](#built-in rules)
</p>

### target:add_values

#### Add custom configuration values

Usage is similar to [target:set_values](#targetset_tools), the difference is that this interface is an additional setting, and will not override the settings each time.

### target:set_rundir

#### Setting the running directory

This interface is used to set the current running directory of the default running target program. If not set, by default, the target is loaded and run in the directory where the executable file is located.

If the user wants to modify the load directory, one is to customize the run logic by `on_run()`, and to do the switch inside, but just to cut the directory, this is too cumbersome.

Therefore, you can quickly switch settings to the default directory environment through this interface.

```lua
target("test")
     set_kind("binary")
     add_files("src/*.c")
     set_rundir("$(projectdir)/xxx")
```

### target:add_runenvs

#### Adding runtime environment variables

This interface is used to add an environment variable that sets the default running target program. Unlike [set_runenv](#targetset_runenv), this interface appends the value in the existing system env and does not overwrite it.

Therefore, for PATH, it is very convenient to append values through this interface, and this interface supports multi-value settings, so it is usually used to set multi-value env with path sep. .

```lua
target("test")
    set_kind("binary")
    add_files("src/*.c")
    add_runenvs("PATH", "/tmp/bin", "xxx/bin")
    add_runenvs("LD_LIBRARY_PATH", "/tmp/lib", "xxx/lib")
```

### target:set_runenv

#### Setting the runtime environment variable

This interface differs from [add_runenvs](#targetadd_runenvs) in that `set_runenv` is an override setting for an environment variable that overrides the env value of the original system environment, and this interface is singular and cannot pass multiple parameters.

So, if you want to override the env that sets the multipath in PATH, you need to splicing yourself:

```lua
target("test")
    set_kind("binary")
    add_files("src/*.c")
    set_runenv("PATH", path.joinenv("/tmp/bin", "xxx/bin"))
    set_runenv("NAME", "value")
```

### target:set_installdir

#### Set the installation directory

By default, `xmake install` will be installed to the system `/usr/local` directory. We can specify other installation directories except `xmake install -o /usr/local`.
You can also set a different installation directory for the target in xmake.lua instead of the default directory.

### target:add_installfiles

#### Add installation files

2.2.5 version of the new interface, used to set the corresponding file for each target, generally used for the `xmake install/uninstall` command.

For example, we can specify to install various types of files to the installation directory:

```lua
target("test")
    add_installfiles("src/*.h")
    add_installfiles("doc/*.md")
```

By default on Linux and other systems, we will install to `/usr/local/*.h, /usr/local/*.md`, but we can also specify to install to a specific subdirectory:

```lua
target("test")
    add_installfiles("src/*.h", {prefixdir = "include"})
    add_installfiles("doc/*.md", {prefixdir = "share/doc"})
```

The above settings, we will install to `/usr/local/include/*.h, /usr/local/share/doc/*.md`

We can also install by subdirectory in the source file by `()`, for example:

```lua
target("test")
    add_installfiles("src/(tbox/*.h)", {prefixdir = "include"})
    add_installfiles("doc/(tbox/*.md)", {prefixdir = "share/doc"})
```

We extract the `trc/*.h` subdirectory structure from the files in `src/tbox/*.h` and install it: `/usr/local/include/tbox/*.h, /usr/local /share/doc/tbox/*.md`

Of course, users can also use the [set_installdir](#targetset_installdir) interface.

For a detailed description of this interface, see: https://github.com/xmake-io/xmake/issues/318

### target:add_headerfiles

#### Add header files

2.2.5 version of the new interface, used to set the corresponding header file for each target, generally used for the `xmake install/uninstall` command.

This interface is used in almost the same way as the [add_installfiles](#targetadd_installfiles) interface. It can be used as a Tianjian installation file, but this interface is only used to install header files.
Therefore, it is much easier to use than `add_installfiles`. By default, prefixfix is not set, and the header files are automatically installed into the corresponding `include` subdirectory.

And this interface for the `xmake project -k vs201x` and other plug-in generated IDE files, will also add the corresponding header file into it.

<p class="tip">
It should be noted that the previous [add_headers](#targetadd_headers) interface has been deprecated. Please replace this with the new version. This old interface will automatically copy the header files to the build directory during the compilation process. This logic is not designed. well.
</p>

### target:set_configdir

#### Set the output directory of configuration files

Version 2.2.5 adds a new interface, mainly used for the output directory of the template configuration file set by the [add_configfiles](#targetadd_configfiles) interface.

### target:set_configvar

#### Set template configuration variable

2.2.5 version of the new interface, used to add some template configuration variables that need to be pre-compiled before compilation, generally used for [add_configfiles](#targetadd_configfiles) interface.

### target:add_configfiles

#### Add template configuration files

2.2.5 version of the new interface, used to add some configuration files that need to be pre-processed before compiling, used to replace the old interface such as [set_config_header](#targetset_config_header).

Because this interface is more versatile, it is not only used to handle the automatic generation and preprocessing of config.h, but also to handle various file types, while `set_config_header` is only used to process header files and does not support template variable substitution.

Let's start with a simple example:

```lua
target("test")
    set_kind("binary")
    add_files("src/*.c")
    set_configdir("$(buildir)/config")
    add_configfiles("src/config.h.in")
```

The above settings will automatically configure the `config.h.in` header file template before compiling. After preprocessing, it will generate the output to the specified `build/config/config.h`.

If `set_configdir` is not set, the default output is in the `build` directory.

The `.in` suffix will be automatically recognized and processed. If you want to store the output as a different file name, you can pass:

```lua
add_configfiles("src/config.h", {filename = "myconfig.h"})
```

The way to rename the output, again, this interface is similar to [add_installfiles](#targetadd_configfiles), which also supports prefixdir and subdirectory extraction settings:

```lua
add_configfiles("src/*.h.in", {prefixdir = "subdir"})
add_configfiles("src/(tbox/config.h)")
```

One of the most important features of this interface is that it can be preprocessed and replaced with some of the template variables in the preprocessing, for example:

Config.h.in

```
#define VAR1 "${VAR1}"
#define VAR2 "${VAR2}"
#define HELLO "${HELLO}"
```

```lua
set_configvar("VAR1", "1")

target("test")
    set_kind("binary")
    add_files("main.c")

    set_configvar("VAR2", 2)
    add_configfiles("config.h.in", {variables = {hello = "xmake"}})
    add_configfiles("*.man", {copyonly = true})
```

The template variable is set via the [set_configvar](#targetset_configvar) interface, and the substitution is handled by the variable set in `{variables = {xxx = ""}}`.

The preprocessed file `config.h` is:

```
#define VAR1 "1"
#define VAR2 "2"
#define HELLO "xmake"
```

The `{copyonly = true}` setting will force `*.man` to be treated as a normal file, copying files only during the preprocessing stage, and not replacing variables.

The default template variable matching mode is `${var}`, of course we can also set other matching modes, for example, to `@var@` matching rules:

```lua
target("test")
    add_configfiles("config.h.in", {pattern = "@(.-)@"})
```

We also have some built-in variables that can be replaced with default variables even if they are not set through this interface:

```
${VERSION} -> 1.6.3
${VERSION_MAJOR} -> 1
${VERSION_MINOR} -> 6
${VERSION_ALTER} -> 3
${VERSION_BUILD} -> set_version("1.6.3", {build = "%Y%m%d%H%M"}) -> 201902031421
${PLAT} and ${plat} -> MACOS and macosx
${ARCH} and ${arch} -> ARM and arm
${MODE} and ${mode} -> DEBUG/RELEASE and debug/release
${DEBUG} and ${debug} -> 1 or 0
${OS} and ${os} -> IOS or ios
```

E.g:

Config.h.in

```c
#define CONFIG_VERSION "${VERSION}"
#define CONFIG_VERSION_MAJOR ${VERSION_MAJOR}
#define CONFIG_VERSION_MINOR ${VERSION_MINOR}
#define CONFIG_VERSION_ALTER ${VERSION_ALTER}
#define CONFIG_VERSION_BUILD ${VERSION_BUILD}
```

Config.h

```c
#define CONFIG_VERSION "1.6.3"
#define CONFIG_VERSION_MAJOR 1
#define CONFIG_VERSION_MINOR 6
#define CONFIG_VERSION_ALTER 3
#define CONFIG_VERSION_BUILD 201902031401
```

We can also perform some variable state control processing on the `#define` definition:

Config.h.in

```c
${define FOO_ENABLE}
```

```lua
set_configvar("FOO_ENABLE", 1) -- or pass true
set_configvar("FOO_STRING", "foo")
```

After setting the above variable, `${define xxx}` will be replaced with:

```c
#define FOO_ENABLE 1
#define FOO_STRING "foo"
```

Or (when set to 0 disable)

```c
/* #undef FOO_ENABLE */
/* #undef FOO_STRING */
```

This method is very useful for some automatic detection generation config.h, such as with the option to do automatic detection:

```lua
option("foo")
    set_default(true)
    set_description("Enable Foo")
    set_configvar("FOO_ENABLE", 1) -- or pass true to enable the FOO_ENABLE variable
    set_configvar("FOO_STRING", "foo")

target("test")
    add_configfiles("config.h.in")

    -- If the foo option is enabled -> Add FOO_ENABLE and FOO_STRING definitions
    add_options("foo")
```

Config.h.in

```c
${define FOO_ENABLE}
${define FOO_STRING}
```

Config.h

```c
#define FOO_ENABLE 1
#define FOO_STRING "foo"
```

Regarding the option option detection, and the automatic generation of config.h, there are some helper functions, you can look at it: https://github.com/xmake-io/xmake/issues/342

In addition to `#define`, if you want to other non`#define xxx` also performs state switching processing. You can use the `${default xxx 0}` mode to set default values, for example:

```
HAVE_SSE2 equ ${default VAR_HAVE_SSE2 0}
```

After `set_configvar("HAVE_SSE2", 1)` is enabled, it becomes `HAVE_SSE2 equ 1`. If no variable is set, the default value is used: `HAVE_SSE2 equ 0`

For a detailed description of this, see: https://github.com/xmake-io/xmake/issues/320

