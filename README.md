The Debian package currently copies:

 * Header files from fpdfsdk/include to /usr/include/pdfium/fpdfsdk
 * All of the static libraries from out/Release/*.a  to /usr/lib/pdfium
 * The test application from out/Release/pdfium_test to /usr/bin/pdfium-test

To build the deb I ran:

     mkdir pdfium-deb
     git clone https://pdfium.googlesource.com/pdfium.git
     cd pdfium
     svn co http://gyp.googlecode.com/svn/trunk build/gyp
     svn co http://v8.googlecode.com/svn/trunk v8
     svn co https://src.chromium.org/chrome/trunk/deps/third_party/icu46 v8/third_party/icu
     rm -rf .git
     find -type d -name .svn -exec rm {} \;
     cd ..
     mv pdfium pdfium-0.1+git20150114
     tar czf pdfium-0.1+git20150114.tar.gz pdfium-0.1+git20150114
     cd pdfium-0.1+git20150114
     cp ../debian-config ./debian
     dpkg-buildpackage -us -uc