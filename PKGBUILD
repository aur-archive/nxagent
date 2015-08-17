# Contributor: Markus Opitz <mastero23 at gmail dot com>
# Maintainer: Milan Knížek <knizek@volny.cz>

pkgname=nxagent
pkgver=3.5.0.12
pkgrel=1
pkgdesc="X proxy server for x2go and NX"
arch=(i686 x86_64)
url="http://www.x2go.org/"
license=('GPL2')
depends=('nxcomp>=3.5.0' 'nxcompshad>=3.5.0' 'nxcompext>=3.5.0' 'gcc-libs')
conflicts=('x2goagent-git')
groups=('x2go' 'alts')
source=('nxagent.keyboard'
        'rgb'
        "http://code.x2go.org/releases/source/nx-libs/nx-libs_${pkgver}-full.tar.gz")

build() {
  cd "$srcdir/nx-libs_${pkgver}"
  sed --in-place=orig \
    's!test -d nxproxy \&\& cd nxproxy \&\& autoconf \&\& ./configure \&\& make!# removed line here!' \
    Makefile
#  patch -p1 < ../nxcomp_Png.cpp.patch
  make || return 1
}

package() {
  cd "$srcdir/nx-libs_${pkgver}"

  install -m 755 -D "bin/nxagent" "${pkgdir}/usr/bin/nxagent"

  install -m 755 -D "nx-X11/programs/Xserver/nxagent" "${pkgdir}/usr/lib/nx/nxagent"

  install -m 755 -d "${pkgdir}/usr/share/nx"
  install -m 644 "${srcdir}/rgb" "${pkgdir}/usr/share/nx/rgb"

  install -m 755 -d "${pkgdir}/etc/nxagent"
  install -m 644 "${srcdir}/nxagent.keyboard" "${pkgdir}/etc/nxagent/nxagent.keyboard"

  install -m 755 -d "${pkgdir}/usr/share/pixmaps"
  install -m 644 "nx-X11/programs/Xserver/hw/nxagent/nxagent.xpm" "${pkgdir}/usr/share/pixmaps/nxagent.xpm"

  install -m 755 -d "${pkgdir}/usr/share/doc/nxagent"
  install -m 644 "nx-X11/programs/Xserver/hw/nxagent/CHANGELOG" "${pkgdir}/usr/share/doc/nxagent/changelog.DEBIAN"
}

md5sums=('31a82daa53bd20a317bcfabf16fdf755'
         '09ee098b83d94c7c046d6b55ebe84ae1'
         'a2011e034a318016cf2260c30a567301')
