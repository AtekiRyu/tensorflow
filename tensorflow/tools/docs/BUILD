# Description:
#   Doc generator

licenses(["notice"])  # Apache 2.0

exports_files(["LICENSE"])

package(
    default_visibility = ["//tensorflow:__subpackages__"],
)

load("//tensorflow:tensorflow.bzl", "py_test")

py_library(
    name = "doc_generator_visitor",
    srcs = [
        "doc_generator_visitor.py",
    ],
    srcs_version = "PY2AND3",
)

py_test(
    name = "doc_generator_visitor_test",
    size = "small",
    srcs = [
        "doc_generator_visitor_test.py",
    ],
    python_version = "PY2",
    srcs_version = "PY2AND3",
    deps = [
        ":doc_generator_visitor",
        ":generate_lib",
        "//tensorflow/python:platform_test",
    ],
)

py_library(
    name = "doc_controls",
    srcs = ["doc_controls.py"],
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
)

py_test(
    name = "doc_controls_test",
    size = "small",
    srcs = ["doc_controls_test.py"],
    python_version = "PY2",
    srcs_version = "PY2AND3",
    deps = [
        ":doc_controls",
        "//tensorflow/python:platform_test",
    ],
)

py_library(
    name = "parser",
    srcs = ["parser.py"],
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
    deps = [
        ":doc_controls",
        "//tensorflow/python:platform",
        "//tensorflow/python:util",
        "@astor_archive//:astor",
    ],
)

py_test(
    name = "parser_test",
    size = "small",
    srcs = ["parser_test.py"],
    python_version = "PY2",
    srcs_version = "PY2AND3",
    deps = [
        ":parser",
        "//tensorflow/python:platform_test",
    ],
)

py_library(
    name = "pretty_docs",
    srcs = ["pretty_docs.py"],
    srcs_version = "PY2AND3",
)

py_library(
    name = "generate_lib",
    srcs = ["generate_lib.py"],
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
    deps = [
        ":doc_controls",
        ":doc_generator_visitor",
        ":parser",
        ":pretty_docs",
        ":py_guide_parser",
        "//tensorflow/python:util",
        "//tensorflow/tools/common:public_api",
        "//tensorflow/tools/common:traverse",
        "@six_archive//:six",
    ],
)

py_test(
    name = "generate_lib_test",
    size = "small",
    srcs = ["generate_lib_test.py"],
    python_version = "PY2",
    srcs_version = "PY2AND3",
    deps = [
        ":generate_lib",
        ":parser",
        "//tensorflow/python:platform_test",
    ],
)

py_binary(
    name = "generate",
    srcs = ["generate.py"],
    python_version = "PY2",
    srcs_version = "PY2AND3",
    deps = [
        ":generate_lib",
        "//tensorflow:tensorflow_py",
        "//tensorflow/python:util",
        "//tensorflow/python/debug:debug_py",
    ],
)

py_test(
    name = "build_docs_test",
    size = "medium",
    srcs = ["build_docs_test.py"],
    python_version = "PY2",
    srcs_version = "PY2AND3",
    tags = [
        # No reason to run sanitizers or fastbuild for this test.
        "noasan",
        "nomsan",
        "notsan",
        "optonly",
    ],
    deps = [
        ":generate_lib",
        "//tensorflow:tensorflow_py",
        "//tensorflow/python/debug:debug_py",
    ],
)

py_test(
    name = "generate2_test",
    srcs = ["generate2_test.py"],
    python_version = "PY2",
    srcs_version = "PY2AND3",
    tags = [
        "manual",
        # No reason to run sanitizers or fastbuild for this test.
        "noasan",
        "nomsan",
        "notsan",
        "optonly",
    ],
    deps = [
        ":generate2_lib",
    ],
)

py_binary(
    name = "generate2",
    srcs = ["generate2.py"],
    python_version = "PY2",
    srcs_version = "PY2AND3",
    deps = [":generate2_lib"],
)

py_library(
    name = "generate2_lib",
    srcs = ["generate2.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow:tensorflow_py",
        "//tensorflow/python:util",
    ],
)

py_library(
    name = "py_guide_parser",
    srcs = ["py_guide_parser.py"],
    srcs_version = "PY2AND3",
)

py_test(
    name = "py_guide_parser_test",
    size = "small",
    srcs = ["py_guide_parser_test.py"],
    python_version = "PY2",
    srcs_version = "PY2AND3",
    deps = [
        ":py_guide_parser",
        "//tensorflow/python:client_testlib",
    ],
)
