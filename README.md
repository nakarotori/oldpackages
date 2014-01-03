packages
========

OpenWrt packages
A drop-in replacement for OpenWrt feeds.
This repo uses feeds as upstream and integrates updates not yet in upstream.


In feeds.conf.default replace the first line with this repository
example:

    src-git packages git://github.com/nakarotori/packages.git
    src-svn xwrt http://x-wrt.googlecode.com/svn/trunk/package
    src-git luci git://nbd.name/luci.git
    src-git routing git://github.com/openwrt-routing/packages.git
    src-git telephony http://feeds.openwrt.nanl.de/openwrt/telephony.git

other possibly interesting repositories:

    https://github.com/tobiaswaldvogel
    https://code.google.com/p/mediawrt
    https://github.com/FranciscoBorges/openwrt-printing-packages
