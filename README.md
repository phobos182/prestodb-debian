presto
=====

Custom debian builds for PrestoDB

Layout
----
* Debian includes a simple init.d SystemV script which calls launcher. 
* Configuration files in /etc/presto, /etc/discovery-server, etc..
* Log files in /var/log/discovery-server. Etc..
* Follows Tomcat style packaging. Everything is in /usr/share/presto, symlinked out to various directories

Requirements
----
* fpm (gem install fpm)
* build-essential (apt-get install build-essential)

Usage
----
make all

debian files will be created in subdirectories for discovery / client / server

Notes
----
* FPM command depends on 'oracle-java7-jdk' as we use OAB internally to build JDK debian artifacts (https://github.com/flexiondotorg/oab-java6). Please change as you see fit, or remove.
* We depend on 'uuid-runtime' to run a 'uuidgen' command to create unique id's for nodes as part of the post installation script. You can modify this build scripts to not reuire this, and instead use different identifiers as 0.54 supports it.
