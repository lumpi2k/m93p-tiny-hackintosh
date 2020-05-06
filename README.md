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

 - Catalina 10.15.4
 - iMessage
 - Airdrop
 - (almost) 4K60 through DP
 - Audio Out
 - Energy Management
 - FileVault
 - App Store
 - Wifi and Bluetooth

 ## What Doesn't Work

 This build is still a bit away from being golden. Here are my current issues:

 - no 4k60
 - no fan readout
 - no sleep
 - still a bit shaky energy management (though it could be that the CPU is just busy most of the time since it clocks up and don just fine)


# Useful Links
# Tools To Download
# Creating the Hackintosh