Attempt to build using

    bazel build ...

This will yield:

    ERROR: /home/ubuntu/.cache/bazel/_bazel_1000/15f46a437a9b92831cf130ac35278560/external/com_grail_bazel_toolchain/platforms/BUILD.bazel:38:9: no such target '@platforms//cpu:armv6k': target 'armv6k' not declared in package 'cpu' defined by /home/ubuntu/.cache/bazel/_bazel_1000/15f46a437a9b92831cf130ac35278560/external/platforms/cpu/BUILD (did you mean 'armv7k'? Tip: use `query "@platforms//cpu:*"` to see all the targets in that package) and referenced by '@com_grail_bazel_toolchain//platforms:linux-armv6k'
    ERROR: /src/workspace/armv6k-repro/src/BUILD:2:10: While resolving toolchains for target //src:hello_world: Target @com_grail_bazel_toolchain//platforms:linux-armv6k was referenced as a platform, but does not provide PlatformInfo
    ERROR: Analysis of target '//src:hello_world' failed; build aborted:
    INFO: Elapsed time: 3.605s
    INFO: 0 processes.
    FAILED: Build did NOT complete successfully (7 packages loaded, 6 targets configured)