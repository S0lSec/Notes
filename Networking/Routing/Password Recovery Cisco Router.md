## How to perform a Cisco router password recovery without losing your configuration.

Submitted by admin on Wed, 02/24/2010 - 11:06pm

- [cisco](http://www.pateconsulting.com/tags/cisco)
- [console](http://www.pateconsulting.com/tags/console)
- [password recovery](http://www.pateconsulting.com/tags/password-recovery)

Forgot your Cisco router password?  Did you know you can change them without losing your configuration?  In this brief how-to, I will walk you through it. In order to perform a password recovery, you will need to reboot the router a couple of times.  This means downtime, but it is a good sacrifice to make in order to get your passwords reset.  
   
First, hook up the DB9 end of the standard light blue serial cable to your serial port.  The other end of the cable should plug into the port labeled “**Console**” on the back of the Cisco router.  If you do  not have a serial port, then you'll need to go purchase a USB-to-serial adapter cable and install it on your computer.  
 

Now that your hardware is connected, establish a serial connection with the router. 

The settings you need are:

Baud: 9600  
Data bits: 8  
Parity: No  
Stop bits: 1  
Flow Control: None  
   
On Windows, I use putty for this connection.  Yes, putty can be used to make serial connections as well as telnet/ssh.  Hyperterminal works great as well.  On Linux, I use minicom and on FreeBSD/OpenBSD, I use cu (cu -s 9600 -l /dev/cuad0).  
   
Reboot the router and **press the Break key** to interrupt the boot sequence. 

For break key sequences, refer to this Cisco link: [http://www.cisco.com/en/US/products/hw/routers/ps133/products_tech_note0...](http://www.cisco.com/en/US/products/hw/routers/ps133/products_tech_note09186a0080174a34.shtml "http://www.cisco.com/en/US/products/hw/routers/ps133/products_tech_note09186a0080174a34.shtml")  
   
Type **confreg 0x2142**.  This tells the router to bypass NVRAM during bootup.  In other words, your existing configuration won't be loaded.  The good news is that it won't be deleted either.  
   
Type **reset** to reboot the router.  Answer No when prompted to run setup.  
   
Type **copy start run**.  This loads your startup configuration into memory.  Now, if you type a **show run config**, you'll see the router configuration.  Also, you should notice that your router name is now in the prompt instead of the default “Router”.  
   
Change the enable secret - “**enable secret new_password**”  
   
Change the register back to 0x2102:  
**config-register 0x2102**  
   
When the router reboots it will load the old configuration with the new password.  
   
Save the password so that it will be persistent during reboots, type **copy run start**  
   
Reboot the router by typing **reload** at the enable prompt.  
   
Now, keep that password in a nice safe place – in your head does not count.  I keep mine saved in a safe place for future retrieval and I make sure my customers have a copy as well.  Remember, passwords are nice until you forget them.