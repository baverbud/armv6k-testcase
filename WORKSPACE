workspace(name = "mower")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

BAZEL_TOOLCHAIN_TAG = "armv6k-testcase"
BAZEL_TOOLCHAIN_SHA = "59d82e144d4fdc526bea5804f160d458012179b8bee9d2a508b77adf965f0732"

http_archive(
    name = "com_grail_bazel_toolchain",
    sha256 = BAZEL_TOOLCHAIN_SHA,
    strip_prefix = "bazel-toolchain-raspi-{tag}".format(tag = BAZEL_TOOLCHAIN_TAG),
    canonical_id = BAZEL_TOOLCHAIN_TAG,
    url = "https://github.com/baverbud/bazel-toolchain-raspi/archive/refs/tags/{tag}.tar.gz".format(tag = BAZEL_TOOLCHAIN_TAG),
)

load("@com_grail_bazel_toolchain//toolchain:deps.bzl", "bazel_toolchain_dependencies")

bazel_toolchain_dependencies()

load("@com_grail_bazel_toolchain//toolchain:rules.bzl", "llvm_toolchain")

llvm_toolchain(
    name = "llvm_toolchain",
    llvm_version = "15.0.6",
)

# Rasperry pi cross compile

# Using armel here for simplicity of the test case, it doesn't match the hardware float support of armv6k though.
http_archive(
    name = "org_chromium_sysroot_linux_armel",
    build_file_content = """
filegroup(
  name = "sysroot",
  srcs = glob(["*/**"]),
  visibility = ["//visibility:public"],
)
""",
    sha256 = "fbf50a63bc78483018239a312d4b4a2d5ca0b6a1b5b5bf73c7edb1a39e8f9386",
    urls = ["https://commondatastorage.googleapis.com/chrome-linux-sysroot/toolchain/0bd4a342d73ee8176c649009d60468034b768a3a/debian_bullseye_armel_sysroot.tar.xz"],
)

llvm_toolchain(
    name = "llvm_toolchain_with_sysroot",
    llvm_version = "15.0.6",
    sysroot = {
        "linux-armv6k": "@org_chromium_sysroot_linux_armel//:sysroot",
    },
    # We can share the downloaded LLVM distribution with the first configuration.
    toolchain_roots = {
        "": "@llvm_toolchain_llvm//",
    },
)

load("@llvm_toolchain//:toolchains.bzl", "llvm_register_toolchains")

llvm_register_toolchains()
