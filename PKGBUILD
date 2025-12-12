# Maintainer: Thayen <thayen@thayen.ca>
pkgname=custom-nftables
pkgver=1.1.0
pkgrel=1
pkgdesc="Modular nftables configuration with dynamic service support"
arch=('any')
license=('MIT')
depends=('nftables')
source=(
    '00-core.nft'
    '50-dynamic-rules.nft'
    '99-catchall.nft'
    'gen-nftable'
    'custom-nftables.conf'
    'nft-input-rule@.service'
    'nft-output-rule@.service'
    'nft-forward-rule@.service'
    'nftables-dropin.conf'
)
sha256sums=(
    'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP'
)

package() {
    install -Dm644 "$srcdir/00-core.nft" "$pkgdir/usr/lib/nftables/static/00-core.nft"
    install -Dm644 "$srcdir/50-dynamic-rules.nft" "$pkgdir/usr/lib/nftables/static/50-dynamic-rules.nft"
    install -Dm644 "$srcdir/99-catchall.nft" "$pkgdir/usr/lib/nftables/static/99-catchall.nft"
    install -Dm755 "$srcdir/gen-nftable" "$pkgdir/usr/lib/nftables/gen-nftable"

    install -Dm644 "$srcdir/custom-nftables.conf" "$pkgdir/usr/lib/tmpfiles.d/custom-nftables.conf"

    install -d "$pkgdir/etc/nftables/static"
    install -d "$pkgdir/etc/nftables/dynamic"

    install -Dm644 "$srcdir/nft-input-rule@.service" "$pkgdir/usr/lib/systemd/system/nft-input-rule@.service"
    install -Dm644 "$srcdir/nft-output-rule@.service" "$pkgdir/usr/lib/systemd/system/nft-output-rule@.service"
    install -Dm644 "$srcdir/nft-forward-rule@.service" "$pkgdir/usr/lib/systemd/system/nft-forward-rule@.service"
    install -Dm644 "$srcdir/nftables-dropin.conf" "$pkgdir/usr/lib/systemd/system/nftables.service.d/nftables-dropin.conf"
}
