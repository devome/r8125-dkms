# Maintainer: Evine Deng <evinedeng@hotmail.com>

_pkgname=r8125
pkgname="${_pkgname}-dkms"
pkgver=9.016.01
pkgrel=2
priority=optional
section=non-free/kernel
url="https://www.realtek.com/Download/List?cate_id=584"
pkgdesc="dkms source for the r8125 network driver"
license=('GPL-2.0-only')
arch=('all')
depends=('dkms')
provides=("${pkgname}")
conflicts=("${pkgname}" "realtek-${pkgname}")
replaces=("realtek-${pkgname}")
postinst="postinst.sh"
prerm="prerm.sh"
optdepends=('linux-headers-amd64: Build the module for Debian kernel'
            'proxmox-default-headers: Build the module for Proxmox VE kernel')
source=("http://rtitwww.realtek.com/rtdrivers/cn/nic1/${_pkgname}-${pkgver}.tar.bz2"
        "kernel-6.17.patch"
        "dkms.conf")
sha256sums=('5434b26500538a62541c55cd09eea099177f59bd9cc48d16969089a9bcdbbd41'
            '1bf140a02a53afb3820b3b35c1c0c83a581dc7db83ede2299f2683b1ea080122'
            'afb4b4a62803309448ea698fb316d405337866ae3d7206ce52e9470c07c4a634')

prepare() {
    cd "${_pkgname}-${pkgver}"
    rm src/Makefile_linux24x
    sed -e "s|@PKGVER@|${pkgver}|g" ../dkms.conf > src/dkms.conf
    patch -Np1 -i ../kernel-6.17.patch
}

package() {
    cd "${_pkgname}-${pkgver}"
    install -Dm644 -t "${pkgdir}/usr/share/doc/${pkgname}"      README
    install -Dm644 -t "${pkgdir}/usr/src/${_pkgname}-${pkgver}" src/*
}
