ZeroTier for Synology 
======

[![irc](https://img.shields.io/badge/IRC-%23zerotier%20on%20freenode-orange.svg)](https://webchat.freenode.net/?channels=zerotier)

**Download pre-built packages here:** [zerotier.com/download.shtml](https://zerotier.com/download.shtml?pk_campaign=github_ZeroTierNAS)

**Last tests on: DSM 6.1.3-15152 Update 1 (2017/07/17)**

***

#### Package Build Instructions:

 - Build ZeroTier binaries for your target architecture: `make ZT_SYNOLOGY=1` [ZeroTier](https://github.com/zerotier/ZeroTierOne)
 - Place binary(ies) in `package/zerotier/app/bin`
 - Name binaries to reflect arch: (e.g. `zerotier-one.x86_64` or `zerotier-one.armv7`)
 - Install Apache Ant
 - Fetch dependencies:

```
export ANT_HOME=/usr/share/ant/ 
ant -f $ANT_HOME/fetch.xml -Ddest=system
```

### Generate GPG Key
`gpg --gen-key`
 - (1) RSA Key
 - Choose size
 - Enter name, email
 - Enter a passphrase (leave blank, otherwise the build process will fail)

After successful generation, the key will be placed in `~/.gnupg/`

To verify the key generation was successful: `gpg -K`, use the key id outputted from this in the `build.xml` file.
If successful, copy it into the `package/zerotier/gpg` folder and then build:

 - Build package:
 ```
 ./package/zerotier/build.sh
 ```

### Entware-ng
 - Alterntively without a GUI, an official ZeroTier package exists for Entware-ng under the name `zerotier`
 - Follow these instructions to install Entware-ng on your Synology NAS: https://github.com/Entware-ng/Entware-ng/wiki/Install-on-Synology-NAS
 - `opkg install zerotier`
 - Modify `package/zerotier/spk/scripts/start-stop-status.sh` script to start and stop ZeroTier. Entware will likely install ZeroTier to `/volumeX/@entware-ng/opt/usr/sbin/`
***

*
Side notes:
 - If required, additional installation instructions can be found here: http://ant.apache.org/manual/install.html
 - If installing Ant from a repo it might not include `fetch.xml` or `get-m2.xml`, copy these into your `$ANT_HOME` manually.
*

