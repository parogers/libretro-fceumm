[![Build Status](https://travis-ci.org/libretro/libretro-fceumm.svg?branch=master)](https://travis-ci.org/libretro/libretro-fceumm)
[![Build status](https://ci.appveyor.com/api/projects/status/etk1vcouybahdbkt/branch/master?svg=true)](https://ci.appveyor.com/project/bparker06/libretro-fceumm/branch/master)

# FCE Ultra mappers modified/FORK

This is a fork of the official libretro-fceumm package. This fork allocates the NES emulator RAM as a block of shared memory under '/dev/shm/fceu-shm', allowing it to be accessed by external programs. (eg peeking and poking bytes, extracting high scores, and otherwise reading or manipulating game state)

There are some scripts for playing with this here:

https://github.com/parogers/nes-high-scorer

The original FCEUmm README text is here:

FCEU "mappers modified" is an unofficial build of FCEU Ultra by CaH4e3, which supports a lot of new mappers including some obscure mappers such as one for unlicensed NES ROM's.

## Installing

Download the source, run 'make' within the root source folder and everything
should build okay. (assuming you have all dependencies installed) If you're
trying to integrate this with an existing retropie distro, you'll need to
update the emulators.cfg and have it use new newly built .so file. That file
is found under '/opt/retropie/configs/nes/emulators.cfg'. Change the first
line so that the path after '-L' points to the new library:

> lr-fceumm="/opt/retropie/emulators/retroarch/bin/retroarch -L /home/pi/libretro-fceumm/fceumm_libretro.so --config /opt/retropie/configs/nes/retroarch.cfg %ROM%"
> (snipped)

Oddly, when I ran retroarch with the library keyboard input stopped working.
It was working fine using the original library, and working fine with the new
library on my development machine. It is possibly caused by using an older
version of retroarch, but a newer version of the plugin. (on my development
machine I checked out the most up-to-date copies from git)

My fix was to include a line in '/opt/retropie/configs/nes/retroarch.cfg',
at the very end of the file:

> input_libretro_device_p1 = "257"

