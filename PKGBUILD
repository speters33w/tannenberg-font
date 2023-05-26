# Maintainer: Stephan Peters <speters33w аt gmail dоt cоm>
# Contributor: Riedler <dev@riedler.wien>
# Contributor: xNN <xNNism@gmail.com>

fontname=tannenberg

_include_webfonts=false
# true to include webfonts with ttf or type1 installation.
# explicitly installing the webfonts-$fontname package overrides this value to true.

_webfontdir=$HOME/www/fonts
# Directory to copy webfonts to.

_pfmdir=/usr/share/fonts/type1/
# Directory for postscript type 1 .pfm and .pfb files.
# Change to install in an alternate location, example: "/psfonts/$fontname/"

_afmdir=/usr/share/fonts/type1/
# Directory for postscript type 1 .afm files.
# Change to install in an alternate location, example: "/psfonts/$fontname/afm"

# Postscript Type 1 fonts are only installed if installing the type1-$fontname package.
# This is a largely obsolete format, and would only be needeed for specialized applications.
# Only the original files from TypeOasis are installed, this package does not include TeX .tfm files.
# TeX .tfm files can be generated from the included Type 1 files with a utility.

#pkgname=("ttf-$fontname" "type1-$fontname" "webfonts-$fontname")
pkgname=("ttf-$fontname")  # use to install a single package locally.
licensefile="ffc.html"
pkgver=2.0.0
pkgrel=1
# name=""
pkgdesc="Tannenberg is a Fraktur-family blackletter typeface, developed in Germany between 1933 and 1935 digitized by Dieter Steffmann"
arch=(any)
url="https://github.com/speters33w/tannenberg-font"
license=("custom:1001Fonts Free For Commercial Use License (FFC)") 
  # This is the current license for Dieter Steffmann's fonts. See http://www.steffmann.de/wordpress/test-2/typoasis/ and https://www.1001fonts.com/tannenberg-font.html .
depends=()
makedepends=()
optdepends=()
conflicts=()
source=("https://github.com/speters33w/tannenberg-font/raw/main/tannenberg-font.tar.gz")
sha256sums=("0bd8cad636d2b751999c96a074d7a1655b23d6b541b1ab859a0cf88de5c492ae")
  # Compiled from source files at https://www.1001fonts.com/tannenberg-font.html , http://moorstation.org/typoasis/designers/steffmann/samples/t/tannenbg.htm 
  # and generated webfonts using https://www.fontsquirrel.com/tools/webfont-generator .

prepare(){
  bsdtar xvf tannenberg-font.tar.gz
}

install_license(){
  if [ ! -f "/usr/share/licenses/$fontname-font/$licensefile" ] ; then
#    mkdir -p "$pkgdir"/usr/share/licenses/$fontname-font"
    install -Dm644 -t "$pkgdir"/"usr/share/licenses"/"$fontname-font" "$srcdir"/"usr/share/licenses"/"$fontname-font"/*.*
  fi
}

install_fonts(){
#  mkdir -p "$pkgdir"/usr/share/fonts/"$1"
  install -Dm644 -t "$pkgdir"/usr/share/fonts/"${1^^}" "$srcdir"/usr/share/fonts/"$1"/*."$1"
}

install_postscript(){
  install -Dm644 -t "$pkgdir"/"$_pfmdir" "$srcdir"/usr/share/fonts/type1/*.pf* 
  install -Dm644 -t "$pkgdir"/"$_afmdir" "$srcdir"/usr/share/fonts/type1/*.afm 
}

install_webfonts(){
  if [ "$_include_webfonts" = true ] ; then
    mkdir -p "$pkgdir"/"$_webfontdir"
    if [ ! -f "$_webfontdir"/"$fontname.bold.woff" ] ; then 
      install -Dm644 -t "$pkgdir"/"$_webfontdir" "$srcdir"/www/fonts/*.woff
    fi
    if [ ! -f "$_webfontdir/$fontname.bold.woff2" ] ; then
      install -Dm644 -t "$pkgdir"/"$_webfontdir" "$srcdir"/www/fonts/*.woff2
    fi
    echo -e "\e[32mWebfonts will be installed in ${_webfontdir}.\e[0m" 
  fi	
}

package_ttf-tannenberg() {
  conflicts+=()          # use if font has an otf version.
  install_license
  install_fonts ttf
  install_webfonts
}

package_type1-tannenberg() {
  install_license
  install_postscript
  install_webfonts
}

package_webfonts-tannenberg() {
  _include_webfonts=true
  install_license
  install_webfonts
}
