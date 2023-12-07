# Pick R83 

The original [Pick Operating System](https://en.wikipedia.org/wiki/Pick_operating_system) and database.

## Quickstart

There is a pre-built image:

```
wget https://github.com/Krowemoh/R83/raw/main/R83-HD.img 
qemu-system-x86_64 -m 8M -hda R83-HD.img 
```

You can also load this image into [v86js](https://copy.sh/v86/) and run R83 directly in the browser. Make sure to limit the memory size to 8MB!

## Software

You will need PCem to build a hard drive with R83 installed on it. You can then continue to use PCem to get into the hard drive or you can use qemu.

- [PCem](https://pcem-emulator.co.uk/downloads.html)

- [qemu](https://www.qemu.org/)

## R83 from Scratch 

This is the instructions to install Pick R83 inside PCem. The hard drive that get's created at the end of this process also works with qemu so that's a pretty big bonus in my eyes.

This is PC 3 R83 V3.1 04 July 1990 - 2 User

This is working with PCem 17 under Arch Linux.

### Creating a AMI 486 Clone

To get R83 going, we will need to first create the universe.

1. Launch PCem

2. Click on the New button and enter a new name

3. Set up the Motherboard tab 
    1. Set Machine to [486] AMI 486 Clone
    2. CPU should be Intel i486DX2/66
    3. Memory should be 8MB

4. Set up the Hard Drive tab
    1. Set HDD to [IDE] Standard IDE
    2. Set FDD1 to 3.5" 720k
    3. Set FDD2 to None

5. Create a new hard drive
    1. Click on the new hard drive button, this will bring up a new tab.
    2. Set Image Format to Raw
    3. Set New File name
    4. Size is set to 25. (This should be set to 512.)
    5. Sectors should be 63.
    6. Heads should be 16.
    7. Cylinders should be 50.
    8. Type is Custom

You will need to remember the sectors, heads and cylinder numbers as we will need it to set up the bios. 

Hit Ok to save everything and this will build out a machine. 

### Installing R83

Now that the machine is set up, we can install R83. Start the machine we just built by selecting it and then pressing the play button.

This will put you at the AMI bios screen. 

1. Press F1 to enter the bios.

2. Enter Standard CMOS Setup by pressing Enter
    1. Hit enter to get past the warning page

3. Use the arrow keys to navigate the Setup Program. Page Up and Page Down will cycle through options.
    1. Set Hard Disk C: Type to 47 = User Type
        i. This will let you set the Cylinders, Head, Sect and Size to the ones that you saved above.
    2. Set Floppy Drive A: to 720KB, 3 1/2"

    3. Press Escape to exit the Standard CMOS Setup 

4. Use the arrow keys to go to Write to CMOS and Exit
    1. Enter Y to Write it out and Exit

5. We should be returned to the bios, we need to press F1 to enter the bios again.

6. Press Escape and then Y to exit without saving.

7. Now it will continue through and it will ask to insert a BOOT diskette.
    1. Right click on the PCem window
    2. Disc -> Change Drive A:
    3. Select the patched disk disk1.patched.img
    4. Once selected, press Enter

8. We should see the Disk being read and Pick is ready to be installed.

9. We should hit the Monitor options now.
    1. Press T to disable the hard disk scan. This will speed things up. 
    2. Press Enter

10. It will list out the installed serial cards.
    1. Press Y to continue

11. Now it will say the ABS area is being initialized. Be patient.

12. The next prompt is to put in the next disk. 
    1. Right click on the PCem window and change Drive A to disk2.img
    2. Press C to continue

13. This should take a second and then will display some information about the entire system. It will then put you at the Media Selection menu.
    1. Press S for the Standard density floppy

14. Now it will prompt you to enter the Pick Data Files disk.
    1. Right click on PCem window and Change Drive A to the data1.img
    2. Press C to continue

15. You will see a list of files being setup and copied.

16. Once the previous step finishes, you will be prompted for the next data disk.
    1. Right click on the PCem window and change Drive A to the data2.img 
    2. Press C to continue

17. Watch as some more files get set up.

18. The next prompt is to Initialize the ABS frames.
    1. Press Y

19. Now you will be prompted to enter in a Country Code
    1. I use US, so press Enter without entering anything as it's the default

20. The next prompt askes for your keyboard type.
    1. Press B for the 101 keys keyboard

21. The next prompt let's you set the shutdown delay, the default is 512.
    1. Press Enter for the default

22. The next prompt is to set the date.

23. The next prompt is to set the time. 

24. The next prompt is to restore an account from a backup.
    1. Press N as I don't have an account to restore.
 
25. The next prompt is to update the accounts.
    1. Press Y because why not.

26. Watch in panic as illegals and protected fly by.

27. The next prompt will ask to create any new accounts
    1. Press N for not right now.

28. The next prompt is to set up passwords.
    1. Press N because security is for wimps.
 
29. SYSTEM setup completed.

30. Press T to Enter TCL

We should now be sitting at TCL in the PICK-SETUP account.

### Minutiae

R83 has some protection and so we will need to patch disk 1 directly.

The work was done by [intel8088 of retrowiki.es](https://www.retrowiki.es/viewtopic.php?style=4&f=58&t=200037833). I followed their instructions but my version was slightly different so my no-ops were off.

The first line of each set is what is in the original. The second line is what I changed the line to. 90 90 is the no-op.

```
74 03 e9 0f 00 86
90 90 e9 0f 00 86

39 1e f8 0a 75 15 be e0 89 
39 1e f8 0a 90 90 be e0 89

e8 1b 00 72 0c 58 80 f0 
e8 1b 00 90 90 58 80 f0


0039 1efa 0a75 061f 595b
0039 1efa 0a90 901f 595b
```

Both the patched and original version are here. 


