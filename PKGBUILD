# Maintainer: Luna Jernberg <droidbittin@gmail.com>
# Contributor: Hilton Medeiros <medeiros.hilton@gmail.com>
# Contributor: Simon Brulhart <simon@brulhart.me>
# Contributor: Det <nimetonmaili g-mail>, Achilleas Pipinellis, speed145a, Schnouki, aus

pkgname=firefox-bin
_pkgname=firefox
pkgver=92.0
pkgrel=1
pkgdesc="Standalone web browser from mozilla.org - official prebuilt binary"
arch=('x86_64')
url="https://www.mozilla.org/en-US/firefox/new/"
license=(MPL GPL LGPL)
depends=(gtk3 libxt mime-types dbus-glib nss ttf-font)
optdepends=('ffmpeg: H264/AAC/MP3 decoding'
            'networkmanager: Location detection via available WiFi networks'
            'libnotify: Notification integration'
            'pulseaudio: Audio support'
            'speech-dispatcher: Text-to-Speech'
            'hunspell-en_US: Spell checking, American English')
provides=("firefox=$pkgver")
conflicts=('firefox')
source=(https://archive.mozilla.org/pub/firefox/releases/92.0/linux-x86_64/en-US/firefox-92.0.tar.bz2
        $_pkgname.sh
        $_pkgname.desktop)
sha256sums=('29050d18670a61585b101f8fa4e196fcfc22d0447178143202301836f3c048eb'
            '9491f195066aa56f4f0bbc83e5f0581a460f4c34ee455ba24db312b540322703'
            'c64008cbf01956ce3dba693230670de58fa9487ad19f4ba76614af13beb1b8ef')
validpgpkeys=('14F26682D0916CDD81E37B6D61B7B526D98F0353') # Mozilla Software Releases <release@mozilla.com>

package() {
  # Create directories
  mkdir -p "$pkgdir"/usr/bin
  mkdir -p "$pkgdir"/usr/share/applications
  mkdir -p "$pkgdir"/opt

  # Install
  cp -r firefox/ "$pkgdir"/opt/$pkgname

  # Launchers
  install -m755 $_pkgname.sh "$pkgdir"/usr/bin/$_pkgname

  # Desktops
  install -m644 *.desktop "$pkgdir"/usr/share/applications/

  # Icons
  #for i in 16x16 32x32 48x48 64x64 128x128; do
  #  install -d "$pkgdir"/usr/share/icons/hicolor/$i/apps/
  #  ln -s /opt/$pkgname/browser/chrome/icons/default/default${i/x*}.png \
  #        "$pkgdir"/usr/share/icons/hicolor/$i/apps/$_pkgname.png
  #done

  # Use system-provided dictionaries
  #rm -r "$pkgdir"/opt/$_pkgname/dictionaries
  ln -Ts /usr/share/hunspell "$pkgdir"/opt/$pkgname/dictionaries
  ln -Ts /usr/share/hyphen "$pkgdir"/opt/$pkgname/hyphenation

  # Use system certificates
  ln -sf /usr/lib/libnssckbi.so "$pkgdir"/opt/$pkgname/libnssckbi.so
}

