# Maintainer: xgdgsc <xgdgsc at gmail dot com>
# Maintainer: Alesandar Trifunović <akstrfn at gmail dot com>

pkgname=mendeleydesktop
pkgver=1.19.1
pkgrel=2
pkgdesc="Academic software for managing and sharing research papers (desktop client)"
url=http://www.mendeley.com/release-notes/
arch=(i686 x86_64)
depends=(qt5-webengine)
license=(custom:mendeley_eula)
source_i686=("https://desktop-download.mendeley.com/download/linux/$pkgname-$pkgver-linux-i486.tar.bz2")
source_x86_64=("https://desktop-download.mendeley.com/download/linux/$pkgname-$pkgver-linux-x86_64.tar.bz2")
sha512sums_i686=('8975d2a1ba3017c2f0dcb5cdd464d008913cddc76eae13b1cbb251adb4d77e77d8267f14b86ed4c3b7f1817316679e7e5a79618cf39154f662aed2173ced09c7')
sha512sums_x86_64=('fd9ecc4d907c267a0416b472931e08179cfd385a37573b6601227c1760cde935280517aea617e31910dbf029ade7dd78cf5a48236df94ce52b2030a0edb7ba11')

if [[ $CARCH = i686 ]];then
$CARCH=i486
fi

prepare() {
    cd "$pkgname-$pkgver-linux-$CARCH"

    # # Remove unneeded lines if gconf is not installed.
    # if ! which gconftool-2 &>/dev/null;then
    # sed -i '/GCONF/d' \
    #     "$pkgdir"/opt/"$pkgname"/bin/install-mendeley-link-handler.sh
    # fi
}

package() {
    cd "$pkgname-$pkgver-linux-$CARCH"

    install -d "$pkgdir/opt/$pkgname/"
    cp -a bin lib share "$pkgdir/opt/$pkgname/"

    install -d "$pkgdir"/usr/bin
    ln -s "/opt/$pkgname/bin/mendeleydesktop" \
          "$pkgdir/usr/bin/mendeleydesktop"

    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    install -Dm644 share/applications/mendeleydesktop.desktop \
                   "$pkgdir"/usr/share/applications/mendeleydesktop.desktop

    cp -a "$pkgdir/opt/$pkgname/share/icons" "$pkgdir/usr/share/icons"

    # Clean share from opt (don't remove mendeleydesktop)
    rm -rf "$pkgdir/opt/$pkgname/share/"{applications,doc,icons}
}
