# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Antonio Rojas <arojas@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>
# Contributor: Pierre Schmitz <pierre@archlinux.de>

pkgbase=oxygen-icons
#pkgname=(oxygen-icons oxygen-icons-svg)
conflicts=(oxygen-icons oxygen-icons-svg)
provides=(oxygen-icons oxygen-icons-svg)
pkgname=(oxygen-icons-git oxygen-icons-svg-git)
pkgver=5.90.0
epoch=1
pkgrel=1
pkgdesc='The Oxygen Icon Theme'
arch=(any)
url='https://community.kde.org/Frameworks'
license=(LGPL)
makedepends=(extra-cmake-modules-git qt5-base)
#source=(https://download.kde.org/stable/frameworks/${pkgver%.*}/${pkgbase}5-$pkgver.tar.xz{,.sig})
#sha256sums=('2f747c4daf561306b25c347cb3a716bec32093ab8bd3e3ab8fbceed89981eec7'
#            'SKIP')
#validpgpkeys=(53E6B47B45CEA3E0D5B7457758D0EE648A48B3BB) # David Faure <faure@kde.org>
source=("git+https://invent.kde.org/frameworks/${pkgname%-git}5.git")
sha256sums=('SKIP')

pkgver() {
  cd ${pkgname%-git}5
  _ver="$(grep -m1 'set(KF_VERSION' CMakeLists.txt | cut -d '"' -f2 | tr - .)"
  echo "${_ver}_r$(git rev-list --count HEAD).g$(git rev-parse --short HEAD)"
}

build() {
  cmake -B build -S ${pkgbase}5
  cmake --build build
}

package_oxygen-icons-git() {
  #groups=(kf5)
  groups=(kf5-git)

  DESTDIR="$pkgdir" cmake --install build
}

package_oxygen-icons-svg-git() {
  pkgdesc='The Oxygen Icon Theme (Scalable Vector Graphics)'

  cd ${pkgbase}5
  find scalable -type f ! -name '*.sh' -exec \
    install -D -m644 "{}" "$pkgdir"/usr/share/icons/oxygen/{} \;
}
