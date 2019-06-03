# Maintainer: Eric Berquist <eric DOT berquist AT gmail>
# Contributor: steabert <steabert@member.fsf.org>
# Contributor: Ricardo Honorato Z.

pkgname=vmd
pkgver=1.9.3
pkgrel=1
pkgdesc="Visual Molecular Dynamics"
url="http://www.ks.uiuc.edu/Research/vmd/"
license=('custom')
arch=('x86_64')
depends=('tcsh' 'perl' 'libxi' 'tcl' 'libxinerama' 'libgl' 'glu')
makedepends=('make')
optdepends=('netcdf: MMTK and AMBER 9 trajectories support'
            'openbabel: additional file formats support'
            'sqlite: dmsplugin')
# You MUST download the package from the VMD url and put it in the PKGBUILD folder!
# Current download should be:
# LINUX_64 OpenGL, CUDA, OptiX, OSPRay (Linux (RHEL 6.7 and later) 64-bit Intel/AMD x86_64 SSE, with CUDA 9.x, OptiX, OSPRay)
source=("local://${pkgname}-${pkgver}.bin.LINUXAMD64-CUDA8-OptiX4-OSPRay111p1.opengl.tar.gz"
        'local://catdcd')
md5sums=('8c10525a79a496beedf1f27fcdcb88b2'
         'd930f06c1d58a31264396f4f84de7b67')

package() {
  cd $srcdir/${pkgname}-${pkgver}
  install -D -m644 LICENSE ${pkgdir}/usr/share/licenses/$pkgname/LICENSE
  export VMDINSTALLBINDIR="${pkgdir}/usr/bin"
  export VMDINSTALLLIBRARYDIR="${pkgdir}/usr/lib/vmd"
  ./configure
  cd src; make install
  sed -i 's|set defaultvmddir=.*|set defaultvmddir=/usr/lib/vmd|' "${pkgdir}/usr/bin/vmd"

  # prepare directories
  mkdir -p ${pkgdir}/usr/bin

  # Executable files
  # install -Dm 755 ${pkgdir}/usr/lib/vmd/plugins/LINUXAMD64/bin/catdcd5.1/catdcd "${pkgdir}"/usr/bin/

  # Install wrapers to avoid install the libraries
  install -Dm755 ${srcdir}/catdcd ${pkgdir}/usr/bin/catdcd

}
