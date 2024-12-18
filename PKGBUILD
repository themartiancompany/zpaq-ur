# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Carol Schulze <aur@ereski.org>
# Contributor: TuxSpirit<tuxpsiritATarchlinuxDOTfr>
# Contributor: Jan Stępień <jstepien@users.sourceforge.net>

_pkg=zpaq
pkgname="${_pkg}"
_pkgdesc=(
  "Programmable file compressor,"
  "library and utilities."
  "Based on the PAQ compression algorithm"
)
pkgdesc="${_pkgdesc[*]}"
_http="http://mattmahoney.net"
url="${_http}/dc/${_pkg}.html"
pkgver=7.15
pkgrel=2
_zpaq_ver=715
arch=(
  'i686'
  'x86_64'
  'pentium4'
  'arm'
  'aarch64'
  'armv7l'
  'armv6l'
  'mips'
  'powerpc'
)
license=(
  "custom"
  "MIT"
)
provides=(
  "lib${_pkg}=${pkgver}"
)
conflicts=(
  "lib${_pkg}"
)
makedepends=(
  "perl"
)
source=(
  "${_http}/dc/${_pkg}${_zpaq_ver}.zip"
)
sha512sums=(
  '4cddcc04dff5e9dceb7138cf9e82b718b696048368ff494339f877d93e4423ed7959c0cfb2e30ba7dcbcdd6bbd59fa1021ceaca6d51e3180d8034b7a3997c265'
)

build()
{
  cd \
    "${srcdir}"
  if [ -z "${CXX}" ]; then
    CXX="g++"
  fi
  msg \
    'Building libzpaq'
  msg \
    "CXX flags:"
  msg \
    "${CXXFLAGS}"
  "${CXX}" \
    $CXXFLAGS \
    $LDFLAGS \
    -fPIC \
    -shared \
    -Dunix \
    -DNDEBUG \
    "lib${_pkg}.cpp" \
    -o \
      "lib${_pkg}.so"
  msg \
    'Building zpaq'
  "${CXX}" \
    ${CXXFLAGS} \
    ${LDFLAGS} \
    -pthread \
    -Dunix \
    -DNDEBUG \
    "zpaq.cpp" \
    -L. \
    -l"${_pkg}" \
    -o \
      "${_pkg}"
  msg \
    'Building man page'
  pod2man \
    "${_pkg}.pod" \
    "${_pkg}.1"
  gzip \
    -9 \
    "${_pkg}.1"
}


package()
{
  install \
    -Dm644 \
    "lib${_pkg}.h" \
    "${pkgdir}/usr/include/lib${_pkg}.h"
  install \
    -Dm644 \
    "lib${_pkg}.so" \
    "${pkgdir}/usr/lib/lib${_pkg}.so"
  install \
    -Dm755 \
    "${_pkg}" \
    "${pkgdir}/usr/bin/${_pkg}"
  install \
    -Dm644 \
    "${_pkg}.1.gz" \
    "${pkgdir}/usr/share/man/man1/${_pkg}.1.gz"
  install \
    -Dm644 \
    "COPYING" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
