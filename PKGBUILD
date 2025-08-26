pkgname=inetutils
pkgver=2.6
pkgrel=1
pkgdesc="A collection of common network programs"
arch=('x86_64')
url="https://www.gnu.org/software/inetutils/"
license=('GPL-3.0-or-later')
groups=('base')
depends=(
    'glibc'
    'readline'
    'ncurses'
)
options=('!emptydirs' '!lto')
source=(https://ftp.gnu.org/gnu/${pkgname}/${pkgname}-${pkgver}.tar.xz)
sha256sums=(68bedbfeaf73f7d86be2a7d99bcfbd4093d829f52770893919ae174c0b2357ca)

prepare() {
    cd ${pkgname}-${pkgver}

    sed -i 's/def HAVE_TERMCAP_TGETENT/ 1/' telnet/telnet.c
}

build() {
    cd ${pkgname}-${pkgver}

    local configure_args=(
        --bindir=/usr/bin
        --localstatedir=/var
        --disable-logger
        --disable-whois
        --disable-rcp
        --disable-rexec
        --disable-rlogin
        --disable-rsh
        --disable-servers
        ${configure_options}
    )

    ./configure "${configure_args[@]}"

    make
}

package() {
    cd ${pkgname}-${pkgver}

    make DESTDIR=${pkgdir} install
}
