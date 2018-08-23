# Z50AYMSound

This is a AY3-8910 / YM2149 based sound/audio/chipmusic card designed
originally for the LiNC80 SBC1 microcomputer, but should be usable
on compatible Z50Bus systems, and also other Z80-based systems with a
suitable bus adapter.

The design of this card is based on an early prototype made by Jon Langseth,
adapted to the Z50Bus. The main "invention" is the address decode/glue logic,
the rest of the circuit is a fairly standard implementation of an AY3-8910
circuit for the Z80. Some inspiration in the analog section comes from the
"Simple AY interface" from hw.speccy.cz, as well as the ZX Spectrum output.

KiCad schamtic and layout files are in the CADFiles directory.
Example software is in the JLPTxPlay directory.

For information about the LiNC80 SBC1, see http://linc.no/go/linc80
For information about the Z50Bus, see http://linc.no/products/z50bus/

## Address selection

The card has a dip-switch for selecting the base address, fully decoded to
any even I/O address. Writing to the Base address sets the selected register,
while writes or reads on Base+1 writes/reads the selected address.

## Stereo control

Selection of ABC/ACB stereo can be done by setting a pair of jumpers either
horizontally or vertically on a pair of jumpers. A simple "fake mono" jumper
is included, it simply shorts Left and Right channels after the output
resistor network.

## Clock generator and tuning

Clock generation for the AY/YM is done using a dedicated, on-board canned
oscillator. A standard, square metal can oscillator in the 8-pin-DIP form
factor should be used. The Address select DIP switch used is 8-way, only 7 
of those are used to achieve even-address-selection. The final switch 
position is used to control the YM2149 pin 26, allowing for selection of 
full or half audio clock. When used with an AY3-8910, this pin does nothing.
As such, any oscillator in the 0-2MHz range can be used with the AY3-8910,
while any oscillator in the 0-4MHz range can be used with an YM2149.
Selection of oscillator decides the tuning of output audio. A value as
close as possible to 1.77MHz will provide tuning close to Spectrum audio.
An easily available and reasonably close variant is 1.8432MHz. A better
option is 3.57954 being a very good candidate for an YM2149 with half-clock.

## Layout

The layout is done on a Standard Z50Bus card, with 100x100mm dimensions.
There was significant "dead space" on the card, so just under half the
board is converted to a prototyping area, with the two digital I/O ports
of the AY/YM provided on a single row of pins.

## Example source code

The example source code is a modified version of Sergey Bulba's PTxPlay.
The base of the code provided here is not directly based on the original
source, but is an extended modification of the version that Ed Brindley
made available for his rc2014-ym2149 sound-card for the RC2014.
See https://github.com/electrified/rc2014-ym2149 for Ed's version,
see https://bulba.untergrund.net/main_e.htm for Sergey Bulbas original version.

## Support documentation

Data sheets for both the AY3-8910 and the YM2149 is included in the
Documentation directory.
