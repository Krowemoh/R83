# Pick R83 

The original [Pick Operating System](https://en.wikipedia.org/wiki/Pick_operating_system) and database.

## Quickstart

There is a pre-built image:

```
wget https://github.com/Krowemoh/R83/raw/main/R83-HD.img 
qemu-system-x86_64 -curses -m 8M -drive format=raw,file=R83-HD.img
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

![image](https://github.com/Krowemoh/R83/assets/8527895/095c9f92-78c4-43bf-8ab4-6501054a93f6)

4. Click on the New button and enter a new name
   
![image](https://github.com/Krowemoh/R83/assets/8527895/29898376-8eb0-4da0-a488-861ec1dfc9f1)

6. Set up the Motherboard tab 
    1. Set Machine to [486] AMI 486 Clone
    2. CPU should be Intel i486DX2/66
    3. Memory should be 8MB

![image](https://github.com/Krowemoh/R83/assets/8527895/62d0f09f-30f9-4a75-9b0e-fddad9ddef68)

7. Set up the Hard Drive tab
    1. Set HDD to [IDE] Standard IDE
    2. Set FDD1 to 3.5" 720k
    3. Set FDD2 to None

![image](https://github.com/Krowemoh/R83/assets/8527895/059967a8-2f18-4f0f-b0e3-4a9193d69919)

8. Create a new hard drive
    1. Click on the new hard drive button, this will bring up a new tab.
    2. Set Image Format to Raw
    3. Set New File name
    4. Size is set to 25. (This should be set to 512.)
    5. Sectors should be 63.
    6. Heads should be 16.
    7. Cylinders should be 50.
    8. Type is Custom

![image](https://github.com/Krowemoh/R83/assets/8527895/274fdcb6-71da-40c6-8dcf-890607507986)

You will need to remember the sectors, heads and cylinder numbers as we will need it to set up the bios. 

Hit Ok to save everything and this will build out a machine. 

![image](https://github.com/Krowemoh/R83/assets/8527895/bbc66d0f-d551-4c88-b41f-ba07423801b8)

### Installing R83

Now that the machine is set up, we can install R83. Start the machine we just built by selecting it and then pressing the play button.

If you are using wayland, then you will need to make sure pcem uses x11:
 
```
GDK_BACKEND=x11 pcem
```

This will put you at the AMI bios screen. 

1. Press F1 to enter the bios.
   
![image](https://github.com/Krowemoh/R83/assets/8527895/8e49a3eb-ec49-47a7-8f52-fce02f197069)

3. Enter Standard CMOS Setup by pressing Enter
    1. Hit enter to get past the warning page
       
![image](https://github.com/Krowemoh/R83/assets/8527895/4b837ebf-729d-4ef1-9eb7-217ffbd0b257)

![image](https://github.com/Krowemoh/R83/assets/8527895/9d12e1d1-4b36-402c-95df-e513c5b84606)

4. Use the arrow keys to navigate the Setup Program. Page Up and Page Down will cycle through options.
    1. Set Hard Disk C: Type to 47 = User Type
        i. This will let you set the Cylinders, Head, Sect and Size to the ones that you saved above.
    2. Set Floppy Drive A: to 720KB, 3 1/2"
    3. Press Escape to exit the Standard CMOS Setup
  
![image](https://github.com/Krowemoh/R83/assets/8527895/b6cd8f76-7535-4e4e-8c73-891f09412c36)

5. Use the arrow keys to go to Write to CMOS and Exit
    1. Enter Y to Write it out and Exit
       
![image](https://github.com/Krowemoh/R83/assets/8527895/7732e82d-3456-4eb5-8be4-ae91615646d2)

6. We should be returned to the bios, we need to press F1 to enter the bios again.
   
![image](https://github.com/Krowemoh/R83/assets/8527895/9e3c9ac4-af85-4fcc-b3f7-37a2b1bf4915)

8. Press Escape and then Y to exit without saving.
   
![image](https://github.com/Krowemoh/R83/assets/8527895/d9cf12d2-8b89-4c05-8356-0fed051daba3)

10. Now it will continue through and it will ask to insert a BOOT diskette.
    1. Right click on the PCem window
    2. Disc -> Change Drive A:
    3. Select the patched disk disk1.patched.img
    4. Once selected, press Enter
       
![image](https://github.com/Krowemoh/R83/assets/8527895/679acbad-71da-4b14-81d2-0fbb0ac9d454)

![image](https://github.com/Krowemoh/R83/assets/8527895/6c9eec4c-50d0-4a00-a63d-c601e8abbaf3)

![image](https://github.com/Krowemoh/R83/assets/8527895/1ac4269e-8a09-42b9-bbb1-f5a7e872ab2f)

9. We should see the Disk being read and Pick is ready to be installed.

![image](https://github.com/Krowemoh/R83/assets/8527895/defaf3ff-056a-4d48-b994-6a9c05a8f1e9)

11. We should hit the Monitor options now.
    1. Press T to disable the hard disk scan. This will speed things up. 
    2. Press Enter

![image](https://github.com/Krowemoh/R83/assets/8527895/7dbbdf36-806d-461b-b141-7da49ba39cda)

12. It will list out the installed serial cards.
    1. Press Y to continue
       
![image](https://github.com/Krowemoh/R83/assets/8527895/2f191751-ebd6-45b7-bc9b-dc0822b4996f)

13. Now it will say the ABS area is being initialized. Be patient.
    
![image](https://github.com/Krowemoh/R83/assets/8527895/cb4c7b18-153b-4e4d-95aa-53c7c398d4e5)

![image](https://github.com/Krowemoh/R83/assets/8527895/9aaa036d-bf15-4182-beaf-55466e3ce13b)


15. The next prompt is to put in the next disk. 
    1. Right click on the PCem window and change Drive A to disk2.img
    2. Press C to continue
       
![image](https://github.com/Krowemoh/R83/assets/8527895/d80522ea-d6ee-4450-a2fd-35bca41808df)

![image](https://github.com/Krowemoh/R83/assets/8527895/a2794411-7d46-424f-9ab6-05f0e1d04c0b)

16. This should take a second and then will display some information about the entire system. It will then put you at the Media Selection menu.
    1. Press S for the Standard density floppy
       
![image](https://github.com/Krowemoh/R83/assets/8527895/f126b6c0-a54e-40b8-b71b-dd5cce8eb271)

![image](https://github.com/Krowemoh/R83/assets/8527895/6c4fe191-8f46-44a0-a13e-ea2d6dd1eacc)

17. Now it will prompt you to enter the Pick Data Files disk.
    1. Right click on PCem window and Change Drive A to the data1.img
    2. Press C to continue
       c
![image](https://github.com/Krowemoh/R83/assets/8527895/8ee5f51a-0c65-44b7-bb02-9b5bd62a5d04)

18. You will see a list of files being setup and copied.

![image](https://github.com/Krowemoh/R83/assets/8527895/ea914929-5003-4958-85ab-0ca36da4e863)

19. Once the previous step finishes, you will be prompted for the next data disk.
    1. Right click on the PCem window and change Drive A to the data2.img 
    2. Press C to continue

![image](https://github.com/Krowemoh/R83/assets/8527895/7a10b342-001f-47b3-a9d7-7d45f6ac9dde)

20. Watch as some more files get set up.
    
![image](https://github.com/Krowemoh/R83/assets/8527895/296e5e43-46f4-4ea3-a1dc-d52f4f1c0765)

22. The next prompt is to Initialize the ABS frames.
    1. Press Y
       
![image](https://github.com/Krowemoh/R83/assets/8527895/f3af7804-f3f7-43d6-b000-638c42b75b4b)

![image](https://github.com/Krowemoh/R83/assets/8527895/fd7dadd0-9d29-4102-a269-f5b7007cf830)

23. Now you will be prompted to enter in a Country Code
    1. I use US, so press Enter without entering anything as it's the default

![image](https://github.com/Krowemoh/R83/assets/8527895/9cdb3cb5-1053-43aa-b9e6-c3472ffd7dd4)

24. The next prompt askes for your keyboard type.
    1. Press B for the 101 keys keyboard
       
![image](https://github.com/Krowemoh/R83/assets/8527895/05b7d15d-90c8-4ce9-867e-09be887cfeba)

25. The next prompt let's you set the shutdown delay, the default is 512.
    1. Press Enter for the default
       
![image](https://github.com/Krowemoh/R83/assets/8527895/605a2834-d8e4-4b73-a0ee-b245d0ae07c2)

26. The next prompt is to set the date.
    
![image](https://github.com/Krowemoh/R83/assets/8527895/656a19aa-76b5-49db-9665-24fda23a2ea1)

28. The next prompt is to set the time.

![image](https://github.com/Krowemoh/R83/assets/8527895/a3ba7acf-c117-43e5-8133-6d4bd2beed5c)

30. The next prompt is to restore an account from a backup.
    1. Press N as I don't have an account to restore.
       
![image](https://github.com/Krowemoh/R83/assets/8527895/5a5ee073-cb55-4215-88d8-7215a527b6aa)

31. The next prompt is to update the accounts.
    1. Press Y because why not.
       
![image](https://github.com/Krowemoh/R83/assets/8527895/7db1d21f-0751-44c9-83b6-28ba9c6130d9)

32. Watch in panic as illegals and protected fly by.

33. The next prompt will ask to create any new accounts
    1. Press N for not right now.
       
![image](https://github.com/Krowemoh/R83/assets/8527895/b0ad347f-c18b-464e-a333-4af0aab8923b)

34. The next prompt is to set up passwords.
    1. Press N because security is for wimps.
       
![image](https://github.com/Krowemoh/R83/assets/8527895/fe16cd99-eb8b-4d9a-906f-79b6b7fc96b3)

35. SYSTEM setup completed.
    
![image](https://github.com/Krowemoh/R83/assets/8527895/ab8d3d0a-3cc0-4306-a4c4-ad27379293c0)

37. Press T to Enter TCL
    
![image](https://github.com/Krowemoh/R83/assets/8527895/59011a6e-a8f0-41d1-bc6e-e637227bcdb3)

We should now be sitting at TCL in the PICK-SETUP account, we can LOGTO SYSPROG.

![image](https://github.com/Krowemoh/R83/assets/8527895/83515f7d-9cf4-46b4-b5ea-cf1ff0855fb4)

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
