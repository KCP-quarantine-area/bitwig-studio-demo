pkgname='bitwig-studio-demo'
pkgver='1.3.11'
pkgrel='1'
pkgdesc='Music production system for production, remixing and performance'
arch=('x86_64')
url='http://www.bitwig.com/'
license=('custom')
depends=('jack2' 'xdg-utils' 'qarma' 'xcb-util-wm' 'libbsd' 'alsa-lib' 'alsa-oss' 'ffmpeg' 'qjackctl')
options=(!strip)
source=("https://downloads.bitwig.com/stable/${pkgver}/bitwig-studio-${pkgver}.deb"
        'bitwig-studio.launcher')
md5sums=('284d1f5ac35553735f7247a383308659'
         '32411d3b742f15addef7b86681825fee')

package() {
  # Create pkgdir folders
  install -d ${pkgdir}/usr/bin
  install -d ${pkgdir}/opt/bitwig-studio
  install -d ${pkgdir}/opt/bitwig-studio/libexec
  install -d ${pkgdir}/usr/share/{applications,icons}
  install -d ${pkgdir}/usr/share/licenses/${pkgname}

  # Unpack package contents
  bsdtar -xf ${srcdir}/data.tar.gz -C ${pkgdir}/

  # Install launcher (replacing default symlink)
  install -m755 ${srcdir}/bitwig-studio.launcher ${pkgdir}/usr/bin/bitwig-studio

  # Workaround MP3 support by providing symlinks to ffmpeg
  ln -s /usr/bin/ffmpeg ${pkgdir}/opt/bitwig-studio/libexec/avconv
  ln -s /usr/bin/ffprobe ${pkgdir}/opt/bitwig-studio/libexec/avprobe

  # Install license
  install -m644 ${pkgdir}/opt/bitwig-studio/EULA.rtf \
    ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE

  # Fix launcher category
  sed -i 's:Categories=Multimedia:Categories=Multimedia;AudioVideo;Player;Recorder;:' \
    ${pkgdir}/usr/share/applications/bitwig-studio.desktop
}
