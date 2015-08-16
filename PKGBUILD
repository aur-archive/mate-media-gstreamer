# Maintainer : Martin Wimpress <code@flexion.org>
# Contributor: Giovanni "Talorno" Ricciardi <kar98k.sniper@gmail.com>
# Contributor: Xpander <xpander0@gmail.com>

_pkgname=mate-media
pkgname=${_pkgname}-gstreamer
pkgver=1.6.0
pkgrel=5
pkgdesc="MATE Media Tools (GStreamer)"
url="http://mate-desktop.org"
arch=('i686' 'x86_64' 'armv6h' 'armv7h')
license=('GPL')
depends=('gstreamer0.10-base-plugins' 'gtk2' 'libcanberra' 'mate-desktop'
         'mate-window-manager')
makedepends=('mate-common' 'mate-doc-utils' 'mate-panel'
             'mate-settings-daemon-gstreamer' 'perl-xml-parser')
optdepends=('mate-panel: Volume control for the panel')
options=('!emptydirs')
conflicts=("${_pkgname}-pulseaudio" 'mate-settings-daemon-pulseaudio')
provides=("${_pkgname}")
source=("http://pub.mate-desktop.org/releases/1.6/${_pkgname}-${pkgver}.tar.xz"
        enable_deprecated.diff)
sha1sums=('06c3418dfe0be26e74b0e40aa92eea6260579a72'
          'f0e38578aacacf9ee852b7a44a34908cc230b91f')
install=${pkgname}.install

prepare() {
    cd "${srcdir}/${_pkgname}-${pkgver}"
    # Enable deprecated
    patch -p1 < ../../enable_deprecated.diff gst-mixer/src/Makefile.am
}

build() {
    cd "${srcdir}/${_pkgname}-${pkgver}"
    ./autogen.sh \
        --prefix=/usr \
        --sysconfdir=/etc \
        --libexecdir=/usr/lib/${_pkgname} \
        --localstatedir=/var \
        --enable-gstmix \
        --enable-gst-mixer-applet \
        --disable-pulseaudio \
        --disable-static \
        --disable-scrollkeeper
    make
}

package() {
    cd "${srcdir}/${_pkgname}-${pkgver}"
    make DESTDIR="${pkgdir}" install
}
