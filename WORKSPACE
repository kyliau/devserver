# WARNING: This file is generated and it's not meant to be edited.
# Before making any changes, please read Bazel documentation.
# https://docs.bazel.build/versions/master/be/workspace.html
# The WORKSPACE file tells Bazel that this directory is a "workspace", which is like a project root.
# The content of this file specifies all the external dependencies Bazel needs to perform a build.

####################################
# ESModule imports (and TypeScript imports) can be absolute starting with the workspace name.
# The name of the workspace should match the npm package where we publish, so that these
# imports also make sense when referencing the published package.
workspace(name = "demo")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

RULES_NODEJS_VERSION = "0.16.8"
http_archive(
    name = "build_bazel_rules_nodejs",
    url = "https://github.com/bazelbuild/rules_nodejs/archive/%s.zip" % RULES_NODEJS_VERSION,
    strip_prefix = "rules_nodejs-%s" % RULES_NODEJS_VERSION,
)

# The @angular repo contains rule for building Angular applications
ANGULAR_VERSION = "8.0.0-beta.3"
http_archive(
    name = "angular",
    url = "https://github.com/angular/angular/archive/%s.zip" % ANGULAR_VERSION,
    strip_prefix = "angular-%s" % ANGULAR_VERSION,
)

# RxJS
RXJS_VERSION = "6.3.3"
http_archive(
    name = "rxjs",
    url = "https://registry.yarnpkg.com/rxjs/-/rxjs-%s.tgz" % RXJS_VERSION,
    strip_prefix = "package/src",
)

####################################
# Load and install our dependencies downloaded above.

load("@build_bazel_rules_nodejs//:defs.bzl", "check_bazel_version", "node_repositories", "yarn_install")
# 0.18.0 is needed for .bazelignore
check_bazel_version("0.18.0")
node_repositories()
yarn_install(
    name = "npm",
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
)

load("@npm//:install_bazel_dependencies.bzl", "install_bazel_dependencies")
install_bazel_dependencies()

load("@build_bazel_rules_karma//:package.bzl", "rules_karma_dependencies")
rules_karma_dependencies()

load("@io_bazel_rules_webtesting//web:repositories.bzl", "browser_repositories", "web_test_repositories")
web_test_repositories()
browser_repositories(
    chromium = True,
    firefox = True,
)

load("@build_bazel_rules_typescript//:defs.bzl", "ts_setup_workspace")
ts_setup_workspace()

load("@angular//:index.bzl", "ng_setup_workspace")
ng_setup_workspace()
