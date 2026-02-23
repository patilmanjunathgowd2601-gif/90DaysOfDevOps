## Environment basics
  1. uname -a

     output : Linux ip-172-31-24-177 6.14.0-1018-aws #18~24.04.1-Ubuntu SMP Mon Nov 24 19:46:27 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux
     What I observed : Linux kernel version confirmed. System architecture x86_64.
  2. lsb_release -a

      output : No LSB modules are available.
                Distributor ID: Ubuntu
                Description:    Ubuntu 24.04.3 LTS
                Release:        24.04
                Codename:       noble
       What I Observed: Ubuntu 22.04 LTS confirmed
 ## Filesystem sanity

  1. mkdir /tmp/runbook-demo
     output : 
            runbook-demo
            snap-private-tmp
            systemd-private-6bb239ba74994af9a552e13872223d0c-ModemManager.service-YBvVWh
            systemd-private-6bb239ba74994af9a552e13872223d0c-chrony.service-DT5vJ9
            systemd-private-6bb239ba74994af9a552e13872223d0c-polkit.service-MBGCiS
            systemd-private-6bb239ba74994af9a552e13872223d0c-systemd-logind.service-ked5Cy
            systemd-private-6bb239ba74994af9a552e13872223d0c-systemd-resolved.service-q4lWqI

  2. cp /etc/hosts /tmp/runbook-demo/hosts-copy && ls -l /tmp/runbook-demo
      output :
            total 4
            -rw-r--r-- 1 ubuntu ubuntu 221 Feb 23 05:43 hosts-copy
     
      What I Observed: Folder and file created successfully. Permissions normal. Filesystem writable.
## CPU / Memory :
  1.   free -h
         output :
                               total        used        free      shared  buff/cache   available
                Mem:           914Mi       353Mi       435Mi       2.7Mi       282Mi       560Mi
                Swap:             0B          0B          0B
       
        What I Observed: How much i memory used, no swap pressure.
  3.  ps -o pcpu

      output : 
              %CPU
               0.0
               0.0

## Disk / IO
  1. df -h
     output :
                Filesystem       Size  Used Avail Use% Mounted on
                /dev/root         19G  2.0G   17G  11% /
                tmpfs            458M     0  458M   0% /dev/shm
                tmpfs            183M  872K  182M   1% /run
                tmpfs            5.0M     0  5.0M   0% /run/lock
                efivarfs         128K  3.8K  120K   4% /sys/firmware/efi/efivars
                /dev/nvme0n1p16  881M   89M  730M  11% /boot
                /dev/nvme0n1p15  105M  6.2M   99M   6% /boot/efi
                tmpfs             92M   12K   92M   1% /run/user/1000
  2. iostat :
      output :
       Linux 6.14.0-1018-aws (ip-172-31-24-177)        02/23/26        _x86_64_        (2 CPU)

        avg-cpu:  %user   %nice %system %iowait  %steal   %idle
                   0.20    0.00    0.14    0.05    0.02   99.59
        
        Device             tps    kB_read/s    kB_wrtn/s    kB_dscd/s    kB_read    kB_wrtn    kB_dscd
        loop0             0.02         0.16         0.00         0.00        345          0          0
        loop1             0.07         2.00         0.00         0.00       4271          0          0
        loop2             0.02         0.51         0.00         0.00       1082          0          0
        loop3             0.03         0.51         0.00         0.00       1097          0          0
        loop4             0.03         0.17         0.00         0.00        371          0          0
        loop5             0.01         0.01         0.00         0.00         14          0          0
        nvme0n1           3.73       112.81        11.00         0.00     240711      23482          0

 ## Network :

  1. ss -tulpn
     
     output :
              Netid          State           Recv-Q          Send-Q                        Local Address:Port                   Peer Address:Port         Process
              udp            UNCONN          0               0                                127.0.0.54:53                          0.0.0.0:*
              udp            UNCONN          0               0                             127.0.0.53%lo:53                          0.0.0.0:*
              udp            UNCONN          0               0                        172.31.24.177%ens5:68                          0.0.0.0:*
              udp            UNCONN          0               0                                 127.0.0.1:323                         0.0.0.0:*
              udp            UNCONN          0               0                                     [::1]:323                            [::]:*
              tcp            LISTEN          0               4096                             127.0.0.54:53                          0.0.0.0:*
              tcp            LISTEN          0               4096                                0.0.0.0:22                          0.0.0.0:*
              tcp            LISTEN          0               4096                          127.0.0.53%lo:53                          0.0.0.0:*
              tcp            LISTEN          0               4096                                   [::]:22                             [::]:*
 2. ping google.com
    output :
            PING google.com (172.217.20.174) 56(84) bytes of data.
            64 bytes from waw02s07-in-f14.1e100.net (172.217.20.174): icmp_seq=1 ttl=118 time=2.56 ms
            64 bytes from waw02s07-in-f14.1e100.net (172.217.20.174): icmp_seq=2 ttl=118 time=2.54 ms
            64 bytes from waw02s07-in-f14.1e100.net (172.217.20.174): icmp_seq=3 ttl=118 time=2.55 ms
            64 bytes from waw02s07-in-f14.1e100.net (172.217.20.174): icmp_seq=4 ttl=118 time=2.57 ms
            64 bytes from waw02s07-in-f14.1e100.net (172.217.20.174): icmp_seq=5 ttl=118 time=2.66 ms
            64 bytes from waw02s07-in-f14.1e100.net (172.217.20.174): icmp_seq=6 ttl=118 time=2.57 ms
            64 bytes from waw02s07-in-f14.1e100.net (172.217.20.174): icmp_seq=7 ttl=118 time=2.56 ms
  ## Logs :

  1. journalctl -u ssh -n 50
       output :
     
        Feb 21 07:29:21 ip-172-31-24-177 systemd[1]: Stopped ssh.service - OpenBSD Secure Shell server.
        Feb 21 07:29:21 ip-172-31-24-177 systemd[1]: ssh.service: Consumed 2.752s CPU time, 9.7M memory peak, 0B memory swap peak.
        -- Boot c765503682814dedbbdd0cf1210b8a1d --
        Feb 23 03:44:32 ip-172-31-24-177 systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
        Feb 23 03:44:32 ip-172-31-24-177 sshd[905]: Server listening on 0.0.0.0 por tail -n 50 /var/log/kern.log
        Feb 23 03:44:32 ip-172-31-24-177 sshd[905]: Server listening on :: port 22.

  2. tail -n 50 /var/log/kern.log
       output : 
              2026-02-23T05:21:24.556630+00:00 ip-172-31-24-177 kernel: Freeing unused decrypted memory: 2028K
              2026-02-23T05:21:24.556631+00:00 ip-172-31-24-177 kernel: Freeing unused kernel image (initmem) memory: 5252K
              2026-02-23T05:21:24.556631+00:00 ip-172-31-24-177 kernel: Write protecting the kernel read-only data: 38912k
              2026-02-23T05:21:24.556632+00:00 ip-172-31-24-177 kernel: Freeing unused kernel image (text/rodata gap) memory: 1072K
              2026-02-23T05:21:24.556633+00:00 ip-172-31-24-177 kernel: Freeing unused kernel image (rodata/data gap) memory: 1256K
     ## If this worsens (next steps)
      1. Restart strategy

          sudo systemctl restart nginx
          
          Monitor CPU and logs after restart.

      2. Increase log verbosity
         
          Modify nginx config → set error_log level to debug temporarily.

      3. Deep process tracing
      
          strace -p <nginx-pid>

      ## What if process is blocked on IO/syscalls.

      4. Check upstream (Node/PM2) if 502 errors appear.
