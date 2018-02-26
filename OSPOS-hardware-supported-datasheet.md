We known that a POS need a barcode reader, a cash drawer, a printer receipt as mention some hardware. Our open source pos support some device in some degree:

| Device  | Related information and documentation |
| ------------- | ------------- |
| Machine runtime | The hardware where OSPOS will run and server, could be any that runs php, mysql and the webserver. Inclusively can run in Androit or RasberryPi hardware, please see [our Hardware requirements wiki page (click here)](OSPOS-development-index#requirements) |
| Machine usage | The hardware where OSPOS will be consume an use it, could be any that runs Firefox or any modern web browser; wiki info at [OSPOS Installation requirements (click here)](OSPOS-development-index#tech-installation), Works perfectly at Mobiles but wrecommended a PC/MAC |
| Barcode scanners | Any barcode scanner will work as if programmed to hit return after scanning. Mobile barcode reading its not supported yet. |
| Printers  | Depends entirely of the browser and OS, wiki info at [OSPOS Printing wiki page (click here)](OSPOS-Printing), recommended Star TSP 143IIU and others normal printers should work. |
| Cash drawers  | Can be handle by some printers, but the manage of the cash drawers currently this are out of the scope due the system are web based.  |
| Credit Card Reader | Not suported. Currently there's no plans to work on. |
| Digital Signature Capture | Not supported yet |
