# Maintainer: Yuri Bochkarev <baltazar dot bz gmail at com>
_hkgname=vcs-revision
pkgname=haskell-$_hkgname
pkgver=0.0.1
pkgrel=1
pkgdesc="Facilities for accessing the version control revision of the current directory"
arch=('any')
url="http://hackage.haskell.org/package/$_hkgname"
license=('GPL')
depends=()
makedepends=('ghc')
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=$pkgname.install
source=(http://hackage.haskell.org/packages/archive/$_hkgname/$pkgver/$_hkgname-$pkgver.tar.gz)
md5sums=('cd2c6f7b2c3f26512effbfa48ed8a06f')
build() {
	cd "$srcdir/$_hkgname-$pkgver"

	runhaskell Setup configure -O -p --enable-split-objs --enable-shared \
		--prefix=/usr --docdir="/usr/share/doc/$pkgname" \
		--libsubdir=\$compiler/site-local/\$pkgid
	runhaskell Setup build
	runhaskell Setup haddock
	runhaskell Setup register   --gen-script
	runhaskell Setup unregister --gen-script
	sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}

package() {
	cd "$srcdir/$_hkgname-$pkgver"

	install -D -m744 register.sh   "$pkgdir/usr/share/haskell/$pkgname/register.sh"
	install	   -m744 unregister.sh "$pkgdir/usr/share/haskell/$pkgname/unregister.sh"
	install -d -m755 "$pkgdir/usr/share/doc/ghc/html/libraries"
	ln -s "/usr/share/doc/$pkgname/html" "$pkgdir/usr/share/doc/ghc/html/libraries/$_hkgname"
	runhaskell Setup copy --destdir="$pkgdir"
}

# vim:set ts=2 sw=2 et:
