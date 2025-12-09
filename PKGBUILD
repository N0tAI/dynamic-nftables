# Maintainer: Thayen <thayen@thayen.ca>
pkgname=custom-nftables
pkgver=1.0.3
pkgrel=1
pkgdesc="Modular nftables configuration with dynamic service support"
arch=('any')
license=('MIT')
depends=('nftables')
source=(
    'base.conf'
    '00-core.nft'
    '10-static.nft'
    '99-catchall.nft'
    'nft-rule@.service'
    'custom-path.conf'
    'gen-nftable'
    'nftables-runtime.conf'
)
sha256sums=(
    'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP'
)

package() {
    install -Dm644 "$srcdir/00-core.nft" "$pkgdir/usr/lib/nftables/static/00-core.nft"
    install -Dm644 "$srcdir/10-static.nft" "$pkgdir/usr/lib/nftables/static/10-static.nft"
    install -Dm644 "$srcdir/99-catchall.nft" "$pkgdir/usr/lib/nftables/static/99-catchall.nft"
    install -Dm755 "$srcdir/gen-nftable" "$pkgdir/usr/lib/nftables/gen-nftable"

    install -Dm644 "$srcdir/nftables-runtime.conf" "$pkgdir/usr/lib/tmpfiles.d/nftables-runtime.conf"

    # /etc/nftables/static is for your local overrides
    # /etc/nftables/dynamic is for the systemd service files
    install -d "$pkgdir/etc/nftables/static"
    install -d "$pkgdir/etc/nftables/dynamic"

    install -Dm644 "$srcdir/nft-rule@.service" "$pkgdir/usr/lib/systemd/system/nft-rule@.service"
    install -Dm644 "$srcdir/custom-path.conf" "$pkgdir/usr/lib/systemd/system/nftables.service.d/custom-path.conf"

    # install -Dm644 "$srcdir/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
