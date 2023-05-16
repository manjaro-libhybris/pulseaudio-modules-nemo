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
            'bc304be0394b1a2b9c30beee493d7a4d50cf850db38c14821fdb80a8d2c5590f')

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
