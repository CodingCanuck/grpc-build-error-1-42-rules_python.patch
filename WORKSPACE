workspace(name = "codingcanuck_grpc_1_42_0_python_rules_patch_repro")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
http_archive(
    name = "com_github_grpc_grpc",
    # This compiles fine with grpc-1.40.0.
    #
    # urls = ["https://github.com/grpc/grpc/archive/v1.40.0.tar.gz"],
    # strip_prefix = "grpc-1.40.0",
    # sha256 = "13e7c6460cd979726e5b3b129bb01c34532f115883ac696a75eb7f1d6a9765ed",

    # But this fails to build on gRPC releases 1.42.0 or later (including
    # 1.44.0).
    urls = ["https://github.com/grpc/grpc/archive/refs/tags/v1.44.0.tar.gz"],
    strip_prefix = "grpc-1.44.0",
    sha256 = "8c05641b9f91cbc92f51cc4a5b3a226788d7a63f20af4ca7aaca50d92cc94a0d",
)

load("@com_github_grpc_grpc//bazel:grpc_deps.bzl", "grpc_deps")

grpc_deps()

# Load anything from the io_bazel_rules_python repo, which looks like it causes
# a conflict with a patch that the gRPC repo tries to apply to
# io_bazel_rule_python: see
# https://github.com/grpc/grpc/pull/27507#discussion_r810549578
load("@io_bazel_rules_python//python:pip.bzl", "pip_import")
