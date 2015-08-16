# $Id: PKGBUILD 174637 2013-01-05 12:59:50Z andrea $
# Maintainer: Andrea Scarpino <andrea@archlinux.org>
# Contributor: Pierre Schmitz <pierre@archlinux.de>

pkgname=kdebase-runtime-kiosmb-fix
_realname=kdebase-runtime
pkgver=4.10.2
pkgrel=1
pkgdesc="Plugins and applications necessary for the running of KDE applications"
arch=('i686' 'x86_64')
url='https://projects.kde.org/projects/kde/kde-runtime'
license=('GPL' 'LGPL')
depends=('nepomuk-core' 'smbclient' 'libssh' 'libcanberra' 'oxygen-icons' 'xorg-xauth'
         'kactivities')
makedepends=('pkg-config' 'cmake' 'automoc4' 'kdepimlibs' 'openslp' 'doxygen'
             'networkmanager')
optdepends=('kdepimlibs: to generate drkonqi reports'
            'htdig: to build the search index in khelpcenter'
            'rarian: needed by khelpcenter'
            'gdb: drkonq crash handler')
install="${_realname}.install"
replaces=('kdebase-runtime')
provides=('kdebase-runtime')
conflicts=('kdebase-runtime')
source=("http://download.kde.org/stable/${pkgver}/src/kde-runtime-${pkgver}.tar.xz" kio_smb_buf_size.patch)
sha1sums=('b7f3c3907b8f19dcd975b1724b8ae01c4cae638b'
          '598c4f1fdadb24bc30b142d6f562dd78a23514d2')
build() {
    cd "${srcdir}/kde-runtime-${pkgver}"
	patch -Np1 -i $srcdir/kio_smb_buf_size.patch
	cd "${srcdir}"
	mkdir build
	cd build
	cmake ../kde-runtime-${pkgver} \
		-DCMAKE_BUILD_TYPE=Release \
		-DCMAKE_SKIP_RPATH=ON \
		-DCMAKE_INSTALL_PREFIX=/usr \
        -DWITH_QNtrack=OFF \
        -DWITH_Xine=OFF
	make
}

package() {
	cd "$srcdir/build"
	make DESTDIR="$pkgdir" install
	rm -f "${pkgdir}/usr/share/icons/hicolor/index.theme"

    ln -sf /usr/lib/kde4/libexec/kdesu "${pkgdir}/usr/bin/"
}
