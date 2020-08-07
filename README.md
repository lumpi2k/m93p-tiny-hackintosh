# m93p-tiny-hackintosh
a Repository containing files for turning a Lenovo M93p tiny into a shiny hackintosh
# Introduction
Setting up Hackintoshes can be a pain and there is a lot to consider. In this Repo I want to document my journey of turning a Lenovo M93p Tiny PC into a Hackintosh running Catalina with the Opencore Bootloader.

 ## My Configuration

 M93p tiny PCs come in many different configurations and here's mine:

 - Intel i5 4570T CPU
 - Intel HD 4600 integrated GPU
 - Q87 Chipset
 - 8GB DDR3 RAM
 - some SSD I had lying around
 - Intel Wifi Card (replaced with a Broadcom BCM94352)

 As far as I'm aware there are M93p out there that don't have any Wifi preinstalled, which would make upgrading the antennas and Wifi card a bit more cumbersome later, though if you don't plan to use Wifi you could save some money here.

 Also there's quadcore configurations out there, which would give you a bit more power, so if you can get one of these, go for it. I found that the most crucial component is the integrated GPU though. My model uses the natively supported HD4600 variant. If yours uses a mobile iGPU like HD4400, prepare for some more fiddling.

 ## What Works

 - Catalina 10.15.6
 - iMessage
 - Airdrop
 - 4K60 through DP
 - Audio Out
 - Energy Management
 - FileVault
 - App Store
 - Wifi

 ## What Doesn't Work

 This build is still a bit away from being golden. Here are my current issues:

 - some glitching in 4k60 with esoteric browsers (Edge Chromium)
 - no fan readout
 - no sleep
 - still a bit shaky energy management (though it could be that the CPU is just busy most of the time since it clocks up and down just fine)
 - Bluetooth with my particular wifi card


# Useful Links
https://dortania.github.io/OpenCore-Install-Guide/ - The OpenCore Desktop Guide is the most important bit of info for this build.

# Tools To Download
https://github.com/corpnewt/gibMacOS - gibMacOS lets you download MacOS recovery images directly from Apple.

https://github.com/corpnewt/ProperTree - ProperTree is a nice plist editor. It's cross platform, so you can use it both when preparing the files in Windows and later in MacOS.

https://github.com/corpnewt/GenSMBIOS - GenSMBIOS is used to create a valid serial number for your hackintosh so you can use iMessage and other iCloud services later.
# Creating the Hackintosh

## Creating the USB Installer
Assuming you're using Windows the [OpenCore Desktop Guide][3] has a very thorough manual on how to use gibMacOS to obtain a legit recovery image of MacOS. I used Catalina 10.15.4.

If you follow this guide you should end up with a drive named "BOOT" with an EFI folder in it.

## Preparation of the EFI Folder
First you should clone or download this repo and the tools I recommended. If you have the same system config as my Lenovo tiny PC there's only one thing you have to set in the config.plist located under EFI/OC/

As you can see in https://github.com/lumpi2k/m93p-tiny-hackintosh/blob/caf13bc817f28be0f482b7b1a78febe9a7ae8a4b/EFI/OC/config.plist#L769-L798

```
	<key>PlatformInfo</key>
	<dict>
		<key>Automatic</key>
		<true/>
		<key>Generic</key>
		<dict>
			<key>AdviseWindows</key>
			<false/>
			<key>MLB</key>
			<string>PUT YOUR OWN HERE</string>
			<key>ROM</key>
			<data>AAAAAAA=</data>
			<key>SpoofVendor</key>
			<true/>
			<key>SystemProductName</key>
			<string>iMac15,1</string>
			<key>SystemSerialNumber</key>
			<string>PUT YOUR OWN HERE</string>
			<key>SystemUUID</key>
			<string>PUT YOUR OWN HERE</string>
		</dict>
		<key>UpdateDataHub</key>
		<true/>
		<key>UpdateNVRAM</key>
		<true/>
		<key>UpdateSMBIOS</key>
		<true/>
		<key>UpdateSMBIOSMode</key>
		<string>Create</string>
	</dict>
```

I blanked my own serial info in the config.plist. This means you'll have to create your very own set of serials.

The OpenCore Desktop Guide shows this in it's chapter  [Fixing iServices][1]. **Don't skip this step, it is very important!** I've left the model iMac15,1 in the config, but you can also use iMac14,1 or iMac14,2 (these should technically work a little better since they're the exact CPU generation. I found no difference though.)

After you've created the SMBIOS with GenSMBIOS put in the values as described [here in the Desktop Guide][2].

You can then follow [this chapter][4] in the OpenCore Guide to see where all the files have to be placed on your boot drive. If everything looks correct, see [this chapter][5] for info on how to boot and install MacOS. You should be all good after installation.

## Versioning of this Repo

I'll loosely update the OpenCore Version and kexts in this repo. This includes Updates to the config.plist. I'll create tags for every OpenCore Version I use. This will include the most recent kext versions from the time I update my machine myself. Since updating OpenCore is a lot of work and my machine runs fairly stable I won't create a release for every OpenCore version.



[1]: https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#generate-a-new-serial
[2]: https://dortania.github.io/OpenCore-Install-Guide/config.plist/haswell.html
[3]: https://dortania.github.io/OpenCore-Install-Guide/installer-guide/winblows-install.html
[4]: https://dortania.github.io/OpenCore-Install-Guide/installer-guide/opencore-efi.html
[5]: https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#double-checking-your-work