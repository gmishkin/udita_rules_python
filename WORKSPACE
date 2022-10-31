workspace(name = "rp_grpcio")

# Inbuilt repos
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive", "http_file")
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository", "new_git_repository")

# Python
http_archive(
    name = "rules_python",
    sha256 = "8c8fe44ef0a9afc256d1e75ad5f448bb59b81aba149b8958f02f7b3a98f5d9b4",
    strip_prefix = "rules_python-0.13.0",
    url = "https://github.com/bazelbuild/rules_python/archive/refs/tags/0.13.0.tar.gz",
)

load("@rules_python//python:repositories.bzl", "python_register_toolchains")

python_register_toolchains(
    name = "python310",
    python_version = "3.10",
)

load("@rules_python//python:pip.bzl", "pip_parse")
load("@python310//:defs.bzl", "interpreter")

pip_parse(
    # (Optional) You can set an environment in the pip process to control its
    # behavior. Note that pip is run in "isolated" mode so no PIP_<VAR>_<NAME>
    # style env vars are read, but env vars that control requests and urllib3
    # can be passed
    # environment = {"HTTPS_PROXY": "http://my.proxy.fun/"},
    name = "pypi",
    # (Optional) You can provide extra parameters to pip.
    # Here, make pip output verbose (this is usable with `quiet = False`).
    # extra_pip_args = ["-v"],

    # (Optional) You can exclude custom elements in the data section of the generated BUILD files for pip packages.
    # Exclude directories with spaces in their names in this example (avoids build errors if there are such directories).
    #pip_data_exclude = ["**/* */**"],

    # (Optional) You can provide a python_interpreter (path) or a python_interpreter_target (a Bazel target, that
    # acts as an executable). The latter can be anything that could be used as Python interpreter. E.g.:
    # 1. Python interpreter that you compile in the build file (as above in @python_interpreter).
    # 2. Pre-compiled python interpreter included with http_archive
    # 3. Wrapper script, like in the autodetecting python toolchain.
    #
    # Here, we use the interpreter constant that resolves to the host interpreter from the default Python toolchain.
    python_interpreter_target = interpreter,

    # (Optional) You can set quiet to False if you want to see pip output.
    #quiet = False,
    requirements_lock = "//:requirements.in",
)

load("@pypi//:requirements.bzl", "install_deps")

# Initialize repositories for all packages in requirements_lock.txt.
install_deps()

# Protobuf And GRPC
http_archive(
    # match server/bazel_rje_deps.bzl
    name = "com_google_protobuf",
    sha256 = "ca983c9d2c8f8c935513642bcc4b2cbc64e4046e0bb16bf2ff893128577ece8c",
    strip_prefix = "protobuf-21.2",
    urls = [
        "https://github.com/protocolbuffers/protobuf/archive/refs/tags/v21.2.tar.gz",
    ],
)

http_archive(
    name = "rules_proto",
    sha256 = "e017528fd1c91c5a33f15493e3a398181a9e821a804eb7ff5acdd1d2d6c2b18d",
    strip_prefix = "rules_proto-4.0.0-3.20.0",
    urls = [
        "https://github.com/bazelbuild/rules_proto/archive/refs/tags/4.0.0-3.20.0.tar.gz",
    ],
)

load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")

rules_proto_dependencies()

rules_proto_toolchains()

http_archive(
    name = "rules_proto_grpc",
    sha256 = "507e38c8d95c7efa4f3b1c0595a8e8f139c885cb41a76cab7e20e4e67ae87731",
    strip_prefix = "rules_proto_grpc-4.1.1",
    urls = ["https://github.com/rules-proto-grpc/rules_proto_grpc/archive/4.1.1.tar.gz"],
)

load("@rules_proto_grpc//:repositories.bzl", "rules_proto_grpc_repos", "rules_proto_grpc_toolchains")

rules_proto_grpc_repos()

rules_proto_grpc_toolchains()

http_archive(
    name = "com_github_grpc_grpc",
    sha256 = "51403542b19e9ed5d3b6551ce4a828e17883a1593d4ca408b098f04b0767d202",
    strip_prefix = "grpc-1.36.2",
    urls = ["https://github.com/grpc/grpc/archive/v1.36.2.tar.gz"],
)

load("@com_github_grpc_grpc//bazel:grpc_deps.bzl", "grpc_deps")

grpc_deps()

load("@com_github_grpc_grpc//bazel:grpc_extra_deps.bzl", "grpc_extra_deps")

grpc_extra_deps()
