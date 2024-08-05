# Solid Gold library for Blitz Basic 2

A Blitz Basic wrapper for a few functions from Frank Willie's game Solid Gold (https://aminet.net/package/game/jump/SolidGold_Source), particularly for direct floppy disk access. From my limited testing, this seems to work in Blitz mode.

This is not well tested, use at your own risk.

Library number is $14, please consider recompiling the source (vasmm68k_mot -kick1hunks -Fhunkexe -nosym -o solidgold.obj solidgold.asm) if you need to change it.

## TD_Init ChipramBuffer.l, DirectoryBuffer.l, WriteBuffer.l
Initialises trackdisk.
ChipramBuffer MUST be a pointer to $1a00 * 2 bytes of chipram.
DirectoryBuffer MUST be a pointer to 512 bytes of ram.
WriteBuffer OPTIONALLY must be a pointer to 11*512 bytes IF write functions are to be used.

## Error = TD_SelectDisk(DiskID.l)
Selects a floppy disk by the long word at $8 of the disk. It will attempt to check all drives, and return an error if the disk isn't found in any of them.
This needs to be run before any other read/write commands.

## Error = TD_Read(FirstBlock.w,NumBlocks.w,Destination.l)
Read a sequence of blocks from disk. Turns on the motor automatically.
Blocks are a division of 512 bytes

## Error = TD_Write(FirstBlock.w,NumBlocks.w,Source.l)
Write a sequence of blocks to disk. Turns on the motor automatically.
Blocks are a division of 512 bytes

## Error = TD_Format(Track.w,Source.l)
Overwrites an entire track with new contents.

## TD_MotorOff
Turns off the disk motor and unselects the disk.
