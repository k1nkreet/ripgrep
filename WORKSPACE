load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "bazel_skylib",
    sha256 = "74d544d96f4a5bb630d465ca8bbcfe231e3594e5aae57e1edbf17a6eb3ca2506",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-skylib/releases/download/1.3.0/bazel-skylib-1.3.0.tar.gz",
        "https://github.com/bazelbuild/bazel-skylib/releases/download/1.3.0/bazel-skylib-1.3.0.tar.gz",
    ],
)
load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")
bazel_skylib_workspace()

http_archive(
    name = "rules_rust",
    sha256 = "50272c39f20a3a3507cb56dcb5c3b348bda697a7d868708449e2fa6fb893444c",
    urls = ["https://github.com/bazelbuild/rules_rust/releases/download/0.22.0/rules_rust-v0.22.0.tar.gz"],
)

# local_repository(
#     name = "rules_rust",
#     path = "../../rules_rust",
# )

load("@rules_rust//rust:repositories.bzl", "rules_rust_dependencies", "rust_register_toolchains")

rules_rust_dependencies()

rust_register_toolchains(
    edition = "2018",
)

load("@rules_rust//crate_universe:repositories.bzl", "crate_universe_dependencies")

# crate_universe_dependencies(bootstrap=True)
crate_universe_dependencies()

load("@rules_rust//crate_universe:defs.bzl", "crates_repository")

crates_repository(
    name = "crate_index",
    cargo_lockfile = "//:Cargo.lock",
    lockfile = "//:cargo-bazel-lock.json",
    # manifests = ["//:Cargo.toml"],
    # generator = "@cargo_bazel_bootstrap//:cargo-bazel",
    manifests = [
        "//:Cargo.toml",
        "//crates/globset:Cargo.toml",
        "//crates/grep:Cargo.toml",
        "//crates/cli:Cargo.toml",
        "//crates/matcher:Cargo.toml",
        "//crates/pcre2:Cargo.toml",
        "//:crates/printer/Cargo.toml",
        "//:crates/regex/Cargo.toml",
        "//:crates/searcher/Cargo.toml",
        "//crates/ignore:Cargo.toml",
    ],
)

load("@crate_index//:defs.bzl", "crate_repositories")

crate_repositories()
