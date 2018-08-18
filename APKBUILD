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
pkgrel=1
pkgdesc="Shared library for mediainfo"
url="https://github.com/MediaArea/MediaInfoLib"
arch="all"
license="BSD-2-Clause"
depends_dev="zlib-dev"
makedepends="$depends_dev cmake curl-dev libmms-dev libzen-dev tinyxml2-dev"
subpackages="$pkgname-dev"
conflicts="${pkgname%%-*}"
source="https://mediaarea.net/download/source/libmediainfo/$pkgver/libmediainfo_$pkgver.tar.xz ad298a84a740b4e93aef0dccfda54ab440bb4f76.patch"
builddir="$srcdir/MediaInfoLib"
_cmakedir="$builddir/Project/CMake"
options="!check"  # upstream does not provide tests

prepare() {
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
0481b9c4f817bde073f10573d8750eb27fdc73c439a88e31b6a067aeb88dc9a2fb7193583f7e89f8c48b217e0d59e1176c5cd4e062a41f79ee8ce7073d41c97e  ad298a84a740b4e93aef0dccfda54ab440bb4f76.patch"
