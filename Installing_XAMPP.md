**INSTALLATION**
- [XAMPP for Linux Download](https://www.apachefriends.org/download.html)

``` bash
    user@fedora:~/Downloads$ cd ~/Downloads
    chmod 755 xampp-linux-x64-*-installer.run
    sudo ./xampp-linux-x64-*-installer.run
    user@fedora:~/Downloads$ sudo /opt/lampp/lampp start
    [sudo] password for user: 
    egrep: warning: egrep is obsolescent; using grep -E
    XAMPP is currently only availably as 32 bit application. Please use a 32 bit compatibility library for your system.
```

**ERRORS**
``` bash
    XAMPP: Stopping Apache...not running.
    XAMPP: Stopping MySQL...not running.
    XAMPP: Stopping ProFTPD...not running.
    XAMPP: Starting Apache...egrep: warning: egrep is obsolescent; using grep -E
    egrep: warning: egrep is obsolescent; using grep -E
    fail.
    httpd: Syntax error on line 522 of /opt/lampp/etc/httpd.conf: Syntax error on line 6 of /opt/lampp/etc/extra/httpd-xampp.conf: Cannot load modules/mod_perl.so into server: libnsl.so.1: cannot open shared object file: No such file or directory
    XAMPP: Starting MySQL...egrep: warning: egrep is obsolescent; using grep -E
    ok.
    XAMPP: Starting ProFTPD...egrep: warning: egrep is obsolescent; using grep -E
    ok.
```
**INSTALLATION: libxcrypt-compat & libnsl**

``` bash
    user@fedora:/opt/lampp$ sudo dnf install libxcrypt-compat
    Updating and loading repositories:
    Repositories loaded.
    Package                      Arch     Version                      Repository           Size
    Installing:
     libxcrypt-compat            x86_64   0:4.5.2-3.fc44               fedora          217.4 KiB
    
    Transaction Summary:
     Installing:         1 package
    
    Total size of inbound packages is 101 KiB. Need to download 101 KiB.
    After this operation, 217 KiB extra will be used (install 217 KiB, remove 0 B).
    Is this ok [y/N]: y
    [1/1] libxcrypt-compat-0:4.5.2-3.fc44.x86_64        100% | 138.2 KiB/s | 101.2 KiB |  00m01s
    --------------------------------------------------------------------------------------------
    [1/1] Total                                         100% |  38.2 KiB/s | 101.2 KiB |  00m03s
    Running transaction
    [1/3] Verify package files                          100% | 111.0   B/s |   1.0   B |  00m00s
    [2/3] Prepare transaction                           100% |   4.0   B/s |   1.0   B |  00m00s
    [3/3] Installing libxcrypt-compat-0:4.5.2-3.fc44.x8 100% | 589.8 KiB/s | 218.8 KiB |  00m00s
    Complete!
```
**ERRORS: Missing requirement for running xampp/lampp**

``` bash
    user@fedora:/opt/lampp$ sudo /opt/lampp/lampp restart
    egrep: warning: egrep is obsolescent; using grep -E
    egrep: warning: egrep is obsolescent; using grep -E
    egrep: warning: egrep is obsolescent; using grep -E
    egrep: warning: egrep is obsolescent; using grep -E
    XAMPP:  SELinux is activated. Making XAMPP fit SELinux...
    chcon: cannot access '/opt/lampp/lib/mysql/*.so': No such file or directory
    egrep: warning: egrep is obsolescent; using grep -E
    Restarting XAMPP for Linux 8.2.12-0...
    XAMPP: Stopping Apache...not running.
    XAMPP: Stopping MySQL...not running.
    XAMPP: Stopping ProFTPD...not running.
    XAMPP: Starting Apache...egrep: warning: egrep is obsolescent; using grep -E
    egrep: warning: egrep is obsolescent; using grep -E
    fail.
    httpd: Syntax error on line 522 of /opt/lampp/etc/httpd.conf: Syntax error on line 6 of /opt/lampp/etc/extra/httpd-xampp.conf: Cannot load modules/mod_perl.so into server: libnsl.so.1: cannot open shared object file: No such file or directory
    XAMPP: Starting MySQL...egrep: warning: egrep is obsolescent; using grep -E
    ok.
    XAMPP: Starting ProFTPD...egrep: warning: egrep is obsolescent; using grep -E
    ok.
    user@fedora:/opt/lampp$ sudo dnf install libnsl
    Updating and loading repositories:
    Repositories loaded.
    Package                      Arch     Version                      Repository           Size
    Installing:
     libnsl                      x86_64   0:2.43-4.fc44                updates         101.8 KiB
    
    Transaction Summary:
     Installing:         1 package
    
    Total size of inbound packages is 123 KiB. Need to download 123 KiB.
    After this operation, 102 KiB extra will be used (install 102 KiB, remove 0 B).
    Is this ok [y/N]: y
    [1/1] libnsl-0:2.43-4.fc44.x86_64                   100% |  40.5 KiB/s | 122.9 KiB |  00m03s
    --------------------------------------------------------------------------------------------
    [1/1] Total                                         100% |  22.6 KiB/s | 122.9 KiB |  00m05s
    Running transaction
    [1/3] Verify package files                          100% | 125.0   B/s |   1.0   B |  00m00s
    [2/3] Prepare transaction                           100% |   5.0   B/s |   1.0   B |  00m00s
    [3/3] Installing libnsl-0:2.43-4.fc44.x86_64        100% | 579.1 KiB/s | 102.5 KiB |  00m00s
    Complete!
```
**FIXED**

``` bash
    user@fedora:/opt/lampp$ sudo /opt/lampp/lampp restart
    egrep: warning: egrep is obsolescent; using grep -E
    egrep: warning: egrep is obsolescent; using grep -E
    egrep: warning: egrep is obsolescent; using grep -E
    egrep: warning: egrep is obsolescent; using grep -E
    egrep: warning: egrep is obsolescent; using grep -E
    Restarting XAMPP for Linux 8.2.12-0...
    XAMPP: Stopping Apache...not running.
    XAMPP: Stopping MySQL...ok.
    XAMPP: Stopping ProFTPD...ok.
    XAMPP: Starting Apache...egrep: warning: egrep is obsolescent; using grep -E
    egrep: warning: egrep is obsolescent; using grep -E
    ok.
    XAMPP: Starting MySQL...egrep: warning: egrep is obsolescent; using grep -E
    ok.
    XAMPP: Starting ProFTPD...egrep: warning: egrep is obsolescent; using grep -E
    ok.
```
  
    
---

## XAMPP Apache error: `libnsl.so.1` missing on Fedora Linux

### Error

When restarting XAMPP, Apache may fail while MySQL and ProFTPD start successfully:

```text
XAMPP: Stopping Apache...not running.
XAMPP: Stopping MySQL...not running.
XAMPP: Stopping ProFTPD...not running.
XAMPP: Starting Apache...fail.
httpd: Syntax error on line 522 of /opt/lampp/etc/httpd.conf: Syntax error on line 6 of /opt/lampp/etc/extra/httpd-xampp.conf: Cannot load modules/mod_perl.so into server: libnsl.so.1: cannot open shared object file: No such file or directory
XAMPP: Starting MySQL...ok.
XAMPP: Starting ProFTPD...ok.
```

### Cause

XAMPP needs the legacy library `libnsl.so.1`, but it is not installed by default on newer Fedora versions.

The `egrep: warning: egrep is obsolescent; using grep -E` messages are only warnings from old XAMPP scripts and can usually be ignored.

### Fix

Install the missing compatibility library:

```bash
sudo dnf install libnsl
```

If you also get an error about `libcrypt.so.1`, install this package too:

```bash
sudo dnf install libxcrypt-compat
```

Restart XAMPP:

```bash
sudo /opt/lampp/lampp restart
```

Check XAMPP status:

```bash
sudo /opt/lampp/lampp status
```

### Expected result

```text
XAMPP: Starting Apache...ok.
XAMPP: Starting MySQL...ok.
XAMPP: Starting ProFTPD...ok.
```
