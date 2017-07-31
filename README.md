# Mini-Firewall
A Linux kernel module that resides on a Linux box (firewall) and blocks incoming traffic according to some predefined rules in ECE573 Homework 5

# Description
main resides into kernel and hooks itself with the existing netfilter hooks specifically the PRE_ROUTING hook. In the topology that is created, we place the gateway at a position such that all the traffic to and from outside the LAN flows through this gateway.

The 'main’ module inspects every packet and based on the rules provided in the problem statement, makes the decision of whether to accept the packet or drop it.

The following are the rules this module implements:

1. Block all unsolicited ICMP packets coming in from outside except the ones going tothe web-server. However, the local hosts should be able to ping outside.2. Block all ssh attempts from outside.3. Block port 80 (http) access from outside except for the web-server and test that aninternal website on a local host is only accessible from inside. 

# How to use the module
Provided in the tar is a main.c file and a Makefile.

1. First run the make command inside the directory you have kept these files. Pre-requisites for successful build are GCC >= 4.8 and a Linux kernel >= 2.4
2. Successful build will generate a main.ko file which is our kernel module
3. Now we can load this module directly in the kernel using command <code>sudo insmod ./main.ko</code>
4. To see which packets pass the filter and which are dropped, we can use <code>sudo tail -f /var/log/kern.log</code>
5. To unload the kernel module, use the command <code>sudo rmmod main</code>

# Linux Distribution used for development and testing
Linux bn19-217.dcs.mcnc.org 3.13.0-86-generic #131-Ubuntu SMP Thu May 12 23:33:13 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux
