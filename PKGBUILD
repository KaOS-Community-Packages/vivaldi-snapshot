pkgname=vivaldi-snapshot
pkgver=5.2.2621.3
pkgrel=1
_branch="snapshot"
pkgdesc='The web browser from Vivaldi / Vivaldi browser is made for power users in mind by people who love the Web. (snapshot version)'
arch=('x86_64')
url="https://vivaldi.com"
license=('custom: Vivaldi')
options=('!strip' '!emptydirs')
depends=('gcc-libs' 'gtk3' 'nss' 'libjpeg-turbo' 'freetype2' 'cairo' 'libxslt'
         'libpng' 'alsa-lib' 'libxss' 'hicolor-icon-theme' 'xdg-utils' 'widevine')
source=("https://downloads.vivaldi.com/${_branch}/${pkgname}-${pkgver}-1.x86_64.rpm")
sha256sums=('3a01ce0565f619ca87ee7877a681bce18d110ab33f7b4cf8209510bb5702cf17')

package() {
	msg "Prepare dirs"
	install -dm755 "${pkgdir}/opt/${pkgname}"
	install -dm755 "${pkgdir}/usr/share"
	install -dm755 "${pkgdir}/usr/bin"

	msg "Copy files"
	cp -r "${srcdir}/opt/${pkgname}/"* "${pkgdir}/opt/${pkgname}"
	install -Dm644 "${srcdir}/usr/share/appdata/${pkgname}.appdata.xml" \
		             "${pkgdir}/usr/share/appdata/${pkgname}.appdata.xml"
	install -Dm644 "${srcdir}/usr/share/applications/${pkgname}.desktop" \
		             "${pkgdir}/usr/share/applications/${pkgname}.desktop"

	msg "Copy icons"
	local i
	for i in 16 22 24 32 48 64 128 256; do
		install -Dm644 "${pkgdir}/opt/${pkgname}/product_logo_${i}.png" \
			             "${pkgdir}/usr/share/icons/hicolor/${i}x${i}/apps/${pkgname}.png"
	done

	msg "Removing duplicated images"
	rm "${pkgdir}/opt/${pkgname}/"product_logo_*.png

	msg "Linkings"
	ln -sf "/opt/${pkgname}/${pkgname}" "${pkgdir}/usr/bin/${pkgname}"
	#rm "${pkgdir}/opt/${pkgname}/lib/libffmpeg.so"
	#ln -sf /usr/lib/chromium/libs/libffmpeg.so "${pkgdir}/opt/${pkgname}/libffmpeg.so.${pkgver%\.*\.*}"
	ln -sf /opt/google/chrome-unstable/WidevineCdm "${pkgdir}/opt/${pkgname}/WidevineCdm"

	msg "Correct rights"
	chmod 4755 "${pkgdir}/opt/${pkgname}/vivaldi-sandbox"
	msg "Installation finished!"
}
sha256sums=('3a01ce0565f619ca87ee7877a681bce18d110ab33f7b4cf8209510bb5702cf17')
sha256sums=('3a01ce0565f619ca87ee7877a681bce18d110ab33f7b4cf8209510bb5702cf17')
