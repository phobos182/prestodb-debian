# Presto CLI
SHELL := /bin/bash 
version = 0.54
name = presto
full_name = $(name)-$(version)
download_url = "http://search.maven.org/remotecontent?filepath=com/facebook/presto/presto-cli/$(version)/$(full_name)-executable.jar"

all: package

clean:
	rm -rf build; \
	rm -rf tmp; \
	mkdir -p tmp; \
	mkdir -p build; \
	rm -rf *.deb

download: clean
	cd tmp; \
	curl -o $(name) $(download_url); \
	chmod a+x $(name)

build: download
	mkdir -p build/usr/bin

bundle: build
	cp tmp/$(name) build/usr/bin/

package: bundle
	cd build; \
	fpm -a all -s dir -t deb -d "oracle-java7-jdk >= 7" -n $(name) -v $(version) -- .; \
	mv *.deb ../

