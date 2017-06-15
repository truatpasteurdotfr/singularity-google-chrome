#!/bin/bash
# 
# Copyright (c) 2015-2016, Gregory M. Kurtzer. All rights reserved.
# 
# "Singularity" Copyright (c) 2016, The Regents of the University of California,
# through Lawrence Berkeley National Laboratory (subject to receipt of any
# required approvals from the U.S. Dept. of Energy).  All rights reserved.
#
# Tru Huynh <tru@pasteur.fr>
# https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
# need 1GB to accomodate requirements
# 2017/06/15: starts chrome in the runscript
# 2017/06/07: adding labels (Singularity 2.3)


BootStrap: debootstrap
OSVersion: jessie
# local mirror
#MirrorURL: file:///var/ftp/pub/debian
MirrorURL: http://ftp.us.debian.org/debian/

%runscript
echo 'google chrome in the container:'
echo 'singularity run -B /run container.img'
echo 'if you want a discardable instance use:'
echo 'singularity run -B /run -H `mktemp -d /dev/shm/chromeXXXX` container.img'
echo ''

/opt/google/chrome/google-chrome \
--bwsi \
--disable-metrics \
--no-first-run \
--no-sandbox \
--disable-translate \
"$@"

%post
echo "Hello from inside the container"
# non interactive debian
export DEBIAN_FRONTEND=noninteractive
apt-get update
apt-get -y install wget
apt-get -y install libcanberra-gtk-module packagekit-gtk3-module
#wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
# no auto update: uncomment the following line *** before installing ***
# touch /etc/default/google-chrome
#dpkg -i google-chrome-stable_current_amd64.deb && /bin/rm google-chrome-stable_current_amd64.deb
# oneline:
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && dpkg -i google-chrome-stable_current_amd64.deb && /bin/rm google-chrome-stable_current_amd64.deb

# install missing requirements if any
apt-get -y install -f
# update all packages
apt-get -y upgrade

# kill hanging dbus
pkill -u 104

%labels
MAINTAINER truatpasteurdotfr
