workspace(name = "grpc_kube_bazel_test")

################################################################################
# Setup Bazel project
################################################################################

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

################################################################################
# Bazel project dependencies
################################################################################

### BAZEL TOOLCHAINS

#http_archive(
#    name = "bazel_toolchains",
#    sha256 = "2431088b38fd8e2878db17e3c5babb431de9e5c52b6d8b509d3070fa279a5be2",
#    strip_prefix = "bazel-toolchains-3.3.1",
#    urls = [
#        "https://github.com/bazelbuild/bazel-toolchains/releases/download/3.3.1/bazel-toolchains-3.3.1.tar.gz",
#        "https://mirror.bazel.build/github.com/bazelbuild/bazel-toolchains/releases/download/3.3.1/bazel-toolchains-3.3.1.tar.gz",
#    ],
#)
#
#load("@bazel_toolchains//rules:rbe_repo.bzl", "rbe_autoconfig")
#
#rbe_autoconfig(name = "rbe_default")

### BAZEL BUILDTOOLS

#http_archive(
#    name = "com_github_bazelbuild_buildtools",
#    strip_prefix = "buildtools-ce0cf814cb03dddf546ea92b3d6bafddb0b9eaf8",
#    url = "https://github.com/bazelbuild/buildtools/archive/ce0cf814cb03dddf546ea92b3d6bafddb0b9eaf8.zip",
#)

### RULES PKG

#http_archive(
#    name = "rules_pkg",
#    sha256 = "352c090cc3d3f9a6b4e676cf42a6047c16824959b438895a76c2989c6d7c246a",
#    url = "https://github.com/bazelbuild/rules_pkg/releases/download/0.2.5/rules_pkg-0.2.5.tar.gz",
#)
#
#load("@rules_pkg//:deps.bzl", "rules_pkg_dependencies")
#
#rules_pkg_dependencies()

################################################################################
# Go dependencies
################################################################################

### RULES GO

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "a8d6b1b354d371a646d2f7927319974e0f9e52f73a2452d2b3877118169eb6bb",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.23.3/rules_go-v0.23.3.tar.gz",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.23.3/rules_go-v0.23.3.tar.gz",
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

go_register_toolchains()

### RULES GAZELLE

http_archive(
    name = "bazel_gazelle",
    sha256 = "cdb02a887a7187ea4d5a27452311a75ed8637379a1287d8eeb952138ea485f7d",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-gazelle/releases/download/v0.21.1/bazel-gazelle-v0.21.1.tar.gz",
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.21.1/bazel-gazelle-v0.21.1.tar.gz",
    ],
)

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")

gazelle_dependencies()

load("//:DEPENDENCIES.bzl", "go_repositories")

# gazelle:repository_macro DEPENDENCIES.bzl%go_repositories
go_repositories()

################################################################################
# Proto dependencies
################################################################################

### RULES PROTO

http_archive(
    name = "rules_proto",
    sha256 = "602e7161d9195e50246177e7c55b2f39950a9cf7366f74ed5f22fd45750cd208",
    strip_prefix = "rules_proto-97d8af4dc474595af3900dd85cb3a29ad28cc313",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_proto/archive/97d8af4dc474595af3900dd85cb3a29ad28cc313.tar.gz",
        "https://github.com/bazelbuild/rules_proto/archive/97d8af4dc474595af3900dd85cb3a29ad28cc313.tar.gz",
    ],
)

load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")

rules_proto_dependencies()

rules_proto_toolchains()

################################################################################
# Kubernetes & Docker dependencies
################################################################################

http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "4521794f0fba2e20f3bf15846ab5e01d5332e587e9ce81629c7f96c793bb7036",
    strip_prefix = "rules_docker-0.14.4",
    urls = ["https://github.com/bazelbuild/rules_docker/releases/download/v0.14.4/rules_docker-v0.14.4.tar.gz"],
)

load("@io_bazel_rules_docker//repositories:repositories.bzl", container_repositories = "repositories")

container_repositories()

load("@io_bazel_rules_docker//repositories:deps.bzl", container_deps = "deps")

container_deps()

load("@io_bazel_rules_docker//repositories:pip_repositories.bzl", "pip_deps")

pip_deps()

load("@io_bazel_rules_docker//go:image.bzl", go_image_repos = "repositories")

go_image_repos()

http_archive(
    name = "io_bazel_rules_k8s",
    sha256 = "d91aeb17bbc619e649f8d32b65d9a8327e5404f451be196990e13f5b7e2d17bb",
    strip_prefix = "rules_k8s-0.4",
    urls = ["https://github.com/bazelbuild/rules_k8s/releases/download/v0.4/rules_k8s-v0.4.tar.gz"],
)

load("@io_bazel_rules_k8s//toolchains/kubectl:kubectl_configure.bzl", "kubectl_configure")

kubectl_configure(
    name = "k8s_config",
    build_srcs = True,
    k8s_commit = "v1.18.5",
    k8s_prefix = "kubernetes-1.18.5",
    k8s_sha256 = "3fd73d1094f3b24f5b94d390b30a0613de272bbdb419f23b5e54185c3060b0e3",
)

load("@io_bazel_rules_k8s//k8s:k8s.bzl", "k8s_repositories")

k8s_repositories()

load("@io_bazel_rules_k8s//k8s:k8s_go_deps.bzl", k8s_go_deps = "deps")

k8s_go_deps()
