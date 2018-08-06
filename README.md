# steam-linux-client
Issues experienced on the Steam linux client

**Problem**
Only the game library displays. Steam browser, store, community, profile, etc. only show a black / blank screen and loading indicator.

*Date:* August 5, 2018
*OS:* Linux Mint 18 Cinnamon 64-bit
*Kernel:* 4.4.0-21-generic

Running steam from the terminal revealed the following, periodic error message:

*libnss3.so: version `NSS_3.22' not found*

More information obtained from the command line:

```bash
$ find ~ -name "libnss3.so" 2> /dev/null

/home/travis/.local/share/Steam/ubuntu12_32/steam-runtime.old/amd64/usr/lib/x86_64-linux-gnu/libnss3.so
/home/travis/.local/share/Steam/ubuntu12_32/steam-runtime.old/i386/usr/lib/i386-linux-gnu/libnss3.so
/home/travis/.local/share/Steam/ubuntu12_32/steam-runtime/amd64/usr/lib/x86_64-linux-gnu/libnss3.so
/home/travis/.local/share/Steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/libnss3.so
/home/travis/firefox/libnss3.so
```

Running the following gave more information:

```bash
$ strings /home/travis/.local/share/Steam/ubuntu12_32/steam-runtime/amd64/usr/lib/x86_64-linux-gnu/libnss3.so | grep -i -e "nss_3"

NSS_3.13
NSS_3.13.2
NSS_3.14
NSS_3.14.1
NSS_3.14.3
NSS_3.15
NSS_3.15.4
NSS_3.16.1
NSS_3.16.2
NSS_3.18
NSS_3.19
NSS_3.19.1
NSS_3.21
```

*Resolution:* After running the following command to update libnss3.so, the problem was resolved:

```bash
$ sudo apt-get install --reinstall libnss3
```

This issue probably happened because my system is not up to date. I'm guessing if I updated my system, the newest library version would have been installed, and Steam wouldn't have any problems.
