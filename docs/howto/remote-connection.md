# Connect remotely to UCL systems

## The VPN

Some UCL services, such as MyFinance and room bookings, can only be accessed from within the UCL network or [VPN (Virtual Private Network)](https://www.ucl.ac.uk/isd/services/get-connected/ucl-virtual-private-network-vpn). Departmental or research-group systems can generally be accessed using SSH (Secure Shell) but only via specific hosts, and in December 2025 even this access was blocked by ISD without advance notice for the duration of the Christmas closure period. So it is worthwhile to install VPN client software on your laptop or home computer even if you don't normally need to use it. Instructions are available from the [UCL VPN page](https://www.ucl.ac.uk/isd/services/get-connected/ucl-virtual-private-network-vpn) and even work on Linux (at least for Fedora 42 as of 5th January 2025).

## SSH

For security reasons [SSH](/training#ssh) access from outside the UCL network is only allowed to a limited number of specific servers, so to connect to a departmental or research group cluster you will normally have to first log in to a dedicated login node before continuing to other machines. There is also a central server, `ssh-gateway.ucl.ac.uk`, which you can connect to using your UCL credentials.
