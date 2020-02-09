#
# thomasweise/docker-texlive-full
#
# This is an image with a full TeX Live installation and several
# fonts and tools.
# Source: http://github.com/thomasWeise/docker-texlive-full/
# License: GNU GENERAL PUBLIC LICENSE, Version 3, 29 June 2007
# The license applies to the way the image is built, while the
# software components inside the image are under the respective
# licenses chosen by their respective copyright holders.
#
FROM ubuntu:20.04
MAINTAINER Thomas Weise <tweise@hfuu.edu.cn>

ENV LANG=C.UTF-8
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get clean &&\
    apt-get update &&\
    apt-get autoclean -y &&\
    apt-get autoremove -y &&\
    apt-get update &&\
# prevent doc and man pages from being installed
# the idea is based on https://askubuntu.com/questions/129566
# and https://askubuntu.com/questions/628407
    printf 'path-exclude /usr/share/doc/*\npath-include /usr/share/doc/*/copyright\npath-exclude /usr/share/man/*\npath-exclude /usr/share/groff/*\npath-exclude /usr/share/info/*\npath-exclude /usr/share/lintian/*\npath-exclude /usr/share/linda/*' > /etc/dpkg/dpkg.cfg.d/01_nodoc &&\
    printf 'Dir::Cache "";\nDir::Cache::archives "";' > /etc/apt/apt.conf.d/02nocache &&\
# remove doc files and man pages already installed
    rm -rf /usr/share/groff/* /usr/share/info/* &&\
    rm -rf /usr/share/lintian/* /usr/share/linda/* /var/cache/man/* &&\
    rm -rf /usr/share/man &&\
    mkdir -p /usr/share/man &&\
    mv /user/share/doc/copyright /tmp  &&\
    rm -rf /usr/share/doc &&\
    mkdir -p /usr/share/doc &&\
    mv /tmp/copyright /user/share/doc &&\
    mkdir -p /usr/share/info &&\
# install utilities
    apt-get install -f -y apt-utils &&\
# install some nice fonts, e.g., for chinese and other
    apt-get install -f -y curl \
                          emacs-intl-fonts \
                          fontconfig \
                          fonts-arphic-bkai00mp \
                          fonts-arphic-bsmi00lp \
                          fonts-arphic-gbsn00lp \
                          fonts-arphic-gkai00mp \
                          fonts-arphic-ukai \
                          fonts-arphic-uming \
                          fonts-dejavu \
                          fonts-dejavu-core \
                          fonts-dejavu-extra \
                          fonts-droid-fallback \
                          fonts-guru \
                          fonts-guru-extra \
                          fonts-liberation \
                          fonts-noto-cjk \
                          fonts-opensymbol \
                          fonts-roboto \
                          fonts-roboto-hinted \
                          fonts-stix \
                          fonts-symbola \
                          fonts-texgyre \
                          fonts-unfonts-core \
                          ttf-wqy-microhei \
                          ttf-wqy-zenhei \
                          xfonts-intl-chinese \
                          xfonts-intl-chinese-big \
                          xfonts-wqy &&\
# now the microsoft core fonts
    echo "ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true" | debconf-set-selections &&\
    echo "ttf-mscorefonts-installer msttcorefonts/present-mscorefonts-eula note" | debconf-set-selections &&\
    curl --output "/tmp/mscorefonts.deb" "http://ftp.de.debian.org/debian/pool/contrib/m/msttcorefonts/ttf-mscorefonts-installer_3.6_all.deb" &&\
    apt install -f -y --no-install-recommends "/tmp/mscorefonts.deb" &&\
    rm -f "/tmp/mscorefonts.deb" &&\
# we make sure to contain the EULA in our container
    curl --output "/root/mscorefonts-eula" "http://corefonts.sourceforge.net/eula.htm" &&\
# install TeX Live and ghostscript as well as other tools
    apt-get install -f -y ghostscript \
                          make \
                          latex-cjk-common \
                          latex-cjk-chinese \
                          texlive-full \
                          texlive-fonts-extra \
                          texlive-fonts-recommended \
                          texlive-lang-all \
                          texlive-lang-cjk \
                          texlive-luatex \
                          texlive-pstricks \
                          texlive-science \
                          texlive-xetex \
                          texlive-bibtex-extra \
                          poppler-utils \
                          latexmk &&\
# update font cache
    fc-cache -fv &&\
# clean up all temporary files
    apt-get clean &&\
    apt-get autoclean -y &&\
    apt-get autoremove -y &&\
    apt-get clean &&\
    rm -rf /var/lib/apt/lists/* &&\
    rm -f /etc/ssh/ssh_host_* &&\
# delete man pages and documentation
    rm -rf /usr/share/man &&\
    mkdir -p /usr/share/man &&\
    mv /user/share/doc/copyright /tmp  &&\
    rm -rf /usr/share/doc &&\
    mkdir -p /usr/share/doc &&\
    mv /tmp/copyright /user/share/doc &&\
    rm -rf /var/cache/apt/archives &&\
    mkdir -p /var/cache/apt/archives &&\
    rm -rf /tmp/* /var/tmp/*

ADD scripts /bin/
