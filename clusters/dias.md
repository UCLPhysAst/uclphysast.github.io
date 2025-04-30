# DIAS

## Overview

The DIAS cluster offers access to a small number of powerful CPU and GPU systems. It is available to researchers in Physics and Astronomy who need more powerful resources than their own desktop or laptop computers, but don't need low-latency networking for multi-node parallel computation (for which the [Hypatia](hypatia.md) cluster may be more suitable) or the larger clusters provided by [ARC](https://www.rc.ucl.ac.uk/docs/) or national facilities. It is available to masters (MSc and MSci) students undertaking research projects, where requested by the student's supervisor.

## Account creation and support

To request an account on DIAS, please e-mail phy.dias.support@ucl.ac.uk with the following information:

- your name;
- your UCL computing ID (e.g. ucapxxx);
- your research group affiliation (Astro, AMOPP, BioP, CMMP, HEP).

UCL email addresses (i.e. of style <first_name>.<surname>.<year>@ucl.ac.uk) are mandatory, as no account information will be sent to non-UCL email addresses.

For masters students, the request must be made by the project supervisor or course leader, and should also include:

- supervisor's name;
- supervisor's UCL computing ID (e.g. ucapxxx);
- supervisor's UCL e-mail address.

Masters students should also contact their supervisor in the first instance with any queries or problems relating to the DIAS cluster. The supervisor can decide if a problem requires system administrator support.

## Access

Access to DIAS is by SSH to dias.hpc.phys.ucl.ac.uk, e.g. `ssh username@dias.hpc.phys.ucl.ac.uk`. DIAS access requires that you be within the UCL network. 

If you are not on site at UCL you can still access the cluster by using 

- [the UCL VPN](https://www.ucl.ac.uk/isd/services/get-connected/ucl-virtual-private-network-vpn));
- [Desktop@UCL Anywhere](https://www.ucl.ac.uk/isd/services/computers/remote-access/desktopucl-anywhere);
- [the SSH gateway](https://www.rc.ucl.ac.uk/docs/Remote_Access/).

If you encounter any issue or need assistance with these services you will need to contact the [ISD Service Desk](https://www.ucl.ac.uk/isd/help-support).

For running graphical applications remotely from a Windows machine you will need an X server application. We recommend you install OpenSSH on your Windows machine. This is the easiest solution to connecting to SSH via windows as it is also a native application on Unix systems.

Alternatively you can find programs such as Exceed, which can be downloaded from the UCL software database: http://swdb.ucl.ac.uk/package/view/id/150 and an SSH client that supports X11 forwarding (e.g. PuTTY: https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

This video tutorial may be useful for Desktop@UCL users: [Connecting to a Linux system from Desktop@UCL](https://www.youtube.com/watch?v=v_Gz8oZcsXQ).

## Using the cluster


The DIAS cluster runs a variant of the CentOS 7 Linux operating system. Using Linux remotely you will mainly use a terminal interface running ‘bash’.

If you are new to Linux or Research computing you can find some helpful online courses and resources provided by UCL ARC in the [ARC Course Catalogue](https://www.ucl.ac.uk/advanced-research-computing/training/course-catalogue).

If you are looking for a more casual approach to learning how to use a Linux system you can find many websites with useful commands, examples and tutorials.

Please note that data on DIAS is not backed up and you should keep code in external source control and otherwise keep copies of data elsewhere.
