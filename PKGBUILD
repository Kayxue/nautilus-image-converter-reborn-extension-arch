# Maintainer: Kay <s0990006@gmail.com>

pkgname=nautilus-image-converter-reborn-extension
pkgver=0.1.0
pkgrel=1
pkgdesc="Modern Nautilus 43+ context menu extension to resize, rotate, and convert images"
arch=('x86_64' 'aarch64')
url="https://github.com/Kayxue/nautilus-image-converter-reborn-extension"
license=('MIT')
depends=(
  'gcc-libs'
  'glib2'
  'glibc'
  'libnautilus-extension'
  'nautilus'
)
makedepends=(
  'cargo'
  'git'
  'pkgconf'
)
optdepends=(
  'nautilus-image-converter-reborn: companion CLI/GUI application to perform resize and rotate actions'
)
install="$pkgname.install"
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('28dbdbc7944731a1f945c144109c42efa788208d1076c206478a2273be95042e')

prepare() {
  cd "$pkgname-$pkgver"
  export RUSTUP_TOOLCHAIN=stable
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  export RUSTUP_TOOLCHAIN=stable
  export CARGO_TARGET_DIR=target
  CFLAGS+=" -ffat-lto-objects"
  cargo build --frozen --release
}

check() {
  cd "$pkgname-$pkgver"
  export RUSTUP_TOOLCHAIN=stable
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm755 "target/release/libnautilus_image_converter_reborn_extension.so" \
    "$pkgdir/usr/lib/nautilus/extensions-4/libnautilus_image_converter_reborn_extension.so"
  install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
