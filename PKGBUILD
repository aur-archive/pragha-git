# Maintainer: Diego <cdprincipe@at@gmail@dot@com>
# Contributor: Matias De Lellis
# Contributor: bailey385 <bailey7698@163.com>

_pkgname=pragha
pkgname=${_pkgname}-git
pkgver=1.2
pkgrel=1
pkgdesc="A lightweight GTK+ music manager - fork of Consonance Music Manager."
arch=('i686' 'x86_64')
url="http://pragha.wikispaces.com/"
license=('GPL')
depends=('git'
         'gstreamer0.10-base'
         'gtk2'
         'libcdio'
         'libnotify'
         'sqlite3'
         'desktop-file-utils'
         'taglib'
         'dbus-glib'
         'hicolor-icon-theme')
optdepends=('exo: better session management'
            'liblastfm_c-git: last.fm scrobbling'
            'keybinder: global keyboard shortcuts'
            'glyr-git: search lyrics, artists info, and album art')
makedepends=('autoconf' 'xfce4-dev-tools')
provides=('pragha')
conflicts=('pragha')
options=('!libtool')

install=pragha.install
source=(git+git://github.com/matiasdelellis/pragha.git#branch=pragha-1.2)
md5sums=('SKIP')


pkgver() {
  cd $srcdir/$_pkgname
  git describe --always --tags | sed 's|-|.|g' | grep -o '[0-9].*[0-9]'
}

build() {
  cd $srcdir/$_pkgname

  LIBS+="-ldbus-glib-1"

  ./autogen.sh
  ./configure --prefix=/usr CPPFLAGS="-DHAVE_PARANOIA_NEW_INCLUDES"

  make
}

package() {
  cd $srcdir/$_pkgname
  make ${MAKEFLAGS} DESTDIR=${pkgdir} install
  
  install -m 644 data/pragha.desktop ${pkgdir}/usr/share/applications
  install -d ${pkgdir}/usr/share/pixmaps
  install -m 644 data/pragha.png ${pkgdir}/usr/share/pixmaps/
  install -m 644 data/pragha.1 ${pkgdir}/usr/share/man/man1/
}

