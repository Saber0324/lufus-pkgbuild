# Maintainer: hog185 <hogman12333@gmail.com>
pkgname=lufus-git
pkgver=r199.c2b2f7d
pkgrel=1
pkgdesc="Physical drive imaging and formatting utility for Linux written in Python"
arch=('any')
url="https://github.com/Hog185/Lufus"
license=('MIT')
depends=(
    'python'
    'python-psutil'
    'python-pyqt6'
    'python-pyudev'
)
makedepends=(
    'git'
    'uv'
    'python-installer'
)
provides=('lufus')
conflicts=('lufus')
source=("$pkgname::git+https://github.com/Hog185/Lufus.git"
        "lufus.desktop")
sha256sums=('SKIP' 'SKIP')

pkgver() {
    cd "$pkgname"
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
    cd "$pkgname"
    UV_NO_SYNC=1 uv build --wheel --no-sources
}

package() {
    cd "$pkgname"
    python -m installer --destdir="$pkgdir" dist/*.whl
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README"
    install -Dm644 ../lufus.desktop "$pkgdir/usr/share/applications/lufus.desktop"

    install -Dm755 /dev/stdin "$pkgdir/usr/bin/lufus" << 'EOF'
#!/usr/bin/env python
from lufus.__main__ import main
main()
EOF
}
