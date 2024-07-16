# Maintainer: Raihan Ahamed <raihan1999ahamed@gmail.com>
# Maintainer: Fabian Bornschein <fabiscafe@archlinux.org>
# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
_mode=host
_crossdirect=false
pkgname=gnome-settings-daemon-mobile
pkgdesc="GNOME Settings Daemon Mobile"
pkgver=46.0
pkgrel=2
_arches=specific
arch=(
    any
)
license=(
    GPL-2.0-or-later
    LGPL-2.0-or-later
)
url="https://gitlab.gnome.org/verdre/gnome-settings-daemon-mobile.git"
depends=(
    alsa-lib
    bash
    cairo
    dconf
    fontconfig
    gcc-libs
    gcr-4
    geoclue
    geocode-glib-2
    glib2
    glibc
    gnome-desktop
    gsettings-desktop-schemas
    gtk3
    libcanberra-pulse
    libcolord
    libcups
    libgudev
    libgweather-4
    libmm-glib
    libnm
    libnotify
    libp11-kit
    libpulse
    librsvg
    libwacom
    libx11
    libxext
    libxfixes
    libxi
    nss
    pango
    polkit
    pulse-native-provider
    systemd
    systemd-libs
    upower
    wayland
    xorg-xrdb
)
makedepends=(
    docbook-xsl
    git
    glib2-devel
    libxslt
    meson
    python
    usbguard
)
checkdepends=(
    python-dbusmock
    python-gobject
)
optdepends=('usbguard: USB protection support')
groups=(gnome)
backup=(etc/xdg/Xwayland-session.d/00-xrdb)
_commit=ee5d1b246da9ac5bdd635e3d5afb322ecacc3912 # 46-mobile-0
source=(
    "git+https://gitlab.gnome.org/verdre/gnome-settings-daemon-mobile.git#commit=$_commit"
    "git+https://gitlab.gnome.org/GNOME/libgnome-volume-control.git"
    0001-subprojects-Update-gvc-to-latest-commit.patch
)
sha256sums=(
    SKIP
    SKIP
    SKIP
)

prepare() {
    cd $pkgname
    git describe --long --tags --abbrev=7 "$_commit" | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
    git apply -3 ../0001-subprojects-Update-gvc-to-latest-commit.patch

    git submodule init
    git submodule set-url subprojects/gvc "$srcdir/libgnome-volume-control"
    git -c protocol.file.allow=always -c protocol.allow=never submodule update
}

build() {
    arch-meson $pkgname build
    meson compile -C build
}

check() {
    meson test -C build --print-errorlogs
}

package() {
    meson install -C build --destdir "$pkgdir"
}

# vim:set sw=2 sts=-1 et:
