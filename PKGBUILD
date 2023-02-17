# Maintainer: Bardia Moshiri <fakeshell@bardia.tech>

pkgname=bluebinder
provides=('bluebinder')
_pkgbase=bluebinder
pkgver=74.d172d0c
pkgrel=1
arch=('aarch64')
url="https://github.com/droidian/bluebinder"
license=('GPL2')
depends=('bluez')
makedepends=('git' 'pkgconfig' 'glib2' 'libglibutil' 'libgbinder' 'systemd-libs')
source=("bluebinder::git+https://github.com/droidian/bluebinder"
        "0001-makefile-sbin2bin.patch"
        "0002-service-sbin2bin.patch"
        "0003-makefile-install.patch")
sha256sums=('SKIP'
           '7b92ee998a7b53af8c6f843f993680965982940903f6f64af2eaf71518ec73cd'
           '8562e088d5e489142daa2245a2a195a5fe39d559030a37a8e9a0e46ec382531d'
           'a1324b4476feaa938d14cfaac93de681a479bfac6f31b409a7dd1889fdbc21d1')

options=(debug !strip)

pkgver() {
  cd "${srcdir}/${_pkgbase}"
  echo $(git rev-list --count HEAD).$(git rev-parse --short HEAD)
}

prepare() {
  cd "${srcdir}/${_pkgbase}"
  git checkout -b bookworm
  git checkout d172d0c2babf9104abd66c9eeaf94580fcf4794b

  local src
  for src in "${source[@]}"; do
      src="${src%%::*}"
      src="${src##*/}"
      [[ $src = *.patch ]] || continue
      echo "Applying patch $src..."
      patch -N < "../$src"
  done
}

build() {
  cd "${srcdir}/${_pkgbase}"
  make
}

package() {
  cd "${srcdir}/${_pkgbase}"
  make DESTDIR="$pkgdir" install
}
