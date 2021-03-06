licenses(["notice"])  # Apache 2.0

package(default_visibility = [":friends"])

package_group(
    name = "friends",
    includes = ["//tensorflow/compiler/jit:friends"],
    packages = [
        "//tensorflow/...",
        "//tensorflow_models/...",
        "//third_party/py/tensor2tensor/...",
    ],
)

load("//tensorflow:tensorflow.bzl", "tf_py_test")
load("//tensorflow:tensorflow.bzl", "cuda_py_test")

py_library(
    name = "compiler_py",
    srcs = [
        "__init__.py",
        "jit.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:framework_for_generated_wrappers",
    ],
)

cuda_py_test(
    name = "jit_test",
    size = "small",
    srcs = ["jit_test.py"],
    additional_deps = [
        ":compiler_py",
        "//third_party/py/numpy",
        "//tensorflow/python:array_ops",
        "//tensorflow/python:client",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:framework",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:gradients",
        "//tensorflow/python:init_ops",
        "//tensorflow/python:math_ops",
        "//tensorflow/python:platform_test",
        "//tensorflow/python:random_ops",
        "//tensorflow/python:variable_scope",
        "//tensorflow/python:variables",
    ],
    xla_enabled = True,
)

py_library(
    name = "xla",
    srcs = ["xla.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow/compiler/jit:xla_ops_py",
        "//tensorflow/compiler/jit/ops:xla_ops_grad",
        "//tensorflow/python:array_ops",
        "//tensorflow/python:control_flow_ops",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:platform",
        "//tensorflow/python:summary_op_util",
        "//tensorflow/python:util",
        "//tensorflow/python:variable_scope",
        "//tensorflow/python/estimator:estimator_py",
    ],
)

cuda_py_test(
    name = "xla_test",
    srcs = ["xla_test.py"],
    additional_deps = [
        ":xla",
        "@absl_py//absl/testing:parameterized",
        "//tensorflow/compiler/tests:xla_test",
        "//tensorflow/contrib/tpu:tpu_estimator",
        "//tensorflow/contrib/tpu:tpu_lib",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:control_flow_ops",
        "//tensorflow/python:control_flow_util",
        "//tensorflow/python:math_ops",
        "//tensorflow/python:platform",
        "//tensorflow/python:state_ops",
        "//tensorflow/python:summary",
        "//tensorflow/python:training",
        "//tensorflow/python:variable_scope",
        "//tensorflow/python/data/ops:dataset_ops",
    ],
    tags = [
        "no_mac",
        "no_windows",
    ],
    xla_enabled = True,
)
