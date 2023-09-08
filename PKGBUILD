# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Mark Wagie <mark at manjaro dot org>
# Contributor: Helmut Stult

# Arch credits:
# Maintainer: Giancarlo Razzolini <grazzolini@archlinux.org>
# Maintainer: Morten Linderud <foxboron@archlinux.org>
# Contributor: Dave Reisner <dreisner@archlinux.org>
# Contributor: Thomas Bächler <thomas@archlinux.org>

pkgname=mkinitcpio
pkgver=36
pkgrel=6
pkgdesc="Modular initramfs image creation utility"
arch=('any')
url='https://gitlab.archlinux.org/archlinux/mkinitcpio/mkinitcpio'
license=('GPL')
depends=('awk' 'mkinitcpio-busybox>=1.19.4-2' 'kmod' 'util-linux>=2.23' 'libarchive' 'coreutils'
         'bash' 'binutils' 'diffutils' 'findutils' 'grep' 'filesystem>=2011.10-1' 'gzip' 'systemd')
makedepends=('asciidoc')
checkdepends=('bash-bats' 'bash-bats-assert' 'lzop')
optdepends=('zstd: Use zstd compression for the initramfs image'
            'xz: Use lzma or xz compression for the initramfs image'
            'bzip2: Use bzip2 compression for the initramfs image'
            'lzop: Use lzo compression for the initramfs image'
            'lz4: Use lz4 compression for the initramfs image'
            'mkinitcpio-nfs-utils: Support for root filesystem on NFS')
provides=('initramfs')
backup=('etc/mkinitcpio.conf')
source=("https://sources.archlinux.org/other/$pkgname/$pkgname-$pkgver.tar.gz"{,.sig}
        'https://gitlab.archlinux.org/archlinux/mkinitcpio/mkinitcpio/-/merge_requests/250.patch'
        'https://gitlab.archlinux.org/archlinux/mkinitcpio/mkinitcpio/-/merge_requests/251.patch'
        # Manjaro patches
        'manjaro.patch'
        'revert-ab6bad7.patch'
        )
install=mkinitcpio.install
sha256sums=('7b3b1cdf546922f47845a3ac4353ca97899a4bb68cfff29098c45135e5fb8b5e'
            'SKIP'
            'af5ed525f15ae687abff1e806c2b01b6aaf4c9e27c0ccd1da77771621671eccb'
            '4a6bd157911116ec41a0eaf85e8cf8dc9c083cd622123a06074c81a8c23492a8'
            'd2c2d58392b21c5505ef9ac0dfa56389f380f5493fdbdf0f7f40e29fd65a604c'
            '257444ea4ffe7ea0d003ce79b21957a850ef08ee768c758668bb0f15f41afee5')
validpgpkeys=('ECCAC84C1BA08A6CC8E63FBBF22FB1D78A77AEAB'    # Giancarlo Razzolini
              'C100346676634E80C940FB9E9C02FF419FECBE16')   # Morten Linderud

prepare() {
  cd "$pkgname-$pkgver"
  local src
  for src in "${source[@]}"; do
      src="${src%%::*}"
      src="${src##*/}"
      [[ $src = *.patch ]] || continue
      echo "Applying patch $src..."
      patch -Np1 < "../$src"
  done
}

check() {
  make -C "$pkgname-$pkgver" check
}

package() {
  make -C "$pkgname-$pkgver" DESTDIR="$pkgdir" install
}
