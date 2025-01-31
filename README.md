# gallery.sh

Bash Script to generate static web galleries. No server-side programs (i.e. PHP, MySQL) required.

[![ShellCheck](https://github.com/Cyclenerd/gallery_shell/actions/workflows/shellcheck.yml/badge.svg?branch=master)](https://github.com/Cyclenerd/gallery_shell/actions/workflows/shellcheck.yml)
[![Ubuntu 20.04 LTS](https://github.com/Cyclenerd/gallery_shell/actions/workflows/ubuntu_2004.yml/badge.svg?branch=master)](https://github.com/Cyclenerd/gallery_shell/actions/workflows/ubuntu_2004.yml)
[![macOS 11](https://github.com/Cyclenerd/gallery_shell/actions/workflows/macos_11.yml/badge.svg?branch=master)](https://github.com/Cyclenerd/gallery_shell/actions/workflows/macos_11.yml)
[![GitHub](https://img.shields.io/github/license/cyclenerd/gallery_shell)](https://github.com/Cyclenerd/gallery_shell/blob/master/LICENSE)

## Overview

`gallery.sh` is simple bash shell script which generates static html thumbnail (image, photo) galleries using the `convert` and `jhead` command-line utilities.
It requires no special server-side script to run to view image galleries because everything is pre-rendered. 

It offers several features:

* Responsive layout
* Thumbnails which fill the browser efficiently
* Download the original image file
* Nice and simple Bootstrap CSS layout
* Locally previewable galleries by accessing images locally (e.g. `file:///home/nils/pics/gallery/index.html`)
* JPEG header EXIF data extraction
* Auto-rotation of vertical images

This combination of features makes a better user experience than pretty much all the big online photo hosts. 
All you need is a place to host your plain html and jpeg files. This can also be Amazon S3.

## Fork Info

This is a fork of [the original gallery.sh by Cyclenerd](https://github.com/Cyclenerd/gallery_shell) - maintained by [Someguy123](https://github.com/Someguy123).

This fork adds the following functionality/changes:

* Moved the JPG "image generation" code into a function `generate_imgs` so it can be used for other file types
* Support for custom user specified image extensions to scan via `MY_IMG_EXTS` - can specify like `MY_IMG_EXTS="webp tiff tga"`
* Added image generation for PNGs, and JPGs that use `.jpeg` as their file extension
  * Set `MY_IMG_EXTS` default value to `webp webm apng gif tif tiff tga` which adds support for those file types
* Adjusted shebang to `#!/usr/bin/env bash` to improve compatibility with systems where bash might not be in `/bin/`
* Wrapped easily adjustable `MY_` vars with `: ${}` so they can be edited via ENV vars, e.g. `MY_QUALITY=50 MY_TITLE="John's Photos" ./gallery.sh`
* Added support for `.env` files - searches the current working directory, followed by the script's directory


## Installation

Download Bash script `gallery.sh`:

```shell
curl -O "https://raw.githubusercontent.com/Cyclenerd/gallery_shell/master/gallery.sh"
```

## Requirements

* [ImageMagick](http://www.imagemagick.org/) for the `convert` utility.
* [JHead](http://www.sentex.net/~mwandel/jhead/) for EXIF data extraction

On a debian-based system (Ubuntu), just run:

```shell
sudo apt install imagemagick jhead
```

Under macOS you can install it with...

[MacPort](https://www.macports.org/):

```shell
sudo port install imagemagick jhead
```

[Homebrew](https://brew.sh/):

```shell
brew install imagemagick jhead
```

## Usage

```text
gallery.sh [-t <title>] [-d <thumbdir>] [-h]:
	[-t <title>]     sets the title (default: Gallery)
	[-d <thumbdir>]  sets the thumbdir (default: __thumbs)
	[-h]             displays help (this message)
```

Example: `gallery.sh` or `gallery.sh -t "My Photos" -d "thumbs"`

`gallery.sh` works in the **current** directory.
Just load the `index.html` in a browser see the output. 

The directory should contain a bunch of JPEG (.jpg or .JPG) files.
It does not work recursively. 
ZIP files (.zip or .ZIP) and movies (.mov, .MOV, .mp4 or .MP4) are also considered.
They appear as a download button in the gallery.

## Hint

Create a Bash alias for `gallery.sh`.

Open the `~/.bash_profile`,  `~/.bashrc` or `~/.bash_aliases` in your text editor:

```shell
nano ~/.bash_aliases
```

Add your alias:

```shell
alias gallery='/home/nils/gallery_shell/gallery.sh'
```

## Demo

This [demo page](https://cyclenerd.github.io/gallery_shell/) is generated with [GitHub Action](https://github.com/Cyclenerd/gallery_shell/blob/master/.github/workflows/main.yml): <https://cyclenerd.github.io/gallery_shell/>

## Screenshots

![Screenshot: Gallery](images/gallery.jpg)

![Screenshot: Image](images/image.jpg)

## License

GNU Public License version 3.
Please feel free to fork and modify this on GitHub (<https://github.com/Cyclenerd/gallery_shell>).