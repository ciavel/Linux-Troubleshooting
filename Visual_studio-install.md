**bash** 
- `sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc`
- `sudo tee /etc/yum.repos.d/vscode.repo > /dev/null <<'EOF'
    [code]
    name=Visual Studio Code
    baseurl=https://packages.microsoft.com/yumrepos/vscode
    enabled=1
    autorefresh=1
    type=rpm-md
    gpgcheck=1
    gpgkey=https://packages.microsoft.com/keys/microsoft.asc
    EOF`
- `sudo dnf check-update`
- `sudo dnf install -y code`
- `code` // to launch the VSCODE

**RESULTS** 
``` bash
    userfedora:~$ sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    
    sudo tee /etc/yum.repos.d/vscode.repo > /dev/null <<'EOF'
    [code]
    name=Visual Studio Code
    baseurl=https://packages.microsoft.com/yumrepos/vscode
    enabled=1
    autorefresh=1
    type=rpm-md
    gpgcheck=1
    gpgkey=https://packages.microsoft.com/keys/microsoft.asc
    EOF
    
    sudo dnf check-update
    sudo dnf install -y code
    Updating and loading repositories:
     Visual Studio Code                                 100% | 306.5 KiB/s | 190.0 KiB |  00m01s
    Repositories loaded.
    Updating and loading repositories:
    Repositories loaded.
    Package                      Arch     Version                      Repository           Size
    Installing:
     code                        x86_64   0:1.119.0-1778006763.el8     code            639.7 MiB
    Installing weak dependencies:
     socat                       x86_64   0:1.8.1.0-2.fc44             fedora            1.4 MiB
    
    Transaction Summary:
     Installing:         2 packages
    
    Total size of inbound packages is 203 MiB. Need to download 203 MiB.
    After this operation, 641 MiB extra will be used (install 641 MiB, remove 0 B).
    [1/2] socat-0:1.8.1.0-2.fc44.x86_64                 100% | 347.7 KiB/s | 394.7 KiB |  00m01s
    [2/2] code-0:1.119.0-1778006763.el8.x86_64          100% |   2.5 MiB/s | 202.7 MiB |  01m21s
    --------------------------------------------------------------------------------------------
    [2/2] Total                                         100% |   2.5 MiB/s | 203.1 MiB |  01m21s
    Running transaction
    [1/4] Verify package files                          100% |   2.0   B/s |   2.0   B |  00m01s
    [2/4] Prepare transaction                           100% |   8.0   B/s |   2.0   B |  00m00s
    [3/4] Installing socat-0:1.8.1.0-2.fc44.x86_64      100% |  39.7 MiB/s |   1.4 MiB |  00m00s
    [4/4] Installing code-0:1.119.0-1778006763.el8.x86_ 100% | 138.1 MiB/s | 641.2 MiB |  00m05s
    Complete!
    user@fedora:~$ code
```
