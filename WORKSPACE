load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive", "http_file")

#--------
# Go
#--------
## rules_go
http_archive(
    name = "io_bazel_rules_go",
    sha256 = "91585017debb61982f7054c9688857a2ad1fd823fc3f9cb05048b0025c47d023",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.42.0/rules_go-v0.42.0.zip",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.42.0/rules_go-v0.42.0.zip",
    ],
)

http_archive(
    name = "bazel_gazelle",
    sha256 = "b7387f72efb59f876e4daae42f1d3912d0d45563eac7cb23d1de0b094ab588cf",
    urls = [
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.34.0/bazel-gazelle-v0.34.0.tar.gz",
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-gazelle/releases/download/v0.34.0/bazel-gazelle-v0.34.0.tar.gz",
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies", "go_repository")

go_register_toolchains(
    version = "1.21.4",
)

go_rules_dependencies()

gazelle_dependencies()

#--------
# Python
#--------
http_archive(
    name = "rules_python",
    sha256 = "9acc0944c94adb23fba1c9988b48768b1bacc6583b52a2586895c5b7491e2e31",
    strip_prefix = "rules_python-0.27.0",
    url = "https://github.com/bazelbuild/rules_python/releases/download/0.27.0/rules_python-0.27.0.tar.gz",
)

load("@rules_python//python:repositories.bzl", "py_repositories", "python_register_toolchains")

py_repositories()

python_register_toolchains(
    name = "python_3_11",
    ignore_root_user_error = True,
    python_version = "3.11.6",
)

load("@python_3_11//:defs.bzl", "interpreter")

load("@rules_python//python:pip.bzl", "pip_parse")

pip_parse(
    name = "pip",
    python_interpreter_target = interpreter,
    requirements_lock = "//:requirements_lock.txt",
)

load("@pip//:requirements.bzl", "install_deps")

install_deps()

# rules_python gazelle extension.
http_archive(
    name = "rules_python_gazelle_plugin",
    sha256 = "9acc0944c94adb23fba1c9988b48768b1bacc6583b52a2586895c5b7491e2e31",
    strip_prefix = "rules_python-0.27.0/gazelle",
    url = "https://github.com/bazelbuild/rules_python/releases/download/0.27.0/rules_python-0.27.0.tar.gz",
)

load("@rules_python//gazelle:deps.bzl", _py_gazelle_deps = "gazelle_deps")

_py_gazelle_deps()
