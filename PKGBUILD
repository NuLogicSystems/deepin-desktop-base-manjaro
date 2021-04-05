# $Id$
# Maintainer: James Kittsmiller (AJSlye) <james@nulogicsystems.com>
# Contributor:Bernhard Landauer <oberon@manjaro.org>
# Contributor: Felix Yan <felixonmars@archlinux.org>
# Contributor: Josip Ponjavic <josipponjavic at gmail dot com>
# Contributor: Xu Fasheng <fasheng.xu[AT]gmail.com>

_pkgname=deepin-desktop-base
pkgname=$_pkgname-manjaro
pkgver=2021.2.20
pkgrel=1
epoch=2
pkgdesc='Base component for Manjaro Deepin Edition'
arch=('any')
url="https://github.com/linuxdeepin/$_pkgname"
license=('GPL3')
groups=('deepin-manjaro')
provides=("$_pkgname")
conflicts=("$_pkgname")
source=("$_pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz"
    distribution.info
    manjaro-deepin.svg)
sha512sums=('90cec3ae08eedadacc62650d697c6ea99361411cf5367ad36fb309553b29ee6da5207bccabaa6266f4263f1dff5f13dbbae6553872207484b930857d7d124147'
            'a4e69dbe780f7318aa2e15e35225b20cfacc8fe7955ddcece902c9a0ecaab6a1db3b7ccf1c8f4cf788006ccd1409bd3511ab3e5cbd6a6aeb74eecf3ba42c5053'
            '5183f5e91c3eb367f1b12f78be576b0006eba465059c50418128facbbfbcb38bb6c3ef43674da1736c4bf31de97f37effca647cc7ab9cfd9e16003b853b02758')

build() {
  cd $_pkgname-$pkgver
  make
}

package() {
  cd $_pkgname-$pkgver
  make DESTDIR="$pkgdir" install

  install -Dm644 "$srcdir"/distribution.info -t "$pkgdir"/usr/share/deepin/
  install -Dm644 "$srcdir"/manjaro-deepin.svg -t "$pkgdir"/usr/share/pixmaps/
  
  # Remove Deepin distro's lsb-release
  rm "$pkgdir"/etc/lsb-release

  # Remove Deepin distro's appstore.json
  rm "$pkgdir"/etc/appstore.json

  # Don't override systemd timeouts
  rm -r "$pkgdir"/etc/systemd

  # 2fe54d45d79571ff9a79bdd4238c52a4dc90838ceb4d5e4ae94703d3e85284b13660932f39e87fbc338aa58c2a306e54f587c72a6b0e65e1ee4a66eff98ec814Make a symlink for deepin-version
  ln -s ../usr/lib/deepin/desktop-version "$pkgdir"/etc/deepin-version

  # Remove Deepins plymouth logo
  rm "$pkgdir"/usr/share/plymouth/deepin-logo.png

  # Remove UOS logo
  rm "$pkgdir"/usr/share/deepin/uos_logo.svg

  # Remove apt-specific templates
  rm -r "$pkgdir"/usr/share/python-apt
}
