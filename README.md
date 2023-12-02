# blog

informations utiles et tutos pour mon Homelab

- [Wiki](https://github.com/Arch30n/blog/wiki)


LED SAS Drive : sdparm --set=RLM --save /dev/sdl

Locate disk by LED
sas2ircu list
identify hba number (probably 0)
sas2ircu 0 display
find drive in list note enclosure and slot number. if its enclosure 2 slot 21
sas2ircu 0 locate 2:21 ON
and that should flash the "issue light"

sas2ircu 0 locate 2:21 OFF
to turn it back off


Hugo Utiliy for HGST drives
https://www.truenas.com/community/resources/hugo.203/

512e to 4Kn
https://www.truenas.com/community/threads/troubleshooting-disk-format-warnings-in-truenas-scale.106051/page-9
