#
# thomasweise/docker-texlive-full
#
# This is an image with a basic TeX Live installation.
# Source: https://github.com/thomasWeise/docker-texlive/
# License: GNU GENERAL PUBLIC LICENSE, Version 3, 29 June 2007
# The license applies to the way the image is built, while the
# software components inside the image are under the respective
# licenses chosen by their respective copyright holders.
#
FROM ubuntu:18.04
MAINTAINER Thomas Weise <tweise@hfuu.edu.cn>

ENV LANG=C.UTF-8
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get clean &&\
    apt-get update &&\
    apt-get autoclean -y &&\
    apt-get autoremove -y &&\
    apt-get update &&\
# install utilities
    apt-get install -f -y apt-utils &&\
# install some nice fonts, e.g., for chinese and other
    apt-get install -f -y fontconfig \
                          fonts-arphic-bkai00mp \
                          fonts-arphic-bsmi00lp \
                          fonts-arphic-gbsn00lp \
                          fonts-arphic-gkai00mp \
                          fonts-arphic-ukai \
                          fonts-arphic-uming \
                          fonts-dejavu-core \
                          ttf-wqy-microhei \
                          ttf-wqy-zenhei \
                          xfonts-intl-chinese \
                          xfonts-intl-chinese-big &&\
# now the microsoft core fonts
    echo "ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true" | debconf-set-selections &&\
    echo "ttf-mscorefonts-installer msttcorefonts/present-mscorefonts-eula note" | debconf-set-selections &&\
    apt-get install -f -y --no-install-recommends ttf-mscorefonts-installer &&\
# we make sure to contain the EULA in our container
    wget --output-document=/root/mscorefonts-eula "http://corefonts.sourceforge.net/eula.htm" &&\
# install TeX Live and ghostscript
    apt-get install -f -y ghostscript \
                          make \
                          latex-cjk-common \
                          latex-cjk-chinese \
                          texlive-full \
                          texlive-fonts-extra \
                          texlive-fonts-recommended \
                          texlive-math-extra \
                          texlive-lang-all \
                          texlive-lang-cjk \
                          texlive-luatex \
                          texlive-pstricks \
                          texlive-science \
                          texlive-xetex &&\
# free huge amount of unused space
    apt-get purge -f -y make-doc \
                        texlive-fonts-extra-doc \
                        texlive-fonts-recommended-doc \
                        texlive-humanities-doc \
                        texlive-latex-base-doc \
                        texlive-latex-extra-doc \
                        texlive-latex-recommended-doc \
                        texlive-metapost-doc \
                        texlive-pictures-doc \
                        texlive-pstricks-doc \
                        texlive-science-doc &&\
# clean up all temporary files
    apt-get clean &&\
    apt-get autoclean -y &&\
    apt-get autoremove -y &&\
    apt-get clean &&\
    rm -rf /tmp/* /var/tmp/* &&\
    rm -rf /var/lib/apt/lists/* &&\
    rm -f /etc/ssh/ssh_host_*
