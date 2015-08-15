# Maintainer: Gustavo Alvarez <sl1pkn07@gmail.com>

pkgname=dvdx-open-edition
pkgver=4.0.1.0
pkgrel=3
pkgdesc="DVDx 4.0 is an audio/video encoder as well as a powerful DVD copier. (Open Edition)"
arch=('i686' 'x86_64')
url="http://www.labdv.com/dvdx"
license=('LGPL' 'GPL3')
depends=('qt4')
optdepends=("mencoder: Encoder Engine"
            "ffmpeg: Encoder Engine"
            "mediainfo: Media Information"
            "mplayer: Player Engine"
            "libdvdcss: Decript DVD")
install="${pkgname}.install"
source=("http://downloads.sourceforge.net/project/dvdx/4.0/${pkgver}/${pkgname}-${pkgver}-src.7z"
        "http://www.labdv.com/dvdx/extras/tools.tar.gz"
        "dvdx4openicon.svg"
        "DVDx_4_Open_Edition.desktop"
        "interfacemplayer.patch")
md5sums=('b3e94cae5c83cf401ad6e261043e334b'
         '27255e4a565c40207e864782622beeb8'
         '1a184efc61b81abfa353524fe3b5eb91'
         'a284cbd70cf1912e9f6d2bfbf6d329ba'
         'ca3cb4f75ea51305cad5040d87b048e1')

prepare() {
  cd "${srcdir}"
  #change executable dependency paths
  sed -e 's|opt/dvdx4-open-edition|usr|g' \
      -e 's|"mplayer"|"/usr/bin/mplayer"|g' \
      -e 's|"mencoder"|"/usr/bin/mencoder"|g' \
      -i src/main/paths.h
  patch --silent -p0 -d src/player -i  "${srcdir}/interfacemplayer.patch"
  cd src
  sed 's|qmake|qmake-qt4|g' -i build-release-linux.sh
}

build() {
  cd "${srcdir}/src"
  sh build-release-linux.sh
}

package() {
  cd "${srcdir}"
  install -Dm644 DVDx_4_Open_Edition.desktop "${pkgdir}/usr/share/applications/DVDx_4_Open_Edition.desktop"
  install -Dm644 dvdx4openicon.svg "${pkgdir}/usr/share/icons/hicolor/scalable/apps/dvdx4openicon.svg"
  install -d "${pkgdir}/usr/share/doc/${pkgname}"
  install -m644 src/LICENSE.{GPL3,LGPL} "${pkgdir}/usr/share/doc/${pkgname}/"
  install -Dm755 build/unix/release/bin/DVDx4 "${pkgdir}/usr/bin/DVDx4"
}
