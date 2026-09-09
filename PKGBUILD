# SPDX-License-Identifier: AGPL-3.0

#    -----------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    -----------------------------------------------------
#
#    This program is free software: you can redistribute
#    it and/or modify it under the terms of the
#    GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of
#    the License, or (at your option) any later version.
#
#    This program is distributed in the hope that it
#    will be useful, but WITHOUT ANY WARRANTY;
#    without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#    See the GNU Affero General Public License for
#    more details.
#
#    You should have received a copy of the
#    GNU Affero General Public License
#    along with this program.
#    If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Contributors:
#   Felix Yan
#     <felixonmars@archlinux.org>
#   Daniel M. Capella
#     <polyzen@archlinux.org>
#   Bruno Galeotti
#     <bgaleotti at gmail dot com>

_os="$(
  uname \
    -o)"
_evmfs_available="$(
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
if [[ ! -v "_offline" ]]; then
  _offline="false"
fi
if [[ ! -v "_git" ]]; then
  _git="false"
fi
if [[ ! -v "_git_service" ]]; then
  _git_service="github"
fi
if [[ ! -v "_tag_name" ]]; then
  if [[ "${_git}" == "false" ]]; then
    _tag_name="tag"
  fi
  _tag_name="commit"
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      _archive_format="zip"
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _archive_format="tar.gz"
    fi
  fi
fi
_Pkg=TypeScript
_pkg=typescript
_name="${_Pkg}"
_node="nodejs"
pkgbase="${_pkg}"
pkgname=(
  "${_pkg}"
)
pkgver=5.8.3
_commit="68cead182cc24afdc3f1ce7c8ff5853aba14b65a"
pkgrel=1
pkgdesc='JavaScript with syntax for types'
arch=(
  'any'
)
url="http://www.${_pkg}lang.org"
license=(
  'Apache'
)
depends=(
  "${_node}"
)
makedepends=(
  'dprint'
  'npm'
  'rsync'
)
source=()
sha256sums=()
_http="https://${_git_service}.com"
_ns="microsoft"
_url="${_http}/${_ns}/${_name}"
_branch="main"
if [[ ! -v "_tag" ]]; then
  if [[ "${_tag_name}" == "tag" ]]; then
    _tag="v${pkgver}"
  fi
fi
_tarname="${_pkg}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
if [[ "${_git}" == true ]]; then
  makedepends+=(
    'git'
  )
fi
if [[ "${_git}" == true ]]; then
  _uri="git+${_url}.git#${_tag_name}=${_tag}"
  source+=(
    "${_tarname}::${_uri}"
  )
  sha256sums+=(
    'SKIP'
  )
elif [[ "${_git}" == false ]]; then
  if [[ "${_tag_name}" == "commit" ]]; then
    _uri="${_url}/archive/${_commit}.${_archive_format}"
  elif [[ "${_tag_name}" == "branch" ]]; then
    _uri="${_url}/archive/refs/heads/${_branch}.zip"
  fi
  source+=(
    "${_tarfile}::${_uri}"
  )
  sha256sums+=(
    'boh'
  )
fi

prepare() {
  cd \
    "${_name}-${_branch}"
  npm \
    ci
}

build() {
  cd \
    "${_name}-${_branch}"
  npx \
    hereby \
      "LKG"
}

check() {
  cd \
    "${_name}-${_branch}"
  npm \
    run \
      "test"
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
    "${_name}-${_branch}"
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
