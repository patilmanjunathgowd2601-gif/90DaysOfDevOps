## check running processes 
   1. ps aux
      Output :
      USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
      root           1  0.2  1.4  22628 13872 ?        Ss   06:56   0:01 /sbin/init
      root           2  0.0  0.0      0     0 ?        S    06:56   0:00 [kthreadd]
      root           3  0.0  0.0      0     0 ?        S    06:56   0:00 [pool_workqueue_release]
      root           4  0.0  0.0      0     0 ?        I<   06:56   0:00 [kworker/R-rcu_gp]
     
   
   2. top - display Linux processes
      Output :
      top - 07:10:26 up 14 min,  1 user,  load average: 0.00, 0.00, 0.00
        Tasks: 111 total,   1 running, 110 sleeping,   0 stopped,   0 zombie
        %Cpu(s):  0.2 us,  0.0 sy,  0.0 ni, 99.8 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
        MiB Mem :    914.2 total,    304.4 free,    363.4 used,    404.9 buff/cache
        MiB Swap:      0.0 total,      0.0 free,      0.0 used.    550.9 avail Mem

        PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
          1 root      20   0   22628  13872   9628 S   0.0   1.5   0:01.72 systemd
          2 root      20   0       0      0      0 S   0.0   0.0   0:00.00 kthreadd
          3 root      20   0       0      0      0 S   0.0   0.0   0:00.00 pool_workqueue_release
       
   3. pgrep ssh -  look up, signal, or wait for processes based on name and other attributes
      Output :1081
              1945
              2018

## Service Checks
  1.  systemctl status - Control the systemd system and service manager
     
      Output:
      ip-172-31-24-177
    State: running
    Units: 413 loaded (incl. loaded aliases)
     Jobs: 0 queued
   Failed: 0 units
    Since: Sat 2026-02-21 06:56:11 UTC; 24min ago
  systemd: 255.4-1ubuntu8.11
   CGroup: /
           ├─init.scope
           │ └─1 /sbin/init
           ├─system.slice
           │ ├─ModemManager.service
           │ │ └─823 /usr/sbin/ModemManager
      
  3. systemctl list-units

     Output:
      UNIT                                                                         LOAD   ACTIVE SUB       DESCRIPTION                                         >
  proc-sys-fs-binfmt_misc.automount                                            loaded active running   Arbitrary Executable File Formats File System Automo>
  sys-devices-pci0000:00-0000:00:04.0-nvme-nvme0-nvme0n1-nvme0n1p1.device      loaded active plugged   Amazon Elastic Block Store cloudimg-rootfs
  sys-devices-pci0000:00-0000:00:04.0-nvme-nvme0-nvme0n1-nvme0n1p14.device     loaded active plugged   Amazon Elastic Block Store 14
  sys-devices-pci0000:00-0000:00:04.0-nvme-nvme0-nvme0n1-nvme0n1p15.device     loaded active plugged   Amazon Elastic Block Store UEFI
  sys-devices-pci0000:00-0000:00:04.0-nvme-nvme0-nvme0n1-nvme0n1p16.device     loaded active plugged   Amazon Elastic Block Store BOOT
  sys-devices-pci0000:00-0000:00:04.0-nvme-nvme0-nvme0n1.device                loaded active plugged   Amazon Elastic Block Store
    
## Log Checks
   1. journalctl -u ssh
      Output:
      Feb 21 06:57:39 ip-172-31-24-177 systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
      Feb 21 06:57:40 ip-172-31-24-177 sshd[1081]: Server listening on 0.0.0.0 port 22.
      Feb 21 06:57:40 ip-172-31-24-177 sshd[1081]: Server listening on :: port 22.
      Feb 21 06:57:40 ip-172-31-24-177 systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
      
   
   2. journalctl -u ssh | tail -n 50
      Output:
      Feb 21 06:57:39 ip-172-31-24-177 systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
      Feb 21 06:57:40 ip-172-31-24-177 sshd[1081]: Server listening on 0.0.0.0 port 22.
      Feb 21 06:57:40 ip-172-31-24-177 sshd[1081]: Server listening on :: port 22.
      Feb 21 06:57:40 ip-172-31-24-177 systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
