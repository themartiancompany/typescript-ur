# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Bruno Galeotti <bgaleotti at gmail dot com>

pkgname=typescript
pkgver=2.6.1
pkgrel=1
pkgdesc="TypeScript is a language for application scale JavaScript development"
arch=('any')
url="http://typescriptlang.org/"
license=('Apache')
depends=('nodejs')
makedepends=('npm')
source=(https://registry.npmjs.org/$pkgname/-/$pkgname-$pkgver.tgz)
noextract=($pkgname-$pkgver.tgz)
sha512sums=('b52db26c6a192971c9a8bfac916452474b7041fdc799519a318f2d35f39d8beb6f9663e8f8937f65801d66e201cc67cf5f1700161769e1f40ce8bc6aa94f5c8a')

package() {
  npm install -g --user root --prefix "$pkgdir"/usr "$srcdir"/$pkgname-$pkgver.tgz
  rm -r "$pkgdir"/usr/etc
}

# vim:set ts=2 sw=2 et:
