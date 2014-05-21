Tasker.Trusted-Devices
======================
Mimic the "Trusted Devices" feature of the Moto X.

## Requirements
* Tasker (Android App)
* Secure Settings (Tasker Plugin)
* Root Access (for manipulating the Lock Screen)

## Version History
* v0.1 - Initial functional release.
* v0.2 - Fixed bugs, issues with unwanted disabling of the lock screen.

## What does it DO?
I used a Moto X for a good long while and it was my absolute favorite phone I've ever used.  One thing made it so handy for me while riding my bicycle or driving the car was the "Trusted Devices" feature.  The feature basically leaves the phone unlocked while a trusted device is connected.

On the Moto X the device was always a Bluetooh device.  I use both my headset and my headphones as trusted devices as they are both Bluetooth.  This can use any device that Tasker can setup as a "State" (WiFi access point, location, etc..) as long as you can sent an entry and exit event, it can be used.

## How do I use it?
### The Short Version
Simple configure a profile in Tasker that has both an entry (when condition is true) and an exit (when condition is no longer true) the entry should be the "Trusted Device Connected" action and the exit should be the "Trusted Device Disconnected" profile.  There, done.  You can have as many of these potential profiles true at any given time, only when NONE of them are true will trusted mode be disabled.

### The Long Version
The basic idea in using this is to be able to have as many trusted conditions true at the same time as you might need.  For instance, you may want to set things up so that your lock screen disables if you're at home on your local WiFi.  At the same time you might also have it set up so that if you're connected to your car's bluetooth system your lock screen is also disabled.

Assuming you start at home and leave for, lets say work, both of these conditions could be true at the same time.  Rather than directly enable or disable the lock screen directly which would be complicated to decide when you're in you car, but leave your home WiFi on your way to work, to keep the lock screen disabled or enable it again.  To simply this we store how many trusted conditions are true in a variable.  Then a profile does nothing but watch that number, if the number is > 0, trusted mode is on.  If the number is 0 (should never be below, but that isn't protected against) trusted mode is turned off.

This way, if you are in your car and on its Bluetooth, then get home and connect to the WiFi but turn your car off and its Bluetooth goes away.  The system knows that at least one of your trusted conditions is still true and leaves your lock screen off.

## Security Concerns
Please be aware that in doing this you are making a certain set of conditions where your lock screen will not enable.  Just like with the Moto X if a device is locked and a trusted device is connected, it will wait for an unlock before disabling the lock screen.  After that, until the trusted device (or condition) is no longer true it the lock screen will not enable.

### What do you need root for EXACTLY?
Specifically, root is required by the Secure Setting plugin for Tasker.  While root is not used to perform the action itself, it is required for Secure Settings to install its "System+" module which requires system privileges to work.  If you can get the System+ module to work without root, things should work just fine.

### Secure Settings Functions Used
* Lock Screen Timeout (System+ Action)
* Keyguard (Standard Action)

## Bugs and Issues
So far I've been testing this for a few days now, there aren't any major bugs that I can see other than the fact that some phones are particularly tenacious about keeping your lock screen enabled.  This is understandable since it is your lock screen and you don't want a random program Bob at the officer finds a way to install on your phone to trigger and disable your lock screen.

* The lock screen does occasionally re-enable itself.

I'm testing this on an HTC One m8 from Verizon running rooted stock OS.  I think that using CyanogenMod or another ASOP based varient may be different, I assume it'll be easier to keep the lock screen disabled but I could be wrong.

When the lock screen reenables itself the behavior is erratic, at times it locks the phone immediately.  Most common on my phone is next time I hit the "Home" button it shows the lock screen.  Once this happens you must enter the PIN code, Pattern Lock, Face Recognition, or Password required to unlock the phone.