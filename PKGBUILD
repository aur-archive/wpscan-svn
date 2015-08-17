# contributor: Roel Blaauwgeers <roel at ttys0.nl>

pkgname=wpscan-svn
pkgver=184
pkgrel=2
pkgdesc="A vulnerability scanner which checks the security of WordPress installations using a black box approach"
arch=('i686' 'x86_64')
url="http://code.google.com/p/wpscan/"
license=('GPL3')
depends=()
makedepends=('subversion' 'rubygems')
provides=()
conflicts=()

_svntrunk="http://wpscan.googlecode.com/svn/trunk/"
_svnmod=wpscan

build() {


  if [ -d $srcdir/.svn ]; then
    msg 'Updating...'
    svn up $srcdir
  else
    msg 'Checking out...'
    svn co $_svntrunk $srcdir
  fi



  cd $srcdir

  install -d $pkgdir/usr/share/wpscan

  cp -a {*,.svn} $pkgdir/usr/share/wpscan/
#  find $pkgdir/usr/share/wpscan -type f -exec chmod 644 {} +

  mkdir -p "${pkgdir}"/usr/bin

  cat > "${pkgdir}"/usr/bin/wpscan << EOF
#!/bin/bash
cd /usr/share/wpscan
ruby ./wpscan.rb \$@
cd \$OLDPWD
EOF
  
  chmod 755 "${pkgdir}"/usr/bin/wpscan

  echo -e '\E[37;41m'"\033[1mTo run 'wpscan' you'll need to install the following ruby gems:\033[0m typhoeus, xml-simple"
  echo "( \$gem install typhoeus xml-simple )"
  echo

##  enable the following lines if you want pacman to handle these gems (I do not recommend this...)
#  local _gemdir="$(ruby -rubygems -e'puts Gem.default_dir')"
#  gem install --ignore-dependencies  -i "$pkgdir$_gemdir" typhoeus xml-simple 


}


#BUILD


