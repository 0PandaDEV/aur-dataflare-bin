# Maintainer: PandaDEV <contact@pandadev.net>
pkgname=dataflare-bin
pkgver=3.1.8
pkgrel=1
pkgdesc="Easily manage your Table, view Data, write SQL and run Query."
arch=(x86_64 aarch64)
url="https://dataflare.app/"
license=('private')
options=('!strip')
depends=()
provides=(dataflare)
conflicts=(dataflare)
source_x86_64=("Dataflare-x86_64.AppImage::https://assets.dataflare.app/release/linux/x86_64/Dataflare-3.1.8.AppImage")
source_aarch64=("Dataflare-aarch64.AppImage::https://assets.dataflare.app/release/linux/aarch64/Dataflare-3.1.8.AppImage")
sha256sums_x86_64=('4a9823afa889969a855ff2aa54f305b592e66c5a0084781add792c6b530e04fa')
sha256sums_aarch64=('e036e5bee5e3def11d449f8442e28aa4d2b4c7bbfe12ccb8292803fd6c18eaca')

package() {
	install -Dm755 *.AppImage "$pkgdir/opt/dataflare/dataflare.appimage"

	install -dm755 "$pkgdir/usr/bin"
	cat > "$pkgdir/usr/bin/dataflare" << 'EOF'
#!/bin/bash
export APPIMAGE_EXTRACT_AND_RUN=1
exec /opt/dataflare/dataflare.appimage "$@"
EOF
	chmod +x "$pkgdir/usr/bin/dataflare"

	chmod +x *.AppImage
	./*.AppImage --appimage-extract >/dev/null 2>&1

	if [ -f squashfs-root/*.desktop ]; then
		install -dm755 "$pkgdir/usr/share/applications"
		desktop_file=$(find squashfs-root -name "*.desktop" -type f | head -1)
		sed 's|Exec=.*|Exec=dataflare %U|g' "$desktop_file" > "$pkgdir/usr/share/applications/dataflare.desktop"
	fi

	png_file=$(find squashfs-root -name "*.png" -type f | head -1)
	if [ -n "$png_file" ]; then
		install -Dm644 "$png_file" "$pkgdir/usr/share/pixmaps/dataflare.png"
	fi

	rm -rf squashfs-root
}
