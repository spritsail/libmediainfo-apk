# Contributor: Carlo Landmeter <clandmeter@gmail.com>
# Maintainer: Corey Oliver <corey.jon.oliver@gmail.com>

# Bundled libraries used in the package:
#
# Name         | License       | Location
# -------------+---------------+---------
# aes-gladman  | custom / GPL  | Source/ThirdParty/aes-gladman
# base64       | unknown       | Source/ThirdParty/base64
# hmac-gladman | custom / GPL  | Source/ThirdParty/hmac-gladman
# md5          | Public domain | Source/ThirdParty/md5
# sha1-gladman | custom / GPL  | Source/ThirdParty/sha1-gladman
# sha2-gladman | custom / GPL  | Source/ThirdParty/sha2-gladman

pkgname=libmediainfo-patched
pkgver=18.05
pkgrel=0
pkgdesc="Shared library for mediainfo"
url="https://github.com/MediaArea/MediaInfoLib"
arch="all"
license="BSD-2-Clause"
depends_dev="zlib-dev"
makedepends="$depends_dev cmake curl-dev libmms-dev libzen-dev tinyxml2-dev"
subpackages="$pkgname-dev"
conflicts="${pkgname%%-*}"
source="https://mediaarea.net/download/source/libmediainfo/$pkgver/libmediainfo_$pkgver.tar.xz 0001-Fix-float64-rounding-stack-overflow.patch"
builddir="$srcdir/MediaInfoLib"
_cmakedir="$builddir/Project/CMake"
options="!check"  # upstream does not provide tests

prepare() {
	# Fix DOS line endings for patching
	find . \( -name '*.cpp' -o -name '*.hpp' -o -name '*.h' \) -exec dos2unix {} \;

	default_prepare
	cd "$builddir"

	rm -rf Project/MS*

	# Make sure that these bundled libs are not used.
	rm -R Project/zlib
	rm -R Source/ThirdParty/tinyxml2

}

build() {
	cd "$_cmakedir"

	cmake \
		-DCMAKE_BUILD_TYPE=Release \
		-DCMAKE_INSTALL_PREFIX=/usr \
		-DCMAKE_VERBOSE_MAKEFILE=ON \
		-DBUILD_SHARED_LIBS=ON
	make
}

package() {
	cd "$_cmakedir"

	make DESTDIR="$pkgdir" install
}

sha512sums="47d03380197f105bbd2e575558f4b4c1fade8c350af0f69a807c042abbf3aa02413fa88c047988f47cef77240e1106800a1dfd4ef1b41a1ceb019e3d52979901  libmediainfo_18.05.tar.xz
fe3a39d3f137eb6010f64ec2b23b4b46f083e8443df4224e72c517d5616cbf168daba307efa57af8f69ca2302ffceb16d6cd4955c81875c52e8cbb41b97e7360  0001-Fix-float64-rounding-stack-overflow.patch"
