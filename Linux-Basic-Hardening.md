# Linux Basic Hardening

When setting up a new Linux server one cannot forget about the security portion of it. Without making sure that your machine is secure, every day you are exposed to dangers from countries like Russia, China, Iran etc. where numerous people just wait for you to make mistakes. Even in the US there is plenty of such people, which is why DEFCON is attended by so many security proffesionals each year. Below you'll find a few general tips and a few one-liners to help you prepare either a new server or a server you have just "inherited" from someone else:

# General Tips
## Find all users with a shell
```grep -vE '^#|^$| false|nologin' /etc/shells |
while read shell; do
grep -E ":${shell}\$" /etc/passwd
done
```

## Change passwords for a list of users
Change replace user_list.txt with a user/password list in the following format:

jdoe password123
bsmith password456

Spaces or tabs work as separators for the list. Once list is complete, run the following command:

```while read user pass; do
echo ${user}:${pass} | chpasswd
done < user_list.txt
```

## Show Arguments for a Running Process
Replace `PID` with the PID of the desired process (e.g., a PID you got from netstat)
`ps -p PID -o args`

Argument Explanation:
- -p PID
- -o format of output (what columns of information to show)

## Show Files in Use by a Process
Replace `PID` with the PID of the desired process (e.g., a PID you got from netstat)
`lsof -p PID`

## Archive a Directory
It is a good idea to archive data directories for services before altering them. For example:
HTTP data: `/var/www`
MySQL data: `/var/lib/mysql`

Replace backup with the name of archive you would like to create. Replace directory with the path of the directory you would like to back up. I recommend you be in the same working directory prior to running this command, as tar preserves paths.
`tar -cvzf backup.tar.gz directory`

Argument Explanation:
- -c compress
- -f file name of archive to create
- -v verbose (optional)
- -z use gzip compression

## Change the Default Password Encryption
It is possible we may be given machines with a weak default password encryption method. SHA512 with at least 5000 rounds is ideal, if SHA512 is available.

### Show Available Encryption Methods
`chpasswd -h`

The encryption methods available and in use are also stored in:
`/etc/login.defs`

`grep -r '^password.*pam_unix.so' /etc/pam.d`

## Auditd Configuration
### Install auditd
RHEL-based:
`yum -y install audit`
Debian-based:
`apt-get install auditd audispd-plugins`

### Configuring a Ruleset
Add the following rules to /etc/audit/rules.d/audit.rules
```## Buffer Size
## Feel free to increase this if the machine panic's
-b 8192
 
# log cronjobs
-w /etc/cron.allow -p wa -k cron
-w /etc/cron.deny -p wa -k cron
-w /etc/cron.d/ -p wa -k cron
-w /etc/cron.daily/ -p wa -k cron
-w /etc/cron.hourly/ -p wa -k cron
-w /etc/cron.monthly/ -p wa -k cron
-w /etc/cron.weekly/ -p wa -k cron

-w /var/spool/cron/crontabs/ -k cron
 
# log changes to user, group, and password databases
-w /etc/group -p wa -k etcgroup
-w /etc/passwd -p wa -k etcpasswd
-w /etc/gshadow -k etcgroup
-w /etc/shadow -k etcpasswd
-w /etc/security/opasswd -k opasswd
 
# monitor usage of passwd
-w /usr/bin/passwd -p x -k passwd_modification
 
# log all root commands
-a exit,always -F arch=b64 -F euid=0 -S execve -k rootcmd
-a exit,always -F arch=b32 -F euid=0 -S execve -k rootcmd
 
# Monitor for use of process ID change (switching accounts) applications
-w /bin/su -p x -k priv_esc
-w /usr/bin/sudo -p x -k priv_esc
-w /etc/sudoers -p rw -k priv
-w /etc/crontab -p wa -k cron
```

Note: In order to log all remote commands the `audit=1` parameter needs to be added to `/etc/default/grub` and the server needs to be rebooted.

### Send Audit Logs to Syslog
Edit the `/etc/audisp/plugins.d/syslog.conf` file and change `active=no` to `active = yes`.

```active = yes
direction = out
path = builtin_syslog
type = builtin
args = LOG_INFO
format = string
```
