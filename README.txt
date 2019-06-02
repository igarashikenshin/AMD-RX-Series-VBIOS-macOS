Should Set BootROM is 138.0.0.0.0 or 140.0.0.0.0 ,
For macOS, Modify VBIOS Serial to
			113-4E353BU-O4E (Samsung) 
			113-4E3531U-O4V (Hynix)
			113-4E353BU-O50 (Micron)
(Serial 113-*E353**-*** is almost OK, 113-*E387**-*** is probably OK. 
		Do NOT Use 113-*E366**-*** For Serial.
		for example, 113-1E3660U-O51, 113-3E366DU-S4Y are NG to use Serial.
)

and For Windows, should use \config.h
		    of	113-3E366DU-S4Y (Samsung,Hynix)
			113-4E353WU-O67 (Hynix)
			113-BE366EU-Z48 (Micron)

For correctly working RX470/480/570/580, Should Set as "Radeon.png" (&See example.png,
https://forums.macrumors.com/threads/turn-a-new-sapphire-rx580-pulse-into-the-mac-edition-card.2101909/page-15#post-27274027)

or recommend to Use Kext relating Radeon from "10.14.0" or "10.14.5 developer beta 4".

in Terminal:
defaults write com.apple.AppleGVA forceATI -boolean YES
defaults write com.apple.AppleGVA forceSWDecoder -boolean NO
sudo update_dyld_shared_cache -force
REBOOT

Or sudo nvram boot-args="shikigva=96 shiki-id=Mac-7BA5B2D9E42DDD94"
Or sudo nvram boot-args="shikigva=61 shiki-id=Mac-7BA5B2D9E42DDD94"
Or sudo nvram boot-args="shikigva=41 shiki-id=Mac-7BA5B2D9E42DDD94"


if recognize wrong, try to change Board-ID basically "Mac-7BA5B2D9E42DDD94" 
or "Mac-F221BEC8" (because iMac19,1,iMac19,2 uses same properties of Mac5,1)