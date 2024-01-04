# Maintainer: Brett Cornwall <ainola@archlinux.org>
# Contributor Maxim Baz <archlinux at maximbaz dot com>
# Contributor: Omar Pakker

pkgname=wlroots
pkgver=0.17.1
pkgrel=1
license=('MIT')
pkgdesc='Modular Wayland compositor library'
url='https://gitlab.freedesktop.org/wlroots/wlroots'
arch=('x86_64')
depends=(
    'libdisplay-info.so'
    'libglvnd'
    'libinput'
    'libpixman-1.so'
    'libseat.so'
    'libudev.so'
    'libvulkan.so'
    'libwayland-client.so'
    'libwayland-server.so'
    'libxcb'
    'libxkbcommon.so'
    'opengl-driver'
    'xcb-util-errors'
    'xcb-util-renderutil'
    'xcb-util-wm'
)
makedepends=(
    'glslang'
    'meson'
    'ninja'
    'systemd'
    'vulkan-headers'
    'wayland-protocols'
    'xorg-xwayland'
)
optdepends=(
    'xorg-xwayland: Xwayland support'
)
provides=(
    'libwlroots.so'
)
options=(
    'debug'
)
source=(
    "$pkgname-$pkgver.tar.gz::https://gitlab.freedesktop.org/wlroots/wlroots/-/releases/$pkgver/downloads/wlroots-$pkgver.tar.gz"
    "https://gitlab.freedesktop.org/wlroots/wlroots/-/releases/$pkgver/downloads/wlroots-$pkgver.tar.gz.sig"
    "Revert-layer-shell-error-on-0-dimension-without-anch.patch"
)
sha256sums=('d58d68e3f90d92de4d49fa43b4d75dc78f8af1d920d090729331cefbdfcf361b'
            'SKIP'
            '1c05f0500a96a3721317d01619aa42d8ad696905a378249e8405968c4e16a065')
validpgpkeys=(
    '34FF9526CFEF0E97A340E2E40FDE7BE0E88F5E48' # Simon Ser
    '9DDA3B9FA5D58DD5392C78E652CB6609B22DA89A' # Drew DeVault
    '4100929B33EEB0FD1DB852797BC79407090047CA' # Sway signing key
)

prepare() {
    cd "${pkgname}-${pkgver}"
    # Allow a minor protocol violation until phosh is fixed without this patch
    # phosh crashes on launch.
    patch -Np1 -i "${srcdir}/Revert-layer-shell-error-on-0-dimension-without-anch.patch"
}

build() {
    arch-meson "$pkgname-$pkgver" build
    ninja -C build
}

package() {
    DESTDIR="$pkgdir" ninja -C build install
    install -Dm644 "$pkgname-$pkgver/LICENSE" -t "$pkgdir/usr/share/licenses/$pkgname/"
}
