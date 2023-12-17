# Pick R83 

The original [Pick Operating System](https://en.wikipedia.org/wiki/Pick_operating_system) and database.

## Quickstart

There is a pre-built image:

```
wget https://github.com/Krowemoh/R83/raw/main/R83-HD.img 
qemu-system-x86_64 -curses -m 8M -drive format=raw,file=R83-HD.img
```

You can also load this image into [v86js](https://copy.sh/v86/) and run R83 directly in the browser. Make sure to limit the memory size to 8MB!

Otherwise you can use qemu or PCem to run the pre-built image.

## Software

You will need PCem to build a hard drive with R83 installed on it. You can then continue to use PCem to get into the hard drive or you can use qemu.

- [PCem](https://pcem-emulator.co.uk/downloads.html) - Working on v17

- [qemu](https://www.qemu.org/)

## Instructions

There are instructions and screenshots in [INSTRUCTIONS.md](https://github.com/Krowemoh/R83/blob/main/INSTRUCTIONS.md) to load R83 into PCem and building an image from scratch.
