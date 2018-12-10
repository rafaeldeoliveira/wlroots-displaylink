# Maintainer: Ainola

pkgname=wlroots
pkgver=0.2
pkgrel=3
license=('MIT')
pkgdesc='Modular Wayland compositor library'
url='https://github.com/swaywm/wlroots'
arch=('x86_64')
depends=(
    'libinput'
    'libxkbcommon'
    'opengl-driver'
    'pixman'
    'xcb-util-errors'
    'xcb-util-image'
    'xcb-util-wm'
)
makedepends=('meson' 'ninja' 'wayland-protocols')
source=("$pkgname-$pkgver.tar.gz::https://github.com/swaywm/wlroots/archive/$pkgver.tar.gz")
sha256sums=('0b690c5db5a1f11051a28f0349655322fe54d92f7c2dc8d3c6e5559b1098bfd8')

build() {
    arch-meson "$pkgname-$pkgver" build \
        -Dlibcap=enabled \
        -Dlogind=enabled \
        -Dlogind-provider=systemd \
        -Dxcb-errors=enabled \
        -Dxcb-icccm=enabled \
        -Dxcb-xkb=enabled \
        -Dxwayland=enabled \
        -Dx11-backend=enabled
    ninja -C build
}

package() {
    DESTDIR="$pkgdir" ninja -C build install
    install -Dm644 "$pkgname-$pkgver/LICENSE" -t "$pkgdir/usr/share/licenses/$pkgname/"
}
