# Maintainer: Leo von Klenze <devel@leo.von-klenze.de> 

pkgname=qooxdoo-sdk-git
pkgver=20140330
pkgrel=1
pkgdesc="Universal JavaScript Framework"
url="http://qooxdoo.org"
arch=('any')
license=('LGPL' 'EGPL')
source=()
makedepends=('git')
provides=('qooxdoo-git')
conflicts=('qooxdoo-git')

_gitname="qooxdoo"
_gitroot="git://github.com/qooxdoo/${_gitname}"


build() {
  cd $srcdir
  msg "Connecting to GIT (${_gitroot}) ..."

  if [ -d $_gitname ]; then
    cd $_gitname
    git checkout -f
    git pull origin
    msg "The local files of ${_gitname} were updated."
  else
    git clone $_gitroot $_gitname
  fi
  
  msg "GIT checkout done or server timeout"
 
  msg "Changing links to python2"
  for x in `find -regex ".*[.]py$"`; do 
    line=`head -n 1 "$x" | head -c 2`; 
    if [ "$line" = '#!' ]; then 
      echo '#!/usr/bin/env python2' > "${x}-edit"; 
      tail -n +2 $x >> "${x}-edit";
      mv "${x}-edit" $x;
      chmod a+x $x;
    fi; 
  done
}

package() {
  mkdir -p $pkgdir/opt/$_gitname/$pkgver
  cp -R $srcdir/$_gitname/* $pkgdir/opt/$_gitname/$pkgver
}

