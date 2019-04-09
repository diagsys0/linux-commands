<div class="container" id="content-container">
										<div id="body">
<h1 id="title">Linux-Commands</h1>
<div id="mw-content-text" lang="en" dir="ltr" class="mw-content-ltr">
<table id="toc" class="toc"><tbody><tr><td><div id="toctitle"><h2>Contents</h2><span class="toctoggle">&nbsp;[<a href="#" class="internal" id="togglelink">hide</a>]&nbsp;</span></div>
<ul>
<li class="toclevel-1 tocsection-1"><a href="#System_Commands"><span class="tocnumber">1</span> <span class="toctext">System Commands</span></a></li>
<li class="toclevel-1 tocsection-2"><a href="#Hardware_related"><span class="tocnumber">2</span> <span class="toctext">Hardware related</span></a></li>
<li class="toclevel-1 tocsection-3"><a href="#Statistics_and_Analyze"><span class="tocnumber">3</span> <span class="toctext">Statistics and Analyze</span></a></li>
<li class="toclevel-1 tocsection-4"><a href="#Users"><span class="tocnumber">4</span> <span class="toctext">Users</span></a></li>
<li class="toclevel-1 tocsection-5"><a href="#File_Commands"><span class="tocnumber">5</span> <span class="toctext">File Commands</span></a></li>
<li class="toclevel-1 tocsection-6"><a href="#Process_Related"><span class="tocnumber">6</span> <span class="toctext">Process Related</span></a></li>
<li class="toclevel-1 tocsection-7"><a href="#File_Permission_Related"><span class="tocnumber">7</span> <span class="toctext">File Permission Related</span></a></li>
<li class="toclevel-1 tocsection-8"><a href="#Network"><span class="tocnumber">8</span> <span class="toctext">Network</span></a></li>
<li class="toclevel-1 tocsection-9"><a href="#Compression_.2F_Archives"><span class="tocnumber">9</span> <span class="toctext">Compression / Archives</span></a></li>
<li class="toclevel-1 tocsection-10"><a href="#Install_Package"><span class="tocnumber">10</span> <span class="toctext">Install Package</span></a></li>
<li class="toclevel-1 tocsection-11"><a href="#Search"><span class="tocnumber">11</span> <span class="toctext">Search</span></a></li>
<li class="toclevel-1 tocsection-12"><a href="#Login_.28ssh_and_telnet.29"><span class="tocnumber">12</span> <span class="toctext">Login (ssh and telnet)</span></a></li>
<li class="toclevel-1 tocsection-13"><a href="#File_transfer"><span class="tocnumber">13</span> <span class="toctext">File transfer</span></a></li>
<li class="toclevel-1 tocsection-14"><a href="#Disk_Usage"><span class="tocnumber">14</span> <span class="toctext">Disk Usage</span></a></li>
<li class="toclevel-1 tocsection-15"><a href="#Directory"><span class="tocnumber">15</span> <span class="toctext">Directory</span></a></li>
<li class="toclevel-1 tocsection-16"><a href="#Keyboard_shortcuts"><span class="tocnumber">16</span> <span class="toctext">Keyboard shortcuts</span></a></li>
</ul>
</td></tr></tbody></table>
<h3> <span class="mw-headline" id="System_Commands">System Commands </span></h3>
<pre>   <b>$ uname –a</b> - display linux system information 
   <b>$ uname –r</b> - display kernel release information 
   <b>$ uptime</b> - show how long system running + load 
   <b>$ hostname</b> - show system host name 
   <b>$ hostname -i</b> - display the IP address of the host 
   <b>$ last reboot</b> - show system reboot history 
   <b>$ date</b> - show the current date and time 
   <b>$ cal</b> - show this month calendar 
   <b>$ w</b> - display who is online
   <b>$ whoami</b> - who you are logged in as 
   <b>$ finger user</b> - display information about user
</pre>
<h3> <span class="mw-headline" id="Hardware_related">Hardware related</span></h3>
<pre>   <b>$ dmesg</b> - detected hardware and boot messages 
   <b>$ cat /proc/cpuinfo</b> - CPU model 
   <b>$ cat /proc/meminfo</b> - hardware memory 
   <b>$ cat /proc/interrupts</b> - lists the number of interrupts per CPU per I/O device 
   <b>$ lshw</b> - displays information on hardware configuration of the system 
   <b>$ lsblk</b> - displays block device related information in Linux 
   <b>$ free -m</b> - used and free memory (-m for MB)
   <b>$ lspci -tv</b> - show PCI devices 
   <b>$ lsusb -tv</b> - show USB devices 
   <b>$ lshal</b> - show a list of all devices with their properties 
   <b>$ dmidecode</b> - show hardware info from the BIOS
   <b>$ hdparm -i /dev/sda</b> -show info about disk sda 
   <b>$ hdparm -tT /dev/sda</b> - do a read speed test on disk sda 
   <b>$ badblocks -s /dev/sda</b> - test for unreadable blocks on disk sda
</pre>
<h3> <span class="mw-headline" id="Statistics_and_Analyze">Statistics and Analyze</span></h3>
<pre>   <b>$ top</b> - display and update the top cpu processes
   <b>$ mpstat 1</b> - display processors related statistics 
   <b>$ vmstat 2</b> - display virtual memory statistics 
   <b>$ iostat 2</b> - display I/O statistics (2sec Intervals)
   <b>$ tail -n 500 /var/log/syslog</b> - last 10 kernel/syslog messages
   <b>$ tcpdump -i eth1</b> - capture all packets flows on interface eth1 
   <b>$ tcpdump -i eth0 'port 80'</b> - monitor all traffic on port 80 ( HTTP ) 
   <b>$ lsof</b> - list all open files belonging to all active processes
   <b>$ lsof -u testuser</b> - list files opened by specific user 
   <b>$ free –m</b> - show amount of RAM 
   <b>$ watch df –h</b> - watch changeable data continuously
</pre>
<h3> <span class="mw-headline" id="Users">Users</span></h3>
<pre>   <b>$ id</b> - show the active user id with login and group
   <b>$ last</b> - show last logins on the system 
   <b>$ who</b> - show who is logged on the system
   <b>$ groupadd admin</b> - add group "admin" (force add existing group) 
   <b>$ useradd -c "Joe Smith" -g admin -m joe</b> - Create user "joe" and add to group "admin"
   <b>$ userdel joe</b> - delete user joe (force,file removal) 
   <b>$ adduser joe</b> - add user "joe" 
   <b>$ usermod</b> - modify user information
</pre>
<h3> <span class="mw-headline" id="File_Commands">File Commands</span></h3>
<pre>   <b>$ ls –al</b> - display all information about files / directories
   <b>$ ls -alR</b> - display all information about files / directories recursively
   <b>$ pwd</b> - show current directory path
   <b>$ mkdir directory-name</b> - create a directory
   <b>$ rm file-name</b> - delete file
   <b>$ rm -r directory-name</b> - delete directory recursively 
   <b>$ rm -f file-name</b> - forcefully remove file 
   <b>$ rm -rf directory-name</b> - forcefully remove directory recursively 
   <b>$ cp file1 file2</b> - copy file1 to file2 
   <b>$ cp -r dir1 dir2</b> - copy dir1 to dir2, create dir2 if it doesn’t exist 
   <b>$ mv file1 file2</b> - move files from one place to another
   <b>$ ln –s /path/to/file-name link-name</b> - create symbolic link to file-name
   <b>$ touch file</b> - create or update file 
   <b>$ cat &gt; file</b> - place standard input into file
   <b>$ more file</b> - output the contents of file 
   <b>$ head file</b> - output the first 10 lines of file
   <b>$ tail file</b> - output the last 10 lines of file
   <b>$ tail -f file</b> - output the contents of file as it grows starting with the last 10 lines 
   <b>$ gpg -c file</b> - encrypt file
   <b>$ gpg file.gpg</b> - decrypt file
</pre>
<h3> <span class="mw-headline" id="Process_Related">Process Related</span></h3>
<pre>   <b>$ ps</b> - display your currently active processes
   <b>$ ps aux | grep 'telnet'</b> - find all process id related to telnet process 
   <b>$ pmap</b> - memory map of process 
   <b>$ top</b> - display all running processes 
   <b>$ kill pid</b> - kill process with mentioned pid id
   <b>$ killall proc</b> - kill all processes named proc 
   <b>$ pkill processname</b> - send signal to a process with its name 
   <b>$ bg</b> - resumes suspended jobs without bringing them to foreground 
   <b>$ fg</b> - brings the most recent job to foreground 
   <b>$ fg n</b> - brings job n to the foreground
</pre>
<h3> <span class="mw-headline" id="File_Permission_Related">File Permission Related</span></h3>
<pre>   <b>$ chmod octal file-name</b> - change the permissions of file to octal , which can be found separately for user, group and world; octal value 4 -read 2 –write 1 –execute
   <b>$ chown owner-user file</b> - change owner of the file 
   <b>$ chown owner-user:owner-group file-name</b> - change owner and group owner of the file 
   <b>$ chown owner-user:owner-group directory</b> - change owner and group owner of the directory
</pre>
<h3> <span class="mw-headline" id="Network">Network</span></h3>
<pre>   <b>$ ifconfig –a</b> - display all network ports and ip address
   <b>$ ifconfig eth1 mtu 9000 up</b> - set mtu to 9000
   <b>$ ifconfig eth0</b> - display specific ethernet port ip address and details 
   <b>$ ifconfig -a | grep HWaddr</b> - display MAC address
</pre>
<pre>   change MAC address:
   # ifconfig eth0 down
   # ifconfig eth0 hw ether 00:80:48:BA:d1:30
   # ifconfig eth0 up
</pre>
<pre>   <b>$ ip addr show</b> - display all network interfaces and ip address (available in iproute2 package,powerful than ifconfig) 
   <b>$ ip address add 192.168.0.1 dev eth0</b> - set ip address 
   <b>$ ethtool eth0</b> - linux tool to show ethernet status (set full duplex , pause parameter) 
   <b>$ mii-tool eth0</b> - linux tool to show ethernet status (more or like ethtool) 
   <b>$ ping host</b> - send echo request to test connection (learn sing enhanced ping tool)
   <b>$ whois domain</b> - get who is information for domain 
   <b>$ dig domain</b> - get DNS information for domain (screenshots with other available parameters) 
   <b>$ dig -x host</b> - reverse lookup host 
   <b>$ host google.com</b> - lookup DNS ip address for the name
   <b>$ hostname –i</b> - lookup local ip address (set hostname too) 
   <b>$ wget file</b> - download file (very useful other option) 
   <b>$ netstat -tupl</b> - listing all active listening ports(tcp,udp,pid) 
</pre>
<pre>   WiFi related:
   <b>$ iwconfig wlan0 essid "mynetworkESSID"</b> - specify ESSID for the WLAN
   <b>$ dhclient wlan0</b> - to receive an IP address, netmask, DNS server and default gateway from the Access Point
   <b>$ iwconfig wlan0 mode managed key [WEP key]</b> - 128 bit WEP use 26 hex characters, 64 bit WEP uses 10
   <b>$ iwconfig wlan0 mode master</b> - set the card to act as an access point mode
   <b>$ iwconfig wlan0 mode managed</b> - set card to client mode on a network with an access point
   <b>$ iwconfig wlan0 mode ad-hoc</b> - set card to peer to peer networking or no access point mode
   <b>$ iwconfig wlan0 mode monitor</b> - set card to RFMON mode
   <b>$ iwconfig wlan0 essid any</b> - with some cards you may  disable the ESSID checking
   <b>$ iwconfig wlan0 key 1111-1111-1111-1111</b> - set 128 bit WEP key
   <b>$ iwconfig wlan0 key off</b> - disable WEP key
   <b>$ iwconfig wlan0 key open</b> - sets open mode, no authentication is used and card may accept non-encrypted sessions
   <b>$ iwlist wlan0 scan</b> - give the list of Access Points and Ad-Hoc cells in range (ESSID, Quality, Frequency, Mode etc.)
   <b>$ iwlist wlan0 power</b> - list the various Power Management attributes and modes of the device
   <b>$ iwlist wlan0 txpower</b> - list the various Transmit Power available on the device
   <b>$ iwlist wlan0 retry</b> - list the transmit retry limits and retry lifetime on the device
</pre>
<h3> <span class="mw-headline" id="Compression_.2F_Archives">Compression / Archives</span></h3>
<pre>   <b>$ tar cf test.tar test</b> - create tar named test.tar containing test/ 
   <b>$ tar xf test.tar</b> - extract the files from test.tar 
   <b>$ tar czf test.tar.gz test</b> - create a tar with gzip compression 
   <b>$ gzip test</b> - compress file and renames it to test.gz
</pre>
<h3> <span class="mw-headline" id="Install_Package">Install Package</span></h3>
<pre>   <b>$ rpm -i pkgname.rpm</b> - install rpm based package
   <b>$ rpm -e pkgname</b> - remove package 
</pre>
<pre>   Install from source 
   $ ./configure 
   $ make 
   $ make install
</pre>
<pre>   <b>$ apt-get update</b> - re-synchronize the package index files from their sources
   <b>$ apt-get upgrade</b> - install the newest versions of all packages currently installed on the system from the sources
   <b>$ apt-get install package</b> - install package
   <b>$ apt-get remove package</b> - remove package
   <b>$ apt-cache search package</b> - search for package
</pre>
<h3> <span class="mw-headline" id="Search">Search</span></h3>
<pre>   <b>$ grep pattern files</b> - search for pattern in files 
   <b>$ grep -r pattern dir</b> - search recursively for pattern in dir 
   <b>$ locate file</b> - find all instances of file 
   <b>$ find /home/tom -name 'index*'</b> - find files names that start with "index"
   <b>$ find /home -size +10000k</b> - find files larger than 10000k in /home
</pre>
<h3> <span class="mw-headline" id="Login_.28ssh_and_telnet.29">Login (ssh and telnet)</span></h3>
<pre>   <b>$ ssh user@host</b> - connect to host as user 
   <b>$ ssh -p port user@host</b> - connect to host using specific port 
   <b>$ telnet host</b> - connect to the system using telnet port
</pre>
<h3> <span class="mw-headline" id="File_transfer">File transfer</span></h3>
<pre>   scp
   <b>$ scp file.txt server2:/tmp</b>  - secure copy file.txt to remote host /tmp folder
   <b>$ scp gordon@server2:/www/*.html /www/tmp</b> - copy *.html files from remote host to current system /www/tmp folder 
   $ <b>scp -r gordon@server2:/www /www/tmp</b> - copy all files and folders recursively from remote server to the current system /www/tmp folder 
</pre>
<pre>   rsync 
   <b>$ rsync -a /home/apps /backup/</b> - synchronize source to destination 
   <b>$ rsync -avz /home/apps gordon@192.168.10.1:/backup</b> - synchronize files/directories between the local and remote system with compression enabled
</pre>
<h3> <span class="mw-headline" id="Disk_Usage">Disk Usage</span></h3>
<pre>   <b>$ df –h</b> - show free space on mounted filesystems
   <b>$ df -i</b> - show free inodes on mounted filesystems 
   <b>$ fdisk -l</b> - show disks partitions sizes and types 
   <b>$ du -ah</b> - display disk usage in human readable form
   <b>$ findmnt</b> - displays target mount point for all filesystem
   <b>$ mount device-path mount-point</b> - mount a device
</pre>
<h3> <span class="mw-headline" id="Directory">Directory</span></h3>
<pre>   <b>$ cd .</b>. - go up one level of the directory tree
   <b>$ cd</b> - go to $HOME directory 
   <b>$ cd /test</b> - change to /test directory
</pre>
<h3> <span class="mw-headline" id="Keyboard_shortcuts">Keyboard shortcuts</span></h3>
<pre>   <b>Alt+Ctrl+T</b> - open Terminal Window
</pre>
<pre>   <b>Alt+Ctrl+L</b> - lock the screen
   <b>Alt+Ctrl+Del</b> - logoff
</pre>
<pre>   <b>Alt+F4</b> - close current window
   <b>Alt+F2</b> - pop up command window (for quickly running commands)
</pre>
<pre>   <b>Super-W</b>  - show all windows in the current workspace
   <b>Ctrl+Super+D</b> - show desktop
</pre>
<pre>   <b>Ctrl+A</b> - select all items on list or text
   <b>Ctrl+C</b> - copy all selected items to clipboard
   <b>Ctrl+X</b> - cut all selected items to clipboard
   <b>Ctrl+V</b> or <b>Mouse middle button click</b> - paste all selected items to clipboard
</pre>
<pre>   <b>PrintScr</b> - takes screenshot
   <b>Alt+PrintScr</b> - takes screenshot of windows
   <b>Shift+PrintScr</b> - takes screenshot of selected window area
</pre>

</div>
</div>
</div>
