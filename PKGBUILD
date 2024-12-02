# Maintainer: Laura <54481689+Laurazepam@users.noreply.github.com> //turns out github doesn't forward to these addresses anymore so I'm not actually reachable there I might make a new address for this but idk who cares anyway right?

pkgname=nginx-mainline-mod-headers-more
pkgver=1.27.2
pkgrel=1
_headersver=0.37

pkgdesc="adds headers-more-nginx-module to nginx-mainline"
arch=('any')
depends=('nginx-mainline')
makedepends=('nginx-mainline-src')
url='https://nginx.org/' #can't have multiple? I guess I'll just put nginx then?
license=('BSD-2-Clause')

source=(https://github.com/openresty/headers-more-nginx-module/archive/refs/tags/v$_headersver.tar.gz)
sha256sums=('CF6E169D6B350C06D0C730B0EAF4973394026AD40094CDDD3B3A5B346577019D')

prepare() {
	mkdir -p build
	cd build
	ln -sf /usr/src/nginx/auto #what's this shit be doing?
	ln -sf /usr/src/nginx/src #what's this shit be doing?

	cd "$srcdir"/headers-more-nginx-module-$_headersver
	sed 's@/usr/local@/usr@' -i config #what's this shit be doing?
}

build() {
	cd build
	/usr/src/nginx/configure --with-compat --add-dynamic-module=../headers-more-nginx-module-$_headersver
	make modules
}

package() {
	cd "$srcdir"/build/objs
	for mod in ngx_*.so; do
		install -Dm755 $mod "$pkgdir"/usr/lib/nginx/modules/$mod
	done
}
