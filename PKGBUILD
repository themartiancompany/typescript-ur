# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Bruno Galeotti <bgaleotti at gmail dot com>

pkgname=typescript
pkgver=2.5.2
pkgrel=1
pkgdesc="TypeScript is a language for application scale JavaScript development"
arch=('any')
url="http://typescriptlang.org/"
license=('Apache')
depends=('nodejs')
makedepends=('npm')
source=(https://registry.npmjs.org/$pkgname/-/$pkgname-$pkgver.tgz)
noextract=($pkgname-$pkgver.tgz)
sha512sums=('7c4c5dd7332527fc50b0d9dafcff4eb1d37cf21a8174180a36182a2b889ec027b805a20e00ef652bafcb0f3c209821470a8435e142ddc672d49908f3bbf6326f')

package() {
  npm install -g --user root --prefix "$pkgdir"/usr "$srcdir"/$pkgname-$pkgver.tgz
  rm -r "$pkgdir"/usr/etc
}

# vim:set ts=2 sw=2 et:
