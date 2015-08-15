# Maintainer: c0nd0r <gcesarmza@gmail.com>
# Contributor: Thomas Dziedzic < gostrc at gmail >
# Contributor: webjdm <web.jdm@gmail.com>

pkgname=firefox32
_pkgname=firefox32
pkgver=9.0.1
pkgrel=2
pkgdesc="bin32-firefox for Arch x86_64 (en-US)"
arch=('x86_64')
license=('MPL' 'GPL' 'LGPL')
url="http://www.mozilla.org/projects/firefox"
depends=('lib32-dbus-glib' 'lib32-gtk2' 'lib32-libxt' 'lib32-alsa-lib' 'lib32-nss' 'lib32-xcb-util')
optdepends=('bin32-firefox-i18n: i18n support'
            'lib32-flashplugin: flash support'
            'bin32-acroread: adobe reader plugin'
            'bin32-icedtea-web: java plugin'
            'lib32-librsvg: svg_loader.so library'
            'lib32-gtk-engines: libclearlooks.so library')
source=("http://releases.mozilla.org/pub/mozilla.org/firefox/releases/${pkgver}/linux-i686/en-US/firefox-${pkgver}.tar.bz2"
        'firefox32.desktop' 'firefox32-safe.desktop' 'mozplugin.patch')
md5sums=('a6ac0d7478410455be816c41597d5a9f'
         'f93c2d52600eaf905b2e9c8df318d9a6'
         '803ab3405d3c30d0a947ffe1d7d224aa'
         '8ef4b2a15b9d5e9d5bd5df323dbf012f')

build() {
  # directory and files
  cd ${pkgdir}
  mkdir -p {usr/bin,usr/lib32}
  cp -r ${srcdir}/firefox usr/lib32/${_pkgname}
  mv usr/lib32/${_pkgname}/firefox usr/lib32/${_pkgname}/firefox32
  mv usr/lib32/${_pkgname}/firefox-bin usr/lib32/${_pkgname}/firefox32-bin
  cat <<EOF > usr/bin/firefox32
#!/bin/bash
/usr/lib32/${_pkgname}/run-mozilla.sh /usr/lib32/${_pkgname}/firefox32 \$*
EOF
  chmod +x usr/bin/firefox32

  # desktop icons
  cd ${srcdir}
  install -d ${pkgdir}/usr/share/applications
  install -Dm644 firefox32.desktop firefox32-safe.desktop ${pkgdir}/usr/share/applications
  install -Dm644 firefox/icons/mozicon128.png ${pkgdir}/usr/share/pixmaps/firefox32.png

  # set MOZ_PLUGIN_PATH variable
  cd ${pkgdir}/usr/lib32/${_pkgname}
  patch -Np0 -i ${srcdir}/mozplugin.patch
}

