# Maintainer: Nikos Toutountzoglou <nikos.toutou@gmail.com>

pkgname=anarchychess
pkgver=0.3.0
pkgrel=1
pkgdesc="DreamChess is an open source chess game. It comes with its own engine called Dreamer."
arch=('i686' 'x86_64')
url="https://github.com/PossibleEmuWrangler/AnarchyChess-DreamyDesktopPrototype"
license=('GPL3')
depends=('sdl2' 'sdl2_image' 'sdl2_mixer' 'expat' 'glew')
makedepends=('flex' 'bison' 'cmake')
provides=('dreamchess')
conflicts=('dreamchess')
source=("anarchychess::git+https://github.com/PossibleEmuWrangler/AnarchyChess-DreamyDesktopPrototype" config.h.in)
sha256sums=('SKIP' '7f86e7ff1251750fc504fc2cecb6a15dd761b1c215d9509b2e2104d09a423475')

pkgver() {
	cd "anarchychess"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
}

prepare() {
	mv $srcdir/anarchychess/CMakeLists.txt $srcdir/anarchychess/CMakeLists.txt.old
	grep -v try_compile $srcdir/anarchychess/CMakeLists.txt.old > $srcdir/anarchychess/CMakeLists.txt
	rm $srcdir/anarchychess/CMakeLists.txt.old
	cp $srcdir/config.h.in $srcdir/anarchychess
}

build() {
        cd "$srcdir/anarchychess/cmake"
        cmake -DCMAKE_INSTALL_PREFIX=/usr ..
        make
}

package() {
        cd "$srcdir/anarchychess/cmake"
        make DESTDIR="$pkgdir/" install
}
