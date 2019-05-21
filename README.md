DualOptiboot
============

Customized Optiboot bootloader allows reflashing Moteino/AVR boards from an external serial FLASH memory chip.
This makes it possible to wirelessly program a Moteino remotely by first transferring the compiled HEX binary wirelessly (ex. with an RFM69 transceiver), then restarting the board to allow the bootloader to pick it up and reflash the atmega's program area.
Copyright Felix Rusu (2013-2019), lowpowerlab.com/contact
More at: http://lowpowerlab.com/Moteino

This Optiboot version is modified to add the capability of reflashing 
from an external SPI flash memory chip. As configured this will work 
with [Moteino](www.lowpowerlab.com/guide/moteino) provided a SPI flash chip
is present on the dedicated onboard footprint.
Summary of how this Optiboot version works:
- it looks for an external flash chip
- if one is found (SPI returns valid data) it will further look
  for a new sketch flash image signature and size
  starting at address 0:   FLXIMG:9999:XXXXXXXXXXX
  where: - 'FLXIMG' is fixed signature indicating FLASH chip
           contains a valid new flash image to be burned
         - '9999' are 4 size bytes indicating how long the
           new flash image is (how many bytes to read)
         - 'XXXXXX' are the de-hexified bytes of the flash 
           pages to be burned
         - ':' colons have fixed positions (delimiters)
- if no valid signature/size are found, it will skip and
  function as it normally would (listen to STK500 protocol on serial port)

The added code will result in a compiled size of just under 1kb
(Originally Optiboot takes just under 0.5kb)

-------------------------------------------------------------------------------------------------------------

To compile copy the Optiboot.c and Makefile files where Optiboot is originally located, mine is at:
arduino-install-dir\hardware\arduino\bootloaders\optiboot\
Backup the original files andbefore overwrite both files.
Then compile by running:
make atmega328
make atmega1284p

##License
GPL 3.0. See License.txt file.