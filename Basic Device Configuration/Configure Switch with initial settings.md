
### Switch Boot Sequence
Before you can configure a switch, you need to turn it on and allow it to go through the five-step boot sequence. This topic covers the basics of configuring a switch and includes a lab at the end.

After a Cisco switch is powered on, it goes through the following five-step boot sequence:

**Step 1:** First, ==the switch loads a power-on self-test (POST) program stored in ROM==. POST checks the CPU subsystem. It tests the CPU, DRAM, and the portion of the flash device that makes up the flash file system.  
  
**Step 2:** Next, ==the switch loads the boot loader software==. The boot loader is a small program stored in ROM that is run immediately after POST successfully completes.  
  
**Step 3:** ==The boot loader performs low-level CPU initialization==. It initializes the CPU registers, which control where physical memory is mapped, the quantity of memory, and its speed.  
  
**Step 4:** The boot loader initializes the flash file system on the system board.  
  
**Step 5:** Finally, the boot loader locates and loads a default IOS operating system software image into memory and gives control of the switch over to the IOS.

### Boot system command
The switch attempts to automatically boot by using information in the BOOT environment variable. If this variable is not set, the switch attempts to load and execute the first executable file it can find. On Catalyst 2960 Series switches, the image file is normally contained in a directory that has the same name as the image file (excluding the .bin file extension).

The IOS operating system then initializes the interfaces using the Cisco IOS commands found in the startup-config file. The startup-config file is called **config.text** and is located in flash.

In the example, the BOOT environment variable is set using the **boot system** global configuration mode command. Notice that the IOS is located in a distinct folder and the folder path is specified. Use the command **show boot** to see what the current IOS boot file is set to.

```cisco
boot system flash:/c2960-lanbasek9-mz.150-2.SE/c2960-lanbasek9-mz.150-2.SE.bin
```

