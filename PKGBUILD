pkgname=vivaldi-snapshot
pkgver=1.0.435.29
pkgrel=1
_branch="snapshot"
pkgdesc='The web browser from Vivaldi / Vivaldi browser is made for power users in mind by people who love the Web. (snapshot version)'
arch=('x86_64')
url="https://vivaldi.com"
license=('custom: Vivaldi')
options=('!strip' '!emptydirs')
depends=('gcc-libs' 'gtk2' 'nss' 'gconf' 'libjpeg-turbo' 'freetype2' 'cairo' 'libxslt'
         'libpng' 'alsa-lib' 'libxss' 'hicolor-icon-theme' 'xdg-utils' 'vivaldi-ffmpeg')
optdepends=('pepper-flash: Pepper Flash plugin')
install=${pkgname}.install
source=("https://vivaldi.com/download/${_branch}/${pkgname}_${pkgver}-1_amd64.deb")
md5sums=('3927f4d0cf8988f6e8d584055362d55e')

package() {
	msg "Extracting Vivaldi"
	bsdtar -xf data.tar.xz -C "${pkgdir}/" 
	msg2 "Done extracting!"
	msg "Actual installation"
	ln -s /usr/lib/libudev.so.1 "${pkgdir}/opt/vivaldi-${_branch}/libudev.so.0"
	for i in 16 22 24 32 48 64 128 256; do
	install -Dm644 "$pkgdir"/opt/vivaldi-${_branch}/product_logo_${i}.png "$pkgdir"/usr/share/icons/hicolor/${i}x${i}/apps/vivaldi-${_branch}.png
	done
	msg "Removing unsupported ffmpeg and duplicated images"
	rm "$pkgdir"/opt/vivaldi-${_branch}/lib/libffmpeg.so
	rm "$pkgdir"/opt/vivaldi-${_branch}/product_logo_*.png
	msg "installing ffmpeg official support (H.264)"
	ln -s /opt/vivaldi/lib/libffmpeg.so "$pkgdir"/opt/vivaldi-${_branch}/lib/libffmpeg.so
	#Correct rights
	chmod 4755 "${pkgdir}/opt/vivaldi-${_branch}/vivaldi-sandbox"
	msg "Installation finished!"
}
