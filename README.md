#Pre-requisite/Command Installation
01.	C-Compiler and PHP Dev Tool
a.	To install C-Compiler use command, dnf install gcc
b.	To install PHP Dev tool, use command dnf install php-devel
02.	make tool
a.	To install make tool, use command dnf install make

#Packages required for GNUPG/GPG installation

#Extension Name - libgpg-error<br>
#Installation Manual Link - https://www.linuxfromscratch.org/blfs/view/svn/general/libgpg-error.html<br>
#Package Download Link - https://www.gnupg.org/ftp/gcrypt/libgpg-error/libgpg-error-1.45.tar.bz2 

#Extension Name - libassuan<br>
#Installation Manual Link - https://www.linuxfromscratch.org/blfs/view/svn/general/libassuan.html<br>
#Package Download Link - https://www.gnupg.org/ftp/gcrypt/libassuan/libassuan-2.5.5.tar.bz2<br> 

#Extension Name - gpgme<br>
#Installation Manual Link - https://www.linuxfromscratch.org/blfs/view/svn/postlfs/gpgme.html<br>
#Package Download Link - https://www.gnupg.org/ftp/gcrypt/gpgme/gpgme-1.17.1.tar.bz2 <br>

#Extension Name - gnupg/gpg<br>
#Installation Manual Link - https://pecl.php.net/package/gnupg<br>
#Package Download Link - https://pecl.php.net/get/gnupg-1.5.1.tgz<br> 

#Installation of libgpg-error

cd libgpg-error-1.45

Install libgpg-error by running the following commands:

./configure --prefix=/usr &&
make

To test the results, issue: make check.
Now, as the root user:

make install &&
install -v -m644 -D README /usr/share/doc/libgpg-error-1.45/README
  
#Installation of libassuan

cd libassuan-2.5.5
Install libassuan by running the following commands:
./configure --prefix=/usr &&
make                      &&
make -C doc html                                                       &&
makeinfo --html --no-split -o doc/assuan_nochunks.html doc/assuan.texi &&
makeinfo --plaintext       -o doc/assuan.txt           doc/assuan.texi

The above commands build the documentation in html and plaintext formats. If you wish to build alternate formats of the documentation, you must have texlive-20220321 installed and issue the following commands:

make -C doc pdf ps

To test the results, issue: make check.
Now, as the root user:

make install &&
install -v -dm755   /usr/share/doc/libassuan-2.5.5/html &&
install -v -m644 doc/assuan.html/* \
                    /usr/share/doc/libassuan-2.5.5/html &&
install -v -m644 doc/assuan_nochunks.html \
                    /usr/share/doc/libassuan-2.5.5      &&
install -v -m644 doc/assuan.{txt,texi} \
                    /usr/share/doc/libassuan-2.5.5
If you built alternate formats of the documentation, install them by running the following commands as the root user:
install -v -m644  doc/assuan.{pdf,ps,dvi} \
                  /usr/share/doc/libassuan-2.5.5

#Installation of GPGME

cd gpgme-1.17.1

First, fix an issue building the package with Glibc-2.34 or later:

sed 's/defined(__sun.*$/1/' -i src/posix-io.c

Next, fix an issue building with Python 3.10 installed:

sed -e 's/3\.9/3.10/'                    \
    -e 's/:3/:4/'                        \
    -e '23653 s/distutils"/setuptools"/' \
    -i configure

Install GPGME by running the following commands:

./configure --prefix=/usr --disable-gpg-test &&
make

To test the results, you should have GnuPG-2.3.6 installed and remove the --disable-gpg-test above. Issue: make -k check.
Now, as the root user:

make install

#Installation of GNUPG

cd gnupg-1.5.1

phpize
./configure
make
sudo make install
