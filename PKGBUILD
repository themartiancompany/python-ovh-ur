# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025  Pellegrino Prevete
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

if [[ ! -v "_docs" ]]; then
  _docs="true"
fi
_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=ovh
pkgbase="${_py}-${_pkg}"
pkgname=(
  "${_py}-${_pkg}"
)
if [[ "${_docs}" == "true" ]]; then
  pkgname+=(
    "${pkgbase}-docs"
  )
fi
pkgver=1.1.2
pkgrel=2
pkgdesc="Lightweight wrapper around OVH's APIs"
arch=(
  'any'
)
_http="https://github.com"
_ns="${_pkg}"
url="${_http}/${_ns}/${pkgbase}"
license=(
  'BSD'
)
depends=(
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
_tarname="${pkgbase}-${pkgver}"
_sum='b24a47bc37ffb14fee2d9525b4aa0b86eeb2aab24755fd6e74707c4e4d0b807a'
_uri="${url}/archive/v${pkgver}.tar.gz"
source=(
  "${_tarname}.tar.gz::${_uri}"
)
sha256sums=(
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

