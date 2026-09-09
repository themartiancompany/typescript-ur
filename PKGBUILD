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
pkgrel=4
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
if [[ "${_git}" == true ]]; then
  makedepends+=(
    'git'
  )
fi
if [[ "${_evmfs}" == true ]]; then
  makedepends+=(
    'evmfs'
  )
fi
provides=(
  "${_node}-${_pkg}=${pkgver}"
)
source=()
sha256sums=()
_github_sum="0c8b8caf2aa399793e51ce27d8d5dd89d961433f181e775deaef3aacf00f2a10"
_github_sig_sum="550793a161c52872dbb0792a601fae900307380c5adfa8f53747a0c9858bd63d"
_http="https://${_git_service}.com"
if [[ ! -v "_ns" ]]; then
  _ns="microsoft"
  _ns="themartiancompany"
fi
_url="${_http}/${_ns}/${_name}"
_branch="main"
if [[ ! -v "_tag" ]]; then
  if [[ "${_tag_name}" == "tag" ]]; then
    _tag="v${pkgver}"
  elif [[ "${_tag_name}" == "commit" ]]; then
    _tag="${_commit}"
  fi
fi
_tarname="${_pkg}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
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
    "${_github_sum}"
  )
fi

prepare() {
  cd \
    "${_tarname}"
  npm \
    ci
}

build() {
  cd \
    "${_tarname}"
  npx \
    hereby \
      "LKG"
}

check() {
  cd \
    "${_tarname}"
  npm \
    run \
      "test"
}

_usr_get() {
  local \
    _bin
  _bin="$(
    dirname \
      "$(command \
           -v \
	   "env")")"
  dirname \
    "${_bin}"
}

package() {
  local \
    _mod_dir \
    _usr
  _usr="$(
    _usr_get)"
  _mod_dir="${_usr}/lib/node_modules/${pkgname}"
  install \
    -d \
    "${pkgdir}/"{"usr/bin","usr/lib/node_modules${pkgname}"}
  ln \
    -s \
    "${_mod_dir}/bin/"{"tsc","tsserver"} \
    "${pkgdir}/usr/bin"
  cd \
    "${_tarname}"
  rsync \
    -r \
    --exclude=".gitattributes" \
    "README.md" \
    "SECURITY.md" \
    "bin" \
    "lib" \
    "package.json" \
    "${pkgdir}/usr/lib/node_modules${pkgname}"
  install \
    -vDt \
    "${pkgdir}/usr/share/licenses/${pkgname}" \
    "ThirdPartyNoticeText.txt"
}

# vim:set sw=2 sts=-1 et:
