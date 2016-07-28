pkgname=vivaldi-snapshot
pkgver=1.3.551.13
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
backup=("opt/vivaldi-${_branch}/resources/vivaldi/style/custom.css")
source=("https://downloads.vivaldi.com/${_branch}/${pkgname}_${pkgver}-1_amd64.deb")
md5sums=('b2e294e30503b42ada2babb35f76421f')

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
	msg "Add a hack to modify UI"
	sed -i 's|^|@import "custom.css";|' "$pkgdir"/opt/vivaldi-${_branch}/resources/vivaldi/style/common.css
	touch "$pkgdir"/opt/vivaldi-${_branch}/resources/vivaldi/style/custom.css
	chmod 666 "$pkgdir"/opt/vivaldi-${_branch}/resources/vivaldi/style/custom.css
	msg "Installation finished!"
}
