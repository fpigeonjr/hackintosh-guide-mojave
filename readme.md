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

### Copying Files to EFI partition on Hackintosh macOS Mojave USB Installer

1. Go to Finder and open mounted EFI. Now open the folder EFI > Clover > drivers64.
1. Copy the [apfs.efi][apfs] file in `drivers64` and the `drivers64UEFI` folder.
1. Now go back to the `Clover` folder and open the `kexts/Other` folder.
1. Copy the [kexts][kextslink] in the `Other` folder.
1. Now go back to Clover folder and Delete `config.plist` file and Paste the empty `config.plist` [file][emptyconfig].

## Step Three: Install

1. Boot from your new USB Drive (on USB2 port) and when it boots up, Go to `Disk Utilty` and format your SSD to use `APFS`.
2. Install MacOSX Mojave.
   -During installation process the Mac OS will reboot several Times.

## Step Four: Post-Install

1. Now you will need to do Clover EFI steps again but this time to your new Mojave SSD. Follow same steps as in Step 2 but choose Mojave SSD rather than the USB Drive.
2. I had issues with Intel 4600 video and sound drivers.

- Sound Issues with my [ALC 892 kexts solution][alcsound]. I've added the sound kexts and Lilu so hope this won't be an issue.
- Video issue was not using 2K screen to full resolution. Solution was found in this [YouTube Video][intel4600youtube] that describes using Clover Configuration to tweak video settings.

3. Save Clover Configuration and reboot to make sure everything is working.

## Step Five: Configuration

The next steps are not related to Hackintosh installation but just things specific to my dev setup.

### Homebrew

First things first is to get [Homebrew setup](https://brew.sh/).

```terminal
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Next install development tools.

```terminal
brew install brew-cask-completion git node python sqlite yarn	zsh-syntax-highlighting gdbm icu4c openssl readline tree zsh gettext libyaml pcre2 ruby xz zsh-completions
```

Next install programs from brew casks.

```terminal
brew cask install adobe-creative-cloud etcher font-inconsolata font-source-code-pro moom transmission alfred firefox font-merriweather font-source-sans-pro plex-media-server visual-studio android-file-transfer font-fantasque-sans-mono font-open-sans google-chrome rocket visual-studio-code bitwarden font-fira-code font-pacifico iterm2 sensiblesidebuttons vlc caffeine font-fontawesome font-raleway mono-mdk slack
```

### Git

[First Time Setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)
<br/>
[vscode as default git editor](https://stackoverflow.com/questions/30024353/how-to-use-visual-studio-code-as-default-editor-for-git)
<br/>
[Git configuration for use with Github and SSH](https://help.github.com/articles/connecting-to-github-with-ssh/).


### Terminal

I use Iterm2 and [oh-my-zshell](https://github.com/robbyrussell/oh-my-zsh) with [night owl iterm theme][nightowliterm].

### Editor

I am using Visual Studio Code with these extensions.

- advanced-new-file
- Auto Rename Tag
- Bracket Pair Colorizer
- Cobalt2 Theme
- colorize
- ESLint
- File Utils
- Material Icon Theme
- Night Owl
- npm Intellisense
- Path Intellisense
- Prettier
- Simple React Snippets
- Sublime Text Keymaps
- SVG Viewer
- TODO Highlight
- vscode-styled-components

## Credits

### [Step By Step Process To Install Hackintosh macOS Mojave][mojaveinstallguide]

### [GUIDE - Create Mojave 10.14 Hackintosh USB Installer](https://markwithtech.com/d/183-guide-create-mojave-10-14-hackintosh-usb-installer)

[githubssh]: https://help.github.com/articles/connecting-to-github-with-ssh/
[nightowliterm]: https://github.com/nickcernis/iterm2-night-owl
[intel4600youtube]: https://youtu.be/sL3JmGvbAxQ
[mojaveinstallguide]: http://techhowdy.com/process-to-install-hackintosh-macos-mojave/
[alcsound]: https://www.reddit.com/r/hackintosh/comments/4e23w6/guide_native_audio_with_clover_applealckext/
[homebrewfonts]: https://github.com/Homebrew/homebrew-cask-fonts
[googleplus]: https://plus.google.com/+FrankPigeon/posts/H5Cm7CXGwxs
[buyersguide]: https://www.tonymacx86.com/buyersguide/building-a-customac-hackintosh-the-ultimate-buyers-guide/
[clover]: https://sourceforge.net/projects/cloverefiboot/
[cloverconfig]: https://mackie100projects.altervista.org/download-clover-configurator/
[techhowdy]: http://techhowdy.com/process-to-install-hackintosh-macos-mojave/
[apfs]: https://drive.google.com/open?id=1Rwtarw3zTXAXsBP6a9Aadul84lNR4x1R
[kextslink]: https://drive.google.com/open?id=1cCO6xVnCuIPAQzBP4YQVnmZDNTevZJWE
[emptyconfig]: https://drive.google.com/open?id=1C7ZITyMw41I2yc_RoZR3apoR3C8eud1K
