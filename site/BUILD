licenses(["notice"])  # Apache 2.0

load("@bazel_tools//tools/build_defs/pkg:pkg.bzl", "pkg_tar")

filegroup(
    name = "jekyll-srcs",
    srcs = glob(
        ["**/*"],
        exclude = [
            "BUILD",
            "jekyll-tree.sh",
            "*.swp",
        ],
    ),
)

pkg_tar(
    name = "jekyll-base",
    srcs = [":jekyll-srcs"],
    strip_prefix = ".",
)

genrule(
    name = "jekyll-tree",
    srcs = [
        ":jekyll-base",
        "//stardoc:stardoc_doc",
        "//skylark:skylark-docs",
    ],
    outs = ["jekyll-tree.tar"],
    cmd = ("$(location jekyll-tree.sh) $@ " +
           "$(location jekyll-base) " +
           "$(location //skylark:skylark-docs) " +
           "$(location //stardoc:stardoc_doc) "),
    tools = ["jekyll-tree.sh"],
)
