# Maintainer: Torsten Sadowski <tsadowski at gmx dot net>

pkgname=passwordmaker-slint-git
pkgver=0.1.r12.aa5ed99
pkgrel=1
epoch=0
pkgdesc='PasswordMaker Slint'
arch=('x86_64')
url='https://passwordmaker.org/'
license=('GPL')
makedepends=('git' 'cargo')
provides=('passwordmaker-slint')
conflicts=('passwordmaker-slint')
source=("passwordmaker-rs::git+https://github.com/tsadowski/passwordmaker-rs.git"
        "${pkgname}::git+https://github.com/tsadowski/passwordmaker-slint.git")
md5sums=('SKIP'
         'SKIP')

pkgver() {
  cd "$pkgname"
  printf "0.1.r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
    cd ${pkgname}
    export RUSTUP_TOOLCHAIN=stable
    cargo fetch --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
    # The flags from makepkg.config can mess with the build
    export CFLAGS=
    export CXXFLAGS=
    export LDFLAGS=
    cd ${pkgname}
    export RUSTUP_TOOLCHAIN=stable
    export CARGO_TARGET_DIR=target
    cargo build --frozen --release --all-features
}

package() {
    cd ${pkgname}
    install -Dm0755 -t "$pkgdir/usr/bin/" "target/release/passwordmaker_slint"
    install -Dm0644 -t "$pkgdir/usr/share/applications" "passwordmaker-slint.desktop"
    install -Dm0644 -t "$pkgdir/usr/share/pixmaps" "img/ring-16x16.png"
    install -Dm0644 -t "$pkgdir/usr/share/pixmaps" "img/ring-24x24.png"
    install -Dm0644 -t "$pkgdir/usr/share/pixmaps" "img/ring-32x32.png"
    install -Dm0644 -t "$pkgdir/usr/share/pixmaps" "img/ring-48x48.png"
    install -Dm0644 -t "$pkgdir/usr/share/pixmaps" "img/ring-64x64.png"
    install -Dm0644 -t "$pkgdir/usr/share/pixmaps" "img/ring-128x128.png"
    install -Dm0644 -t "$pkgdir/usr/share/pixmaps" "img/ring-256x256.png"
}
