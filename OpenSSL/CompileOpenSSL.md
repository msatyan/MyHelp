
# OpenSSL x64 compilation on Windows:

## Prerequisite:
1. ActivePerl v5.22 or above.
http://www.activestate.com/activeperl/downloads

2. Visual Studio 
https://www.visualstudio.com/downloads/

3. OpenSSL source code. 
https://www.openssl.org/source/


## My Setup
1. Windows 7 Pro x64
2. ActivePerl v5.24.0
3. VS2015
4. openssl-1.1.0c.tar.gz
5. Source extracted at C:\Work0\openssl


## Build Win x64:
### FYI: The OpenSSL build process has changed since OpenSSL v1.1.0 release

```
Open VS2015 x64 command window

cd C:\Work0\openssl
perl Configure debug-VC-WIN64A no-asm   > out.cfg.txt 2>&1
nmake -f makefile      > out.cmp.txt 2>&1
nmake -f makefile test > out.test.txt 2>&1
```


