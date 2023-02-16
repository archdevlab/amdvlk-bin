# _     _            _        _          _____
#| |__ | | __ _  ___| | _____| | ___   _|___ /
#| '_ \| |/ _` |/ __| |/ / __| |/ / | | | |_ \
#| |_) | | (_| | (__|   <\__ \   <| |_| |___) |
#|_.__/|_|\__,_|\___|_|\_\___/_|\_\\__, |____/
#                                  |___/

#Maintainer: blacksky3 <https://github.com/blacksky3>

major=2023.Q1.1

pkgbase=amdvlk
pkgname=(amdvlk lib32-amdvlk)
pkgver=${major}
pkgrel=1
arch=(x86_64)
url='https://github.com/GPUOpen-Drivers/AMDVLK'
license=(MIT)
source=(https://github.com/GPUOpen-Drivers/AMDVLK/releases/download/v-${major}/amdvlk_${major}_amd64.deb
        https://github.com/GPUOpen-Drivers/AMDVLK/releases/download/v-${major}/amdvlk_${major}_i386.deb)

# extracts a debian package
# $1: deb file to extract
extract_deb(){
  local tmpdir="$(basename "${1%.deb}")"
  rm -Rf "$tmpdir"
  mkdir "$tmpdir"
  cd "$tmpdir"
  ar x "$1"
  tar -C "${pkgdir}" -xf data.tar.gz
}

# move ubuntu specific /usr/lib/x86_64-linux-gnu to /usr/lib
# $1: debian package library dir (goes from opt/amdgpu or opt/amdgpu-pro and from x86_64 or i386)
# $2: arch package library dir (goes to usr/lib or usr/lib32)
move_libdir(){
  local deb_libdir="$1"
  local arch_libdir="$2"

  if [ -d "${pkgdir}/${deb_libdir}" ]; then
    if [ ! -d "${pkgdir}/${arch_libdir}" ]; then
      mkdir -p "${pkgdir}/${arch_libdir}"
    fi
    mv -t "${pkgdir}/${arch_libdir}/" "${pkgdir}/${deb_libdir}"/*
    find ${pkgdir} -type d -empty -delete
  fi
}

rm -rf "$pkgdir"/usr/share/doc# move copyright file to proper place and remove debian changelog
move_copyright(){
  find ${pkgdir}/usr/share/doc -name "changelog.Debian.gz" -delete
  mkdir -p ${pkgdir}/usr/share/licenses/${pkgname}
  find ${pkgdir}/usr/share/doc -name "copyright" -exec mv {} ${pkgdir}/usr/share/licenses/${pkgname} \;
  find ${pkgdir}/usr/share/doc -type d -empty -delete
}

package_amdvlk(){
  pkgdesc="AMD's standalone Vulkan driver"

  extract_deb "${srcdir}"/amdvlk_${major}_amd64.deb
  move_libdir "usr/lib/x86_64-linux-gnu" "usr/lib"
  move_libdir "etc" "usr/share"
  sed -i 's|/x86_64-linux-gnu||' "$pkgdir/"usr/share/vulkan/icd.d/amd_icd64.json
  sed -i 's|/x86_64-linux-gnu||' "$pkgdir/"usr/share/vulkan/implicit_layer.d/amd_icd64.json
  mv "$pkgdir/"usr/share/vulkan/implicit_layer.d/amd_icd64.json "$pkgdir/"usr/share/vulkan/implicit_layer.d/amd_icd64.json.hide
  move_copyright
  mv "$pkgdir"/usr/share/doc/amdvlk/LICENSE.txt "$pkgdir"/usr/share/licenses/amdvlk/
  rm -rf "$pkgdir"/usr/share/doc
}

package_lib32-amdvlk(){
  pkgdesc="AMD's standalone Vulkan driver (32-bit)"

  extract_deb "${srcdir}"/amdvlk_${major}_i386.deb
  move_libdir "usr/lib/i386-linux-gnu" "usr/lib32"
  move_libdir "etc" "usr/share"
  sed -i 's|/i386-linux-gnu||' "$pkgdir/"usr/share/vulkan/icd.d/amd_icd32.json
  sed -i 's|/lib|/lib32|' "$pkgdir/"usr/share/vulkan/icd.d/amd_icd32.json
  sed -i 's|/i386-linux-gnu||' "$pkgdir/"usr/share/vulkan/implicit_layer.d/amd_icd32.json
  sed -i 's|/lib|/lib32|' "$pkgdir/"usr/share/vulkan/implicit_layer.d/amd_icd32.json
  mv "$pkgdir/"usr/share/vulkan/implicit_layer.d/amd_icd32.json "$pkgdir/"usr/share/vulkan/implicit_layer.d/amd_icd32.json.hide
  move_copyright
  mv "$pkgdir"/usr/share/doc/amdvlk/LICENSE.txt "$pkgdir"/usr/share/licenses/lib32-amdvlk/
  rm -rf "$pkgdir"/usr/share/doc
}

sha256sums=('102a0b16fb24330e436e844182e919e9d8798f247a458e25a13776c657a7db68'
            'c919444deae07b23e8c293838ebf1790a6e9a1c50200c6539bb7c96bc3965f1b')
