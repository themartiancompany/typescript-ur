# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer:  Pellegrino Prevete <cGVsbGVncmlub3ByZXZldGVAZ21haWwuY29tCg== | base -d>
# Maintainer:  Truocolo <truocolo@aol.com>
# Maintainer:  Felix Yan <felixonmars@archlinux.org>
# Maintainer:  Daniel M. Capella <polyzen@archlinux.org>
# Contributor: Bruno Galeotti <bgaleotti at gmail dot com>

_git=false
_name=TypeScript
pkgname=typescript
pkgver=5.3.3
pkgrel=1
pkgdesc='JavaScript with syntax for types'
arch=('any')
url=http://www.typescriptlang.org
license=(
  'Apache'
)
depends=(
  'nodejs'
)
makedepends=(
  'npm'
  'rsync'
)
source=()
b2sums=()
_http="https://github.com"
_ns="microsoft"
_url="${_http}/${_ns}/${_name}"
_branch="main"
[[ "${_git}" == true ]] && \
  makedepends+=(
    'git'
  ) && \
  source+=(
    "git+${_url}.git#tag=v${pkgver}"
  ) && \
  b2sums+=(
    'SKIP'
  )
[[ "${_git}" == false ]] && \
  source+=(
    "${url}/archive/refs/heads/${_branch}.zip"
  ) && \
  b2sums+=(
    'ciao'
  )

prepare() {
  cd \
    $_name
  npm \
    ci
}

build() {
  cd \
    $_name
  npx \
    hereby \
      LKG
}

check() {
  cd \
    $_name
  npm \
    run \
      test
}

package() {
  local \
    mod_dir=/usr/lib/node_modules/$pkgname
  install \
    -d \
    "$pkgdir"/{usr/bin,$mod_dir}
  ln \
    -s \
    $mod_dir/bin/{tsc,tsserver} \
    "$pkgdir"/usr/bin
  cd \
    $_name
  rsync \
    -r \
    --exclude=.gitattributes \
    README.md \
    SECURITY.md \
    bin \
    lib \
    package.json \
    "$pkgdir"/$mod_dir
  install \
    -Dt \
    "$pkgdir"/usr/share/licenses/$pkgname \
    ThirdPartyNoticeText.txt
}

# vim:set sw=2 sts=-1 et:
