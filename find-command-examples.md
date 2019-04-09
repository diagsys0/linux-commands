<p>Apart from the basic operation of looking for files under a directory structure, you can also perform several practical operations using find command that will make your command line journey easy.

In this article, let us review 15 practical examples of Linux find command that will be very useful to both newbies and experts.

<span id="more-412"></span>
First, create the following sample empty files under your home directory to try some of the find command examples mentioned below.</p>
<pre># vim create_sample_files.sh
touch MybashProgram.sh
touch mycprogram.c
touch MyCProgram.c
touch Program.c

mkdir backup
cd backup

touch MybashProgram.sh
touch mycprogram.c
touch MyCProgram.c
touch Program.c

<span># chmod +x create_sample_files.sh</span>
<span># ./create_sample_files.sh</span>

<span># ls -R</span>
.:
backup                  MybashProgram.sh  MyCProgram.c
create_sample_files.sh  mycprogram.c      Program.c

./backup:
MybashProgram.sh  mycprogram.c  MyCProgram.c  Program.c</pre>
<h3>1. Find Files Using Name</h3>
<p>This is a basic usage of the find command. This example finds all files with name — MyCProgram.c in the current directory and all its sub-directories.</p>
<pre># find -name "MyCProgram.c"
./backup/MyCProgram.c
./MyCProgram.c</pre>
<h3>2. Find Files Using Name and Ignoring Case</h3>
<p>This is a basic usage of the find command. This example finds all files with name — MyCProgram.c (ignoring the case) in the current directory and all its sub-directories.</p>
<pre># find -iname "MyCProgram.c"
./mycprogram.c
./backup/mycprogram.c
./backup/MyCProgram.c
./MyCProgram.c</pre>
<h3>3. Limit Search To Specific Directory Level Using mindepth and maxdepth</h3>
<p>Find the passwd file under all sub-directories starting from root directory.</p>
<pre># find / -name passwd
./usr/share/doc/nss_ldap-253/pam.d/passwd
./usr/bin/passwd
./etc/pam.d/passwd
./etc/passwd</pre>
<p>
Find the passwd file under root and one level down. (i.e root — level 1, and one sub-directory — level 2)</p>
<pre># find -maxdepth 2 -name passwd
./etc/passwd</pre>
<p>
Find the passwd file under root and two levels down. (i.e root — level 1, and two sub-directories — level 2 and 3 )</p>
<pre># find / -maxdepth 3 -name passwd
./usr/bin/passwd
./etc/pam.d/passwd
./etc/passwd</pre>
<p>
Find the password file between sub-directory level 2 and 4.</p>
<pre># find -mindepth 3 -maxdepth 5 -name passwd
./usr/bin/passwd
./etc/pam.d/passwd</pre>
<h3>4. Executing Commands on the Files Found by the Find Command.</h3>
<p>In the example below, the find command calculates the md5sum of all the files with the name MyCProgram.c (ignoring case). {} is replaced by the current file name.</p>
<pre># find -iname "MyCProgram.c" -exec md5sum {} \;
d41d8cd98f00b204e9800998ecf8427e  ./mycprogram.c
d41d8cd98f00b204e9800998ecf8427e  ./backup/mycprogram.c
d41d8cd98f00b204e9800998ecf8427e  ./backup/MyCProgram.c
d41d8cd98f00b204e9800998ecf8427e  ./MyCProgram.c</pre>
<h3>5. Inverting the match.</h3>
<p>Shows the files or directories whose name are not MyCProgram.c .Since the maxdepth is 1, this will look only under current directory.</p>
<pre># find -maxdepth 1 -not -iname "MyCProgram.c"
.
./MybashProgram.sh
./create_sample_files.sh
./backup
./Program.c</pre>
<h3>6. Finding Files by its inode Number.</h3>
<p>Every file has an unique inode number, using that we can identify that file. Create two files with similar name. i.e one file with a space at the end.</p>
<pre># touch "test-file-name"
<span># touch "test-file-name "</span>
[Note: There is a space at the end]

<span># ls -1 test*</span>
test-file-name
test-file-name</pre>
<p>
From the ls output, you cannot identify which file has the space at the end. Using option -i, you can view the inode number of the file, which will be different for these two files.</p>
<pre><span># ls -i1 test*</span>
16187429 test-file-name
16187430 test-file-name</pre>
<p>
You can specify inode number on a find command as shown below. In this example, find command renames a file using the inode number.</p>
<pre># find -inum 16187430 -exec mv {} new-test-file-name \;

<span># ls -i1 *test*</span>
16187430 new-test-file-name
16187429 test-file-name</pre>
<p>
You can use this technique when you want to do some operation with the files which are named poorly as shown in the example below. For example, the file with name — file?.txt has a special character in it. If you try to execute “rm file?.txt”, all the following three files will get removed. So, follow the steps below to delete only the “file?.txt” file.</p>
<pre># ls
file1.txt  file2.txt  file?.txt</pre>
<p>
Find the inode numbers of each file.</p>
<pre># ls -i1
804178 file1.txt
804179 file2.txt
804180 file?.txt</pre>
<p>
Use the inode number to remove the file that had special character in it as shown below.</p>
<pre># find -inum 804180 -exec rm {} \;
<span># ls</span>
file1.txt  file2.txt
[Note: The file with name "file?.txt" is now removed]</pre>
<h3>7. Find file based on the File-Permissions</h3>
<p>Following operations are possible.</p>
<ul>
<li>Find files that match exact permission</li>
<li>Check whether the given permission matches, irrespective of other permission bits</li>
<li>Search by giving octal / symbolic representation</li>
</ul>
<p>
For this example, let us assume that the directory contains the following files. Please note that the file-permissions on these files are different.</p>
<pre># ls -l
total 0
-rwxrwxrwx 1 root root 0 2009-02-19 20:31 all_for_all
-rw-r--r-- 1 root root 0 2009-02-19 20:30 everybody_read
---------- 1 root root 0 2009-02-19 20:31 no_for_all
-rw------- 1 root root 0 2009-02-19 20:29 ordinary_file
-rw-r----- 1 root root 0 2009-02-19 20:27 others_can_also_read
----r----- 1 root root 0 2009-02-19 20:27 others_can_only_read</pre>
<p>
Find files which has read permission to group. Use the following command to find all files that are readable by the world in your home directory, irrespective of other permissions for that file.</p>
<pre># find . -perm -g=r -type f -exec ls -l {} \;
-rw-r--r-- 1 root root 0 2009-02-19 20:30 ./everybody_read
-rwxrwxrwx 1 root root 0 2009-02-19 20:31 ./all_for_all
----r----- 1 root root 0 2009-02-19 20:27 ./others_can_only_read
-rw-r----- 1 root root 0 2009-02-19 20:27 ./others_can_also_read</pre>
<p>
Find files which has read permission only to group.</p>
<pre># find . -perm g=r -type f -exec ls -l {} \;
----r----- 1 root root 0 2009-02-19 20:27 ./others_can_only_read</pre>
<p>
Find files which has read permission only to group [ search by octal ]</p>
<pre># find . -perm 040 -type f -exec ls -l {} \;
----r----- 1 root root 0 2009-02-19 20:27 ./others_can_only_read</pre>
<h3>8. Find all empty files (zero byte file) in your home directory and its subdirectory</h3>
<p>Most files of the following command output will be lock-files and place holders created by other applications.</p>
<pre># find ~ -empty</pre>
<p>
List all the empty files only in your home directory.</p>
<pre># find . -maxdepth 1 -empty</pre>
<p>
List only the non-hidden empty files only in the current directory.</p>
<pre><span># find . -maxdepth 1 -empty -not -name ".*"</span></pre>
<h3>9. Finding the Top 5 Big Files</h3>
<p>The following command will display the top 5 largest file in the current directory and its subdirectory. This may take a while to execute depending on the total number of files the command has to process.</p>
<pre># find . -type f -exec ls -s {} \; | sort -n -r | head -5</pre>
<h3>10. Finding the Top 5 Small Files</h3>
<p>Technique is same as finding the bigger files, but the only difference the sort is ascending order.</p>
<pre># find . -type f -exec ls -s {} \; | sort -n  | head -5</pre>
<p>
In the above command, most probably you will get to see only the ZERO byte files ( empty files ). So, you can use the following command to list the smaller files other than the ZERO byte files.</p>
<pre># find . -not -empty -type f -exec ls -s {} \; | sort -n  | head -5</pre>
<h3>11. Find Files Based on file-type using option -type</h3>
<p>Find only the socket files.</p>
<pre># find . -type s</pre>
<p>
Find all directories</p>
<pre># find . -type d</pre>
<p>
Find only the normal files</p>
<pre># find . -type f</pre>
<p>
Find all the hidden files</p>
<pre><span># find . -type f -name ".*"</span></pre>
<p>
Find all the hidden directories</p>
<pre><span># find -type d -name ".*"</span></pre>
<h3>12. Find files by comparing with the modification time of other file.</h3>
<p>Show files which are modified after the specified file. The following find command displays all the files that are created/modified after ordinary_file.</p>
<pre># ls -lrt
total 0
-rw-r----- 1 root root 0 2009-02-19 20:27 others_can_also_read
----r----- 1 root root 0 2009-02-19 20:27 others_can_only_read
-rw------- 1 root root 0 2009-02-19 20:29 ordinary_file
-rw-r--r-- 1 root root 0 2009-02-19 20:30 everybody_read
-rwxrwxrwx 1 root root 0 2009-02-19 20:31 all_for_all
---------- 1 root root 0 2009-02-19 20:31 no_for_all

<span># find -newer ordinary_file</span>
.
./everybody_read
./all_for_all
./no_for_all</pre>
<h3>13. Find Files by Size</h3>
<p>Using the -size option you can find files by size.
Find files bigger than the given size</p>
<pre># find ~ -size +100M</pre>
<p>
Find files smaller than the given size</p>
<pre># find ~ -size -100M</pre>
<p>
Find files that matches the exact given size</p>
<pre># find ~ -size 100M</pre>
<p>
Note: – means less than the give size, + means more than the given size, and no symbol means exact given size.</p>
<h3>14. Create Alias for Frequent Find Operations</h3>
<p>If you find some thing as pretty useful, then you can make it as an alias. And execute it whenever you want.</p>
<p>
Remove the files named a.out frequently.</p>
<pre># alias rmao="find . -iname a.out -exec rm {} \;"
# rmao</pre>
<p>
Remove the core files generated by c program.</p>
<pre># alias rmc="find . -iname core -exec rm {} \;"
# rmc</pre>
<h3>15. Remove big archive files using find command</h3>
<p><span>The following command removes *.zip files that are over 100M.</span></p>
<pre><span># find / -type f -name *.zip -size +100M -exec rm -i {} \;"</span></pre>
<p><span>Remove all *.tar file that are over 100M using the alias rm100m (Remove 100M). Use the similar concepts and create alias like rm1g, rm2g, rm5g to remove file size greater than 1G, 2G and 5G respectively.</span></p>
<pre><span># alias rm100m="find / -type f -name *.tar -size +100M -exec rm -i {} \;"
# alias rm1g="find / -type f -name *.tar -size +1G -exec rm -i {} \;"
# alias rm2g="find / -type f -name *.tar -size +2G -exec rm -i {} \;"
# alias rm5g="find / -type f -name *.tar -size +5G -exec rm -i {} \;"
</span></pre>
