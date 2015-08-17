# Maintainer: Přemysl Janouch <p.janouch@gmail.com>

pkgname=sdtui-git
_pkgname=sdtui
pkgver=r71.99116d0
pkgrel=1
pkgdesc="StarDict terminal UI"
url="https://github.com/pjanouch/sdtui"
arch=('i686' 'x86_64')
license=('BSD')
options=(zipman)
conflicts=('sdtui')
provides=('sdtui')
makedepends=('cmake' 'pkg-config' 'git' 'libxslt')
depends=('zlib' 'glib2' 'gtk3' 'ncurses' 'pango')
source=('git+https://github.com/pjanouch/sdtui.git')
md5sums=('SKIP')

pkgver() {
  cd "$srcdir/$_pkgname"
  ( set -o pipefail
    git describe --long --tags 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

prepare() {
  cd "$srcdir/$_pkgname"
  git submodule init
  git submodule update
}

build() {
  cd $srcdir/$_pkgname
  mkdir build
  cd build
  cmake .. -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release -DWITH_GTK=ON
  make
}

package() {
  cd $srcdir/$_pkgname/build
  make install DESTDIR=$pkgdir
}
