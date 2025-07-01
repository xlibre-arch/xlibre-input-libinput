# Maintainer:  Vitalii Kuzhdin <vitaliikuzhdin@gmail.com>

_basename="xf86-input-libinput"
pkgname="${_basename//xf86/xlibre}"
pkgver=1.5.0.1
pkgrel=5
pkgdesc="Generic input driver for the XLibre server based on libinput"
arch=('aarch64' 'x86_64')
url="https://github.com/X11Libre/${_basename}"
license=('MIT')
depends=('glibc' 'libinput>=1.11')
makedepends=('libx11' 'libxi' 'meson>=0.50' 'xlibre-server-devel' 'xorgproto' 'X-ABI-XINPUT_VERSION=26.0')
provides=('xf86-input-libinput-xlibre') # "${_basename}"
conflicts=("${_basename}" 'xf86-input-libinput-xlibre' 'xorg-server<1.19.0' 'X-ABI-XINPUT_VERSION<26' 'X-ABI-XINPUT_VERSION>=27')
replaces=('xf86-input-libinput-xlibre')
groups=('xlibre-drivers')
_pkgsrc="${_basename}-xlibre-${_basename}-${pkgver}"
source=("${_pkgsrc}.tar.gz::${url}/archive/refs/tags/xlibre-${_basename}-${pkgver}.tar.gz")
b2sums=('af5543cc59a94f1ecdce92b1cf205896855c36ddbac7efb9669e1ec6641e2e4b4ced3a417ea308c6c49f4a73a377dd8b647c303e6314e7808a56b7589bc2c209')

build() {
  local meson_options=(
    "${_pkgsrc}"
    "${_pkgsrc}/build"
  )
  cd "${srcdir}"
  arch-meson "${meson_options[@]}"
  meson compile -C "${_pkgsrc}/build"
}

package() {
  cd "${srcdir}"
  meson install -C "${_pkgsrc}/build" --destdir "${pkgdir}"

  cd "${_pkgsrc}"
  install -vDm644 "README.md" "${pkgdir}/usr/share/doc/${pkgname}/README.md"
  install -vDm644 "COPYING"   "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
}
