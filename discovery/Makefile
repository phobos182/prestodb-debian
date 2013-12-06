# Presto Discovery Server
SHELL := /bin/bash 
version = 1.16
name = discovery-server
package_name = presto-$(name)
full_name = $(name)-$(version)
download_url = "http://search.maven.org/remotecontent?filepath=io/airlift/discovery/$(name)/$(version)/$(full_name).tar.gz"

all: package

clean:
	rm -rf build; \
	rm -rf tmp; \
	mkdir -p tmp; \
	mkdir -p build; \
	rm -rf *.deb

download: clean
	cd tmp; \
	curl -o $(name).tar.gz $(download_url); \
	tar -zxvf $(name).tar.gz; \
	mv $(full_name) $(name)

prep-build: download
	mkdir -p build/usr/share/$(name); \
	mkdir -p build/etc/init.d; \
	mkdir -p build/etc/$(name); \
	mkdir -p build/var/lib/$(name); \
	mkdir -p build/var/log; \
	pushd build/usr/share/$(name); \
	ln -s /var/lib/$(name) data; \
	ln -s /etc/$(name) etc; \
	ln -s /var/lib/$(name)/var/log log; \
	popd; \
	pushd build/var/log; \
	ln -s /var/lib/$(name)/var/log $(name); \
	popd;

build: prep-build
	cp -rp tmp/$(name)/* build/usr/share/$(name); \
	cp -rp scripts/$(name) build/etc/init.d/; \
	cp -rp configs/* build/etc/$(name)/; \

package: build
	pushd build; \
	fpm -a all -s dir -t deb -d "uuid-runtime" -d "oracle-java7-jdk" -n $(package_name) -v $(version) --after-install ../scripts/postinst -- .; \
	mv *.deb ../; \
	popd;
