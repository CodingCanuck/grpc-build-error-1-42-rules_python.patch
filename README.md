# Minimal reproduction of the gRPC build bug discussed in https://github.com/grpc/grpc/pull/27507#discussion_r810549578.

Reproduce by running:
```
bazel build //:dummy
```

This error reproduces on bazel 4.2.1 and 5.0.0.

Sample error:
```
$ bazel build //:dummygit statusStarting local Bazel server and connecting to it...
INFO: Repository io_bazel_rules_python instantiated at:
  /home/$USER/dev/grpc-build-error-1-42-rules_python.patch/WORKSPACE:20:10: in <toplevel>
  /home/$USER/.cache/bazel/_bazel_$USER/0c42c3dc6ae2ab207d18d04a4f66821c/external/com_github_grpc_grpc/bazel/grpc_deps.bzl:459:21: in grpc_deps
  /home/$USER/.cache/bazel/_bazel_$USER/0c42c3dc6ae2ab207d18d04a4f66821c/external/com_github_grpc_grpc/bazel/grpc_python_deps.bzl:53:21: in grpc_python_depsRepository rule http_archive defined at:  /home/$USER/.cache/bazel/_bazel_$USER/0c42c3dc6ae2ab207d18d04a4f66821c/external/bazel_tools/tools/build_defs/repo/http.bzl:364:31: in <toplevel>
INFO: Repository 'io_bazel_rules_python' used the following cache hits instead of downloading the corresponding file. * Hash '954aa89b491be4a083304a2cb838019c8b8c3720a7abb9c4cb81ac7a24230cea' for https://github.com/bazelbuild/rules_python/releases/download/0.4.0/rules_python-0.4.0.tar.gz
If the definition of 'io_bazel_rules_python' was updated, verify that the hashes were also updated.
ERROR: An error occurred during the fetch of repository 'io_bazel_rules_python':   Traceback (most recent call last):        File "/home/$USER/.cache/bazel/_bazel_$USER/0c42c3dc6ae2ab207d18d04a4f66821c/external/bazel_tools/tools/build_defs/repo/http.bzl", line 122, column 10, in _http_archive_impl
                patch(ctx, auth = auth)        File "/home/$USER/.cache/bazel/_bazel_$USER/0c42c3dc6ae2ab207d18d04a4f66821c/external/bazel_tools/tools/build_defs/repo/utils.bzl", line 167, column 22, in patch
                ctx.patch(patchfile, strip)Error in patch: Unable to load package for //third_party:rules_python.patch: BUILD file not found in any of the following directories. Add a BUILD file to a directory to mark it as a package. - /home/$USER/dev/grpc-build-error-1-42-rules_python.patch/third_party
ERROR: /home/$USER/dev/grpc-build-error-1-42-rules_python.patch/WORKSPACE:20:10: fetching http_archive rule //external:io_bazel_rules_python: Traceback (most recent call last):        File "/home/$USER/.cache/bazel/_bazel_$USER/0c42c3dc6ae2ab207d18d04a4f66821c/external/bazel_tools/tools/build_defs/repo/http.bzl", line 122, column 10, in _http_archive_impl
                patch(ctx, auth = auth)
        File "/home/$USER/.cache/bazel/_bazel_$USER/0c42c3dc6ae2ab207d18d04a4f66821c/external/bazel_tools/tools/build_defs/repo/utils.bzl", line 167, column 22, in patch                ctx.patch(patchfile, strip)Error in patch: Unable to load package for //third_party:rules_python.patch: BUILD file not found in any of the following directories. Add a BUILD file to a directory to mark it as a package.
 - /home/$USER/dev/grpc-build-error-1-42-rules_python.patch/third_partyERROR: no such package '@io_bazel_rules_python//python': Unable to load package for //third_party:rules_python.patch: BUILD file not found in any of the following directories. Add a BUILD file to a directory to mark it as a package.
 - /home/$USER/dev/grpc-build-error-1-42-rules_python.patch/third_party
INFO: Elapsed time: 4.444s
INFO: 0 processes.
FAILED: Build did NOT complete successfully (0 packages loaded)
```