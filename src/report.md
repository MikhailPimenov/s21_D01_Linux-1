# Report


## Part 1. Installation of the OS

- Version of the OS installed: Ubuntu 20.04 Server LTS without GUI
![text](../screenshots/part1.png)


## Part 2. Creating a user

- Add user using sudo adduser command and gave the user admin rights using sudo
![text](../screenshots/part2-1.png)

- Result of cat /etc/passwd command output
![text](../screenshots/part2-2.png)


## Part 3. Setting up the OS network

1. Set the machine name as user-1: Look up the hostname with hostnamectl: $ hostnamectl And edit it using: $ hostnamectl set-hostname 'user-1'

- Result of the hostname look up and hostname change
![text](../screenshots/part3-1.png)


2. Set the time zone corresponding to your current location: View all available timezones using $ timedatectl list-timezones Set the timezone using $ sudo timedatectl set-timezone <Etc/GMT+3>

- Result of the timezone change
![text](../screenshots/part3-2.png)


3. Output the names of the network interfaces using a console command: To show all available interfaces I need to use $ ip link show command

- Show all network interfaces
![text](../screenshots/part3-3.png)
lo – Loopback interface. The loopback network interface is a virtual network device implemented entirely in software. All traffic sent to it "loops back" and just targets services on your local machine. It represents the Linux-host itself.

4. Use the console command to get the ip address of the device you are working on from the DHCP server: To get the IP-address call the command $ ip r or $ ip address (since I got the IP using DHCP either way)

- The IP is 10.0.2.15
![text](../screenshots/part3-4.png)
DHCP - Dynamic Host Configuration Protocol.


5. Define and display the external ip address of the gateway (ip) and the internal IP address of the gateway, aka default ip address (gw):
To find and display the internal IP of the gateway (default IP) use the following command: $ ip addr show

- Internal IP address of the gateway
![text](../screenshots/part3-5-1.png)
To find the external IP address I need to parse IP-address from a webpage. Wget command can be used for that with flags q and O: $ wget -qO- eth0.me

- External IP address of the gateway
![text](../screenshots/part3-5-2.png)


6. Set static (manually set, not received from DHCP server) ip, gw, dns settings (use public DNS servers, e.g. 1.1.1.1 or 8.8.8.8):
Open the interfaces file with a text editor and admin rights: $ sudo nano /etc/network/interfaces

- Open interfaces to edit
![text](../screenshots/part3-6-1.png)

- Enter new values: enter new IP, gateway, mask, dns
![text](../screenshots/part3-6-2.png)

- Entered the new dns servers
![text](../screenshots/part3-6-3.png)

- Restart the virtual machine using $ sudo reboot: restarted the network
Ping
![text](../screenshots/part3-6-4.png)


## Part 4. OS Update

- What to do to update the OS: $ apt-get update and $ sudo apt-get upgrade
OS update
![text](../screenshots/part4.png)


## Part 5. Using the sudo command

- Sudo command grants root power to administrators (members of group admin or sudo) based on the rules defined in /etc/sudoers.
 sudo usermod -aG sudo second_admin
- Switch to the second user and change the hostname
![text](../screenshots/part5.png)

Sudo stands for either "substitute user do" or "super user do" and it allows you to temporarily elevate your current user account to have root privileges. This allows you to do everything that user can do on linux, so no restrictions on your actions anymore.


## Part 6. Installing and configuring the time service


- Install and set up Chrony to synchronize time:
Synchronized using Chrony
![text](../screenshots/part6.png)


## Part 7. Installing and using text editors

- To exit with the changes saved: ESC, :wq, ENTER
![text](../screenshots/part7-vim1.png)

- To exit with the changes saved: control + x, y

![text](../screenshots/part7-nano1.png)

- To exit with the changes saved: control + k, q, y

![text](../screenshots/part7-joe1.png)


- To exit without saving changes: ESC, :q!, ENTER

![text](../screenshots/part7-vim2.png)

- To exit without saving changes: control + x, n

![text](../screenshots/part7-nano2.png)

- To exit without saving changes: control + k, q, n

![text](../screenshots/part7-joe2.png)




- Replacing using vim:
Command to find and substitute: :s/\<elviaatt\>/21 School 21/ and :q! to exit without saving the changes.


![text](../screenshots/part7-vim3-1.png)
![text](../screenshots/part7-vim3-2.png)
![text](../screenshots/part7-vim3-3.png)

- Replacing using nano:
Command to find and substitute: Alt (Optinon key on Mac) + Shift + 5 then enter the string to find, string to replace the found string with and enter y to confirm replacement. select which occurrences to change Ctrl + X + C to exit, enter q to not save the changes and enter yes to exit even though there's modified buffer.
![text](../screenshots/part7-nano3-1.png)
![text](../screenshots/part7-nano3-2.png)
![text](../screenshots/part7-nano3-3.png)

- Replacing using joe:
Command to find and substitute: Alt (Optinon key on Mac) + Shift + 5 then enter the string to find, string to replace the found string with and enter y to confirm replacement. select which occurrences to change Ctrl + X + C to exit, enter q to not save the changes and enter yes to exit even though there's modified buffer.
![text](../screenshots/part7-joe3-1.png)
![text](../screenshots/part7-joe3-2.png)
![text](../screenshots/part7-joe3-3.png)
![text](../screenshots/part7-joe3-4.png)


## Part 8. Installing and basic setup of the SSHD service

- Installed and enabled the SSHd service
![text](../screenshots/part8-1.png)

- Edit the file: $ sudo nano /etc/ssh/sshd_config
![text](../screenshots/part8-2.png)

- Show the presence of the sshd process using the ps command. To do this, you need to match the keys to the command.
![text](../screenshots/part8-3.png)

- Reboot the system: $ sudo reboot
![text](../screenshots/part8-4.png)


- Explain the meaning of the -tan keys, the value of each output column, the value 0.0.0.0. in the report:

-a - Displays all active connections and the TCP and UDP ports on which the computer is listening.

-n - Displays active TCP connections, however, addresses and port numbers are expressed numerically and no attempt is made to determine names.

-t - Displays only TCP connections.

Proto - The protocol of the connection.

Recv-Q - The data which has not yet been pulled from the socket buffer by the application. High Recv-Q means the data is put on TCP/IP receive buffer, but the application does not call recv() to copy it from TCP/IP buffer to the application buffer.

Send-Q - The data which the sending application has given to the transport, but has yet to be acknowledged by the receiving TCP. High Send-Q means the data is put on TCP/IP send buffer, but it is not sent or it is sent but not acknowledged. So, high value in Send-Q can be related to server network congest, server performance issue or data packet flow control.

Local Address – The IP address of the local computer and the port number being used.

Foreign Address – The IP address and port number of the remote computer to which the socket is connected.

State – Indicates the state of a TCP connection. The possible states are as follows: CLOSE_WAIT, CLOSED, ESTABLISHED, FIN_WAIT_1, FIN_WAIT_2, LAST_ACK, LISTEN, SYN_RECEIVED, SYN_SEND, and TIME_WAIT.

0.0.0.0 - The client devices like PCs show 0.0.0.0 address when they aren’t connected to any TCP/IP network. A device may get this address by default if it’s offline. In the case of address assignment failures, it may be automatically assigned by DHCP. Just in case your device is set to this address, it can’t talk to any other devices on the network over IP.


## Part 9. Installing and using the top, htop utilities:

- Install and run the top and htop utilities:
![text](../screenshots/part9-1.png)

- uptime
- number of authorised users
- total system load
- total number of processes
- cpu load
- memory load
![text](../screenshots/part9-2.png)

- pid of the process with the highest memory usage
![text](../screenshots/part9-3.png)

- pid of the process taking the most CPU time
![text](../screenshots/part9-4.png)


- sorted by PID
![text](../screenshots/part9-htop-1-pid.png)


- sorted by PERCENT_CPU
![text](../screenshots/part9-htop-2-cpu_percentage.png)


- sorted by PERCENT_MEM
![text](../screenshots/part9-htop-3-mem_percentage.png)


- sorted by TIME
![text](../screenshots/part9-htop-4-time.png)


- filtered for sshd process
![text](../screenshots/part9-htop-5-sshd.png)


- with the syslog process found by searching
![text](../screenshots/part9-htop-6-syslog.png)


- with hostname, clock and uptime output added
![text](../screenshots/part9-htop-7-hostname.png)


## Part 10. Using the fdisk utility

- List all devices: $ sudo fdisk -l /dev/sda
Go over each device to see extended info: $ sudo fdisk -l /dev/sda[number of the disk]

- Names of the disks, capacity and number of sectors:
![text](../screenshots/part10-1.png)

- Write the swap size: Check the swap size: $ free -h

![text](../screenshots/part10-2.png)


## Part 11. Using the df utility

- $ df /root Partition size, space used, space free, percentage used for the root partition:

![text](../screenshots/part11-1.png)

The measurement unit is 1k-blocks - 1024 bytes.


- $ df -Th Partition size, space used, space free, percentage used for the root partition:

![text](../screenshots/part11-2.png)


## Part 12. Using the du utility

- The size of the /home in bytes and human readable format:

![text](../screenshots/part12-1.png)


- The size of the /var in bytes and human readable format:

![text](../screenshots/part12-2.png)


- The size of the /var/log in bytes and human readable format:

![text](../screenshots/part12-3.png)


- The size of all contents in /var/log:

![text](../screenshots/part12-4.png)



- $ sudo du /var/log -a | less:
![text](../screenshots/part12-5.png)
![text](../screenshots/part12-6.png)

- $ sudo du /var/log -ah | less:
![text](../screenshots/part12-7.png)
![text](../screenshots/part12-8.png)



## Part 13. Installing and using the ncdu utility

- The size of the /home:
![text](../screenshots/part13-1.png)

- The size of the /var:
![text](../screenshots/part13-2.png)

- The size of the /var/log:
![text](../screenshots/part13-3.png)


## Part 14. Working with system logs

- /var/log/dmesg – Contains kernel ring buffer information. When the system boots up, it prints number of messages on the screen that displays information about the hardware devices that the kernel detects during boot process.

- var/log/syslog - Logs everything, except auth related messages.

- var/log/auth.log - Contains system authorization information, including user logins and authentication machinsm that were used.

- The last successful login time, user name and login method:

![text](../screenshots/part14-1.png)


- Stopped and restarted SSH:
![text](../screenshots/part14-2.png)



## Part 15. Using the CRON job scheduler

- Using the job scheduler, run the uptime command in every 2 minutes:

$ crontab -e and select the text editor - To edit the configuration file.
$ */2 * * * * uptime - New task added.
Lines in the system logs (at least two within a given time range) about the execution:

![text](../screenshots/part15-1.png)

- Display a list of current jobs for CRON $ crontab -l:
![text](../screenshots/part15-2.png)


- Remove all tasks from the job scheduler:

$ crontab -r - remove all tasks;
$ crontab -l - list all tasks;
The list of current tasks for CRON:

![text](../screenshots/part15-3.png)
