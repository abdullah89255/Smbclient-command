# Smbclient-command
Here are the details of the most commonly used options and examples for the `smbclient` command.

### **Basic Command**
```bash
smbclient [options] //server/share -U username
```
This command connects to the SMB/CIFS share on a server with the specified username.

---

### **Help Options**
Run the following command to view help options:
```bash
smbclient --help
```

Key options from the help output:
- **`-U username[%password]`**: Specifies the username (and optional password) to authenticate with the share.
- **`-W workgroup`**: Specifies the workgroup or domain name.
- **`-L host`**: Lists the shares available on the host.
- **`-c 'command'`**: Executes a single command on the share and exits.
- **`-p port`**: Specifies the port to connect to (default is 445 or 139 for SMB).
- **`-I ip`**: Specifies the IP address of the server if the hostname cannot be resolved.
- **`--no-pass`**: Disables password prompts.
- **`-d level`**: Sets the debug level (0-10, where higher is more verbose).

---

### **Examples**

#### 1. **List Available Shares**
Use the `-L` option to list the available shares on a host:
```bash
smbclient -L //192.168.1.10 -U username
```
You will be prompted for a password. Replace `192.168.1.10` with the server's IP or hostname.

---

#### 2. **Connect to a Share**
Connect to a specific share on a server:
```bash
smbclient //192.168.1.10/share -U username
```
Once connected, you'll enter an interactive shell where you can use SMB commands (e.g., `ls`, `get`, `put`).

---

#### 3. **Authenticate Without a Password Prompt**
You can pass the password directly:
```bash
smbclient //192.168.1.10/share -U username%password
```
This is useful for scripting but may expose passwords.

---

#### 4. **Download a File**
Run a specific command with `-c` to download a file:
```bash
smbclient //192.168.1.10/share -U username -c 'get filename.txt'
```
Replace `filename.txt` with the file name you want to download.

---

#### 5. **Upload a File**
Upload a file to the share:
```bash
smbclient //192.168.1.10/share -U username -c 'put /path/to/localfile.txt remotefile.txt'
```
Replace `/path/to/localfile.txt` with the path to your file and `remotefile.txt` with the desired destination name.

---

#### 6. **Specify a Workgroup**
If the server is part of a specific workgroup or domain:
```bash
smbclient //192.168.1.10/share -U username -W WORKGROUP
```

---

#### 7. **Debug Mode**
Increase verbosity to debug connection issues:
```bash
smbclient //192.168.1.10/share -U username -d 3
```
Replace `3` with a higher number (up to 10) for more detailed logs.

---

#### 8. **Use a Different Port**
If the server uses a non-standard port:
```bash
smbclient //192.168.1.10/share -U username -p 1445
```

---

### **Interactive Commands**
Once connected to a share, you can use the following interactive commands:

- **`ls`**: List files and directories.
- **`cd`**: Change directory.
- **`pwd`**: Print the current directory.
- **`get`**: Download a file (e.g., `get filename.txt`).
- **`put`**: Upload a file (e.g., `put localfile.txt remotefile.txt`).
- **`exit`**: Quit the session.

---

Let me know if you'd like more detailed examples or assistance with any specific scenario!
