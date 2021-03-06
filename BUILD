load("@io_bazel_rules_go//go:def.bzl", "go_binary", "go_embed_data", "go_library")
load("@rules_proto//proto:defs.bzl", "proto_library")
load("@io_bazel_rules_go//proto:def.bzl", "go_proto_library")

##
## Binaries.
##
go_binary(
    name = "redird",
    srcs = [
        "redird.go",
        "redird_release.go",
    ],
    pure = "on",
    deps = [
        ":assets",
        ":handler",
        ":redird_go_proto",
        "@com_github_golang_protobuf//proto:go_default_library",
        "@org_golang_x_crypto//acme:go_default_library",
        "@org_golang_x_crypto//acme/autocert:go_default_library",
    ],
)

go_binary(
    name = "redird_debug",
    srcs = [
        "redird.go",
        "redird_debug.go",
    ],
    pure = "on",
    deps = [
        ":assets",
        ":handler",
        ":redird_go_proto",
        "@com_github_golang_protobuf//proto:go_default_library",
    ],
)

##
## Libraries.
##
go_library(
    name = "handler",
    srcs = ["handler.go"],
    importpath = "github.com/BranLwyd/redird/handler",
    deps = [":assets"],
)

##
## Protobuf libraries.
##
proto_library(
    name = "redird_proto",
    srcs = ["redird.proto"],
)

go_proto_library(
    name = "redird_go_proto",
    importpath = "github.com/BranLwyd/redird/redird_go_proto",
    proto = ":redird_proto",
)

##
## Static assets.
##
go_embed_data(
    name = "embed_assets",
    srcs = glob(["assets/**"]),
    package = "assets",
    var = "Asset",
)

go_library(
    name = "assets",
    srcs = [
        "assets.go",
        ":embed_assets",
    ],
    importpath = "github.com/BranLwyd/redird/assets",
)
