rsync -av --exclude "node_modules" personal/ "/media/defithom/2T TOSHI/backups/Backup-popos-22-4-4/personal"



cp command in Linux with examples
cp stands for copy. This command is used to copy files or group of files or directory. It creates an exact image of a file on a disk with different file name. cp command require at least two filenames in its arguments.

Syntax:

`cp [OPTION] Source Destination`
`cp [OPTION] Source Directory`
`cp [OPTION] Source-1 Source-2 Source-3 Source-n Directory`

`cp -f cpsi-fhir-core.jar cpsi-fhir-server.jar cpsi-fhir-thrive.jar /usr1/usr/java/standalone/cpsi-fhir/dist/`

First and second syntax is used to copy Source file to Destination file or Directory.
Third syntax is used to copy multiple Sources(files) to Directory.
cp command works on three principal modes of operation and these operations depend upon number and type of arguments passed in cp command :

Two file names : If the command contains two file names, then it copy the contents of 1st file to the 2nd file. If the 2nd file doesn’t exist, then first it creates one and content is copied to it. But if it existed then it is simply overwritten without any warning. So be careful when you choose destination file name.
`cp Src_file Dest_file`
Suppose there is a directory named geeksforgeeks having a text file a.txt.
Example:

`$ ls`
a.txt

`$ cp a.txt b.txt`

`$ ls`
a.txt  b.txt
One or more arguments : If the command has one or more arguments, specifying file names and following those arguments, an argument specifying directory name then this command copies each source file to the destination directory with the same name, created if not existed but if already existed then it will be overwritten, so be careful !!.
`cp Src_file1 Src_file2 Src_file3 Dest_directory`
Suppose there is a directory named geeksforgeeks having a text file a.txt, b.txt and a directory name new in which we are going to copy all files.
Example:



`$ ls`
a.txt  b.txt  new

Initially new is empty
`$ ls new`

`$ cp a.txt b.txt new`

`$ ls new`
a.txt  b.txt
Note: For this case last argument must be a directory name. For the above command to work, Dest_directory must exist because cp command won’t create it.

Two directory names : If the command contains two directory names, cp copies all files of the source directory to the destination directory, creating any files or directories needed. This mode of operation requires an additional option, typically R, to indicate the recursive copying of directories.
`cp -R Src_directory Dest_directory`
In the above command, cp behavior depend upon whether Dest_directory is exist or not. If the Dest_directory doesn’t exist, cp creates it and copies content of Src_directory recursively as it is. But if Dest_directory exists then copy of Src_directory becomes sub-directory under Dest_directory.

Options:

There are many options of cp command, here we will discuss some of the useful options:
Suppose a directory named geeksforgeeks contains two files having some content named as a.txt and b.txt. This scenario is useful in understanding the following options.

`$ ls geeksforgeeks`
a.txt  b.txt

`$ cat a.txt`
GFG

`$ cat b.txt`
GeeksforGeeks
1. -i(interactive): i stands for Interactive copying. With this option system first warns the user before overwriting the destination file. cp prompts for a response, if you press y then it overwrites the file and with any other option leave it uncopied.

`$ cp -i a.txt b.txt`
cp: overwrite 'b.txt'? y

`$ cat b.txt`
GFG
2. -b(backup): With this option cp command creates the backup of the destination file in the same folder with the different name and in different format.

`$ ls`
a.txt  b.txt

`$ cp -b a.txt b.txt`

`$ ls`
a.txt  b.txt  b.txt~
`3. -f(force): If the system is unable to open destination file `for writing operation because the user doesn’t have writing permission for this file then by using -f option with cp command, destination file is deleted first and then copying of content is done from source to destination file.

`$ ls -l b.txt`
-r-xr-xr-x+ 1 User User 3 Nov 24 08:45 b.txt

User, group and others doesn't have writing permission.

Without -f option, command not executed
`$ cp a.txt b.txt`
cp: cannot create regular file 'b.txt': Permission denied

With -f option, command executed successfully
`$ cp -f a.txt b.txt`
4. -r or -R: Copying directory structure. With this option cp command shows its recursive behavior by copying the entire directory structure recursively.
Suppose we want to copy geeksforgeeks directory containing many files, directories into gfg directory(not exist).

`$ ls geeksforgeeks/`
a.txt  b.txt  b.txt~  Folder1  Folder2

Without -r option, error
`$ cp geeksforgeeks gfg`
cp: -r not specified; omitting directory 'geeksforgeeks'

With -r, execute successfully
`$ cp -r geeksforgeeks gfg`

`$ ls gfg/`
a.txt  b.txt  b.txt~  Folder1  Folder2

5. -p(preserve): With -p option cp preserves the following characteristics of each source file in the corresponding destination file: the time of the last data modification and the time of the last access, the ownership (only if it has permissions to do this), and the file permission-bits.
Note: For the preservation of characteristics you must be the root user of the system, otherwise characteristics changes.

`$ ls -l a.txt`
-rwxr-xr-x+ 1 User User 3 Nov 24 08:13 a.txt

`$ cp -p a.txt c.txt`

`$ ls -l c.txt`
-rwxr-xr-x+ 1 User User 3 Nov 24 08:13 c.txt
As we can see above both a.txt and c.txt(created by copying) have same characteristics.

Examples:

Copying using * wildcard: The star wildcard represents anything i.e. all files and directories. Suppose we have many text document in a directory and wants to copy it another directory, it takes lots of time if we copy files 1 by 1 or command becomes too long if specify all these file names as the argument, but by using * wildcard it becomes simple.

Initially Folder1 is empty
`$ ls`
a.txt  b.txt  c.txt  d.txt  e.txt  Folder1

`$ cp *.txt Folder1`

`$ ls Folder1`
a.txt  b.txt  c.txt  d.txt  e.txt
