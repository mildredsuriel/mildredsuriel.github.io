# SECURITY HARDENING

```bash
msuriel@ubuntu:~/security$ git clone https://github.com/CISOfy/lynis
Cloning into 'lynis'...
remote: Enumerating objects: 25, done.
remote: Counting objects: 100% (25/25), done.
remote: Compressing objects: 100% (24/24), done.
remote: Total 13500 (delta 13), reused 5 (delta 1), pack-reused 13475
Receiving objects: 100% (13500/13500), 7.03 MiB | 6.94 MiB/s, done.
Resolving deltas: 100% (9955/9955), done.
msuriel@ubuntu:~/security$ ls
lynis
msuriel@ubuntu:~/security$ cd lynis/
msuriel@ubuntu:~/security/lynis$ chmod 640 include/*
msuriel@ubuntu:~/security/lynis$ ./lynis audit system

[ Lynis 3.0.2 ]

################################################################################
  Lynis comes with ABSOLUTELY NO WARRANTY. This is free software, and you are
  welcome to redistribute it under the terms of the GNU General Public License.
  See the LICENSE file for details about using this software.

  2007-2020, CISOfy - https://cisofy.com/lynis/
  Enterprise support available (compliance, plugins, interface and tools)
################################################################################


[+] Initializing program
------------------------------------

  ###################################################################
  #                                                                 #
  #   NON-PRIVILEGED SCAN MODE                                      #
  #                                                                 #
  ###################################################################

  NOTES:
  --------------
  * Some tests will be skipped (as they require root permissions)
  * Some tests might fail silently or give different results

  - Detecting OS...                                           [ DONE ]
  - Checking profiles...                                      [ DONE ]

  ---------------------------------------------------
  Program version:           3.0.2
  Operating system:          Linux
  Operating system name:     Ubuntu
  Operating system version:  20.04
  Kernel version:            5.4.0
  Hardware platform:         aarch64
  Hostname:                  ubuntu
  ---------------------------------------------------
  Profiles:                  /home/msuriel/security/lynis/default.prf
  Log file:                  /home/msuriel/lynis.log
  Report file:               /home/msuriel/lynis-report.dat
  Report version:            1.0
  Plugin directory:          ./plugins
  ---------------------------------------------------
  Auditor:                   [Not Specified]
  Language:                  en
  Test category:             all
  Test group:                all
  ---------------------------------------------------
  - Program update status...                                  [ NO UPDATE ]

[+] System tools
------------------------------------
  - Scanning available tools...
  - Checking system binaries...

[+] Plugins (phase 1)
------------------------------------
 Note: plugins have more extensive tests and may take several minutes to complete

  - Plugin: pam
    [..]
  - Plugin: systemd
    [.
  [WARNING]: Test PLGN-0010 had a long execution: 20.827224 seconds

...
  [WARNING]: Test PLGN-3804 had a long execution: 17.769865 seconds

...Hint: You are currently not seeing messages from other users and the system.
      Users in groups 'adm', 'systemd-journal' can see all messages.
      Pass -q to turn off this notice.
Hint: You are currently not seeing messages from other users and the system.
      Users in groups 'adm', 'systemd-journal' can see all messages.
      Pass -q to turn off this notice.
..Hint: You are currently not seeing messages from other users and the system.
      Users in groups 'adm', 'systemd-journal' can see all messages.
      Pass -q to turn off this notice.
.Hint: You are currently not seeing messages from other users and the system.
      Users in groups 'adm', 'systemd-journal' can see all messages.
      Pass -q to turn off this notice.
......]

[+] Boot and services
------------------------------------
  - Service Manager                                           [ systemd ]
    - Boot loader                                             [ NONE FOUND ]
  - Check running services (systemctl)                        [ DONE ]
        Result: found 34 running services
Failed to list unit files: Connection timed out
  - Check enabled services at boot (systemctl)                [ DONE ]
        Result: found 0 enabled services

  [WARNING]: Test BOOT-5177 had a long execution: 25.369104 seconds

  - Check startup files (permissions)                         [ OK ]
  - Running 'systemd-analyze security'
        - ModemManager.service:                               [ MEDIUM ]
        - NetworkManager.service:                             [ EXPOSED ]
        - accounts-daemon.service:                            [ UNSAFE ]
        - apache2.service:                                    [ UNSAFE ]
        - apport.service:                                     [ UNSAFE ]
        - atd.service:                                        [ UNSAFE ]
        - avahi-daemon.service:                               [ UNSAFE ]
        - collectl.service:                                   [ UNSAFE ]
        - colord.service:                                     [ EXPOSED ]
        - cron.service:                                       [ UNSAFE ]
        - dbus.service:                                       [ UNSAFE ]
        - dm-event.service:                                   [ UNSAFE ]
        - dmesg.service:                                      [ UNSAFE ]
        - emergency.service:                                  [ UNSAFE ]
        - fail2ban.service:                                   [ UNSAFE ]
        - fwupd.service:                                      [ MEDIUM ]
        - gdm.service:                                        [ UNSAFE ]
        - getty@tty1.service:                                 [ UNSAFE ]
        - irqbalance.service:                                 [ MEDIUM ]
        - iscsid.service:                                     [ UNSAFE ]
        - lvm2-lvmpolld.service:                              [ UNSAFE ]
        - lxd-agent.service:                                  [ UNSAFE ]
        - multipathd.service:                                 [ UNSAFE ]
        - networkd-dispatcher.service:                        [ UNSAFE ]
        - ondemand.service:                                   [ UNSAFE ]
        - plymouth-start.service:                             [ UNSAFE ]
        - polkit.service:                                     [ UNSAFE ]
        - rc-local.service:                                   [ UNSAFE ]
        - rescue.service:                                     [ UNSAFE ]
        - rsync.service:                                      [ UNSAFE ]
        - rsyslog.service:                                    [ UNSAFE ]
        - rtkit-daemon.service:                               [ MEDIUM ]
        - serial-getty@ttyS0.service:                         [ UNSAFE ]
        - snap.lxd.daemon.service:                            [ UNSAFE ]
        - snapd.service:                                      [ UNSAFE ]
        - ssh.service:                                        [ UNSAFE ]
        - switcheroo-control.service:                         [ EXPOSED ]
        - systemd-ask-password-console.service:               [ UNSAFE ]
        - systemd-ask-password-plymouth.service:              [ UNSAFE ]
        - systemd-ask-password-wall.service:                  [ UNSAFE ]
        - systemd-fsckd.service:                              [ UNSAFE ]
        - systemd-initctl.service:                            [ UNSAFE ]
        - systemd-journald.service:                           [ OK ]
        - systemd-logind.service:                             [ OK ]
        - systemd-networkd.service:                           [ OK ]
        - systemd-resolved.service:                           [ OK ]
        - systemd-rfkill.service:                             [ UNSAFE ]
        - systemd-timesyncd.service:                          [ OK ]
        - systemd-udevd.service:                              [ EXPOSED ]
        - unattended-upgrades.service:                        [ UNSAFE ]
        - upower.service:                                     [ OK ]
        - user@1002.service:                                  [ UNSAFE ]
        - user@121.service:                                   [ UNSAFE ]
        - uuidd.service:                                      [ OK ]
        - wpa_supplicant.service:                             [ UNSAFE ]

[+] Kernel
------------------------------------
  - Checking default run level                                [ RUNLEVEL 5 ]
  - Checking kernel version and release                       [ DONE ]
  - Checking kernel type                                      [ DONE ]
  - Checking loaded kernel modules                            [ DONE ]
      Found 73 active modules
  - Checking Linux kernel configuration file                  [ FOUND ]
  - Checking default I/O kernel scheduler                     [ NOT FOUND ]
  - Checking for available kernel update                      [ OK ]
  - Checking core dumps configuration
    - configuration in systemd conf files                     [ DEFAULT ]
    - configuration in etc/profile                            [ DEFAULT ]
    - 'hard' configuration in security/limits.conf            [ DEFAULT ]
    - 'soft' configuration in security/limits.conf            [ DEFAULT ]
    - Checking setuid core dumps configuration                [ PROTECTED ]
  - Check if reboot is needed                                 [ YES ]

[+] Memory and Processes
------------------------------------
  - Checking /proc/meminfo                                    [ FOUND ]
  - Searching for dead/zombie processes                       [ NOT FOUND ]
  - Searching for IO waiting processes                        [ NOT FOUND ]
  - Search prelink tooling                                    [ NOT FOUND ]

[+] Users, Groups and Authentication
------------------------------------
  - Administrator accounts                                    [ OK ]
  - Unique UIDs                                               [ OK ]
  - Unique group IDs                                          [ OK ]
  - Unique group names                                        [ OK ]
  - Password file consistency                                 [ SUGGESTION ]
  - Checking minimum group password hashing rounds            [ DISABLED ]
  - Checking maximum group password hashing rounds            [ DISABLED ]
  - Query system users (non daemons)                          [ DONE ]
  - NIS+ authentication support                               [ NOT ENABLED ]
  - NIS authentication support                                [ NOT ENABLED ]
  - Sudoers file(s)                                           [ FOUND ]
  - PAM password strength tools                               [ SUGGESTION ]
  - PAM configuration files (pam.conf)                        [ FOUND ]
  - PAM configuration files (pam.d)                           [ FOUND ]
  - PAM modules                                               [ NOT FOUND ]
  - LDAP module in PAM                                        [ NOT FOUND ]
  - Accounts without expire date                              [ OK ]
  - Accounts without password                                 [ OK ]
  - Locked accounts                                           [ OK ]
  - Checking user password aging (minimum)                    [ DISABLED ]
  - User password aging (maximum)                             [ DISABLED ]
  - Checking Linux single user mode authentication            [ OK ]
  - Determining default umask
    - umask (/etc/profile)                                    [ NOT FOUND ]
    - umask (/etc/login.defs)                                 [ SUGGESTION ]
  - LDAP authentication support                               [ NOT ENABLED ]
  - Logging failed login attempts                             [ ENABLED ]

[+] Shells
------------------------------------
  - Checking shells from /etc/shells
    Result: found 9 shells (valid shells: 9).
    - Session timeout settings/tools                          [ NONE ]
  - Checking default umask values
    - Checking default umask in /etc/bash.bashrc              [ NONE ]
    - Checking default umask in /etc/profile                  [ NONE ]

[+] File systems
------------------------------------
  - Checking mount points
    - Checking /home mount point                              [ SUGGESTION ]
    - Checking /tmp mount point                               [ SUGGESTION ]
    - Checking /var mount point                               [ SUGGESTION ]
  - Query swap partitions (fstab)                             [ NONE ]
  - Testing swap partitions                                   [ OK ]
  - Testing /proc mount (hidepid)                             [ SUGGESTION ]
  - Checking for old files in /tmp                            [ OK ]
  - Checking /tmp sticky bit                                  [ OK ]
  - Checking /var/tmp sticky bit                              [ OK ]
  - Mount options of /                                        [ NON DEFAULT ]
  - Mount options of /dev                                     [ HARDENED ]
  - Mount options of /dev/shm                                 [ PARTIALLY HARDENED ]
  - Mount options of /run                                     [ HARDENED ]
  - Total without nodev:6 noexec:15 nosuid:12 ro or noexec (W^X): 7 of total 42
  - Disable kernel support of some filesystems
    - Discovered kernel modules: cramfs freevxfs hfs hfsplus jffs2 udf

[+] USB Devices
------------------------------------
  - Checking usb-storage driver (modprobe config)             [ NOT DISABLED ]
  - Checking USB devices authorization                        [ ENABLED ]
  - Checking USBGuard                                         [ NOT FOUND ]

[+] Storage
------------------------------------
  - Checking firewire ohci driver (modprobe config)           [ DISABLED ]

[+] NFS
------------------------------------
  - Check running NFS daemon                                  [ NOT FOUND ]

[+] Name services
------------------------------------
  - Checking /etc/resolv.conf options                         [ FOUND ]
  - Searching DNS domain name                                 [ UNKNOWN ]
  - Checking /etc/hosts
    - Duplicate entries in hosts file                         [ NONE ]
    - Presence of configured hostname in /etc/hosts           [ NOT FOUND ]
    - Hostname mapped to localhost                            [ NOT FOUND ]
    - Localhost mapping to IP address                         [ OK ]

[+] Ports and packages
------------------------------------
  - Searching package managers
    - Searching dpkg package manager                          [ FOUND ]
      - Querying package manager

  [WARNING]: Test PKGS-7345 had a long execution: 25.129922 seconds

    - Query unpurged packages                                 [ FOUND ]
  - Checking security repository in sources.list file         [ OK ]
  - Checking upgradeable packages                             [ SKIPPED ]
  - Checking package audit tool                               [ NONE ]
  - Toolkit for automatic upgrades (unattended-upgrade)       [ FOUND ]

[+] Networking
------------------------------------
  - Checking IPv6 configuration                               [ ENABLED ]
      Configuration method                                    [ AUTO ]
      IPv6 only                                               [ NO ]
  - Checking configured nameservers
    - Testing nameservers
        Nameserver: 127.0.0.53                                [ OK ]
    - DNSSEC supported (systemd-resolved)                     [ NO ]
  - Checking default gateway                                  [ DONE ]
  - Getting listening ports (TCP/UDP)                         [ DONE ]
  - Checking promiscuous interfaces                           [ OK ]
  - Checking waiting connections                              [ OK ]
  - Checking status DHCP client                               [ NOT ACTIVE ]
  - Checking for ARP monitoring software                      [ NOT FOUND ]
  - Uncommon network protocols                                [ 0 ]

[+] Printers and Spools
------------------------------------
  - Checking cups daemon                                      [ NOT FOUND ]
  - Checking lp daemon                                        [ NOT RUNNING ]

[+] Software: e-mail and messaging
------------------------------------

[+] Software: firewalls
------------------------------------
  - Checking iptables kernel module                           [ FOUND ]
  - Checking host based firewall                              [ ACTIVE ]

[+] Software: webserver
------------------------------------
  - Checking Apache (binary /usr/sbin/apache2)                [ FOUND ]
      Info: Configuration file found (/etc/apache2/apache2.conf)
      Info: No virtual hosts found
    * Loadable modules                                        [ FOUND (118) ]
        - Found 118 loadable modules
          mod_evasive: anti-DoS/brute force                   [ NOT FOUND ]
          mod_reqtimeout/mod_qos                              [ FOUND ]
          ModSecurity: web application firewall               [ NOT FOUND ]
  - Checking nginx                                            [ NOT FOUND ]

[+] SSH Support
------------------------------------
  - Checking running SSH daemon                               [ FOUND ]
    - Searching SSH configuration                             [ FOUND ]
    - OpenSSH option: AllowTcpForwarding                      [ NOT FOUND ]
    - OpenSSH option: ClientAliveCountMax                     [ NOT FOUND ]
    - OpenSSH option: ClientAliveInterval                     [ NOT FOUND ]
    - OpenSSH option: Compression                             [ NOT FOUND ]
    - OpenSSH option: FingerprintHash                         [ NOT FOUND ]
    - OpenSSH option: GatewayPorts                            [ NOT FOUND ]
    - OpenSSH option: IgnoreRhosts                            [ NOT FOUND ]
    - OpenSSH option: LoginGraceTime                          [ NOT FOUND ]
    - OpenSSH option: LogLevel                                [ NOT FOUND ]
    - OpenSSH option: MaxAuthTries                            [ NOT FOUND ]
    - OpenSSH option: MaxSessions                             [ NOT FOUND ]
    - OpenSSH option: PermitRootLogin                         [ NOT FOUND ]
    - OpenSSH option: PermitUserEnvironment                   [ NOT FOUND ]
    - OpenSSH option: PermitTunnel                            [ NOT FOUND ]
    - OpenSSH option: Port                                    [ NOT FOUND ]
    - OpenSSH option: PrintLastLog                            [ NOT FOUND ]
    - OpenSSH option: StrictModes                             [ NOT FOUND ]
    - OpenSSH option: TCPKeepAlive                            [ NOT FOUND ]
    - OpenSSH option: UseDNS                                  [ NOT FOUND ]
    - OpenSSH option: X11Forwarding                           [ NOT FOUND ]
    - OpenSSH option: AllowAgentForwarding                    [ NOT FOUND ]
    - OpenSSH option: AllowUsers                              [ NOT FOUND ]
    - OpenSSH option: AllowGroups                             [ NOT FOUND ]

[+] SNMP Support
------------------------------------
  - Checking running SNMP daemon                              [ NOT FOUND ]

[+] Databases
------------------------------------
    No database engines found

[+] LDAP Services
------------------------------------
  - Checking OpenLDAP instance                                [ NOT FOUND ]

[+] PHP
------------------------------------
  - Checking PHP                                              [ NOT FOUND ]

[+] Squid Support
------------------------------------
  - Checking running Squid daemon                             [ NOT FOUND ]

[+] Logging and files
------------------------------------
  - Checking for a running log daemon                         [ OK ]
    - Checking Syslog-NG status                               [ NOT FOUND ]
    - Checking systemd journal status                         [ FOUND ]
    - Checking Metalog status                                 [ NOT FOUND ]
    - Checking RSyslog status                                 [ FOUND ]
    - Checking RFC 3195 daemon status                         [ NOT FOUND ]
    - Checking minilogd instances                             [ NOT FOUND ]
  - Checking logrotate presence                               [ OK ]
  - Checking remote logging                                   [ NOT ENABLED ]
  - Checking log directories (static list)                    [ DONE ]
  - Checking open log files                                   [ DONE ]
  - Checking deleted files in use                             [ FILES FOUND ]

[+] Insecure services
------------------------------------
  - Installed inetd package                                   [ NOT FOUND ]
  - Installed xinetd package                                  [ OK ]
    - xinetd status                                           [ NOT ACTIVE ]
  - Installed rsh client package                              [ OK ]
  - Installed rsh server package                              [ OK ]
  - Installed telnet client package                           [ OK ]
  - Installed telnet server package                           [ NOT FOUND ]
  - Checking NIS client installation                          [ OK ]
  - Checking NIS server installation                          [ OK ]
  - Checking TFTP client installation                         [ OK ]
  - Checking TFTP server installation                         [ OK ]

[+] Banners and identification
------------------------------------
  - /etc/issue                                                [ FOUND ]
    - /etc/issue contents                                     [ WEAK ]
  - /etc/issue.net                                            [ FOUND ]
    - /etc/issue.net contents                                 [ WEAK ]

[+] Scheduled tasks
------------------------------------
  - Checking crontab and cronjob files                        [ DONE ]
  - Checking atd status                                       [ RUNNING ]
    - Checking at users                                       [ DONE ]
    - Checking at jobs                                        [ NONE ]

[+] Accounting
------------------------------------
  - Checking accounting information                           [ NOT FOUND ]
  - Checking sysstat accounting data                          [ NOT FOUND ]
  - Checking auditd                                           [ NOT FOUND ]

[+] Time and Synchronization
------------------------------------
  - NTP daemon found: systemd (timesyncd)                     [ FOUND ]
  - Checking for a running NTP daemon or client               [ OK ]
  - Last time synchronization                                 [ 874s ]

[+] Cryptography
------------------------------------
  - Checking for expired SSL certificates [0/143]             [ NONE ]

  [WARNING]: Test CRYP-7902 had a long execution: 70.752827 seconds

  - Kernel entropy is sufficient                              [ YES ]
  - HW RNG & rngd                                             [ NO ]
  - SW prng                                                   [ NO ]

[+] Virtualization
------------------------------------

[+] Containers
------------------------------------

[+] Security frameworks
------------------------------------
  - Checking presence AppArmor                                [ FOUND ]
    - Checking AppArmor status                                [ UNKNOWN ]
  - Checking presence SELinux                                 [ NOT FOUND ]
  - Checking presence TOMOYO Linux                            [ NOT FOUND ]
  - Checking presence grsecurity                              [ NOT FOUND ]
  - Checking for implemented MAC framework                    [ NONE ]

[+] Software: file integrity
------------------------------------
  - Checking file integrity tools
Cannot initialize device-mapper, running as non-root user.
  - dm-integrity (status)                                     [ DISABLED ]
Cannot initialize device-mapper, running as non-root user.
  - dm-verity (status)                                        [ DISABLED ]
  - Checking presence integrity tool                          [ NOT FOUND ]

[+] Software: System tooling
------------------------------------
  - Checking automation tooling
  - Automation tooling                                        [ NOT FOUND ]
  - Checking presence of Fail2ban                             [ FOUND ]
2020-11-15 20:59:23,428 fail2ban                [152703]: ERROR   Failed during configuration: File contains no section headers.
file: '/etc/fail2ban/jail.local', line: 1
'enable = true\n'
2020-11-15 20:59:23,428 fail2ban                [152703]: ERROR   Init of command line failed
    - Checking Fail2ban jails                                 [ DISABLED ]
  - Checking for IDS/IPS tooling                              [ FOUND ]

[+] Software: Malware
------------------------------------

[+] File Permissions
------------------------------------
  - Starting file permissions check
    File: /etc/at.deny                                        [ SUGGESTION ]
    File: /etc/crontab                                        [ SUGGESTION ]
    File: /etc/group                                          [ OK ]
    File: /etc/group-                                         [ OK ]
    File: /etc/hosts.allow                                    [ OK ]
    File: /etc/hosts.deny                                     [ OK ]
    File: /etc/issue                                          [ OK ]
    File: /etc/issue.net                                      [ OK ]
    File: /etc/passwd                                         [ OK ]
    File: /etc/passwd-                                        [ OK ]
    File: /etc/ssh/sshd_config                                [ SUGGESTION ]
    Directory: /etc/cron.d                                    [ SUGGESTION ]
    Directory: /etc/cron.daily                                [ SUGGESTION ]
    Directory: /etc/cron.hourly                               [ SUGGESTION ]
    Directory: /etc/cron.weekly                               [ SUGGESTION ]
    Directory: /etc/cron.monthly                              [ SUGGESTION ]

[+] Home directories
------------------------------------
  - Permissions of home directories                           [ WARNING ]

  [WARNING]: Test HOME-9304 had a long execution: 10.403898 seconds

  - Ownership of home directories                             [ OK ]
  - Checking shell history files                              [ OK ]

[+] Kernel Hardening
------------------------------------
  - Comparing sysctl key pairs with scan profile
    - fs.suid_dumpable (exp: 0)                               [ DIFFERENT ]
    - kernel.core_uses_pid (exp: 1)                           [ DIFFERENT ]
    - kernel.ctrl-alt-del (exp: 0)                            [ OK ]
    - kernel.dmesg_restrict (exp: 1)                          [ DIFFERENT ]
    - kernel.kptr_restrict (exp: 2)                           [ DIFFERENT ]
    - kernel.randomize_va_space (exp: 2)                      [ OK ]
    - kernel.sysrq (exp: 0)                                   [ DIFFERENT ]
    - kernel.yama.ptrace_scope (exp: 1 2 3)                   [ OK ]
    - net.ipv4.conf.all.accept_redirects (exp: 0)             [ DIFFERENT ]
    - net.ipv4.conf.all.accept_source_route (exp: 0)          [ OK ]
    - net.ipv4.conf.all.bootp_relay (exp: 0)                  [ OK ]
    - net.ipv4.conf.all.forwarding (exp: 0)                   [ OK ]
    - net.ipv4.conf.all.log_martians (exp: 1)                 [ DIFFERENT ]
    - net.ipv4.conf.all.mc_forwarding (exp: 0)                [ OK ]
    - net.ipv4.conf.all.proxy_arp (exp: 0)                    [ OK ]
    - net.ipv4.conf.all.rp_filter (exp: 1)                    [ DIFFERENT ]
    - net.ipv4.conf.all.send_redirects (exp: 0)               [ DIFFERENT ]
    - net.ipv4.conf.default.accept_redirects (exp: 0)         [ DIFFERENT ]
    - net.ipv4.conf.default.accept_source_route (exp: 0)      [ DIFFERENT ]
    - net.ipv4.conf.default.log_martians (exp: 1)             [ DIFFERENT ]
    - net.ipv4.icmp_echo_ignore_broadcasts (exp: 1)           [ OK ]
    - net.ipv4.icmp_ignore_bogus_error_responses (exp: 1)     [ OK ]
    - net.ipv4.tcp_syncookies (exp: 1)                        [ OK ]
    - net.ipv4.tcp_timestamps (exp: 0 1)                      [ OK ]
    - net.ipv6.conf.all.accept_redirects (exp: 0)             [ DIFFERENT ]
    - net.ipv6.conf.all.accept_source_route (exp: 0)          [ OK ]
    - net.ipv6.conf.default.accept_redirects (exp: 0)         [ DIFFERENT ]
    - net.ipv6.conf.default.accept_source_route (exp: 0)      [ OK ]

[+] Hardening
------------------------------------
    - Installed compiler(s)                                   [ FOUND ]
    - Installed malware scanner                               [ NOT FOUND ]

[+] Custom tests
------------------------------------
  - Running custom tests...                                   [ NONE ]

[+] Plugins (phase 2)
------------------------------------
  - Plugins (phase 2)                                         [ DONE ]

================================================================================

  -[ Lynis 3.0.2 Results ]-

  Warnings (2):
  ----------------------------
  ! Reboot of system is most likely needed [KRNL-5830]
    - Solution : reboot
      https://cisofy.com/lynis/controls/KRNL-5830/

  ! All jails in Fail2ban are disabled [TOOL-5104]
    - Details  : /etc/fail2ban/jail.local
      https://cisofy.com/lynis/controls/TOOL-5104/

  Suggestions (42):
  ----------------------------
  * Consider hardening system services [BOOT-5264]
    - Details  : Run '/usr/bin/systemd-analyze security SERVICE' for each service
      https://cisofy.com/lynis/controls/BOOT-5264/

  * If not required, consider explicit disabling of core dump in /etc/security/limits.conf file [KRNL-5820]
      https://cisofy.com/lynis/controls/KRNL-5820/

  * Run pwck manually and correct any errors in the password file [AUTH-9228]
      https://cisofy.com/lynis/controls/AUTH-9228/

  * Configure minimum encryption algorithm rounds in /etc/login.defs [AUTH-9230]
      https://cisofy.com/lynis/controls/AUTH-9230/

  * Configure maximum encryption algorithm rounds in /etc/login.defs [AUTH-9230]
      https://cisofy.com/lynis/controls/AUTH-9230/

  * Install a PAM module for password strength testing like pam_cracklib or pam_passwdqc [AUTH-9262]
      https://cisofy.com/lynis/controls/AUTH-9262/

  * Configure minimum password age in /etc/login.defs [AUTH-9286]
      https://cisofy.com/lynis/controls/AUTH-9286/

  * Configure maximum password age in /etc/login.defs [AUTH-9286]
      https://cisofy.com/lynis/controls/AUTH-9286/

  * Default umask in /etc/login.defs could be more strict like 027 [AUTH-9328]
      https://cisofy.com/lynis/controls/AUTH-9328/

  * To decrease the impact of a full /home file system, place /home on a separate partition [FILE-6310]
      https://cisofy.com/lynis/controls/FILE-6310/

  * To decrease the impact of a full /tmp file system, place /tmp on a separate partition [FILE-6310]
      https://cisofy.com/lynis/controls/FILE-6310/

  * To decrease the impact of a full /var file system, place /var on a separate partition [FILE-6310]
      https://cisofy.com/lynis/controls/FILE-6310/

  * Consider disabling unused kernel modules [FILE-6430]
    - Details  : /etc/modprobe.d/blacklist.conf
    - Solution : Add 'install MODULENAME /bin/true' (without quotes)
      https://cisofy.com/lynis/controls/FILE-6430/

  * Disable drivers like USB storage when not used, to prevent unauthorized storage or data theft [USB-1000]
      https://cisofy.com/lynis/controls/USB-1000/

  * Check DNS configuration for the dns domain name [NAME-4028]
      https://cisofy.com/lynis/controls/NAME-4028/

  * Add the IP name and FQDN to /etc/hosts for proper name resolving [NAME-4404]
      https://cisofy.com/lynis/controls/NAME-4404/

  * Purge old/removed packages (6 found) with aptitude purge or dpkg --purge command. This will cleanup old configuration files, cron jobs and startup scripts. [PKGS-7346]
      https://cisofy.com/lynis/controls/PKGS-7346/

  * Install debsums utility for the verification of packages with known good database. [PKGS-7370]
      https://cisofy.com/lynis/controls/PKGS-7370/

  * Install package apt-show-versions for patch management purposes [PKGS-7394]
      https://cisofy.com/lynis/controls/PKGS-7394/

  * Install a package audit tool to determine vulnerable packages [PKGS-7398]
      https://cisofy.com/lynis/controls/PKGS-7398/

  * Remove any unneeded kernel packages [PKGS-7410]
    - Details  : 6 kernels
    - Solution : validate dpkg -l output and perform cleanup with apt autoremove
      https://cisofy.com/lynis/controls/PKGS-7410/

  * Determine if protocol 'dccp' is really needed on this system [NETW-3200]
      https://cisofy.com/lynis/controls/NETW-3200/

  * Determine if protocol 'sctp' is really needed on this system [NETW-3200]
      https://cisofy.com/lynis/controls/NETW-3200/

  * Determine if protocol 'rds' is really needed on this system [NETW-3200]
      https://cisofy.com/lynis/controls/NETW-3200/

  * Determine if protocol 'tipc' is really needed on this system [NETW-3200]
      https://cisofy.com/lynis/controls/NETW-3200/

  * Install Apache mod_evasive to guard webserver against DoS/brute force attempts [HTTP-6640]
      https://cisofy.com/lynis/controls/HTTP-6640/

  * Install Apache modsecurity to guard webserver against web application attacks [HTTP-6643]
      https://cisofy.com/lynis/controls/HTTP-6643/

  * Enable logging to an external logging host for archiving purposes and additional protection [LOGG-2154]
      https://cisofy.com/lynis/controls/LOGG-2154/

  * Check what deleted files are still in use and why. [LOGG-2190]
      https://cisofy.com/lynis/controls/LOGG-2190/

  * Add a legal banner to /etc/issue, to warn unauthorized users [BANN-7126]
      https://cisofy.com/lynis/controls/BANN-7126/

  * Add legal banner to /etc/issue.net, to warn unauthorized users [BANN-7130]
      https://cisofy.com/lynis/controls/BANN-7130/

  * Enable process accounting [ACCT-9622]
      https://cisofy.com/lynis/controls/ACCT-9622/

  * Enable sysstat to collect accounting (no results) [ACCT-9626]
      https://cisofy.com/lynis/controls/ACCT-9626/

  * Enable auditd to collect audit information [ACCT-9628]
      https://cisofy.com/lynis/controls/ACCT-9628/

  * Check output of aa-status [MACF-6208]
    - Details  : /sys/kernel/security/apparmor/profiles
    - Solution : Run aa-status
      https://cisofy.com/lynis/controls/MACF-6208/

  * Install a file integrity tool to monitor changes to critical and sensitive files [FINT-4350]
      https://cisofy.com/lynis/controls/FINT-4350/

  * Determine if automation tools are present for system management [TOOL-5002]
      https://cisofy.com/lynis/controls/TOOL-5002/

  * Consider restricting file permissions [FILE-7524]
    - Details  : See screen output or log file
    - Solution : Use chmod to change file permissions
      https://cisofy.com/lynis/controls/FILE-7524/

  * Double check the permissions of home directories as some might be not strict enough. [HOME-9304]
      https://cisofy.com/lynis/controls/HOME-9304/

  * One or more sysctl values differ from the scan profile and could be tweaked [KRNL-6000]
    - Solution : Change sysctl value or disable test (skip-test=KRNL-6000:<sysctl-key>)
      https://cisofy.com/lynis/controls/KRNL-6000/

  * Harden compilers like restricting access to root user only [HRDN-7222]
      https://cisofy.com/lynis/controls/HRDN-7222/

  * Harden the system by installing at least one malware scanner, to perform periodic file system scans [HRDN-7230]
    - Solution : Install a tool like rkhunter, chkrootkit, OSSEC
      https://cisofy.com/lynis/controls/HRDN-7230/

  Follow-up:
  ----------------------------
  - Show details of a test (lynis show details TEST-ID)
  - Check the logfile for all details (less /home/msuriel/lynis.log)
  - Read security controls texts (https://cisofy.com)
  - Use --upload to upload data to central system (Lynis Enterprise users)

================================================================================

  Lynis security scan details:

  Hardening index : 59 [###########         ]
  Tests performed : 251
  Plugins enabled : 2

  Components:
  - Firewall               [V]
  - Malware scanner        [X]

  Scan mode:
  Normal [ ]  Forensics [ ]  Integration [ ]  Pentest [V] (running non-privileged)

  Lynis modules:
  - Compliance status      [?]
  - Security audit         [V]
  - Vulnerability scan     [V]

  Files:
  - Test and debug information      : /home/msuriel/lynis.log
  - Report data                     : /home/msuriel/lynis-report.dat

================================================================================

  Skipped tests due to non-privileged mode
    BOOT-5108 - Check Syslinux as bootloader
    BOOT-5109 - Check rEFInd as bootloader
    BOOT-5116 - Check if system is booted in UEFI mode
    AUTH-9216 - Check group and shadow group files
    AUTH-9229 - Check password hashing methods
    AUTH-9252 - Check ownership and permissions for sudo configuration files
    AUTH-9288 - Checking for expired passwords
    FILE-6368 - Checking ACL support on root file system
    PKGS-7390 - Check Ubuntu database consistency
    PKGS-7392 - Check for Debian/Ubuntu security updates
    FIRE-4508 - Check used policies of iptables chains
    FIRE-4512 - Check iptables for empty ruleset
    FIRE-4513 - Check iptables for unused rules
    FIRE-4586 - Check firewall logging
    CRYP-7930 - Determine if system uses LUKS block device encryption
    CRYP-7931 - Determine if system uses encrypted swap

================================================================================

  Lynis 3.0.2

  Auditing, system hardening, and compliance for UNIX-based systems
  (Linux, macOS, BSD, and others)

  2007-2020, CISOfy - https://cisofy.com/lynis/
  Enterprise support available (compliance, plugins, interface and tools)

================================================================================

  [TIP]: Enhance Lynis audits by adding your settings to custom.prf (see /home/msuriel/security/lynis/default.prf for all settings)
```