<h2>Find Files Based on Access / Modification / Change Time</h2>
<p>You can find files based on following three file time attribute.</p>
<ol>
<li><strong>Access time</strong> of the file. Access time gets updated when the <strong>file accessed</strong>.</li>
<li><strong>Modification time</strong> of the file. Modification time gets updated when the <strong>file content modified</strong>.</li>
<li><strong>Change time</strong> of the file. Change time gets updated when the <strong>inode data changes</strong>.</li>
</ol>
<p>
In the following examples, the difference between the <strong>min option</strong> and the <strong>time option</strong> is the argument.</p>
<ul>
<li><strong>min argument</strong> treats its argument as <strong>minutes</strong>. For example, min 60 = 60 minutes (1 hour).</li>
<li><strong>time argument</strong> treats its argument as <strong>24 hours</strong>. For example, time 2 = 2*24 hours (2 days).</li>
<li>While doing the 24 hours calculation, the fractional parts are ignored so 25 hours is taken as 24 hours, and 47 hours is also taken as 24 hours, only 48 hours is taken as 48 hours. To get more clarity refer the -atime section of the <strong>find command</strong> man page.</li>
</ul>
<h3>Example 1: Find files whose content got updated within last 1 hour</h3>
<p>To find the files based up on the content modification time, the option -mmin, and -mtime is used. Following is the definition of mmin and mtime from man page.</p>
<ul>
<li><strong>-mmin n</strong> File’s data was last modified <strong>n minutes</strong> ago.</li>
<li><strong>-mtime n</strong> File’s data was last modified <strong>n*24 hours</strong> ago.</li>
</ul>
<p>
Following example will find files in the current directory and sub-directories, whose content got updated within last 1 hour (60 minutes)</p>
<pre># find . -mmin -60</pre>
<p>
In the same way, following example finds all the files (under root file system /) that got updated within the last 24 hours (1 day).</p>
<pre># find / -mtime -1</pre>
<h3>Example 2: Find files which got accessed before 1 hour</h3>
<p>To find the files based up on the file access time, the option -amin, and -atime is used. Following is the definition of amin and atime from find man page.</p>

<ul>
<li><strong>-amin n</strong> File was last accessed <strong>n minutes</strong> ago</li>
<li><strong>-atime n</strong> File was last accessed <strong>n*24 hours</strong> ago</li>
</ul>
<p>
Following example will find files in the current directory and sub-directories, which got accessed within last 1 hour (60 minutes)</p>
<pre># find -amin -60</pre>
<p>
In the same way, following example finds all the files (under root file system /) that got accessed within the last 24 hours (1 day).</p>
<pre># find / -atime -1</pre>
<h3>Example 3: Find files which got changed exactly before 1 hour</h3>
<p>To find the files based up on the file inode change time, the option -cmin, and -ctime is used. Following is the definition of cmin and ctime from find man page.</p>
<ul>
<li><strong>-cmin n</strong> File’s status was last changed <strong>n minutes</strong> ago.</li>
<li><strong>-ctime n</strong> File’s status was last changed <strong>n*24 hours</strong> ago.</li>
</ul>
<p>
Following example will find files in the current directory and sub-directories, which changed within last 1 hour (60 minutes)</p>
<pre># find . -cmin -60</pre>
<p>
In the same way, following example finds all the files (under root file system /) that got changed within the last 24 hours (1 day).</p>
<pre># find / -ctime -1</pre>
<h3>Example 4: Restricting the find output only to files. (Display only files as find command results)</h3>
<p>The above find command’s will also show the directories because directories gets accessed when the file inside it gets accessed. But if you want only the files to be displayed then give -type f in the find command as<br>

The following <strong>find command</strong> displays files that are accessed in the last 30 minutes.</p>
<pre># find /etc/sysconfig -amin -30
.
./console
./network-scripts
./i18n
./rhn
./rhn/clientCaps.d
./networking
./networking/profiles
./networking/profiles/default
./networking/profiles/default/resolv.conf
./networking/profiles/default/hosts
./networking/devices
./apm-scripts
[Note: The above output contains both files and directories]

# find /etc/sysconfig -amin -30 -type f
./i18n
./networking/profiles/default/resolv.conf
./networking/profiles/default/hosts
[Note: The above output contains only files]</pre>
<h3>Example 5: Restricting the search only to unhidden files. (Do not display hidden files in find output)</h3>
<p>When we don’t want the hidden files to be listed in the find output, we can use the following regex.<br>
The below find displays the files which are modified in the last 15 minutes. And it lists only the unhidden files. i.e hidden files that starts with a . (period) are not displayed in the find output.</p>
<pre># find . -mmin -15 \( ! -regex ".*/\..*" \)</pre>
<h2>Finding Files Comparatively Using Find Command</h2>
<p>Human mind can remember things better by reference such as, i want to find files which i edited after editing the file “test”. You can find files by referring to the other files modification as like the following.</p>
<h3>Example 6: Find files which are modified after modification of a particular FILE</h3>
<pre>Syntax: find -newer FILE</pre>
<p>
Following example displays all the files which are modified after the /etc/passwd files was modified. This is helpful, if you want to track all the activities you’ve done after adding a new user.</p>
<pre># find -newer /etc/passwd</pre>
<h3>Example 7: Find files which are accessed after modification of a specific FILE</h3>
<pre>Syntax: find -anewer FILE</pre>
<p>
Following example displays all the files which are accessed after modifying /etc/hosts. If you remember adding an entry to the /etc/hosts and would like to see all the files that you’ve accessed since then, use the following command.</p>
<pre># find -anewer /etc/hosts</pre>
<h3>Example 8: Find files whose status got changed after the modification of a specific FILE.</h3>
<pre>Syntax: find -cnewer FILE</pre>
<p>
Following example displays all the files whose status got changed after modifying the /etc/fstab. If you remember adding a mount point in the /etc/fstab and would like to know all the files who status got changed since then, use the following command.</p>
<pre>find -cnewer /etc/fstab</pre>
<h2>Perform Any Operation on Files Found From Find Command</h2>
<p>We have looked at many different ways of finding files using <strong>find command</strong> in this article and also in our previous article. If you are not familiar in finding files in different ways, i strongly recommend you to read the part 1.<br>

This section explains about how to do different operation on the files from the find command. i.e how to manipulate the files returned by the find command output.<br>

We can specify any operation on the files found from find command.</p>
<pre>find &lt;CONDITION to Find files&gt; -exec &lt;OPERATION&gt; \;</pre>
<p>
The OPERATION can be anything such as:</p>
<ul>
<li><strong>rm command</strong> to remove the files found by find command.</li>
<li><strong>mv command</strong> to rename the files found.</li>
<li><strong>ls -l command</strong> to get details of the find command output files.</li>
<li><strong>md5sum</strong> on find command output files</li>
<li><strong>wc command</strong> to count the total number of words on find command output files.</li>
<li>Execute any <strong>Unix shell command</strong> on find command output files.</li>
<li>or Execute your own <strong>custom shell script</strong> / command on find command output files.</li>
</ul>
<h3>Example 9: ls -l in find command output. Long list the files which are edited within the last 1 hour.</h3>
<pre># find -mmin -60
./cron
./secure

<span># find -mmin -60 -exec ls -l {} \;</span>
-rw-------  1 root root 1028 Jun 21 15:01 ./cron
-rw-------  1 root root 831752 Jun 21 15:42 ./secure</pre>
<h3>Example 10: Searching Only in the Current Filesystem</h3>
<p>System administrators would want to search in the root file system, but not in the other mounted partitions. When you have multiple partitions mounted, and if you want to search in /. You can do the following.<br>

Following command will search for *.log files starting from /. i.e If you have multiple partitions mounted under / (root), the following command will search all those mounted partitions.</p>
<pre># find / -name "*.log"</pre>
<p>
This will search for the file only in the current file system. Following is the xdev definition from find man page:</p>
<ul>
<li><strong>-xdev</strong> Don’t descend directories on other filesystems.</li>
</ul>
<p>
Following command will search for *.log files starting from / (root) and only in the current file system. i.e If you have multiple partitions mounted under / (root), the following command will NOT search all those mounted partitions.</p>
<pre># find / -xdev -name "*.log"</pre>
<h3>Example 11: Using more than one { } in same command</h3>
<p>Manual says only one instance of the {} is possible. But you can use more than one {} in the same command as shown below.</p>
<pre># find -name "*.txt" cp {} {}.bkup \;</pre>
<p>
Using this {} in the same command is possible but using it in different command it is not possible, say you want to rename the files as following, which will not give the expected result.</p>
<pre>find -name "*.txt" -exec mv {} `basename {} .htm`.html \;</pre>
<h3>Example 12: Using { } in more than one instance.</h3>
<p>You can simulate it by writing a shell script as shown below.</p>
<pre># mv "$1" "`basename "$1" .htm`.html"</pre>
<p>
These double quotes are to handle spaces in file name. And then call that shell script from the <strong>find command</strong> as shown below.</p>
<pre>find -name "*.html" -exec ./mv.sh '{}' \;</pre>
<p>So for any reason if you want the same file name to be used more than once then writing the simple shell script and passing the file names as argument is the simplest way to do it.</p>
<h3>Example 13: Redirecting errors to /dev/null</h3>
<p>Redirecting the errors is not a good practice. An experienced user understands the importance of getting the error printed on terminal and fix it.<br>

Particularly in find command redirecting the errors is not a good practice. But if you don’t want to see the errors and would like to redirect it to null do it as shown below.</p>
<pre>find -name "*.txt" 2&gt;&gt;/dev/null</pre>
<p>
Sometimes this may be helpful. For example, if you are trying to find all the *.conf file under / (root) from your account, you may get lot of “Permission denied” error message as shown below.</p>
<pre>$ find / -name "*.conf"
/sbin/generate-modprobe.conf
find: /tmp/orbit-root: Permission denied
find: /tmp/ssh-gccBMp5019: Permission denied
find: /tmp/keyring-5iqiGo: Permission denied
find: /var/log/httpd: Permission denied
find: /var/log/ppp: Permission denied
/boot/grub/grub.conf
find: /var/log/audit: Permission denied
find: /var/log/squid: Permission denied
find: /var/log/samba: Permission denied
find: /var/cache/alchemist/printconf.rpm/wm: Permission denied
[Note: There are two valid *.conf files burned in the "Permission denied" messages]</pre>
<p>
So, if you want to just view the real output of the <strong>find command</strong> and not the “Permission denied” error message you can redirect the error message to /dev/null as shown below.</p>
<pre>$ find / -name "*.conf" 2&gt;&gt;/dev/null
/sbin/generate-modprobe.conf
/boot/grub/grub.conf
[Note: All the "Permission denied" messages are not displayed]</pre>
<h3>Example 14: Substitute space with underscore in the file name.</h3>
<p>Audio files you download from internet mostly come with the spaces in it. But having space in the file name is not so good for Linux kind of systems. You can use the find and rename command combination as shown below to rename the files, by substituting the space with underscore.<br>

The following replaces space in all the *.mp3 files with _</p>
<pre>$ find . -type f -iname “*.mp3″ -exec rename “s/ /_/g” {} \;</pre>
<h3>Example 15: Executing two find commands at the same time</h3>
<p>As shown in the examples of the find command in its manual page, the following is the syntax which can be used to execute two commands in single traversal.<br>

The following find command example, traverse the filesystem just once, listing setuid files and directories into /root/suid.txt and large files into /root/big.txt.</p>
<pre># find /    \( -perm -4000 -fprintf /root/suid.txt '%#m %u %p\n' \) , \
 \( -size +100M -fprintf /root/big.txt '%-10s %p\n' \)</pre>
