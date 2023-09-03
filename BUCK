
load("//bucktools/lua:defs.bzl", "lua_library")
load("//bucktools/util:util.bzl", "select_file")

cxx_library(
    name = "lfs_cc",
    srcs = glob(["src/*.c"]),
    headers = glob(["**/*.h"]),
    visibility = ["PUBLIC"],
    deps = select({
        "config//os:linux": ["//third-party/lua/luajit:luajit-lib-headers-only"],
        "config//os:windows": ["//third-party/lua/luajit:luajit-lib"],
    }),
)

# Rename to match the expected require path
select_file(
    name = "lfs-shared-lib",
    filter = select({
        "DEFAULT": "**/*.so",
        "config//os:windows": "**/*.dll",
    }),
    srcs = [":lfs_cc"],
    out = select({
        "DEFAULT": "lfs.so",
        "config//os:windows": "lfs.dll",
    }),
)

lua_library(
    name = "lfs",
    srcs = [
        ":lfs-shared-lib",
    ],
    visibility = ["PUBLIC"],
)
