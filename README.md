# openvpn-scramble

The Scramble options can be used to obfuscate the connection this can be useful to escape censoring.
It is supported by a number of OpenVPN providers e.g. TorGuard, [StrongVPN](https://blog.strongvpn.com/strongvpn-scramble/), IPvanish etc.
For some backgroend please read: https://tunnelblick.net/cOpenvpn_xorpatch.html

Scramble options must be added to OpenVPN by adding a series of patches and compilie your own build with it (or the OpenVPN-OpenSSL package)

Patches are available for OpenVPN 2.5.x and for 2.6.x and are based on Tunelblick's patches but adapted to work seamlessly with with OpenWRT

## To compile:
Copy all patch files to `feeds/packages/net/openvpn/patches`
For OpenVPN 2.5.x use the patches form the 2.5 directory
For OpenVPN 2.6.x use the patches from the 2.6 directory, but take note this is not comaptible with DCO so for OpenVPN 2.6.x add to the makefile (`feeds/packages/net/openvpn/makefile): --disable-dco

On compiling the patches are executed automatically

## Usage
Note: scramble options must be the same on client and server side!

In the OpenVPN config add:
scramble "password"
scramble is the leftmost option name. This can be followed by a string which will be used to perform a simple xor operation the packet payload.
Note for tunnelblick this option is:
scramble xormask "password"

However if the following is used instead, a different action will occur.
scramble reverse
This simply reverses all the data in the packet. This should be enough to get past the regular expression detection in both China and Iran.

scramble xorptrpos
This performs a xor operation, utilising the current position in the packet payload.

scramble obfuscate "password"
This method is more secure. It utilises the 3 types of scrambling mentioned above. "password" is the string which you want to use.

Both DDWRT OpenVPN Client and server supports scramble there are also clients available for Android and Windows:
https://github.com/lawtancool

Android:
https://github.com/lawtancool/ics-openvpn-xor/releases

Windows:
https://github.com/lawtancool/openvpn-windows-xor/releases

See also:
https://forum.openwrt.org/t/scramble-obfuscate-in-openvpn/151570



