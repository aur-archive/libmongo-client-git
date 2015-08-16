# Maintainer: Brian Knox <taotetek at gmail>

pkgname=libmongo-client-git
pkgver=20120401
pkgrel=1
pkgdesc="Minimalistic C client for mongodb"
arch=('i686' 'x86_64')
url="http://github.com/algernon/libmongo-client/"
license=('Apache 2.0')
depends=('gcc-libs')
makedepends=('git make')
conflicts=('libmongo-client')
provides=('libmongo-client')
_gitroot="git://github.com/algernon/libmongo-client.git"
_gitname="libmongo-client"
unset CFLAGS

build() {
  cd "$srcdir"
  msg "Connecting to Git server...."

  if [ -d $_gitname ]; then
    pushd $_gitname && git pull origin && popd
    msg "The local files are updated"
  else
    git clone $_gitroot
  fi

  msg "Git checkout done or server timeout"
  msg "Starting make..."

  rm -rf $_gitname-build
  git clone $_gitname $_gitname-build
  cd $_gitname-build
}

package() {
  cd "$srcdir/$_gitname-build"
  autoreconf -fvi
  ./configure --prefix=/usr
  make install DESTDIR=${pkgdir}
}
