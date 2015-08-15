# Maintainer: Ainola <opp310@alh.rqh> (ROT13 this.)
# Contributor: speps <speps at aur dot archlinux dot org> (Did all the work, I just updated it)
# Contributor: Bernardo Barros <bernardobarros@gmail.com>

pkgname=csound6
pkgver=6.03.2
pkgrel=1
pkgdesc="A programming language for sound rendering and signal processing."
arch=(i686 x86_64)
url="http://csound.github.io"
license=('LGPL')
depends=('fltk' 'fluidsynth' 'liblo' 'portaudio' 'portmidi' 'tk' 'curl' 'stk')
makedepends=('cmake' 'gmm' 'swig' 'java-environment' 'dssi' 'boost' 'pd' 'luajit' 'eigen')
optdepends=('qutecsound: qt frontend'
            'cecilia: tcl/tk frontend'
            'cecilia4: wxpython frontend'
            'vim: vim frontend'
            'java-environment: java wrapper'
            'luajit: lua wrapper'
            'python2: python wrapper')
provides=('csound6')
conflicts=('csound6')
source=("http://downloads.sourceforge.net/project/csound/csound${pkgver:0:1}/Csound${pkgver:0:4}/Csound${pkgver}.tar.gz" csound.sh)
md5sums=('94c836cf9b491cfceec55982ab8f3237'
         '2e3a1f546dcb2c125ae5b7247eb81d6d')

prepare() {
  cd Csound$pkgver

  # install modules to proper paths
  sed -i '/^set.*MODULE_INSTALL_DIR/d' CMakeLists.txt
  sed -i '/pdname/{n;s/LIBRARY/PD_MODULE/2}' frontends/CMakeLists.txt
}

build() {
  cd Csound$pkgver
  [ -d bld ] || mkdir bld && cd bld
  cmake .. -DCMAKE_INSTALL_PREFIX=/usr \
           -DPYTHON_MODULE_INSTALL_DIR=/usr/lib/python2.7/site-packages \
           -DJAVA_MODULE_INSTALL_DIR=/usr/lib/csound/java \
           -DLUA_MODULE_INSTALL_DIR=/usr/lib/lua/5.1 \
           -DPD_MODULE_INSTALL_DIR=/usr/lib/pd/extra
  make
}

package() {
  cd Csound$pkgver/bld
  make DESTDIR="$pkgdir/" install

  # export vars in profile.d
  install -Dm755 "$srcdir/csound.sh" "$pkgdir/etc/profile.d/csound.sh"
}

# vim:set ts=2 sw=2 et:
