
# Linux FOO

## Using TTY2 - access the command-line before login

I. LOAD Pre-login Terminal `alt + F2`

- Delivers a commandline: Enter username (return) password (return) to login.

Pop!_OS and Ubuntu use GNOME: Display Manager GDM

- Restarting gdm: `sudo systemctl restart gdm`

backup. `gnome-session`: Starts GNOME Desktop Session
backup. `startx`: Starts Xorg Desktop.

- Disabling Automatic Login: `sudo vi /etc/gdm3/custom.conf`
  - Comment out Automatic lines


## Running Scripts

Suppose we have a bash script with a cp command inside, copying a file, called "copy_file.sh"

0. ensure we have `#!/bin/bash` as the first line of the script, so ensure bash runs it for us.

i. to run the program, we "call" the script from the commandline by typing the name of the script and hitting enter.
`copy_file.sh` 

ii. to capture error and standard output:
`${i} &> specifiedLog`
append rather than overwrite: use `&>>` rather than `&>`



## Commands
`rsync` will transfer files easily across local and network domains.
try `rsync -av --progress --exclude="node_modules" /home/defithom/dev /media/defithom/2T TOSHI/backups/` to backup

`chmod` will modify permissions on a file or directory.
We use this to change read/write/execute betweeen owner/group.
-- seealso: [https://chmod-calculator.com/](CalculatePermissions)

i. Personal Scripts and Directories
  chmod 744

Begin Webserver permissions
ii. chmod 644
  6: the owner of the file/directory can read and write, but not execute. Since files are not executable, you don't need to have "x" rights here (6 means r+w. 7 means r+w+x).
  44: The group that the file/directory belongs to (see the group by using ls -l) and everyone else (the public) are able to read the file, but not execute or write to it (permission number 4).
iii. chmod 711
  7: the owner of the file/directory can read, write, and execute. This is needed for directories! Without "execute" when you try to list the directory you'll get permission denied.
  11: The group that the file/directory belongs to and the public have execute rights only. This is suitable for directories where you don't want other people browsing through the contents but do want to give them access to selected files further down the directory.
iv. chmod 755
    7: the owner of the file/directory can read, write, and execute.
    55: The group that the file/directory belongs to and the public have read and execute permissions but not write. This allows users to be able to view what files are in a directory, and be able to read those files, but not alter them.
I. `cp`

ls -a |more
-returns .files, especially from home directory.

.vimrc has some elflord stuff.

/usr1/tmp$ ls -ltr compile*
ls -ltr orderByTimeCreated search list


II. `ln`

- Understand logical links in Linux. They are quite powerful.

## Alias & Processes 

*ps with cgroups*

- ` $ alias al='echo "Story Trains are awesome"' `
- ` $ alias psc='ps xawf -eo pid,user,cgroup,args' `
  
### systemd 

I. <h4>systemd is a suite of basic building blocks for a Linux system</h4>
> It provides a `system and service manager` that runs as `PID 1` and starts the rest of the system. systemd provides aggressive parallelization capabilities, uses socket and D-Bus activation for starting services, offers on-demand starting of daemons, keeps track of processes using `Linux control groups`, maintains `mount` and `automount points`, and implements an elaborate `transactional dependency-based service control logic`.

`/etc/systemd/system/`

* List running services
`$ systemctl`

## SYSTEMD - SYSTEMCTL controls Units (services, which are programs packed with configuration for the environment)

I. Units can be, for example:
  1. **services (_.service_)**
  2. **mount points (_.mount_)**
  3. **devices (_.device_)**
  4. **sockets (_.socket_)**

II. Unit CMDS: let unit = 'cpsi-fhir-serverd.service'
  A. Status
     * **Manual Pages**: `systemctl help unit`
     * **Status**      : `systemctl status unit`
     * **Is-Enabled**  : `systemctl is-enabled unit`
  B. Spin | Restart | Reload 
     * **Start**       : `systemctl start unit`
     * **Stop**        : `systemctl stop unit`
     * **Restart**     : `systemctl restart unit`
     * **Reload**      : `systemctl reload unit`
       * Reload a unit and its configuration. 
     * **Reload**      : `systemctl daemon-reload`
       * Reload systemd manager configuration, scanning for new or changed units, update symlinks.
  C. Enabling | Masking
     * **Enable**       : `systemctl enable unit`
     * **Enable-Start** : `systemctl enable --now unit`
     * **Disable**      : `systemctl disable unit`
     * **Mask**         : `systemctl mask unit`
     * **Un-Mask**      : `systemctl unmask unit`

* All targets currently active
`$ systemctl list-units --type=target`

* Check the **Control Group Tree**
`$ systemd-cgls`

* If you want systemd to calculate the "initial" transaction it would execute on boot; something like:
`$ systemd --test --system --unit=multi-user.target`

* If you want to figure out which services a target like multi-user.target pulls in; something like:
`$ systemctl show -p "Wants" multi-user.target`

* daemon-reload --- Read and update configs (log files)
  * go read the service files and directories, and update all the symlinks.
  * Once the .wants directory 
  * `$ systemctl daemon-reload`

`/etc/systemd/system/multi-user.target.wants`

### Queries.get()
* For someone else: 
`ps -fU ccf3661`

* For current logged in user:
`ps -x` 

* For any and every:
`ps -eF | grep fhir`

### Process.destroy()
`kill -9 <process number>` process number <=5 digits. First column>


### Find
* Directory
    `find / -name "0.0.44"`
* File
    ` / -findname "*api-server-2.1.jar*"`
    `locate <.jar name>` to find locations for jars | files, efficiently and inconsistently.
* Strings inside files
    `grep -rnw '/path/to/somewhere/' -e 'pattern'`

    grep -rnw '/' -e 'userinfo?username=root'
    grep -rnw '/usr1/usr/java/cpsi-oauth-2.2.9/conf.d/' -e 'c2016_16'




       
