# Maintainer: PandaDEV <contact@pandadev.net>
pkgname=dataflare-appimage
pkgver=1.1.0
pkgrel=1
pkgdesc="Easily manage your Table, view Data, write SQL and run Query."
arch=(x86_64 aarch64)
url="https://dataflare.app/"
license=('private')
depends=(krb5 hicolor-icon-theme cairo gdk-pixbuf2 gtk3 glibc libsoup gcc-libs webkit2gtk glib2)
provides=(dataflare)
conflicts=(dataflare)
source_x86_64=("Dataflare-x86_64.AppImage::https://assets.dataflare.app/release/linux/x86_64/Dataflare.AppImage")
source_aarch64=("Dataflare-aarch64.AppImage::https://assets.dataflare.app/release/linux/aarch64/Dataflare.AppImage")
sha256sums_x86_64=('fghj')
sha256sums_aarch64=('dfgh')

prepare() {
	chmod +x ./*.AppImage
	./*.AppImage --appimage-extract
	pushd squashfs-root
	rm -rf usr/share/glib-2.0
	rm -rf usr/lib
	rm usr/bin/xdg-open
}

package() {
	pushd squashfs-root
	cp -av usr/ $pkgdir/

	install -vDm644 *.desktop -t $pkgdir/usr/share/applications/
	install -vDm644 *.png -t $pkgdir/usr/share/pixmaps/
	find $pkgdir -type d -print -empty -delete
}
