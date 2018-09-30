# Hackintosh Build Guide for OSX Mojave - 10.14

Having had to rebuild my system this past weekend I thought I would document my journey for my Hackinstosh. This guide is intended as a roadmap as a fresh install for my developer setup.

> Be kind to your future self

## Prerequisites

- 8GB USB Drive
- OSX Mojave from the App Store
- 🤞 Lots of patience

## My System Specs

![All my parts are finally in, time to get building!](hw.jpg)

- NZXT Tempest 210 case
- GIGABYTE GA-Z87X-D3H motherboard
- Intel Core i5-4670K Haswell 3.4GHz
- 16GB memory
- Corsair CX500 Power Supply
- 256 SSD and 1TB HD

Hard to believe [this build is over 4years old][googleplus] and is still running great. Hackintosh's are very picky on hw so make sure you choose wisely. [Tonymacx86 Buyers Guide][buyersguide] is a great resource to choose from guaranteed working builds.

## Step One: Bootable USB

[![Mojave USB Creation](http://img.youtube.com/vi/f5Nn9DE_O4o/0.jpg)](http://www.youtube.com/watch?v=f5Nn9DE_O4o)

<figcaption>
  Great video explaining the process
</figcaption>

1. You will need to have a copy of Mojave from the App store.
2. Format USB Drive to `MacOS Extended(Journaled)` and name it `USB`.
   ![USB Creation](https://markwithtech.com/assets/files/2018-06-16/1529185565-56194-disk-utility-3.png)
3. Open Terminal and run:

```terminal
sudo /Applications/Install\ macOS\ Mojave.app/Contents/Resources/createinstallmedia --volume /Volumes/USB/
```

## Step Two: Clover Configuration

Clover configuration is a two part process. You'll have to do it once on the USB Drive and then again on the install drive. [TechHowdy][techhowdy] has a great guide for this.

### USB Drive Config

1. [Download Clover EFI Bootloader][clover]
2. Make sure your USB Drive is inserted.
3. On the Destination Select tab, click on the option Change Install Location.
4. Select the USB Flash Drive.
5. Now on the Installation Type Tab Click on the Customize option. Select the option Install for UEFI booting only.
6. Click on the Dropdown for Drivers64UEFI and Select the following options:

![Clover](http://techhowdy.com/wp-content/uploads/2018/06/How-to-Create-bootable-USB-for-Hackintosh-Mojave-20.png)

- AppleImageCodec-64.UEFI
- AppleKeyAggregator-64.UEFI
- AppleUITheme-64.UEFI
- DataHubDxe-64.UEFI
- FirmwareVolume-64.UEFI
- FSInject-64.UEFI
- SMCHelper-64.UEFI
- VboxHfs-64.UEFI
- Apfs
- OsxAptioFix2Drv-64
- PartitionDxe-64

7. Once it is completed, you can close Clover Bootloader.

### Copying Files to EFI partition on Hackintosh macOS Mojave USB Installer
1. Go to Finder and open mounted EFI. Now open the folder EFI > Clover > drivers64.
1. Copy the [apfs.efi][apfs] file in `drivers64` and the `drivers64UEFI` folder.
1. Now go back to the Clover folder and open the `kexts` folder.
1. Open the `Other` Folder in kexts.
1. Copy the [kexts][kextsLink] in the `Other` folder. 
1. Now go back to Clover folder and Delete `config.plist` file and Paste the `config.plist` [file][emptyConfig].

## Step Three: Install

## Step Four: Post-Install

## Step Five: Configuration

### Homebrew

### Git

### Terminal

### Editor

## Resources

[githubssh]: https://help.github.com/articles/connecting-to-github-with-ssh/
[nightowliterm]: https://github.com/nickcernis/iterm2-night-owl
[intel4600youtube]: https://www.youtube.com/watch?v=sL3JmGvbAxQ&t=47s
[mojaveinstallguide]: http://techhowdy.com/process-to-install-hackintosh-macos-mojave/
[alcsound]: https://www.reddit.com/r/hackintosh/comments/4e23w6/guide_native_audio_with_clover_applealckext/
[homebrewfonts]: https://github.com/Homebrew/homebrew-cask-fonts
[googleplus]: https://plus.google.com/+FrankPigeon/posts/H5Cm7CXGwxs
[buyersguide]: https://www.tonymacx86.com/buyersguide/building-a-customac-hackintosh-the-ultimate-buyers-guide/
[clover]: https://sourceforge.net/projects/cloverefiboot/
[techhowdy]: http://techhowdy.com/process-to-install-hackintosh-macos-mojave/
[apfs]: https://drive.google.com/open?id=1Rwtarw3zTXAXsBP6a9Aadul84lNR4x1R
[kextsLink]: https://drive.google.com/open?id=1cCO6xVnCuIPAQzBP4YQVnmZDNTevZJWE
[emptyConfig]: https://drive.google.com/open?id=1C7ZITyMw41I2yc_RoZR3apoR3C8eud1K