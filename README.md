# `rules_boost` -- Bazel build rules for Boost

To use these rules, add the following to your `WORKSPACE` file:

```bazel
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "com_github_nelhage_rules_boost",
    url = "https://github.com/dfshan/rules_boost/archive/716accc67dc7cd4f7a1988e5ecc8e3e3ccd3cdcf.zip",
    strip_prefix = "rules_boost-716accc67dc7cd4f7a1988e5ecc8e3e3ccd3cdcf",
    sha256 = "0d0f871812224842ce595f9a8f70cd8ac0980ce6cb025f97afe3e8cb7ec70c4e",
)

load("@com_github_nelhage_rules_boost//:boost/boost.bzl", "boost_deps")
boost_deps()
```

You can then use libraries in `deps` through the `@boost` repository, for
example `@boost//:algorithm`.


Based in part on rules from https://github.com/mzhaom/trunk.

## ASIO SSL support

These rules implement support for Boost ASIO's SSL support. To use
ASIO-SSL, you must depend on the `"@boost//:asio_ssl"` target, instead
of `"@boost//:asio"`. ASIO-SSL depends on OpenSSL; By default,
`rules_boost` will download and build a recent
[BoringSSL](https://boringssl.googlesource.com/boringssl/) commit; To
use a different OpenSSL implementation, create a remote named
`openssl` before calling `boost_deps`. This remote must make available
OpenSSL's libssl at `@openssl//:ssl`.
