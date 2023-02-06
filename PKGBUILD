# Maintainer: Nikos Toutountzoglou <nikos.toutou@gmail.com>
pkgname=balena-etcher-appimage
pkgver=1.15.5
pkgrel=1
pkgdesc="Flash OS images to SD cards & USB drives, safely and easily"
arch=('x86_64')
url="https://www.balena.io/etcher"
license=("Apache")
depends=('fuse2')
provides=("balena-etcher-appimage=${pkgver}")
conflicts=('balena-etcher-appimage' 'balena-etcher')
source=("https://github.com/balena-io/etcher/releases/download/tags%2Fv${pkgver}/balenaEtcher-${pkgver}-x64.AppImage"
	'balena-etcher.sh'
	)
sha256sums=('88032d475d22eb72a790d8e9105f3c199721da23e408825494283d91c26cc217'
            'ff83e497ce3e030d6181ed07e4c25bed90a9c5a959e66b2613ba7ec1f7537cd8')
options=(!strip) # necessary otherwise the AppImage file in the package is truncated
_image="$(basename "${source[0]}")"

prepare() {
  cd "${srcdir}"
  chmod +x "${_image}"
  ./"${_image}" --appimage-extract
  sed -i 's/Exec=.*/Exec=\/usr\/bin\/balena-etcher %U/' "${srcdir}/squashfs-root/balena-etcher.desktop"
}

package() {
  install -Dm755 "${srcdir}/${_image}" "${pkgdir}/opt/balena-etcher/balena-etcher.AppImage"
  install -Dm755 "${srcdir}/balena-etcher.sh" "${pkgdir}/usr/bin/balena-etcher"
  install -dm755 "${pkgdir}/usr/share/"
  cp -r --no-preserve=mode,ownership "${srcdir}/squashfs-root/usr/share/icons" "${pkgdir}/usr/share/"
  install -Dm644 "${srcdir}/squashfs-root/balena-etcher.desktop" "${pkgdir}/usr/share/applications/balena-etcher.desktop"
}
