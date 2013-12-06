presto
=====

Custom debian builds for PrestoDB

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
FPM command depends on 'oracle-java7-jdk' as we use OAB internally to build JDK debian artifacts (https://github.com/flexiondotorg/oab-java6). Please change as you see fit, or remove.
