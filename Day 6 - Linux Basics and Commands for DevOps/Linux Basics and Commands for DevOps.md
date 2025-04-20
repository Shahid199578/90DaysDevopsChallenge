## 1. What is Linux?
Linux is a Unix-like operating system kernel initially developed by Linus Torvalds in 1991. It is widely used in servers, embedded systems, and desktop environments. Linux is known for its stability, security, and flexibility.


[![](https://img.youtube.com/vi/ZR7D9k8dBC8/0.jpg)](https://www.youtube.com/watch?v=ZR7D9k8dBC8)

[Watch the video](https://www.youtube.com/watch?v=ZR7D9k8dBC8)

### Key Features of Linux:
1. **Open Source**: Free to use, modify, and distribute.
2. **Multiuser**: Supports multiple users at the same time.
3. **Multitasking**: Can run multiple processes simultaneously.
4. **Portability**: Runs on a wide range of hardware.
5. **Security**: Built-in features for file permissions and user authentication.
6. **Shell**: Provides a command-line interface (CLI) for interacting with the system.

## 2. Types of Linux Distributions
Linux distributions can be broadly classified into the following types based on their origin and package management system:

| Type        | Popular Distros                | Package Manager | Target Audience           |
|------------|--------------------------------|----------------|---------------------------|
| Debian     | Ubuntu, Mint, Kali, MX Linux  | apt, dpkg      | Desktop, Server, Security |
| Red Hat    | RHEL, CentOS, Fedora, Rocky  | yum, dnf, rpm  | Enterprise, Servers       |
| Arch       | Arch, Manjaro, EndeavourOS    | pacman        | Advanced users, Customization |
| Gentoo     | Gentoo, Calculate, Sabayon   | emerge        | Power users, Custom builds |
| Slackware  | Slackware, Salix, Zenwalk    | slackpkg      | Minimalist, Unix-like      |
| Independent| Alpine, Clear, Solus, NixOS  | Varies        | Various specialized use cases |

## 3. Linux Directory Structure
The Linux file system follows a hierarchical structure starting from the root (/). Here’s an overview of the most important directories:

| Directory | Description |
|-----------|-------------|
| /        | Root directory. All files and directories start here. |
| /bin     | Essential binaries and commands. |
| /boot    | Boot loader files. |
| /dev     | Device files (e.g., disk drives, USB). |
| /etc     | Configuration files and scripts. |
| /home    | User home directories. |
| /lib     | Shared libraries and kernel modules. |
| /mnt     | Temporary mount point for filesystems. |
| /opt     | Optional software packages. |
| /proc    | Kernel and process files. |
| /root    | Home directory of the root user. |
| /sbin    | System administration binaries. |
| /tmp     | Temporary files. |
| /usr     | User-related programs and data. |
| /var     | Variable data files (e.g., logs, cache). |

## 4. Linux Shell
A shell is a command interpreter that allows users to interact with the operating system. The most common shell in Ubuntu is Bash (Bourne Again SHell). To check the current shell, use:
```bash
echo $SHELL
```

## 5. Basic Linux Commands

### Viewing the Current Directory
```bash
pwd  # Prints the current working directory
```

### Listing Files and Directories
```bash
ls  # Displays a list of files and directories
```
**Options:**
- `ls -l` - Long listing format with file permissions.
- `ls -a` - Shows hidden files.
- `ls -lh` - Human-readable file sizes.
- `ls -R` - Lists directories and subdirectories recursively.

### Changing Directories
```bash
cd /path/to/directory  # Changes the current directory
```
Examples:
- `cd /home/user` - Moves to the user's home directory.
- `cd ..` - Moves one level up in the directory hierarchy.
- `cd ~` - Moves to the home directory.
- `cd -` - Switches to the previous directory.

## 6. File and Directory Operations

### Creating a Directory
```bash
mkdir myfolder  # Creates a new directory named "myfolder"
```
Options:
- `mkdir -p /path/to/new/folder` - Creates parent directories if they do not exist.

### Removing a Directory
```bash
rmdir myfolder  # Removes an empty directory
```
Options:
- `rm -r myfolder` - Removes a directory and its contents recursively.
- `rm -rf myfolder` - Forcefully deletes a directory and all its contents.

### Creating a File
```bash
touch file.txt  # Creates an empty file named "file.txt"
```

### Viewing File Content
```bash
cat file.txt  # Displays the content of a file
```
Other Commands:
- `more file.txt` - Shows content page by page.
- `less file.txt` - Similar to "more" but allows backward navigation.
- `head -n 5 file.txt` - Shows the first 5 lines.
- `tail -n 5 file.txt` - Shows the last 5 lines.
- `tail -f file.txt` - Monitors the file in real-time.

### Copying Files and Directories
```bash
cp file1.txt file2.txt  # Copies "file1.txt" to "file2.txt"
```
Options:
- `cp -r dir1 dir2` - Copies a directory and its contents recursively.
- `cp -i file1.txt file2.txt` - Prompts before overwriting.

### Moving or Renaming Files
```bash
mv file.txt /path/to/destination/  # Moves the file to the specified destination
```
Options:
- `mv file1.txt file2.txt` - Renames the file.

### Deleting Files
```bash
rm file.txt  # Removes a file
```
Options:
- `rm -i file.txt` - Prompts before deleting.
- `rm -f file.txt` - Force deletes without prompt.

## 7. File Permissions and Ownership

### Viewing Permissions
```bash
ls -l  # Displays file permissions in the long listing format
```

### Changing Permissions
```bash
chmod 755 file.txt  # Full access for owner, read & execute for others
chmod 644 file.txt  # Read & write for owner, read-only for others
chmod +x script.sh  # Add execute permission for everyone
```

### Changing Ownership
```bash
chown user:group file.txt  # Change file ownership
```
Example:
```bash
sudo chown john file.txt  # Change owner to 'john'
sudo chown john:developers file.txt  # Change owner to 'john' and group to 'developers'
```

### Recursively Change Permissions
```bash
chmod -R 755 /var/www/html  # Sets permissions for all files & directories under /var/www/html
sudo chown -R john:developers /home/john/  # Changes owner to john and group to developers
```

## 8. Disk and Storage Management

### Checking Disk Usage
```bash
df -h  # Displays disk space usage in a human-readable format
```

### Checking Directory Size
```bash
du -sh /path/to/directory  # Shows the size of a directory
```

