#t SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
#   Samuel-Zacharie Faure
#     <samuel.faure.dev@gmail.com>
# Contributors:
#   Mahdi Sarikhani
#     <mahdisarikhani@outlook.com>
#   ebiadsu
#     <ebiadsu@posteo.de>

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
if [[ ! -v "_git" ]]; then
  _git="false"
fi
if [[ ! -v "_git_service" ]]; then
  _git_service="github"
fi
if [[ ! -v "_tag_name" ]]; then
  _tag_name="commit"
  _tag_name="pkgver"
fi
if [[ ! -v "_docs" ]]; then
  _docs="true"
fi
_pkg=ovh
if [[ ! -v "_ns" ]]; then
  _ns="themartiancompany"
  # _ns="${_pkg}"
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    _archive_format="tar.gz"
    if [[ "${_tag_name}" == "commit" ]]; then
      if [[ "${_git_service}" == "github" ]]; then
        _archive_format="zip"
      fi
    fi
  fi
fi
_py="python"
_pyver="$(
  "${_py}" \
    -V |
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$((
  ${_pyminver} + 1))"
pkgbase="${_py}-${_pkg}"
pkgname=(
  "${pkgbase}"
)
if [[ "${_docs}" == "true" ]]; then
  pkgname+=(
    "${pkgbase}-docs"
  )
fi
pkgver=1.1.2
_commit="7532f33038f01777bf74a2ec57d6aa0666039542"
pkgrel=7
pkgdesc="Lightweight wrapper around OVH's APIs"
arch=(
  'any'
)
_http="https://${_git_service}.com"
url="${_http}/${_ns}/${pkgbase}"
license=(
  'BSD'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}-requests"
)
makedepends=(
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
  "${_py}-wheel"
)
if [[ "${_docs}" == "true" ]]; then
  makedepends+=(
    "make"
    "${_py}-sphinx"
  )
fi
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs"
  )
fi
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
_url="${url}"
# _tag="${_commit}"
_tag="${pkgver}"
_tag_name="pkgver"
_tarname="${pkgbase}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
_release_sum='b24a47bc37ffb14fee2d9525b4aa0b86eeb2aab24755fd6e74707c4e4d0b807a'
_release_sig_sum="9031637a3fdbd932db3cb1a976086ff890704c08429d26cd64f606459682a754"
_uri="${url}/archive/v${pkgver}.tar.gz"
_gitlab_sum="728ece7c8aea5504dd921850e40821768169a846dd5a825087ed5ade2636d91b"
_gitlab_sig_sum="ab3de9fafca46637417c2aeab9e4aac41643c1ee61ec5ed958e4d23d2c91ac15"
_github_sum="7a55511d466126a07ac33ac26b6fd3c82bef9ff5016d48dbb66d6522e9e0d489"
_github_sig_sum="61bcb3eedd422bd48d6c19ae91b955ab4ade5b92f2a2dd1c7f34c34087ef59a3"
if [[ "${_git_service}" == "gitlab" ]]; then
  if [[ "" == "pkgver" ]]; then
    _sum="${_release_sum}"
    _sig_sum="${_release_sig_sum}"
  fi
  _sum="${_gitlab_sum}"
  _sig_sum="${_gitlab_sig_sum}"
  # Dvorak
  _evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
elif [[ "${_git_service}" == "github" ]]; then
  _sum="${_github_sum}"
  _sig_sum="${_github_sig_sum}"
  # Truocolo
  _evmfs_ns="0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b"
  # Dvorak
  _evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
fi
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_evmfs_uri="${_evmfs_dir}/${_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_sig_uri="${_evmfs_dir}/${_sig_sum}"
_sig_src="${_tarfile}.sig::${_sig_uri}"
source=()
sha256sums=()
if [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_git}" == "false" ]]; then
    _src="${_evmfs_src}"
    source+=(
      "${_sig_src}"
    )
    sha256sums+=(
      "${_sig_sum}"
    )
  fi
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == true ]]; then
    _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
    _sum="SKIP"
  elif [[ "${_git}" == false ]]; then
    _uri=""
    if [[ "${_git_service}" == "github" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/archive/${_commit}.${_archive_format}"
        _sum="${_github_sum}"
      fi
    elif [[ "${_git_service}" == "gitlab" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/-/archive/${_tag}/${_tag}.${_archive_format}"
      fi
    fi
    _src="${_tarfile}::${_uri}"
  fi
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)

build() {
  local \
    _build_opts=()
  _build_opts+=(
    --wheel
    --no-isolation
  )
  cd \
    "${_tarname}"
  "${_py}" \
    -m \
      "build" \
    "${_build_opts[@]}"
  if [[ "${_docs}" == "true" ]]; then
    cd \
      "docs"
    PYTHONPATH="..:${PYTHONPATH}" \
    make \
      man
  fi
}

package_python-ovh() {
  local \
    _installer_opts=() \
    _install_opts=()
  _install_opts+=(
    -Dm644
  )
  _installer_opts+=(
    --destdir="${pkgdir}"
  )
  cd \
    "${_tarname}"
  "${_py}" \
    -m \
      "installer" \
    "${_installer_opts[@]}" \
    "dist/"*".whl"
  install \
    "${_install_opts[@]}" \
    "LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

package_python-ovh-docs() {
  local \
    _install_opts=()
  _install_opts+=(
    -Dm644
  )
  cd \
    "${_tarname}"
  install \
    "${_install_opts[@]}" \
    "docs/_build/man/${pkgbase}.1" \
    "${pkgdir}/usr/share/man/man1/${pkgbase}.1"
  install \
    "${_install_opts[@]}" \
    "LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

