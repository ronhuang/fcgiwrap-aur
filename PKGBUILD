# Contributor: Ron Huang <ronhuang+aur at gmail dot com>
pkgname=fcgiwrap
pkgver=20091201
pkgrel=1
pkgdesc="Simple FastCGI wrapper for CGI scripts"
arch=('i686' 'x86_64')
url="http://github.com/gnosek/fcgiwrap/"
license=('MIT')
depends=('spawn-fcgi')
makedepends=('git' 'fcgi')
backup=('/etc/conf.d/$pkgname')
install=fcgiwrap.install
source=(conf initscript)
md5sums=('e5c762dba6620d51a194a0abae94e620'
         '003bd57f1b1006f7d9cef75379ea478d')

_gitroot="git://github.com/gnosek/fcgiwrap.git"

build() {
  msg "Connecting to GIT server..."
  if [[ -d $srcdir/$pkgname-$pkgver ]]; then
    cd $srcdir/$pkgname-$pkgver && git pull origin || return 1
  else
    git clone $_gitroot $srcdir/$pkgname-$pkgver || return 1
    cd $srcdir/$pkgname-$pkgver
  fi
  msg "GIT checkout done or server timeout"

  make || return 1
  mkdir -p $pkgdir/usr/bin
  cp $srcdir/$pkgname-$pkgver/$pkgname $pkgdir/usr/bin/$pkgname
  chmod +x $pkgdir/usr/bin/$pkgname

  mkdir -p $pkgdir/etc/rc.d
  cp $srcdir/initscript $pkgdir/etc/rc.d/$pkgname
  chmod +x $pkgdir/etc/rc.d/$pkgname

  mkdir -p $pkgdir/etc/conf.d
  cp $srcdir/conf $pkgdir/etc/conf.d/$pkgname
}

# vim:set ts=2 sw=2 et:
