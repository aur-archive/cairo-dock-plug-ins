# Maintainer: Tofe <chris.chapuis@gmail.com>
# Contributor: zhuqin <zhuqin83@gmail.com>
# Contributor: tri1976 <trile7@gmail.com>
# Contributor: snoopy33
# Contributor: 4javier

pkgname=cairo-dock-plug-ins
_pkgname=cairo-dock-plugins
pkgver=3.2.0
pkgrel=0
pkgdesc="Plugins for cairo-dock"
url="https://launchpad.net/cairo-dock"
license="GPL"
arch=('i686' 'x86_64')
depends=("cairo-dock" 'libxxf86vm' 'vte' 'alsa-lib' 'gvfs' 'upower' 'libdbusmenu-gtk3')
optdepends=('libzeitgeist: to enable the Recent-Events applet' 'webkit: to enable the Weblet applet' 'indicator: to enable the Indicator applet' 'ruby: to support applets written in Ruby' 'mono: to support applets written in Mono/.Net' 'libpulse: to enable the Impulse applet' 'fftw: to enable the Impulse applet' 'libetpan: to enable the Mail applet' 'ido: to enable the Indicator applet' 'indicator-me: to enable the Me-Messaging applet')
makedepends=('cmake' 'pkgconfig' 'libtool')
options=('!libtool')
source=(http://launchpad.net/$pkgname/3.2/$pkgver/+download/$_pkgname-$pkgver.tar.gz applet-host-ias.patch)
md5sums=('b4e2ce504b4a6ccfdb380482ebe6e77e' '28ae9bce2bced1a8270a94ec43993103')

build() {
  cd $srcdir/$_pkgname-$pkgver

  patch -p1 < $srcdir/applet-host-ias.patch

  sed -i "22 i #include <sys/types.h>" alsaMixer/src/applet-struct.h

  [[ -e build ]] || mkdir build
  cd build

  cmake .. -DCMAKE_INSTALL_PREFIX=/usr -DROOT_PREFIX=$startdir/pkg \
  -Denable-network-monitor=yes \
  -Denable-disks=yes \
  -Denable-doncky=yes \
  -Denable-scooby-do=yes
  make
}

package() {
  cd $srcdir/$_pkgname-$pkgver/build
  make install DESTDIR=$pkgdir
}

