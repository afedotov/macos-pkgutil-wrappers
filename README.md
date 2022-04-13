# Handy wrappers for macOS pkgutil

Have you ever messed around with macOS `pkgutil` tool? For example, try to get a list of installed packages with metadata such as package version or installation date. Or figure out which package owns specified file. This is not so comfy with plain `pkgutil`.

Here are wrappers around `pkgutil` written in `bash` that can make this tasks handy:

- `pkg-list` - List all currently installed packages

  ```
  Usage: pkg-list [-h] [-t|-n] [-r] [-d] [-s REGEX_1 [REGEX_2 ...]]

  List all currently installed packages

  Options:

      -h  Show help message
      -t  Sort by INSTALLED
      -n  Sort by PKGID
      -r  Reverse sort order
      -d  Display as raw table data
      -s  Show only packages with PKGID mathing REGEXes
  ```

- `pkg-list-files` - List files installed by the specified package checking the existence at once

  ```
  Usage: pkg-list-files [-h] [-e] PKGID

  List files installed by the specified package checking the existence at once

  Options:

      -h  Show help message
      -e  Display only missing files (marked as ERROR in the first column)
  ```

- `pkg-file-info` - List packages owning specified file

  ```
  Usage: pkg-file-info FILE_PATH

  List packages owning specified file
  ```

### Installation:

Just run `sudo ./install.sh` script. \
It will copy `bin/pkg-*` scripts to `/usr/local/bin` directory.

### Example:

```
~ $ pkg-list -t -r
INSTALLED                  PKGID                                                VERSION                LOCATION
2022-04-13T14:42:50+03:00  org.golang.go                                        go1.17.9               /
2022-04-11T23:03:56+03:00  com.apple.pkg.CLTools_macOS_SDK                      13.3.1.0.1.1648687083  /
2022-04-11T23:03:56+03:00  com.apple.pkg.CLTools_SwiftBackDeploy                13.3.1.0.1.1648687083  /
2022-04-11T23:03:55+03:00  com.apple.pkg.CLTools_SDK_macOS110                   13.3.1.0.1.1648687083  /
2022-04-11T23:03:53+03:00  com.apple.pkg.CLTools_SDK_macOS12                    13.3.1.0.1.1648687083  /
2022-04-11T23:03:53+03:00  com.apple.pkg.CLTools_Executables                    13.3.1.0.1.1648687083  /
2022-04-09T15:31:30+03:00  com.apple.pkg.Pages12                                12.0.1.1647602567      /
2022-04-09T15:29:16+03:00  com.apple.pkg.Keynote12                              12.0.1.1647602567      /
2022-04-09T15:28:15+03:00  com.apple.pkg.Numbers12                              12.0.1.1647602567      /
2022-04-09T15:25:57+03:00  com.crowdcafe.windowmagnet                           2.8.0                  /Applications
2022-04-01T23:13:44+03:00  com.apple.pkg.IncompatibleAppList.12_0.16U2172       1.0.0.0.1.1621908336   /
2022-04-01T20:24:08+03:00  com.apple.files.data-template                        12.3.1                 /
2022-03-18T21:47:59+03:00  org.nodejs.npm.pkg                                   v8.5.0                 /
2022-03-18T21:47:59+03:00  org.nodejs.node.pkg                                  v16.14.2               /
2022-03-18T15:39:38+03:00  com.apple.pkg.XProtectPlistConfigData_10_15.16U4185  2158.1.1646957467      /
2022-03-18T15:39:38+03:00  com.apple.pkg.MRTConfigData_10_15.16U4184            1.91.1.1646956548      /
2022-03-15T20:42:53+03:00  com.apple.pkg.CoreTypes.1500A24                      1.0.0.0.1.1633538941   /
2022-03-11T19:51:51+03:00  ru.keepcoder.Telegram                                8.6.0                  /Applications
2022-02-08T15:10:56+03:00  com.microsoft.rdc.macos                              10.7.6                 /Applications
2022-01-23T16:26:52+03:00  org.virtualbox.pkg.virtualboxcli                     6.1.32                 /usr/local/bin
2022-01-23T16:26:52+03:00  org.virtualbox.pkg.virtualbox                        6.1.32                 /Applications
2022-01-23T16:26:52+03:00  org.virtualbox.pkg.vboxkexts                         6.1.32                 /Library/Application Support/VirtualBox
2022-01-23T16:26:52+03:00  com.github.osxfuse.pkg.Core                          3.10.4                 /
2021-12-16T23:05:59+03:00  org.macports.MacPorts                                0.2.7.1.0.0.0.0.0      /
2021-12-16T04:02:51+03:00  com.tuxera.pkg.Tuxera_NTFS                           2021.0.0               /
2021-11-08T15:28:59+03:00  com.okatbest.boop                                    1.4.0                  /Applications
2021-05-02T01:15:09+03:00  com.vutienthinh.macos.MacMerge                       2.18.0                 /Applications
2020-11-26T18:16:14+03:00  org.wireshark.ChmodBPF.pkg                           1.1                    /

~ $ pkg-list-files org.virtualbox.pkg.virtualboxcli
OK     -rwxr-xr-x  root        wheel                 80  2022-01-13T22:29:26+0300  /usr/local/bin/VBoxAutostart*
OK     -rwxr-xr-x  root        wheel                 82  2022-01-13T22:29:26+0300  /usr/local/bin/VBoxBalloonCtrl*
OK     -rwxr-xr-x  root        wheel                 80  2022-01-13T22:29:26+0300  /usr/local/bin/VBoxBugReport*
OK     -rwxr-xr-x  root        wheel                 77  2022-01-13T22:29:26+0300  /usr/local/bin/VBoxDTrace*
OK     -rwxr-xr-x  root        wheel                 79  2022-01-13T22:29:26+0300  /usr/local/bin/VBoxHeadless*
OK     -rwxr-xr-x  root        wheel                 77  2022-01-13T22:29:26+0300  /usr/local/bin/VBoxManage*
OK     -rwxr-xr-x  root        wheel                 79  2022-01-13T22:29:26+0300  /usr/local/bin/VBoxVRDP*
OK     -rwxr-xr-x  root        wheel                 77  2022-01-13T22:29:26+0300  /usr/local/bin/VirtualBox*
OK     -rwxr-xr-x  root        wheel                115  2022-01-13T22:29:26+0300  /usr/local/bin/VirtualBoxVM*
OK     -rwxr-xr-x  root        wheel                 75  2022-01-13T22:29:26+0300  /usr/local/bin/vbox-img*
OK     -rwxr-xr-x  root        wheel                 80  2022-01-13T22:29:26+0300  /usr/local/bin/vboximg-mount*
OK     -rwxr-xr-x  root        wheel                 77  2022-01-13T22:29:26+0300  /usr/local/bin/vboxwebsrv*

~ $ pkg-file-info /usr/local/bin
Packages owning target file: /usr/local/bin
INSTALLED                  PKGID                             VERSION   LOCATION
2022-01-23T16:26:52+03:00  org.virtualbox.pkg.virtualboxcli  6.1.32    /usr/local/bin
2022-03-18T21:47:59+03:00  org.nodejs.node.pkg               v16.14.2  /

```
