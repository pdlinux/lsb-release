# Maintainer : Daniel Bermond <dbermond@archlinux.org>
# Contributor: Jonas Witschel <diabonas@archlinux.org>
# Contributor: Sven-Hendrik Haase <sh@lutzhaase.com>
# Contributor: Malte Rabenseifner <malte@zearan.de>
# Contributor: John Gerritse <reaphsharc@gmail.com>

pkgname=lsb-release
pkgver=2.0.r55.a25a4fc
_commit=a25a4fcd73c79bd5af0dd8d948a7c96dcbfd2d07
pkgrel=1
pkgdesc='LSB version query program'
arch=('any')
url='https://refspecs.linuxfoundation.org/lsb.shtml'
license=('GPL-2.0-or-later')
depends=('sh')
makedepends=('git')
source=("git+https://github.com/LinuxStandardBase/lsb-samples.git#commit=${_commit}"
        'lsb-release'
        'lsb_release_make_man_page_reproducible.patch')
sha256sums=('924805b889f49c88691c7894ddb43fd7750a76aaf44657e5f282f7347d6e3b60'
            'b68bca433bb6b36e7d285daf52a8b93f9a284ecede61aded2e25ec6f78b134af'
            'a1e9323e991cdc6d1183d2faf158fbd358feb4ce73046227d5c932f6660925cf')

pkgver() {
	cd lsb-samples/lsb_release/src
	printf '%s.r%s.%s' "$(grep -Po 'SCRIPTVERSION="\K[^"]*' lsb_release)" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
	patch -d lsb-samples/lsb_release/src -Np1 -i "${srcdir}/lsb_release_make_man_page_reproducible.patch"
}

build() {
	make -C lsb-samples/lsb_release/src
}

package() {
	install -D -m755 lsb-samples/lsb_release/src/lsb_release -t "${pkgdir}/usr/bin"
	install -D -m644 lsb-samples/lsb_release/src/lsb_release.1.gz -t "${pkgdir}/usr/share/man/man1"
	install -D -m644 lsb-release -t "${pkgdir}/etc"
}
