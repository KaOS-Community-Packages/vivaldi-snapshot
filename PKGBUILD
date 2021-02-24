pkgname=vivaldi-snapshot
pkgver=3.7.2209.3
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
sha1sums=('72fa394037f16d3815f8129a4dffdb0809c1554e')

package() {
	msg "Extracting Vivaldi"
	bsdtar -xf data.tar.xz -C "${pkgdir}/" 
	msg2 "Done extracting!"
	msg "Actual installation"
	local i
	for i in 16 22 24 32 48 64 128 256; do
	install -Dm644 "$pkgdir"/opt/vivaldi-${_branch}/product_logo_${i}.png "$pkgdir"/usr/share/icons/hicolor/${i}x${i}/apps/vivaldi-${_branch}.png
	done
	msg "Removing duplicated images"
	#rm "$pkgdir"/opt/vivaldi-${_branch}/lib/libffmpeg.so
	rm "$pkgdir"/opt/vivaldi-${_branch}/product_logo_*.png
	msg "installing proprietary codecs"
	#ln -s /usr/lib/chromium/libs/libffmpeg.so "$pkgdir"/opt/vivaldi-${_branch}/lib/libffmpeg.so
	#ln -sf /opt/google/chrome-unstable/WidevineCdm/_platform_specific/linux_x64/libwidevinecdm.so "$pkgdir"/opt/vivaldi-${_branch}/libwidevinecdm.so
	ln -sf /usr/lib/chromium/libs/libffmpeg.so "${pkgdir}/opt/vivaldi-${_branch}/libffmpeg.so.${pkgver%\.*\.*}"
	ln -sf /opt/google/chrome-unstable/WidevineCdm "${pkgdir}/opt/vivaldi-${_branch}/WidevineCdm"
	#Correct rights
	chmod 4755 "${pkgdir}/opt/vivaldi-${_branch}/vivaldi-sandbox"
	msg "Installation finished!"
}
