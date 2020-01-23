# Maintainer: Brett Cornwall <ainola@archlinux.org>
# Contributor: Omar Pakker

pkgname=wlroots
pkgver=0.10.0
pkgrel=2
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
makedepends=(
    'meson'
    'ninja'
    'wayland-protocols'
)
provides=(
    'libwlroots.so'
)
source=(
    "$pkgname-$pkgver.tar.gz::https://github.com/swaywm/wlroots/archive/$pkgver.tar.gz"
    "https://github.com/swaywm/wlroots/releases/download/$pkgver/wlroots-$pkgver.tar.gz.sig"
)
sha256sums=('9414ba761c321f9c2b3e0426e1bbed55443fa8f97d46643d1706d1ddd614f6cd'
            'SKIP')
validpgpkeys=('9DDA3B9FA5D58DD5392C78E652CB6609B22DA89A') # Drew DeVault

build() {
    meson "$pkgname-$pkgver" build \
        --prefix=/usr \
        --buildtype=plain \
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
