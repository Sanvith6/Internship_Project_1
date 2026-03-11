# Linux Commands Reference

A practical list of commonly used Linux commands, grouped by task.

## 1) Files and Directories

```bash
pwd                         # print current directory
ls                          # list files
ls -la                      # list all files (including hidden) with details
cd /path/to/dir             # change directory
cd ..                       # go up one directory
mkdir newdir                # create directory
mkdir -p a/b/c              # create nested directories
rmdir emptydir              # remove empty directory
touch file.txt              # create empty file
cp source.txt dest.txt      # copy file
cp -r srcdir destdir        # copy directory recursively
mv old.txt new.txt          # move/rename
rm file.txt                 # remove file
rm -r dir                   # remove directory recursively
rm -rf dir                  # force remove directory recursively (danger)
file my.bin                 # show file type
stat file.txt               # detailed file metadata
```

## 2) Viewing and Editing Files

```bash
cat file.txt                # print full file
less file.txt               # scroll file viewer
head -n 20 file.txt         # first 20 lines
tail -n 20 file.txt         # last 20 lines
tail -f app.log             # follow log updates
nano file.txt               # edit with nano
vim file.txt                # edit with vim
wc -l file.txt              # count lines
sort file.txt               # sort lines
uniq file.txt               # remove adjacent duplicate lines
cut -d',' -f1 data.csv      # extract column 1 from CSV-like data
paste a.txt b.txt           # merge lines side by side
tr 'a-z' 'A-Z' < in.txt     # translate lowercase to uppercase
```

## 3) Search and Text Processing

```bash
grep "error" app.log                # search text
grep -R "TODO" .                    # recursive search
grep -n "main" program.c            # show matching line numbers
find . -name "*.py"                 # find files by name
find . -type f -size +100M           # find files larger than 100 MB
which python                          # show command location
whereis ssh                           # command source/manual/binary locations
locate nginx.conf                     # fast indexed file lookup (if database exists)
sed -n '1,20p' file.txt              # print lines 1-20
sed 's/foo/bar/g' file.txt           # replace text in output
awk '{print $1}' file.txt            # print first column
xargs -n1 echo < items.txt           # pass input as command arguments
```

## 4) Permissions and Ownership

```bash
chmod 644 file.txt           # rw-r--r--
chmod +x script.sh           # make executable
chmod -R 755 mydir           # set recursive permissions
chown user:group file.txt    # change owner and group
chown -R user:group mydir    # recursive ownership change
umask 022                    # set default permission mask
```

## 5) Compression and Archives

```bash
tar -cvf archive.tar dir/             # create tar
tar -xvf archive.tar                  # extract tar
tar -czvf archive.tar.gz dir/         # create gzip tar
tar -xzvf archive.tar.gz              # extract gzip tar
zip -r archive.zip dir/               # create zip
unzip archive.zip                     # extract zip
gzip file.txt                         # compress to file.txt.gz
gunzip file.txt.gz                    # decompress
```

## 6) Processes and Jobs

```bash
ps aux                      # list processes
top                         # live process monitor
htop                        # interactive process monitor (if installed)
pgrep nginx                 # process ids by name
kill 1234                   # terminate process by PID
kill -9 1234                # force kill PID
pkill node                  # kill by process name
jobs                        # list background jobs
bg %1                       # continue job in background
fg %1                       # bring job to foreground
nohup command &             # run command immune to hangups in background
```

## 7) System and Hardware Info

```bash
uname -a                    # kernel/system info
hostnamectl                 # host + OS details (systemd)
cat /etc/os-release         # distro details
uptime                      # uptime and load
free -h                     # memory usage
df -h                       # disk usage by filesystem
du -sh *                    # folder sizes in current dir
lsblk                       # block devices
lscpu                       # CPU info
ip a                        # network interfaces
```

## 8) Networking

```bash
ping google.com                      # connectivity test
curl https://example.com             # HTTP request
curl -I https://example.com          # headers only
wget https://example.com/file.zip    # download file
ssh user@server                      # remote shell
scp file.txt user@server:/tmp/       # secure copy
rsync -avz src/ user@server:/dst/    # efficient sync
ss -tulnp                            # listening sockets
netstat -tulnp                       # older socket view (if available)
dig example.com                      # DNS query
nslookup example.com                 # DNS lookup
```

## 9) Package Management (by distro)

```bash
# Debian/Ubuntu
sudo apt update
sudo apt install git
sudo apt remove git

# RHEL/CentOS/Fedora
sudo dnf install git
sudo yum install git

# Arch
sudo pacman -Syu
sudo pacman -S git
```

## 10) Users and Groups

```bash
whoami                      # current user
id                          # uid/gid and groups
who                         # logged-in users
sudo adduser alice          # add user (Debian style)
sudo useradd alice          # add user (low-level)
sudo passwd alice           # set/change password
groups alice                # list user groups
sudo usermod -aG sudo alice # add user to sudo group
```

## 11) Shell and Environment

```bash
echo $PATH                  # view PATH
export APP_ENV=prod         # set env var in current shell
env                         # list environment vars
history                     # command history
alias ll='ls -la'           # command alias
source ~/.bashrc            # reload shell config
```

## 12) Useful Shortcuts

```bash
Ctrl + C    # stop running command
Ctrl + Z    # suspend running command
Ctrl + D    # logout/end input
Ctrl + R    # reverse search history
!!          # run previous command
!123        # run command number 123 from history
```

## 13) Redirection and Pipes

```bash
command > out.txt           # stdout to file (overwrite)
command >> out.txt          # stdout to file (append)
command 2> err.txt          # stderr to file
command > out.txt 2>&1      # stdout + stderr to same file
command1 | command2         # pipe output to next command
tee out.txt                 # write output to file and screen
```

## 14) Scheduling and Automation

```bash
crontab -e                  # edit cron jobs
crontab -l                  # list cron jobs
at 10:30                    # schedule one-time task (if installed)
systemctl status nginx      # service status (systemd)
sudo systemctl restart nginx# restart service
journalctl -u nginx         # service logs
```

## 15) Quick Safety Notes

- Always double-check before `rm -rf`.
- Prefer `cp -i`, `mv -i`, `rm -i` to prompt before overwrite/delete.
- Use least privilege; only run `sudo` when required.
- Validate remote targets before `scp`/`rsync`.
