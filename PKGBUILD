# Contributor: Ron Huang <ronhuang+aur at gmail dot com>
pkgname=fcgiwrap
pkgver=20100710
pkgrel=1
pkgdesc="Simple FastCGI wrapper for CGI scripts"
arch=('i686' 'x86_64')
url="http://github.com/gnosek/fcgiwrap/"
license=('MIT')
depends=('spawn-fcgi')
makedepends=('git' 'autoconf' 'automake' 'fcgi')
backup=('etc/conf.d/fcgiwrap')
install=fcgiwrap.install
source=(conf initscript)
md5sums=('2a4fa3e8a96610423875040fba35d53e'
         '0716a447478c478f0a00a34b85076173')

_gitroot="http://github.com/gnosek/fcgiwrap.git"

build() {
  msg "Connecting to GIT server..."
  if [[ -d $srcdir/$pkgname ]]; then
    cd $srcdir/$pkgname && git pull origin || return 1
  else
    git clone $_gitroot $srcdir/$pkgname || return 1
    cd $srcdir/$pkgname
  fi
  msg "GIT checkout done or server timeout"

  autoreconf -i || return 1
  ./configure --prefix /usr || return 1
  make || return 1
  make DESTDIR="$pkgdir/" install || return 1

  mkdir -p $pkgdir/etc/rc.d
  cp $srcdir/initscript $pkgdir/etc/rc.d/$pkgname
  chmod +x $pkgdir/etc/rc.d/$pkgname

  mkdir -p $pkgdir/etc/conf.d
  cp $srcdir/conf $pkgdir/etc/conf.d/$pkgname
}

# vim:set ts=2 sw=2 et:
