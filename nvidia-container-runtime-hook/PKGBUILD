_srcdir='nvidia-container-runtime-1.4.0-1'
pkgname=nvidia-container-runtime-hook
pkgver=1.4.0
pkgrel=2
pkgdesc='NVIDIA container runtime hook'
arch=('x86_64')
url='https://github.com/NVIDIA/nvidia-container-runtime'
license=('custom')
depends=('libnvidia-container-tools')
makedepends=('go')
source_x86_64=('https://github.com/NVIDIA/nvidia-container-runtime/archive/v1.4.0-1.tar.gz')
sha256sums_x86_64=('4266ae78717301ad6e38ee700a7600b908c323a7d99ea913e816e06882d1de1a')

prepare() {
  mkdir -p gopath/src
  ln -rTsf "${_srcdir}/hook/nvidia-container-runtime-hook" "gopath/src/$pkgname"
}

build() {
  GOPATH="$srcdir/gopath" go install -buildmode=pie -ldflags " -s -w" "$pkgname"
}

package() {
  install -D -m755 "$srcdir/gopath/bin/nvidia-container-runtime-hook" "$pkgdir/usr/bin/nvidia-container-runtime-hook"
  install -D -m644 "${_srcdir}/hook/config.toml.centos" "$pkgdir/etc/nvidia-container-runtime/config.toml"
  install -D -m644 "${_srcdir}/LICENSE" "$pkgdir/usr/share/$pkgname/licenses/LICENSE"
}
