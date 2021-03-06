package(default_visibility = ["//visibility:public"])

# TODO(lberki): Remove this once cc_toolchain_alias is in a Bazel release
load("//tools/cpp:alias_rules.bzl", "cc_toolchain_alias")

cc_toolchain_alias(name = "current_cc_toolchain")

cc_library(
    name = "malloc",
)

cc_library(
    name = "stl",
)

filegroup(
    name = "empty",
    srcs = [],
)

# This is the entry point for --crosstool_top.  Toolchains are found
# by lopping off the name of --crosstool_top and searching for
# "cc-compiler-${CPU}" in this BUILD file, where CPU is the target CPU
# specified in --cpu.
#
# This file group should include
#   * all cc_toolchain targets supported
#   * all file groups that said cc_toolchain might refer to,
# including the default_grte_top setting in the CROSSTOOL
# protobuf.
alias(
    name = "toolchain",
    actual = "//external:cc_toolchain",
)

# Hardcoded toolchain, legacy behaviour.
cc_toolchain_suite(
    name = "default-toolchain",
    toolchains = {
        "armeabi-v7a|compiler": ":cc-compiler-armeabi-v7a",
        "darwin|compiler": ":cc-compiler-darwin",
        "freebsd|compiler": ":cc-compiler-freebsd",
        "local|compiler": ":cc-compiler-local",
        "x64_windows|compiler": ":cc-compiler-x64_windows",
        "x64_windows_msvc|compiler": ":cc-compiler-x64_windows_msvc",
        "ppc|compiler": ":cc-compiler-ppc",
        "ios_x86_64|compiler": ":cc-compiler-ios_x86_64",
    },
)

cc_toolchain(
    name = "cc-compiler-local",
    all_files = ":empty",
    compiler_files = ":empty",
    cpu = "local",
    dwp_files = ":empty",
    dynamic_runtime_libs = [":empty"],
    linker_files = ":empty",
    objcopy_files = ":empty",
    static_runtime_libs = [":empty"],
    strip_files = ":empty",
    supports_param_files = 1,
)

cc_toolchain(
    name = "cc-compiler-ppc",
    all_files = ":empty",
    compiler_files = ":empty",
    cpu = "ppc",
    dwp_files = ":empty",
    dynamic_runtime_libs = [":empty"],
    linker_files = ":empty",
    objcopy_files = ":empty",
    static_runtime_libs = [":empty"],
    strip_files = ":empty",
    supports_param_files = 1,
)

cc_toolchain(
    name = "cc-compiler-armeabi-v7a",
    all_files = ":empty",
    compiler_files = ":empty",
    cpu = "local",
    dwp_files = ":empty",
    dynamic_runtime_libs = [":empty"],
    linker_files = ":empty",
    objcopy_files = ":empty",
    static_runtime_libs = [":empty"],
    strip_files = ":empty",
    supports_param_files = 1,
)

cc_toolchain(
    name = "cc-compiler-k8",
    all_files = ":empty",
    compiler_files = ":empty",
    cpu = "local",
    dwp_files = ":empty",
    dynamic_runtime_libs = [":empty"],
    linker_files = ":empty",
    objcopy_files = ":empty",
    static_runtime_libs = [":empty"],
    strip_files = ":empty",
    supports_param_files = 1,
)

cc_toolchain(
    name = "cc-compiler-darwin",
    all_files = ":osx_wrapper",
    compiler_files = ":osx_wrapper",
    cpu = "darwin",
    dwp_files = ":empty",
    dynamic_runtime_libs = [":empty"],
    linker_files = ":osx_wrapper",
    objcopy_files = ":empty",
    static_runtime_libs = [":empty"],
    strip_files = ":empty",
    supports_param_files = 0,
)

cc_toolchain(
    name = "cc-compiler-freebsd",
    all_files = ":empty",
    compiler_files = ":empty",
    cpu = "local",
    dwp_files = ":empty",
    dynamic_runtime_libs = [":empty"],
    linker_files = ":empty",
    objcopy_files = ":empty",
    static_runtime_libs = [":empty"],
    strip_files = ":empty",
    supports_param_files = 0,
)

cc_toolchain(
    name = "cc-compiler-x64_windows",
    all_files = ":empty",
    compiler_files = ":empty",
    cpu = "local",
    dwp_files = ":empty",
    dynamic_runtime_libs = [":empty"],
    linker_files = ":empty",
    objcopy_files = ":empty",
    static_runtime_libs = [":empty"],
    strip_files = ":empty",
    supports_param_files = 0,
)

cc_toolchain(
    name = "cc-compiler-x64_windows_msvc",
    all_files = ":every-file-x64_windows",
    compiler_files = ":compile-x64_windows",
    cpu = "x64_windows",
    dwp_files = ":empty",
    dynamic_runtime_libs = [":empty"],
    linker_files = ":empty",
    objcopy_files = ":empty",
    static_runtime_libs = [":empty"],
    strip_files = ":empty",
    supports_param_files = 1,
)

cc_toolchain(
    name = "cc-compiler-ios_x86_64",
    all_files = ":empty",
    compiler_files = ":empty",
    cpu = "local",
    dwp_files = ":empty",
    dynamic_runtime_libs = [":empty"],
    linker_files = ":empty",
    objcopy_files = ":empty",
    static_runtime_libs = [":empty"],
    strip_files = ":empty",
    supports_param_files = 0,
)

filegroup(
    name = "every-file-x64_windows",
    srcs = [
        ":compile-x64_windows",
    ],
)

filegroup(
    name = "compile-x64_windows",
    srcs = glob([
        "wrapper/bin/msvc_*",
        "wrapper/bin/pydir/msvc*",
    ]),
)

filegroup(
    name = "srcs",
    srcs = glob(["**"]),
)

filegroup(
    name = "interface_library_builder",
    srcs = ["build_interface_so"],
    visibility = ["//visibility:public"],
)

filegroup(
    name = "link_dynamic_library",
    srcs = ["link_dynamic_library.sh"],
)

filegroup(
    name = "osx_wrapper",
    srcs = ["osx_cc_wrapper.sh"],
)

cc_toolchain_type(name = "toolchain_type")

# A dummy toolchain is necessary to satisfy toolchain resolution until platforms
# are used in c++ by default.
# TODO(b/64754003): Remove once platforms are used in c++ by default.
toolchain(
    name = "dummy_cc_toolchain",
    toolchain = "dummy_cc_toolchain_impl",
    toolchain_type = ":toolchain_type",
)

load(":dummy_toolchain.bzl", "dummy_toolchain")

dummy_toolchain(name = "dummy_cc_toolchain_impl")

filegroup(
    name = "lib_cc_configure",
    srcs = ["lib_cc_configure.bzl"],
    visibility = ["//visibility:public"],
)
