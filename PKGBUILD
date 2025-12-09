# Maintainer: Thayen <thayen@thayen.ca>
pkgname=nftables-custom-config
pkgver=1.0.0
pkgrel=1
pkgdesc="Modular nftables configuration with dynamic service support"
arch=('any')
license=('MIT')
depends=('nftables')
source=(
    'nftables.conf'
    '00-core.nft'
    '10-static.nft'
    '99-catchall.nft'
    'nft-rule@.service'
    'custom-path.conf'
)
sha256sums=(
    'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP'
)

package() {
    # 1. Install the Main Loader
    install -Dm644 "$srcdir/nftables.conf" "$pkgdir/etc/nftables/nftables.conf"

    # 2. Install Base Rules (into /etc/nftables/static/)
    install -Dm644 "$srcdir/00-core.nft" "$pkgdir/etc/nftables/static/00-core.nft"
    install -Dm644 "$srcdir/10-static.nft" "$pkgdir/etc/nftables/static/10-static.nft"
    install -Dm644 "$srcdir/99-catchall.nft" "$pkgdir/etc/nftables/static/99-catchall.nft"

    # 3. Create the Dynamic Directory (Empty)
    install -d "$pkgdir/etc/nftables/dynamic"

    # 4. Install the Dynamic Service Template
    install -Dm644 "$srcdir/nft-rule@.service" "$pkgdir/usr/lib/systemd/system/nft-rule@.service"

    # 5. Install the Service Override (Drop-in)
    # We install to /usr/lib to avoid cluttering /etc, acting as a "vendor" supplied config
    install -Dm644 "$srcdir/custom-path.conf" "$pkgdir/usr/lib/systemd/system/nftables.service.d/custom-path.conf"

    # 6. Safety: Prevent overwriting your live config on update
    backup=(
        'etc/nftables/nftables.conf'
        'etc/nftables/static/00-core.nft'
        'etc/nftables/static/10-static.nft'
        'etc/nftables/static/99-catchall.nft'
    )
}
