load("@rules_foreign_cc//tools/build_defs:cmake.bzl", "cmake_external")
load("@gmaven_rules//:defs.bzl", "gmaven_artifact")

cmake_external(
    name = "libhello",
    lib_source = "//cmake_hello_world_lib/static:srcs",
    out_include_dir = "include/version123",
)

cc_library(
    name = "hello_lib_usage_example",
    srcs = ["hello_lib-example.cpp"],
    linkstatic = True,
    deps = [":libhello"],
    alwayslink = True,
)

android_library(
    name = "lib",
    srcs = ["java/com/example/android/bazel/MainActivity.java"],
    custom_package = "com.example.android.bazel",
    manifest = "LibraryManifest.xml",
    resource_files = glob(["res/**/*"]),
    deps = [
        ":hello_lib_usage_example",
        gmaven_artifact("com.android.support:appcompat-v7:aar:26.1.0"),
        gmaven_artifact("com.android.support.constraint:constraint-layout:aar:1.1.2"),
    ],
)

android_binary(
    name = "app",
    custom_package = "com.example.android.bazel",
    manifest = "AndroidManifest.xml",
    deps = [":lib"],
)
