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
#   David Runge
#     <dvzrv@archlinux.org>
#   Antonio Rojas
#     <arojas@archlinux.org>
#   Allan McRae
#     <allan@archlinux.org>
#   damir
#     <damir@archlinux.org>

_os="$(
  uname \
    -o)"
if [[ "${_os}" == "Android" ]]; then
  _libc="ndk-sysroot"
  _compiler="clang"
  _libcompiler="llvm-libs"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _libc="glibc"
  _compiler="gcc"
  _libcompiler="libgcc"
elif [[ "${_os}" == "Msys" ]]; then
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
else
  _msg=(
    "Unknown os '${_os}'."
  )
  msg \
    "${_msg[*]}"
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
fi
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
if [[ ! -v "_ns" ]]; then
  if [[ "${_evmfs}" == "true" ]]; then
    _ns="themartiancompany"
  elif [[ "${_evmfs}" == "false" ]]; then
    _ns="gnu"
  fi
fi
if [[ ! -v "_git" ]]; then
  if [[ "${_ns}" == "gnu" ]]; then
    _git="false"
  elif [[ "${_ns}" == "themartiancompany" ]]; then
    _git="true"
  fi
fi
if [[ ! -v "_git_service" ]]; then
  if [[ "${_ns}" == "gnu" ]]; then
    _git_service="gnu"
  elif [[ "${_ns}" == "themartiancompany" ]]; then
    _git_service="github"
  fi
fi
if [[ ! -v "_offline" ]]; then
  _offline="false"
fi
if [[ ! -v "_tag_name" ]]; then
  if [[ "${_ns}" == "gnu" ]]; then
    _tag_name="pkgver"
  elif [[ "${_ns}" == "themartiancompany" ]]; then
    _tag_name="commit"
  fi
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_ns}" == "gnu" ]]; then
      _archive_format="tar.xz"
    elif [[ "${_ns}" == "themartiancompany" ]]; then
      if [[ "${_git_service}" == "github" ]]; then
        _archive_format="zip"
      elif [[ "${_git_service}" == "gitlab" ]]; then
        _archive_format="tar.gz"
      fi
    fi
  fi
fi
_pkg=mpfr
pkgname="${_pkg}"
_pkgver=4.2.2
_bundle_commit="839a2709425ce5fa60dd5806f44f5548d7eda99e"
_commit="736ef3903ce50fc592268f69b6895c73da6adfb4" 
_patchver=0
if (( "${_patchver}" == 0 )); then
  pkgver="${_pkgver}"
else
  pkgver="${_pkgver}.p${_patchver}"
fi
pkgrel=1
_pkgdesc=(
  'Multiple-precision floating-point library'
)
pkgdesc="${_pkgdesc[*]}"
arch=(x86_64)
url="https://www.${_pkg}.org"
license=(
  "GPL-3.0-or-later"
  "LGPL-3.0-or-later"
)
depends=(
  "glibc"
  "gmp"
)
provides=(
  "lib${_pkg}=${pkgver}"
  "lib${_pkg}.so"
)
if [[ "${_os}" == "Msys" ]]; then
  makedepends+=(
    "${_libc_headers}"
    "windows-default-manifest"
  )
fi
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs"
  )
fi
# NOTE: download potentially existing patches from upstream:
# `curl patches.diff -o https://www.mpfr.org/mpfr-${_pkgver}/allpatches`
# Tallero
_evmfs_ns="0x6ec7cC56dCeC0a00CB15E97C64B1a5Ec7A31403c"
_bundle_sum="aa923bdf90f3e4a569f66943ea483b98f075a7bc44de6405a7511bfb0ee7f427"
_bundle_sig_sum="bf4e7a1574147cea78d7c0e82a17eb974c48cb2aa82773f24ed190f1632cbd4d"
_4_2_2_bundle_sum="66d10959e5ec4e13773248a10a5657d0606fff018877ec9057d47a1be2fd1ca3"
_4_2_2_bundle_sig_sum="d9d9c6046c9076f2af622216f43fdc298af28ad7e5e8db4de931509a47b8166c"
_gnu_sum="SKIP"
if [[ ! -v "_tag" ]]; then
  if [[ "${_git}" == "false" ]]; then
    if [[ "${_ns}" == "gnu" ]]; then
      if [[ "${_tag_name}" == "pkgver" ]]; then
        _tag="${pkgver/_/-}"
      fi
    fi
  elif [[ "${_git}" == "true" ]]; then
    _tag="${_commit}"
  fi
fi
_tarname="${_pkg}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
_4_2_2_bundle_name="${_pkg}-${_bundle_commit}..${_commit}"
_4_2_2_bundle_file="${_4_2_2_bundle_name}.${_archive_format}"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_evmfs_uri="${_evmfs_dir}/${_bundle_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_4_2_2_bundle_uri="${_evmfs_dir}/${_4_2_2_bundle_sum}"
_4_2_2_bundle_src="${_bundle_tag_file}::${_4_2_2_bundle_uri}"
_sig_uri="${_evmfs_dir}/${_bundle_sig_sum}"
_sig_src="${_tarfile}.sig::${_sig_uri}"
_4_2_2_bundle_sig_uri="${_evmfs_dir}/${_4_2_2_bundle_sum}"
_4_2_2_bundle_sig_src="${_4_2_2_bundle_file}.sig::${_4_2_2_bundle_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _src="${_evmfs_src}"
    _sum="${_bundle_sum}"
    _sig_sum="${_bundle_sig_sum}"
    source+=(
      "${_sig_src}"
      "${_4_2_2_bundle_src}"
      "${_4_2_2_bundle_sig_src}"
    )
    sha256sums+=(
      "${_bundle_sig_sum}"
      "${_4_2_2_bundle_sum}"
      "${_4_2_2_bundle_sig_sum}"
    )
  fi
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == true ]]; then
    _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
    _sum="SKIP"
  elif [[ "${_git}" == false ]]; then
    _uri=""
    if [[ "${_ns}" == "gnu" ]]; then
      _http="https://ftp.gnu.org"
      _url="${_http}/${_ns}/${_pkg}"
      _uri="${_url}/${_tarname}.tar.xz"
      _sum="${_gnu_sum}"
      _sig_src="${_tarfile}.sig::${_uri}.sig"
      _sig_sum="SKIP"
      source+=(
        "${_sig_src}"
      )
      sha256sums+=(
        "${_sig_sum}"
      )
    elif [[ "${_ns}" == "themartiancompany" ]]; then
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
    fi
    _src="${_tarfile}::${_uri}"
  fi
fi
if [[ "${_ns}" == "gnu" ]]; then
  source=(
    "https://ftp.gnu.org/gnu/${_pkg}/${_pkg}-${_pkgver}.tar.xz"{"",".sig"}
)
  sha512sums=(
    'eb9e7f51b5385fb349cc4fba3a45ffdf0dd53be6dfc74932dc01258158a10514667960c530c47dd9dfc5aa18be2bd94859d80499844c5713710581e6ac6259a9'
    'SKIP'
  )
  b2sums=(
    '6bbf5658e70fbb673a3b65246a6bac708d1571aa6943c6742efd92f468ac71e6f0fe351b757f7133440ea312d9a5fc3549acd89d54f4d975c58bdc204d7b21ec'
    'SKIP'
  )
  validpgpkeys=(
    # Vincent Lefevre <vincent@vinc17.net>
    '07F3DBBECC1A39605078094D980C197698C3739D'
    'A534BE3F83E241D918280AEB5831D11A0D4DB02A'
  )
fi
source=(
  "${_src}"
  "${_sig_src}"
)
sha256sums=(
  "${_sum}"
  "${_sig_sum}"
)

_git_unbundle() {
  local \
    _tarname="${1}" \
    _bundle \
    _repo \
    _msg=()
  _bundle="${srcdir}/${_tarname}.bundle"
  _repo="${srcdir}/${_tarname}"
  _msg=(
    "Cloning '${_bundle}' into '${_repo}'."
  )
  msg \
    "${_msg[*]}"
  git \
    clone \
      "${_bundle}" \
      "${_repo}" || \
  git \
    -C \
      "${_repo}" \
      pull || \
  true
}

_git_unbundle_update() {
  local \
    _repo="${1}" \
    _bundle="${2}" \
    _repo \
    _msg=()
  _bundle_name="$(
    basename \
      "${_bundle}")"
  _msg=(
    "Updating '${_repo}' from '${_bundle}'."
  )
  msg \
    "${_msg[*]}"
  git \
    -C \
      "${_repo}" \
      remote \
        add \
          "${_bundle_name}" \
          "${_bundle}" ||
  true
  git \
    -C \
      "${_repo}" \
    pull \
      "${_bundle_name}" || \
  true
}

prepare() {
  local \
    _src
  if [[ "${_evmfs}" == "true" ]]; then
    if [[ "${_git}" == "false" ]]; then
      ur \
        "${_like}"
    elif [[ "${_git}" == "true" ]]; then
      _git_unbundle \
        "${_tarname}"
      _git_unbundle_update \
        "${srcdir}/${_tarname}" \
        "${srcdir}/${_4_2_2_bundle_file}"
    fi
  fi
  cd \
    "${_tarname}"
  for _src in "${source[@]}"; do
    [[ "${_src}" == *.diff ]] || \
    [[ "${_src}" == *.patch ]] || \
      continue
    printf \
      "Applying patch %s...\n" "$src"
    patch \
      -Np1 \
      -i \
      "../${_src}"
  done
  autoreconf \
    -fiv
}

build() {
  local \
    _configure_opts=()
  _configure_opts+=(
    --prefix="/usr"
    --enable-thread-safe
    --enable-shared
  )
  cd \
    "${pkgname}-${_pkgver}"
  ./configure \
    "${_configure_opts[@]}"
  make
}

check() {
  cd \
    "${pkgname}-${_pkgver}"
  make \
    check
  make \
    check-exported-symbols
}

package() {
  local \
    _make_opts=()
  _make_opts+=(
    DESTDIR="${pkgdir}"
  )
  cd \
    "${pkgname}-${_pkgver}"
  make \
    "${_make_opts[@]}" \
    install
}
