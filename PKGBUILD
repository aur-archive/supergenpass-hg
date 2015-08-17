# Maintainer: Vianney le Clément <vleclement AT gmail · com>
pkgname=supergenpass-hg
pkgver=5
pkgrel=1
pkgdesc="SuperGenPass Python module and GTK interface"
arch=(any)
url="https://bitbucket.org/vianney/supergenpass"
license=('GPL3')
depends=('python')
makedepends=('mercurial')
optdepends=('gtk3: for GTK interface'
            'python-gobject: for GTK interface')

_hgroot=https://bitbucket.org/vianney
_hgrepo=supergenpass

build() {
  cd "$srcdir"
  msg "Connecting to Mercurial server...."

  if [[ -d "$_hgrepo" ]]; then
    cd "$_hgrepo"
    hg pull -u
    msg "The local files are updated."
  else
    hg clone "$_hgroot" "$_hgrepo"
  fi

  msg "Mercurial checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_hgrepo-build"
  cp -r "$srcdir/$_hgrepo" "$srcdir/$_hgrepo-build"
  cd "$srcdir/$_hgrepo-build"
}

package() {
  cd "$srcdir/$_hgrepo-build"
  python setup.py install --root="$pkgdir/" --optimize=1
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
}

# vim:set ts=2 sw=2 et:
