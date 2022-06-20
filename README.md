# foo2zjs
HBPLv1  driver for CUPS

This is based on Dave Coffin's work from here:
http://cybercom.net/~dcoffin/hbpl/

tweaked by a few people, most recently me: https://github.com/UltraSalem/

From Dave:
this is a Linux driver I wrote for printers that use Host Based Printer Language version 1. You cannot use these printers in Linux without my driver. Known HBPLv1 printer models are:

Dell 1250c

Dell C1660w

Dell C1760nw

Epson AcuLaser C1700

Fuji-Xerox DocuPrint CP105b
## The year is 2022. I have been running a windows VM for YEARS just to print. This driver never worked for me.
## I have created a new PPD file for the CP105b.
## I needed the hint from this blog https://blog.shines.me.uk/dell-1660w-linux-printer-drivers-ubuntu-18-04-lts/
## The line "and amended the problem file foo2hbpl1-wrapper.in so it can now uses number parameters, or paper strings parameters."
## I found it actually didn't allow numbers, using the fork he linked (maybe there was a regression?). So instead I just made the PPD file use the actual paper codes like 'a4' and 'letter' (for the paper sizes I will actually use. Might need tidying up to finish the other paper sizes. But after 4 hours hacking away at this just to print one address label, I am ready for bed.)

There's also an HBPLv2, already supported in Linux, which compresses image data more efficiently. Less expensive printers tend to avoid version 2, either because it requires more processing power, or because it uses patented technology.

This list may be incomplete. If the self-test page says "HBPL" but the printer won't work with Linux, it's probably version 1. To use an HBPLv1 printer, either download this modified foo2zjs package or apply this patch to the offical foo2zjs release.

## My cp105b test print page had "HBPL V2.13". But I couldn't get it to work, so have used hbpl1 for this implementation. I might try again with hbpl2 now that I kind of know what I am doing.

The essential commands are:

foo2hbpl1 to convert PBM, PGM, PPM, and PAM CMYK images to HBPLv1 format.

foo2hbpl1-wrapper to convert Postscript and PDF documents to HBPLv1 format.

hbpldecode to convert HBPL files, including those generated in other operating systems, to PGM or PPM images.

Images to print should be 5100x6600 pixels for US Letter paper or 4961x7016 pixels for A4 paper. Resolution is always 600x600 dpi. Stay at least 50 pixels (2mm) away from the edges to avoid clipping.


Printing HBPL files is easy -- either "cat" them to the printer device (/dev/usb/lp0 in my case), or use the "lpr" command.
