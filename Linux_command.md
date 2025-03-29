# Essential Linux Commands

## 1. File and Directory Management
```sh
ls          # List files and directories
ls -l       # Detailed list with permissions, owner, size, etc.
ls -a       # Show hidden files
pwd         # Print working directory
cd /path    # Change directory
mkdir dir   # Create a directory
rmdir dir   # Remove an empty directory
rm file.txt # Remove a file
rm -r dir   # Remove directory and its contents
cp file1 file2  # Copy a file
cp -r dir1 dir2 # Copy directory and its contents
mv file1 file2  # Move or rename a file
find / -name "file.txt"  # Search for a file by name
locate file.txt # Find file using locate database
```

## 2. File Permissions & Ownership
```sh
chmod 755 file.txt   # Set file permissions using numeric mode
chmod u+x file.txt   # Add execute permission for the owner
chmod g-w file.txt   # Remove write permission for the group
chmod o+r file.txt   # Add read permission for others
chown user:group file.txt   # Change file ownership
chown -R user:group /dir  # Change ownership recursively
```

## 3. Viewing & Editing Files
```sh
cat file.txt   # Display file contents
tac file.txt   # Display file in reverse
less file.txt  # View file one page at a time
head -n 10 file.txt  # Show first 10 lines
tail -n 10 file.txt  # Show last 10 lines
touch file.txt  # Create a new empty file
nano file.txt   # Edit file in Nano editor
vim file.txt    # Edit file in Vim editor
```

## 4. User & Group Management
```sh
whoami         # Show current user
who            # Show logged-in users
id             # Show user ID and group ID
adduser user   # Create a new user
userdel -r user # Delete a user
passwd user    # Change password
groupadd group # Create a group
usermod -aG group user # Add user to a group
groups user    # Show user groups
```

## 5. Process Management
```sh
ps aux         # Show running processes
top            # Show active processes
kill PID       # Kill a process by PID
killall process # Kill all processes by name
nohup command & # Run command in background
jobs           # Show background jobs
fg             # Bring job to foreground
bg             # Resume background job
```

## 6. Disk Usage & Management
```sh
df -h          # Show disk usage
du -sh /path   # Show directory size
mount /dev/sdX /mnt  # Mount a device
umount /mnt    # Unmount a device
fdisk -l       # Show partitions
mkfs.ext4 /dev/sdX  # Format a partition
fsck /dev/sdX  # Check and repair filesystem errors
```

## 7. Networking Commands
```sh
ifconfig       # Show IP address
ip a           # Show network interfaces
ping google.com # Check connectivity
netstat -tulnp  # Show open ports
traceroute google.com # Show route to host
wget URL       # Download file
curl -O URL    # Download file
scp file user@host:/path # Secure copy
rsync -avz source/ user@host:/path # Sync files
```

## 8. Package Management
### Debian-based (Ubuntu, Debian)
```sh
apt update           # Update package list
apt upgrade          # Upgrade all packages
apt install package  # Install package
apt remove package   # Remove package
dpkg -i package.deb  # Install a .deb package
dpkg -r package      # Remove a .deb package
```

### RHEL-based (CentOS, Fedora)
```sh
yum update           # Update packages
yum install package  # Install package
yum remove package   # Remove package
rpm -ivh package.rpm # Install a .rpm package
rpm -e package       # Remove a .rpm package
```

## 9. Archive & Compression
```sh
tar -cvf archive.tar file  # Create tar archive
tar -xvf archive.tar       # Extract tar archive
tar -cvzf archive.tar.gz file # Create compressed archive
tar -xvzf archive.tar.gz   # Extract compressed archive
zip archive.zip file       # Create zip file
unzip archive.zip          # Extract zip file
```

## 10. System Monitoring & Logs
```sh
uptime         # Show system uptime
free -h        # Show memory usage
dmesg          # View kernel logs
journalctl -xe # View system logs
tail -f /var/log/syslog # View logs in real-time
```

## 11. Shutdown & Reboot
```sh
shutdown -h now   # Shutdown system immediately
shutdown -r now   # Reboot system immediately
reboot           # Reboot system
halt             # Stop system
poweroff         # Power off system
```

