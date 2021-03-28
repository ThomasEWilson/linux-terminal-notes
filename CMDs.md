# Commands
I. `ln`
  * Understand logical links in Linux. They are quite powerful.
II. `cp`
 
ls -a |more
-returns .files, especially from home directory.

.vimrc has some elflord stuff.

/usr1/tmp$ ls -ltr compile*
ls -ltr orderByTimeCreated search list



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

#### Units
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
462
72978
## 
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




       