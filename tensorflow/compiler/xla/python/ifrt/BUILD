load("//tensorflow/compiler/xla:xla.bzl", "xla_cc_test")

package_group(
    name = "friends",
    includes = [
        "//tensorflow/compiler/xla/python:friends",
    ],
    packages = [
        "//tensorflow/compiler/xla/python/...",
    ],
)

package_group(
    name = "internal",
    packages = [
        "//tensorflow/compiler/xla/python/ifrt/...",
    ],
)

package(
    default_visibility = [
        ":friends",
        ":internal",
    ],
    licenses = ["notice"],
)

exports_files([
    "BUILD",
])

cc_library(
    name = "ifrt",
    srcs = [
        "array.cc",
        "client.cc",
        "compiler.cc",
        "dtype.cc",
        "executable.cc",
        "future.cc",
        "shape.cc",
        "sharding.cc",
    ],
    hdrs = [
        "array.h",
        "client.h",
        "compiler.h",
        "device.h",
        "dtype.h",
        "executable.h",
        "future.h",
        "shape.h",
        "sharding.h",
    ],
    deps = [
        "//tensorflow/compiler/xla:status",
        "//tensorflow/compiler/xla:statusor",
        "//tensorflow/compiler/xla:util",
        "//tensorflow/compiler/xla/pjrt:pjrt_client",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/container:inlined_vector",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/strings:str_format",
        "@com_google_absl//absl/synchronization",
        "@com_google_absl//absl/types:span",
        "@llvm-project//llvm:Support",
        "@tf_runtime//:ref_count",
    ],
)

xla_cc_test(
    name = "array_test",
    size = "small",
    srcs = ["array_test.cc"],
    deps = [
        ":ifrt",
        "@com_google_googletest//:gtest_main",
        "@llvm-project//llvm:Support",
    ],
)

xla_cc_test(
    name = "future_test",
    size = "small",
    srcs = ["future_test.cc"],
    deps = [
        ":ifrt",
        "//tensorflow/tsl/lib/core:status_test_util",
        "@com_google_absl//absl/types:span",
        "@com_google_googletest//:gtest_main",
    ],
)

xla_cc_test(
    name = "shape_test",
    size = "small",
    srcs = ["shape_test.cc"],
    deps = [
        ":ifrt",
        "@com_google_googletest//:gtest_main",
    ],
)

xla_cc_test(
    name = "sharding_test",
    size = "small",
    srcs = ["sharding_test.cc"],
    deps = [
        ":ifrt",
        "//tensorflow/tsl/lib/core:status_test_util",
        "@com_google_googletest//:gtest_main",
        "@llvm-project//llvm:Support",
    ],
)

cc_library(
    name = "test_util",
    testonly = 1,
    srcs = ["test_util.cc"],
    hdrs = ["test_util.h"],
    deps = [
        ":ifrt",
        "//tensorflow/compiler/xla:statusor",
        "@com_google_absl//absl/synchronization",
    ],
)

cc_library(
    name = "no_impl_test_main",
    testonly = 1,
    srcs = ["no_impl_test_main.cc"],
    deps = [
        "@com_google_googletest//:gtest",
    ],
)

cc_library(
    name = "array_impl_test_lib",
    testonly = 1,
    srcs = ["array_impl_test_lib.cc"],
    deps = [
        ":ifrt",
        ":test_util",
        "//tensorflow/tsl/lib/core:status_test_util",
        "//tensorflow/tsl/platform:test",
    ],
    alwayslink = 1,
)

xla_cc_test(
    name = "array_test_no_impl",
    srcs = [],
    deps = [
        ":array_impl_test_lib",
        ":no_impl_test_main",
    ],
)

cc_library(
    name = "client_impl_test_lib",
    testonly = 1,
    srcs = ["client_impl_test_lib.cc"],
    deps = [
        ":ifrt",
        ":test_util",
        "//tensorflow/tsl/platform:test",
    ],
    alwayslink = 1,
)

xla_cc_test(
    name = "client_test_no_impl",
    srcs = [],
    deps = [
        ":client_impl_test_lib",
        ":no_impl_test_main",
        "@com_google_googletest//:gtest",
    ],
)

cc_library(
    name = "executable_impl_test_lib",
    testonly = 1,
    srcs = ["executable_impl_test_lib.cc"],
    deps = [
        ":ifrt",
        ":test_util",
        "//tensorflow/compiler/xla/pjrt:mlir_to_hlo",
        "//tensorflow/tsl/lib/core:status_test_util",
        "//tensorflow/tsl/platform:statusor",
        "//tensorflow/tsl/platform:test",
        "@com_google_absl//absl/strings",
    ],
    alwayslink = 1,
)

xla_cc_test(
    name = "executable_test_no_impl",
    srcs = [],
    deps = [
        ":executable_impl_test_lib",
        ":no_impl_test_main",
        "@com_google_googletest//:gtest",
    ],
)
