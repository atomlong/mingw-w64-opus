pkgname=mingw-w64-opus
pkgver=1.3
pkgrel=1
pkgdesc="Codec designed for interactive speech and audio transmission over the Internet (mingw-w64)"
arch=(any)
url="http://www.opus-codec.org"
license=("BSD")
makedepends=('mingw-w64-configure')
depends=('mingw-w64-crt')
options=('staticlibs' '!strip' '!buildflags')
source=("http://downloads.us.xiph.org/releases/opus/opus-$pkgver.tar.gz")
sha256sums=('4f3d69aefdf2dbaf9825408e452a8a414ffc60494c70633560700398820dc550')

_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

build() {
  cd "${srcdir}/opus-${pkgver}"
  for _arch in ${_architectures}; do
    mkdir -p build-${_arch} && pushd build-${_arch}
    ${_arch}-configure \
      --enable-custom-modes \
      --disable-doc \
      --disable-extra-programs
    make
    popd
  done
}

package() {
  for _arch in ${_architectures}; do
    cd "${srcdir}/opus-${pkgver}/build-${_arch}"
    make DESTDIR="$pkgdir" install
    rm -r "$pkgdir/usr/${_arch}/share"
    ${_arch}-strip --strip-unneeded "$pkgdir"/usr/${_arch}/bin/*.dll
    ${_arch}-strip -g "$pkgdir"/usr/${_arch}/lib/*.a
  done
}
