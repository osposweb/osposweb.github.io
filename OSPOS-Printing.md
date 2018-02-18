The printing depends of the print setup and the print behaviour.. The recommend receipt 
is the Star TSP 100 ECO using the Firefox or Chrome browsers, with this if there's no fiscal kit, 
we can print directly. Our recommended label printer is the Zebra LP 2824 Plus printer with 2 x 1 labels. 
Other customers have had success with other printers from companies. If you plan to purchase a different receipt printer than the recommend, try to get one that prints on paper that is 72 mm or greater.

Obviously prints depends of the browser, so must be first configure here, and then in ospos 
the printing configuration has some options, only enable with some changes over the browser.
For the Zebra its recomended also search at https://www.peninsula-group.com/mac-thermal-printer-driver/ 
the CUPS interface for Unixes comes with basic enought support that works as its.

## General Printing

First need OS configuration/installation printer, then browser configuration and lasted go to **Office->StoreConfig->Invoice**, here the most important settings are *Format* and *Font size*.

* **Format** defines how the receipt will be printed, if *Default* will out and let control printing default area, 
but if *Order* will print defined sale receipt area, and bypass some settings, please for that see notes below.
* *FontSize* defines size of the font this must be set in correct size number depending of the output of the printing.

The **Autoprinting** are explained here in below specific section. The format `Order` must be selected for.

Unless margings and show dialog printing option rest of the options are self xplanatory, those two options need 
extra work in the web browser, please read section below for.

### Preparation printing for firefox/palemoon

1. download, configure and install the printer in the OS, and config that can print a simple letter at least.
2. In firefox, Palemoon, Icecat click the menu button at top right of screen (three horizontal bars)
3. Choose Print
4. Click Page Setup (Make sure print background images is unchecked)
5. Click Margins & Header/Footer
6. Set all margins to 0.
7. Set Headers and Footers to --Blank--

### Preparing printing for Chome/Chromium

1. download, configure and install the printer in the OS, and confir that can print a simple letter at least.
2. In the menu button at top right of screen (three horizontal bars) select Print
3. In the dialog the pops up, select the printer destination that just instaled and configured in OS
4. In same dialog, click "More settings", or "advanced settings"
5. and select Layout:Portrait, Paper:75mm, Margings:default, 
6 also in Options deactivate headers and deactivate background

## Recommended Printing settings

Remenber that the printer its recomended 75mm paper setup.

1. Go to OS printers interface, in MAC/Linux got CUPS at http://localhost:631
2. Select the printer and then Printer Properties
3. Click Device Settings Tab or General Options
4. In the Form to Tray Assignment or Media size choose 72mm x Receipt
5. Cash Drawer options select 1 and 2
6. Choose media of 2x1 and resoltuo

# Advanced and Autoprinting

Advanced printing allows set margins, and the "direct printer" to, only by selecting the "Order" format.

This feature is currently available in combination with browsers Palemoon, Icecat, Iceweasel, Firefox and with some little changes in Chrome. Theres another way to do by changinh deep settings in firefox `about:config` interface options.

### Firefox, Palemoon, Icecat

AutoPrinting support also advanced feature are only enabled with installing the jsPrint addon at
https://addons.mozilla.org/es/firefox/addon/js-print-setup The supported browsers must be **firefox << 49.9**, **Palemoon >> 24**, and **Icedcat >> 16**. The new Firefox Quantum and chrome api are not supported, 
newer firefox can try https://addons.mozilla.org/es/firefox/addon/seamless-print/

Enable jsprint/seamlessprint settings in Firefox, must configure with enable for all the sites (low security, sorry).

After enabling/configurie this addon, the osposweb print settings will be available and can be configured.

Go to Store config and reselect the printers, occasionally had to select a different printer. Submit. 
Then go back and select the correct printer. Then submit.

**Alternate way**: Type about:config at Firefox’s location bar and hit Enter. Right click at anywhere on the page and select New > Boolean.  Enter the preference name as print.always_print_silent and click OK. Then set the boolean value to true. Restart firefox. This need that the default OS printer must be the desired receipt printer.

### Chrome

Not recomended, but receipt auto printing is also available in Chrome by using kiosk mode. A printer 
should be selected once after launching Chrome using a custom shortcut.

A new icon application laucher or lauch/invoke the binary adding the `--kiosk --kiosk-printing ` option 
to the executable. By the way, to make the kiosk mode effecting you need to close all the chrome 
apps and restart otherwise it doesn't work. Open a Terminal, and write the command: `google-chrome --kiosk --kiosk-printing `

After enabling/configure kiosk, the osposweb print settings will be available and can be configured.

Go to Store config and reselect the printers, occasionally had to select a different printer. Submit. 
Then go back and select the correct printer. Then submit.

## Fiscal printing

Some countries need some special communications with internal chip in the printers, this feature are 
only done locally and its not possible unless a specific ad-hoc can be done or with special device that 
receive the raw printing and send from the browser to the printer.
