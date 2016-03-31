# Presto CLI
SHELL := /bin/bash 
version = 0.143
name = presto-cli
full_name = $(name)-$(version)
download_url = "http://repo1.maven.org/maven2/com/facebook/presto/presto-cli/$(version)/$(full_name)-executable.jar"

all: package

clean:
	rm -rf build; \
	rm -rf tmp; \
	mkdir -p build; \
	rm -rf *.deb

download: clean
	cd build; \
	curl -o $(name) $(download_url); \
	chmod a+x $(name)

package: download
	pushd build; \
	fpm -a all -s dir -t deb -d "oracle-java7-jdk" -n $(name) -v $(version) --prefix=/usr/local/bin -- .; \
	mv *.deb ../; \
	popd;

