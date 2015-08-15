# Maintainer: Alexander Rødseth <rodseth@gmail.com>

pkgname=go-goweb
pkgver=20120919
pkgrel=2
pkgdesc='Lightweight RESTful web framework'
arch=('x86_64' 'i686')
url='http://code.google.com/p/goweb/'
license=('MIT')
makedepends=('go' 'go-check')
options=('!strip' '!emptydirs')
install=$pkgname.install
_gourl=code.google.com/p/goweb/goweb

build() {
  cd "$srcdir"
  GOPATH="$srcdir" go get -v -x ${_gourl}
}

check() {
  source /etc/profile.d/go.sh
  GOPATH="$GOPATH:$srcdir" go test -v -x ${_gourl}
}

package() {
  source /etc/profile.d/go.sh
  mkdir -p "$pkgdir/$GOPATH"
  cp -Rv --preserve=timestamps ${srcdir}/{src,pkg} "${pkgdir}/$GOPATH"

  # Package license (if available)
  for f in LICENSE COPYING; do
    if [ -e "$srcdir/src/$_gourl/$f" ]; then
      install -Dm644 "$srcdir/src/$_gourl/$f" \
        "$pkgdir/usr/share/licenses/$pkgname/$f"
    fi
  done

  # Symbolic link for easy imports (doesn't work, deprecated method)
  #for f in "${pkgdir}${GOPATH}/pkg/"*"/$_gourl"*'.a'; do
  #  ln -s `echo $f | sed "s:$pkgdir::"` `echo $f | sed "s:$_gourl.a::"``basename $f`
  #done
}

# vim:set ts=2 sw=2 et:
