# $Id: PKGBUILD 176924 2013-02-02 17:56:28Z andrea $
# Maintainer:
# Contributor: Andrea Scarpino <andrea@archlinux.org>
# Contributor: Dan McGee <dan@archlinux.org>

pkgname=rdesktop
pkgver=1.7.1
pkgrel=4
pkgdesc="An open source client for Windows Remote Desktop Services"
arch=('i686' 'x86_64')
url="http://www.rdesktop.org/"
license=('GPL3')
depends=('openssl' 'libao' 'libsamplerate' 'xorg-xrandr')
source=("http://downloads.sourceforge.net/${pkgname}/${pkgname}-${pkgver}.tar.gz"
        'rdesktop-send_physical_buttons.diff'
        'rdesktop-libao.patch'
        'rdesktop_config.patch')
md5sums=('c4b39115951c4a6d74f511c99b18fcf9'
         '880d3aeac67b901e6bf44d1323374768'
         'bd2c9bc68bddcc2652c668753d787df7'
         '8e5f757b57dd80609800f3866be41ab0')

build() {
  cd ${pkgname}-${pkgver}

  # FS#15113
  patch -i "${srcdir}/rdesktop-send_physical_buttons.diff"

  # Fix libao segfault, from Fedora
  patch -i "${srcdir}/rdesktop-libao.patch"
  
  # enable rdesktop_config
  patch -Np1 -i "${srcdir}/rdesktop_config.patch"

  ./configure --prefix=/usr \
    --enable-smartcard \
    --with-ipv6
  make
}

package() {
  cd ${pkgname}-${pkgver}
  make DESTDIR="${pkgdir}" install
}
