# Maintainer: Bardia Moshiri <fakeshell@bardia.tech>

pkgname=pulseaudio-modules-nemo
pkgver=14.2
pkgrel=2
pkgdesc="PulseAudio modules for Nemo"
arch=('x86_64' 'aarch64')
url="https://github.com/sailfishos/pulseaudio-modules-nemo"
license=('LGPLv2+')
depends=('alsa-lib' 'pulseaudio-hybris')
makedepends=('meson' 'pulsecore-headers' 'check')
source=('pulseaudio-modules-nemo::git+https://github.com/sailfishos/pulseaudio-modules-nemo'
        'module-version.patch')
sha256sums=('SKIP'
            '1762c6ec7949add66f64c12839579ce25aae63ce1ddbdcf87b5a62fac30e2af0')

prepare() {
    cd pulseaudio-modules-nemo
    echo "14.2" > .tarball-version

    local src
    for src in "${source[@]}"; do
      src="${src%%::*}"
      src="${src##*/}"
      [[ $src = *.patch ]] || continue
      echo "Applying patch $src..."
      patch -Np1 < "../$src"
    done
}

build() {
    meson setup --prefix=/usr --buildtype=plain pulseaudio-modules-nemo build
    meson compile -C build
}

package() {
    meson install -C build --destdir "$pkgdir"
}
