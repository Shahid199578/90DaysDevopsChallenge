# Day 14 - Deeper into Linux (Permissions, Processes, Services)
## 1. **File Permissions and Ownership**



[![](https://img.youtube.com/vi/7MU50J-vYCc/0.jpg)](https://www.youtube.com/watch?v=7MU50J-vYCc)

[Watch the video](https://www.youtube.com/watch?v=7MU50J-vYCc)

### Viewing Permissions
- **ls -l**: Displays file permissions in the long listing format.

---

### 2. **Understanding File Permissions in Linux**
- **File Permissions** determine who can read, write, or execute a file. 
- Represented in two formats: **Symbolic** and **Numeric (Octal)**

---

#### **Numeric Format (Octal Representation)**
- Each permission is assigned a numerical value:
  - Read (r) = 4
  - Write (w) = 2
  - Execute (x) = 1

| Octal | Binary  | Permission | Meaning            |
|-------|---------|------------|--------------------|
| 0     | 000     | ---        | No permissions     |
| 1     | 001     | --x        | Execute only       |
| 2     | 010     | -w-        | Write only         |
| 3     | 011     | -wx        | Write and Execute  |
| 4     | 100     | r--        | Read only          |
| 5     | 101     | r-x        | Read and Execute   |
| 6     | 110     | rw-        | Read and Write     |
| 7     | 111     | rwx        | Full permissions   |

---

#### **Changing File Permissions Using `chmod`**

**Example:**
```bash
chmod 755 file.txt
````

* 7 → Owner: Read (4) + Write (2) + Execute (1)
* 5 → Group: Read (4) + Execute (1)
* 5 → Others: Read (4) + Execute (1)

---

#### **Symbolic Format for `chmod`**

* **u** → Owner (User)
* **g** → Group
* **o** → Others
* **a** → All users

**Example Commands:**

```bash
chmod u+x file.sh   # Adds execute permission for the owner
chmod g-w file.txt  # Removes write permission from the group
chmod o+r file.txt  # Adds read permission for others
chmod a-x script.sh # Removes execute permission for everyone
```

---

### 3. **Changing Ownership Using `chown`**

* The `chown` command changes the owner or group of a file.

```bash
sudo chown john file.txt       # Change owner to 'john'
sudo chown john:developers file.txt  # Change owner to 'john' and group to 'developers'
```

* **Recursively change ownership**:

```bash
sudo chown -R user:group /path   # Changes ownership recursively
```

---

### 4. **Special File Permissions (SetUID, SetGID, Sticky Bit)**

| Special Bit | Octal | Description                 |
| ----------- | ----- | --------------------------- |
| SetUID      | 4xxx  | Runs as file owner          |
| SetGID      | 2xxx  | Runs as group               |
| Sticky Bit  | 1xxx  | Only owner can delete files |

**Example Commands:**

```bash
chmod 4755 script.sh  # SetUID: Runs as file owner
chmod 2755 directory/ # SetGID: Inherits group
chmod 1755 /tmp       # Sticky Bit: Only owner can delete files
```

---

## 5. **Disk and Storage Management**

### Checking Disk Usage

```
df -h
```

Displays disk space usage in a human-readable format.

---

### Checking Directory Size

```
du -sh /path/to/directory
```

Shows the size of the specified directory.

---

### Finding Files and Directories

```
find / -name "file.txt"
```

Searches for a file named "file.txt" starting from the root directory.

---

## 6. **Process and System Monitoring**

### Viewing Running Processes

```
ps aux
```

Displays a list of all running processes.

---

### Real-Time Process Monitoring

```
top
```

Shows a dynamic, real-time view of system processes.

**Alternative:**

```
htop
```

Provides an interactive process viewer (requires installation).

---

### Killing a Process

```bash
kill 1234
```

Terminates the process with the given ID (PID).

**Force Kill:**

```bash
kill -9 1234
```

Forcefully kills the process.

---

## 7. **Networking and Connectivity**

### Display Network Configuration

```bash
ifconfig
```

Shows network interfaces and IP addresses.

**Alternative:**

```bash
ip addr
```

Displays detailed network interface information.

---

### Check Network Connectivity

```bash
ping google.com
```

Tests connectivity to a remote server.

---

### View Open Network Ports

```bash
netstat -tuln
```

Displays active connections and listening ports.