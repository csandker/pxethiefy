# pxethiefy.py

pxethiefy is a tool to enumerate PXE boot media provided from an SCCM server in a target network by broadcasting for PXE servers, requesting offered boot media and trying to decrypt it.  

This tool is heavily based on the tool [PXEThief](https://github.com/MWR-CyberSec/PXEThief).
While [PXEThief](https://github.com/MWR-CyberSec/PXEThief) is a Windows-based tool (and provides more features), `pxethiefy.py` has a limited feature set, but can be used from Linux hosts as well.
**Shoutout and all credits go to [MWR-CyberSec](https://github.com/MWR-CyberSec/)**.

This tool is a byproduct of SCCM research, which can be found in this blog: [https://www.securesystems.de/blog/active-directory-spotlight-attacking-the-microsoft-configuration-manager/](https://www.securesystems.de/blog/active-directory-spotlight-attacking-the-microsoft-configuration-manager/)

## Install 

```sh
$:> virtualenv -p python3 venv
$:> source venv/bin/activate
## We need to send and receive raw packets, which usually requires sudo permissions, therefore you got two options here
## Either install and run as sudo
$:> sudo venv/bin/python3 -m pip install -r requirements.txt 
$:> sudo venv/bin/python3 pxethiefy.py -h

## OR install as normal user as follows
$:> python3 -m pip install -r requirements.txt
$:> sudo setcap CAP_NET_RAW=+eip /usr/bin/python3.8 ## change with your python3 version --> run ls -lah /usr/bin/python3* to check symlinks
$:> python3 pxethiefy.py -h
```

## Usage

![Overview](img/main-help.png "Overview")

Sample from an SCCM lab with encrypted PXE boot media:

![Example use](img/explore_example_with_pw.png "Example use")

In case the PXE boot media is encrypted, [this](https://github.com/MWR-CyberSec/configmgr-cryptderivekey-hashcat-module) hashcat module - once again by [MWR-CyberSec](https://github.com/MWR-CyberSec/) - can be used to decrypt the downloaded media file.

Once the password has been cracked, `pxethiefy.py` can be used to read the media file and show potential next steps:

![Decrypt boot media with pxethiefy.py](img/decrypt_example.png "Decrypt boot media with pxethiefy.py")
