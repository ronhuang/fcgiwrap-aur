# Contributor: Ron Huang <ronhuang+aur at gmail dot com>
pkgname=fcgiwrap
pkgver=20100611
pkgrel=1
pkgdesc="Simple FastCGI wrapper for CGI scripts"
arch=('i686' 'x86_64')
url="http://github.com/gnosek/fcgiwrap/"
license=('MIT')
depends=('spawn-fcgi')
makedepends=('git' 'autoconf' 'automake' 'fcgi')
backup=('etc/conf.d/$pkgname')
install=fcgiwrap.install
source=(conf initscript)
md5sums=('b56d102805e8ec6cbbbc67ce9df482e7'
         '436473f30af08984aa18885df9240606')

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
