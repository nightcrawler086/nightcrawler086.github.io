## Linux Installation and Configuration

### Linux Distributions

**Linux is the kernel**

`uname -r`, short for unix name, the `-r` meaning **release**, will print the kernel version.

`lsb_release -a` will show the distribution name (Centos, Ubuntu, etc)

distrowatch.com is a good resource to discover/research/download linux distributions

### Installing Linux

All distributions (that I'm aware of) can be installed with a CD/DVD.  Nowadays this is done by using and ISO

#### Ubuntu

- Ubuntu is a debian-based system

- Ubuntu seems to use a preseed file to for network/pxe installs

- Ubuntu also has some kickstart compatibility

#### Centos

- Centos is based on Red Hat

- Uses the annoconda install

- Fully supports kickstart installations

#### SUSE Enterprise Linux

- SLES is based on Slackware Linux

- Uses AutoYAST files (similar to kickstart)

	* YAST in SLES is synonymous with the Control Panel in Windows

### Determine Hardware Settings

Physical consoles are named like `ttyX` where `X` is a number (typically 1-6)

The command `tty` can identify your connected terminal

Use the `who` or `w` command to identify all connected terminals

To switch consoles/terminals you can use `chvt` (change foreground virtual terminal)

#### Hardware Information

`lsscsi` will list scsi devices
`lsusb` will list usb devices
`lspci` will list pci devices
`hwinfo` 
`free` will show memory usage (`-m` for MB and `-h` for human readable)
`uptime`

#### Pseudo File Systems

Pseudo file systems are created and stored in RAM when the system boots.  These file systems are needed for the system to run, and are there for users to easily interact with (because, they look like files).  These file systems are like the HKLM:...CurrentControlSet in Windows.

**/proc**

A pseudo file system to store information about processes running on the system.

Contains `/proc/interrupts` which define the systems IRQ for different devices.

PID 1 is always `init`.  This process brings the system up.

each numbered directory in /proc represents resource usage of a running process on the system.

**/dev**

a pseudo file system about the devices in the system

### Managing Boot Loader and Understand Runlevels

### Software and Package Management

### Management of Shared Software Libraries

### Understand and Managing Linux File System

Most IDE/SATA devices appear as (emulated) SCSI devices.  

`lsblk` will list all block devices the OS can see.

`fidsk` can be used for MBR style partitions

`parted` can be used for GPT style partitions

`gdisk` can also be used to for GPT style partitions, but may need to be installed manually.


### Virtual Memory and File System Tools

### Controlling Access to File Systems

To be able to read/write to a file, you need permissions to the file.  To delete a file, you need permissions on the directory (b/c you are modifying the directory).

the /usr directory (usr for unix system resources)