# Presto Server
SHELL := /bin/bash 
version = 0.54
name = presto-server
full_name = $(name)-$(version)
download_url = "http://repo1.maven.org/maven2/com/facebook/presto/$(name)/$(version)/$(full_name).tar.gz"

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
	mkdir -p build/usr/share/presto; \
	mkdir -p build/etc/init.d; \
	mkdir -p build/etc/presto; \
	mkdir -p build/var/lib/presto; \
	mkdir -p build/var/log; \
	pushd build/usr/share/presto; \
	ln -s /var/lib/presto data; \
	ln -s /etc/presto etc; \
	ln -s /var/lib/presto/var/log log; \
	popd; \
	pushd build/var/log; \
	ln -s /var/lib/presto/var/log presto; \
	popd;

build: prep-build
	cp -rp tmp/$(name)/* build/usr/share/presto; \
	cp -rp scripts/$(name) build/etc/init.d/; \
	cp -rp configs/* build/etc/presto/; \

package: build
	pushd build; \
	fpm -a all -s dir -t deb -d "uuid-runtime" -d "oracle-java7-jdk" -n $(name) -v $(version) --after-install ../scripts/postinst -- .; \
	mv *.deb ../; \
	popd;
