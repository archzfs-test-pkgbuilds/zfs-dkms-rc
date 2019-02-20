# Maintainer: Jan Houben <jan@nexttrex.de>
# Contributor: Jesus Alvarez <jeezusjr at gmail dot com>
#
# This PKGBUILD was generated by the archzfs build scripts located at
#
# http://github.com/archzfs/archzfs
#
pkgname="zfs-dkms-rc"
pkgdesc="Kernel modules for the Zettabyte File System."

pkgver=0.8.0_rc3
pkgrel=1
makedepends=()
arch=("x86_64")
url="http://zfsonlinux.org/"
source=("https://github.com/zfsonlinux/zfs/releases/download/zfs-${pkgver/_/-}/zfs-${pkgver/_/-}.tar.gz"
        "upstream-4f981f6-additional-fixes-for-current_kernel_time-in-4.20.patch")
sha256sums=("5c344d6ff876d4c5286d83745700127054858cea379d31741fe96589ac40baff"
            "6f27c3dae57c424e06aec31df6c1e1a821e547aa4e933f2f9b894b5e6762b52d")
license=("CDDL")
depends=("zfs-utils-rc=${pkgver}" "lsb-release" "dkms")
provides=("zfs" "zfs-headers" "spl" "spl-headers")
groups=("archzfs-dkms-rc")
conflicts=("zfs" "zfs-headers" "spl" "spl-headers")

build() {
    cd "${srcdir}/zfs-${pkgver/_rc*/}"
    ./autogen.sh
}

package() {
    dkmsdir="${pkgdir}/usr/src/zfs-${pkgver}"
    install -d "${dkmsdir}"
    cp -a ${srcdir}/zfs-${pkgver/_rc*/}/. ${dkmsdir}
    cd "${dkmsdir}"
    find . -name ".git*" -print0 | xargs -0 rm -fr --
    scripts/dkms.mkconf -v ${pkgver} -f dkms.conf -n zfs
    chmod g-w,o-w -R .
}
