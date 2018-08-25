# [thomasWeise/docker-texlive-full](http://hub.docker.com/r/thomasweise/docker-texlive-full/)

[![Docker Pulls](http://img.shields.io/docker/pulls/thomasweise/docker-texlive-full.svg)](http://hub.docker.com/r/thomasweise/docker-texlive-full/)
[![Docker Stars](http://img.shields.io/docker/stars/thomasweise/docker-texlive-full.svg)](http://hub.docker.com/r/thomasweise/docker-texlive-full/)

This is a Docker image containing a full [`TeX Live`](http://en.wikipedia.org/wiki/TeX_Live) installation with several fonts. The goal is to provide a base image for my other LaTeX-related containers. Regarding the fonts, we have, e.g., the several pre-installed open Chinese fonts.

## 1. Building and Components

The image has the following components:

- [`TeX Live`](http://www.tug.org/texlive/)
- [`ghostscript`](http://ghostscript.com/)
- [`poppler-utils`](http://poppler.freedesktop.org/)

## 2. License

This image is licensed under the GNU GENERAL PUBLIC LICENSE Version 3, 29 June 2007, which you can find in file [LICENSE.md](http://github.com/thomasWeise/docker-texlive/blob/master/LICENSE.md). The license applies to the way the image is built, while the software components inside the image are under the respective licenses chosen by their respective copyright holders.

### 3. Utility Scripts

Currently, we provide the following utility scripts in folder `/bin/`:

- `filterPdf.sh <document>` transform a document (either in [PostScript](http://en.wikipedia.org/wiki/PostScript)/`PS`, `EPS`, or `PDF` format) to `PDF` and include as many of the fonts used inside the document into the final `PDF`. This uses ghostscripts `gs` and checks the output with `pdftotext` from `poppler-utils` before replacing `<document>` with the hope to build a final pdf that can display on as many machines correctly as possible.

## 4. Contact

If you have any questions or suggestions, please contact [Thomas Weise](mailto:tweise@hfuu.edu.cn) of the [Institute of Applied Optimization](http://iao.hfuu.edu.cn) of [Hefei University](http://www.hfuu.edu.cn) in Hefei, Anhui, China.
