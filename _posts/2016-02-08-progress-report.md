---
layout: post
title: Progress Report - January 2016
date: 2016-02-08 16:00
---

So, I wanted to do a progress report of how my training has been going.  I'd like to do one of these each month if possible, but if not I will cover more than one month in a single post.

### Completed Items

Since most of my training currently are via online courses ([Pluralsight](pluralsight.com) and the like), this section will mostly contain the course I've completed.  If there are other items worth mentioning, I will add them here as well.

-  [Linux Installation and Initial Configuration](https://app.pluralsight.com/library/courses/linux-installation-configuration) by [Andrew Mallett](http://twitter.com/theurbanpenguin)

- [Linux Command Line Interface (CLI) Fundamentals](https://app.pluralsight.com/library/courses/linux-cli-fundamentals) by [Andrew Mallett](http://twitter.com/theurbanpenguin)

- [Docker and Containers:  The Big Picture](https://app.pluralsight.com/library/courses/docker-containers-big-picture) by [Nigel Poulton](http://twitter.com/nigelpoulton)

When I wrote my [training plan](http://blog.nightcrawler.me/2015/12/30/training-plan/) I intended to follow that list in order.  I was actually getting a little bored which was no fault of the authors.  I'm not a newbie when it comes to Linux, I just don't have a solid foundation.  So I decided to switch things up for a little bit and throw in something a little more exciting, like [Docker](https://www.docker.com).  I'll circle back to the general Linux courses after I finish the current Docker course I'm on.

### In-progress Items

-  [Docker Deep Dive](http://app.pluralsight.com/courses/docker-deep-dive) by [Nigel Poulton](http://twitter.com/nigelpoulton)

- [Linux System Administration Fundamentals](https://app.pluralsight.com/library/courses/linux-system-administration-fundamentals) by [Andrew Mallett](http://twitter.com/theurbanpenguin)

### Interesting Items

This section will be a list of interesting things I picked up from my training.

-  You can discover hardware on Linux by using the corresponding `ls` commands
	
	- `lspci` for list PCI devices
	
	- `lsblk` for listing block storage devices
	
	- `lsusb` for listing USB devices
	
	- `hwinfo` <- this is a more comprehensive command, but I had to install it on both CentOS and Ubuntu
	
	- `lsscsi` for listing SCSI devices
	
	- `free -h` for listing the amount of RAM.  The `-h` is for human-readable, aka not in bytes

- Pseudo File Systems

	- Parts of the Linux file system that are built at startup and stored in RAM

	- `/dev` is a pseudo file system to store information about devices

	- `/proc` is another pseudo file system to store information about processes running on the system

- Containers

	- Containers take virtualization to the next level.  Hypervisors today virtualize the hardware on which they run, and present virtual hardware to multiple virtual machines that run on top of them.

		-  This is super cool, but inefficient.  Each VM still needs an operating system.  Typically, on a single host there are several instances of the same operating system and that creates a lot of overhead.

		- Containers virtualize the operating system that's already running on the hardware.  Meaning there is a single OS on a pieces of hardware, and the containers only contain (<- ha) the services/processes/apps.  So, a container can just be an instance of apache without requiring an instance of an OS in the container.