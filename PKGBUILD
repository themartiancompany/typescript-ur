# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>
# Contributor: Bruno Galeotti <bgaleotti at gmail dot com>

_name=TypeScript
pkgname=typescript
pkgver=5.1.3
pkgrel=1
pkgdesc='JavaScript with syntax for types'
arch=('any')
url=http://www.typescriptlang.org
license=('Apache')
depends=('nodejs')
makedepends=('npm' 'rsync')
source=("https://github.com/microsoft/$_name/archive/v$pkgver/$pkgname-$pkgver.tar.gz")
b2sums=('61d60574aeb94a00df33015517d0613f2e625ebc346bb82516c91529814f1378a1f2864088b480df66ad50b261f85635bccbb27b2b5b1b072d48f87795ef081e')

prepare() {
  cd $_name-$pkgver
  npm ci
}

build() {
  cd $_name-$pkgver
  npx hereby LKG
}

check() {
  cd $_name-$pkgver
  npm run test
}

package() {
  install -d "$pkgdir"/usr/{bin,lib/node_modules/$pkgname}
  ln -s ../lib/node_modules/$pkgname/bin/{tsc,tsserver} "$pkgdir"/usr/bin

  cd $_name-$pkgver
  rsync -r --exclude .gitattributes README.md SECURITY.md bin lib package.json \
    "$pkgdir"/usr/lib/node_modules/$pkgname
  install -Dt "$pkgdir"/usr/share/licenses/$pkgname ThirdPartyNoticeText.txt
}
