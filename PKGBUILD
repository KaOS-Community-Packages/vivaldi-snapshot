pkgname=vivaldi-snapshot
pkgver=2.0.1309.25
pkgrel=1
_branch="snapshot"
pkgdesc='The web browser from Vivaldi / Vivaldi browser is made for power users in mind by people who love the Web. (snapshot version)'
arch=('x86_64')
url="https://vivaldi.com"
license=('custom: Vivaldi')
options=('!strip' '!emptydirs')
depends=('gcc-libs' 'gtk3' 'nss' 'libjpeg-turbo' 'freetype2' 'cairo' 'libxslt'
         'libpng' 'alsa-lib' 'libxss' 'hicolor-icon-theme' 'xdg-utils' 'chromium-ffmpeg-codecs' 'widevine')
optdepends=('pepper-flash: Pepper Flash plugin')
source=("https://downloads.vivaldi.com/${_branch}/${pkgname}_${pkgver}-1_amd64.deb")
sha1sums=('b92dcec1080679a3d2ecee43ac5cca4772005756')

package() {
	msg "Extracting Vivaldi"
	bsdtar -xf data.tar.xz -C "${pkgdir}/" 
	msg2 "Done extracting!"
	msg "Actual installation"
	local i
	for i in 16 22 24 32 48 64 128 256; do
	install -Dm644 "$pkgdir"/opt/vivaldi-${_branch}/product_logo_${i}.png "$pkgdir"/usr/share/icons/hicolor/${i}x${i}/apps/vivaldi-${_branch}.png
	done
	msg "Removing unsupported ffmpeg and duplicated images"
	rm "$pkgdir"/opt/vivaldi-${_branch}/lib/libffmpeg.so
	rm "$pkgdir"/opt/vivaldi-${_branch}/product_logo_*.png
	msg "installing ffmpeg official support (H.264)"
	ln -s /usr/lib/chromium/libs/libffmpeg.so "$pkgdir"/opt/vivaldi-${_branch}/lib/libffmpeg.so
	ln -sf /opt/google/chrome-unstable/libwidevinecdm.so "$pkgdir"/opt/vivaldi-${_branch}/libwidevinecdm.so
	#Correct rights
	chmod 4755 "${pkgdir}/opt/vivaldi-${_branch}/vivaldi-sandbox"
	msg "Installation finished!"
}
