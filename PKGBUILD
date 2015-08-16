# Maintainer: Philipp 'TamCore' B. <philipp {at} tamcore {dot} eu>
# Contributor: skydrome <irc.freenode.net>
# Contributor: Étienne Deparis <etienne@depar.is>

pkgname=mom
pkgver=4.1.15
pkgrel=7
pkgdesc="Management interface software for products offered by OVH"
url="https://www.ovh.com/fr/support/outils/mom.xml"
license=('custom')
arch=('i686' 'x86_64')
depends=('krb5' 'xdg-utils')
source=("http://mirror.ovh.net/ftp.ovh.net/MoM/MoM-${pkgver}.tar.gz"
        'mom.desktop'
        'mom.xpm')
md5sums=('5b950f058a0e5106e573023e9b9cef67'
         'b24f40485459f0f613bc7dcd863ab941'
         '339ef7af508acd58822e3ee8d16920af')


# this is leftover from the original maintainer of this pkgbuild
# i dont have an x64 system to test it on
[[ "$CARCH" = "x86_64" ]] &&
    depends=('lib32-krb5' 'lib32-fontconfig' 'lib32-libsm' 'lib32-libxext' 'lib32-gcc-libs' 'xdg-utils')

build() {

  msg2 'Patching MoM script'

  sed -i "s|LD_LIBRARY_PATH=\$dirname/.lib|LD_LIBRARY_PATH='/usr/lib/mom:/usr/lib'|" $srcdir/MoM/MoM
  sed -i "s|/\.\$appname-bin|/\$appname-bin|" $srcdir/MoM/MoM

  cd $srcdir/MoM
  mkdir deb
  cd deb

  msg2 'Install debian dependancies'
  wget http://ftp.fr.debian.org/debian/pool/main/libx/libxinerama/libxinerama1_1.1-3+squeeze1_i386.deb
  ar x libxinerama1_1.1-3+squeeze1_i386.deb
  tar xzf data.tar.gz
  install -m 755 usr/lib/libXinerama.so.1.0.0 ../.lib/libXinerama.so.1
  rm control.tar.gz data.tar.gz debian-binary
  
  wget http://ftp.fr.debian.org/debian/pool/main/libx/libxi/libxi6_1.3-8_i386.deb
  ar x libxi6_1.3-8_i386.deb
  tar xzf data.tar.gz
  install -m 755 usr/lib/libXi.so.6.1.0 ../.lib/libXi.so
  rm control.tar.gz data.tar.gz debian-binary
  
  wget http://ftp.fr.debian.org/debian/pool/main/libx/libxrandr/libxrandr2_1.3.0-3+squeeze1_i386.deb
  ar x libxrandr2_1.3.0-3+squeeze1_i386.deb
  tar xzf data.tar.gz
  install -m 755 usr/lib/libXrandr.so.2.2.0 ../.lib/libXrandr.so.2
  rm control.tar.gz data.tar.gz debian-binary
  
  wget http://ftp.fr.debian.org/debian/pool/main/libx/libxfixes/libxfixes3_4.0.5-1+squeeze1_i386.deb
  ar x libxfixes3_4.0.5-1+squeeze1_i386.deb
  tar xzf data.tar.gz
  install -m 755 usr/lib/libXfixes.so.3.1.0 ../.lib/libXfixes.so
  rm control.tar.gz data.tar.gz debian-binary
  
  wget http://ftp.fr.debian.org/debian/pool/main/o/openssl/libssl0.9.8_0.9.8o-4squeeze14_i386.deb
  ar x libssl0.9.8_0.9.8o-4squeeze14_i386.deb
  tar xzf data.tar.gz
  install -m 755 usr/lib/libssl.so.0.9.8 ../.lib/libssl.so.0.9.8
  install -m 755 usr/lib/libcrypto.so.0.9.8 ../.lib/libcrypto.so.0.9.8
  install -dm 755 ../.lib/ssl
  mv usr/lib/ssl/* ../.lib/ssl/
  rm control.tar.gz data.tar.gz debian-binary

  wget http://ftp.fr.debian.org/debian/pool/main/q/qjson/libqjson0_0.7.1-1_i386.deb
  ar x libqjson0_0.7.1-1_i386.deb
  tar xzf data.tar.gz
  install -m 755 usr/lib/libqjson.so.0.7.1 ../.lib/libqjson.so.0
  rm control.tar.gz data.tar.gz debian-binary

  wget http://ftp.fr.debian.org/debian/pool/main/libx/libxcursor/libxcursor1_1.1.10-2+squeeze1_i386.deb
  ar x libxcursor1_1.1.10-2+squeeze1_i386.deb
  tar xzf data.tar.gz
  install -m 755 usr/lib/libXcursor.so.1.0.2 ../.lib/libXcursor.so.1
  rm control.tar.gz data.tar.gz debian-binary
  
  cd ../
  rm -r deb
}

package() {
  install -dm 755 $pkgdir/usr/{bin,lib/mom}
  install -dm 755 $pkgdir/usr/share/{pixmaps,applications,licenses/mom}
  
  install -Dm 755 $srcdir/MoM/MoM                     $pkgdir/usr/bin/mom
  install -Dm 755 $srcdir/MoM/.MoM-bin                $pkgdir/usr/bin/mom-bin
  mv              $srcdir/MoM/.lib/*                  $pkgdir/usr/lib/mom/
  install -Dm 644 $srcdir/mom.xpm                     $pkgdir/usr/share/pixmaps
  install -Dm 644 $srcdir/mom.desktop                 $pkgdir/usr/share/applications
  install -Dm 644 $srcdir/MoM/licenses/license-en.txt $pkgdir/usr/share/licenses/mom/LICENSE
}
