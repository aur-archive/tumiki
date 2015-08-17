# Maintainer: Anntoin Wilkinson <anntoin gmail com>
# Contributor: Nick B <Shirakawasuna at gmail _dot_ com>

pkgname=tumiki
_pkgname=tumiki-fighters
pkgver=0.2
pkgrel=7
pkgdesc="An addictive game by Kenta Cho.  Assimilate your enemies to gain strength!"
arch=('i686' 'x86_64')
url="http://tumiki.sourceforge.net/"
license=('custom')
depends=('libgl' 'sdl_mixer' 'libbulletml')
makedepends=('gdc1')
source=(http://abagames.sakura.ne.jp/windows/tf0_2.zip
	http://ftp.de.debian.org/debian/pool/main/t/${_pkgname}/${_pkgname}_${pkgver}.dfsg1-5.debian.tar.gz)
md5sums=('ff68363954f256c30fb4e15636a824be'
         'c72f3a83609209d6f9ade4babe7cef82')

prepare() {
  cd $srcdir/tf

  _patchdir="../debian/patches"
  cat $_patchdir/series | egrep -v '^#|^\ #' | sed "s:^:$_patchdir/:" | xargs -n1 patch -p1 -i

  sed -i 's:\/games::' ./src/abagames/util/sdl/{texture,sound}.d \
                       ./src/abagames/tf/{stagemanager,field,tumikiset,enemyspec,barragemanager}.d
  sed -i 's:gdmd-v1:gdmd1:' Makefile
  sed -i 's:gdc-v1:gdc1:' Makefile
}

build() {
  cd $srcdir/tf
  make
}

package() {
  cd $srcdir/tf

  # Install binary
  install -D -m755 $_pkgname $pkgdir/usr/bin/$_pkgname

  # Install other resources
  find {barrage,enemy,field,sounds,stage,tumiki} -type f -exec install -Dm644 {} $pkgdir/usr/share/$_pkgname/{} \;

  # Install man page and debian copyright license
  install -D -m644 ../debian/$_pkgname.6 $pkgdir/usr/share/man/man6/$_pkgname.6
  install -D -m644 ../debian/copyright $pkgdir/usr/share/licenses/$pkgname/copyright

  # Install desktop file and icon
  install -D -m644 ../debian/$_pkgname.desktop $pkgdir/usr/share/applications/$_pkgname.desktop
  install -D -m644 ../debian/$_pkgname.xpm $pkgdir/usr/share/pixmaps/$_pkgname.xpm
}

# vim:set ts=2 sw=2 et:
