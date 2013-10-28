# Contributor: heithe <heithe01 [at] g m a i l [dot] com>
pkgname=mkinitcpio-ngencrypt
pkgver=1
pkgrel=1
pkgdesc="Rewritten extended mkinitcpio encrypt hook"
arch=(any)
url="https://github.com/heithe/mkinitcpio-ngencrypt"
license=('MIT')
depends=(mkinitcpio cryptsetup)
install=${pkgname}.install
source=(mkinitcpio-ngencrypt_hook mkinitcpio-ngencrypt_install)

package() {
    install -o root -g root -D ${srcdir}/mkinitcpio-ngencrypt_install ${pkgdir}/lib/initcpio/install/ngencrypt
    install -o root -g root -D ${srcdir}/mkinitcpio-ngencrypt_hook ${pkgdir}/lib/initcpio/hooks/ngencrypt
}

sha512sums=('8ec42e4c62c4b290c638e0cf979b4c244b16e6ffae18f349b3a0cb0215122f06ab1451088bf63b3f81975ccfa401030f0c7304b12616ac4a54d3e4e4951573dc' 
            '327dba773ea8e4426b35e2966b9236390392de39ef60749770d43717e0768a15d6b50c289c3c95523920b953ef5b3427d771385eb88ce618d30cdb3cae9a6937')