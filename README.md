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

Here are some practical **`smbclient` usage examples** for interacting with SMB shares:

---

### **1. Listing Available Shares on a Server**
Discover the shared directories on a remote SMB server.

#### Command:
```bash
smbclient -L //<SERVER_IP_OR_HOSTNAME> -U <USERNAME>
```

#### Example:
```bash
smbclient -L //192.168.1.100 -U admin
```
You’ll be prompted to enter the password for the specified user.

---

### **2. Accessing a Shared Folder**
Connect to a specific SMB share and access its contents.

#### Command:
```bash
smbclient //<SERVER_IP_OR_HOSTNAME>/<SHARE_NAME> -U <USERNAME>
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U user1
```
Once connected, you'll see an interactive prompt similar to an FTP client.

#### Commands to Use Inside the SMB Session:
- `ls` – List files and directories.
- `cd <directory>` – Change directory.
- `get <file>` – Download a file from the share.
- `put <file>` – Upload a file to the share.
- `exit` – Quit the session.

---

### **3. Download a File from an SMB Share**
Directly download a file from an SMB share to your local machine.

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME> -c "get <FILENAME>"
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U admin -c "get important_file.txt"
```
This downloads `important_file.txt` to the current directory.

---

### **4. Upload a File to an SMB Share**
Directly upload a file to an SMB share.

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME> -c "put <LOCAL_FILE>"
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U admin -c "put local_file.txt"
```
This uploads `local_file.txt` to the shared folder.

---

### **5. Browse an SMB Share Without Interactive Mode**
List the contents of a shared folder without entering the interactive mode.

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME> -c "ls"
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U user1 -c "ls"
```

---

### **6. Specify a Workgroup**
If the SMB server requires a specific workgroup, specify it with the `-W` option.

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME> -W <WORKGROUP>
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U user1 -W WORKGROUP
```

---

### **7. Connect to an Anonymous Share**
Some shares don’t require authentication (anonymous access).

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -N
```

#### Example:
```bash
smbclient //192.168.1.100/public -N
```

---

### **8. Set a Password in the Command**
Provide the password directly in the command (not recommended for security).

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME>%<PASSWORD>
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U admin%password123
```

---

### **9. Recursive File Download**
Download all files and directories from an SMB share.

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME> -c "recurse; prompt; mget *"
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U admin -c "recurse; prompt; mget *"
```

---

### **10. Connect to an SMB Share on a Specific Port**
If the SMB service runs on a custom port, specify it using the `-p` option.

#### Command:
```bash
smbclient //<SERVER_IP>:<PORT>/<SHARE_NAME> -U <USERNAME>
```

#### Example:
```bash
smbclient //192.168.1.100:445/shared_folder -U admin
```

---

### **11. Test SMB Authentication**
Check if the SMB credentials work without connecting to a share.

#### Command:
```bash
smbclient -L //<SERVER_IP> -U <USERNAME>%<PASSWORD>
```

#### Example:
```bash
smbclient -L //192.168.1.100 -U admin%password123
```

---

### **12. Mount an SMB Share Locally**
Mount the SMB share to a directory on your local filesystem.

#### Install Required Package:
```bash
sudo apt install cifs-utils
```

#### Command:
```bash
sudo mount -t cifs //<SERVER_IP>/<SHARE_NAME> /mnt -o username=<USERNAME>,password=<PASSWORD>
```

#### Example:
```bash
sudo mount -t cifs //192.168.1.100/shared_folder /mnt -o username=admin,password=password123
```

To unmount the share:
```bash
sudo umount /mnt
```

---

### **13. Search for a Specific File on an SMB Share**
If you are looking for a specific file on a share, use the `smbclient` interactive session.

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U admin
```
Inside the session:
```bash
smb: \> dir *keyword*.txt
```

---

### **14. Retrieve Metadata for a File**
Get details about a file such as its size and last modification date.

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME> -c "allinfo <FILENAME>"
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U admin -c "allinfo important_file.txt"
```

---

### **15. Recursive Upload**
Upload an entire directory to an SMB share.

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME> -c "recurse; prompt; mput <LOCAL_DIRECTORY>/*"
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U admin -c "recurse; prompt; mput /home/user/docs/*"
```

---

### **16. Change File Permissions on a Share**
Modify the permissions of files on the SMB server.

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME> -c "chmod 777 <FILENAME>"
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U admin -c "chmod 755 script.sh"
```

---

### **17. Delete a File on an SMB Share**
Remove a file directly from the share.

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME> -c "del <FILENAME>"
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U admin -c "del old_file.txt"
```

---

### **18. Batch Process Files**
Run multiple commands in one session.

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME> -c "command1; command2; command3"
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U admin -c "mkdir new_folder; cd new_folder; put local_file.txt"
```

---

### **19. List Hidden Files**
Some shares may contain hidden files. Use the `ls` command with wildcard options to reveal them.

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U admin -c "ls .*"
```

---

### **20. Interact with a Read-Only Share**
You can still browse and download files from a read-only share.

#### Example:
```bash
smbclient //192.168.1.100/readonly_share -U guest -c "ls"
```

---

### **21. Access a Share Using Kerberos Authentication**
If the server requires Kerberos authentication, ensure you have the proper ticket.

#### Command:
```bash
kinit <USERNAME>
smbclient //<SERVER_IP>/<SHARE_NAME> -k
```

#### Example:
```bash
kinit admin
smbclient //192.168.1.100/secured_share -k
```

---

### **22. Specify an SMB Protocol Version**
Some servers may require a specific SMB protocol version (e.g., SMB1, SMB2, SMB3).

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME> --option='client min protocol=SMB2'
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U admin --option='client min protocol=SMB3'
```

---

### **23. Debug SMBClient Operations**
Enable debugging to troubleshoot connection issues.

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME> -d <DEBUG_LEVEL>
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U admin -d 3
```
`<DEBUG_LEVEL>` can range from 1 to 10, with higher numbers providing more detail.

---

### **24. Using a Different Network Interface**
Specify a particular network interface for connecting to the SMB server.

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME> -I <INTERFACE_IP>
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U admin -I 192.168.1.50
```

---

### **25. Brute Force SMB Credentials**
Use a tool like **Hydra** for credential brute-forcing.

#### Command:
```bash
hydra -L <USER_LIST> -P <PASSWORD_LIST> smb://<SERVER_IP>
```

#### Example:
```bash
hydra -L users.txt -P passwords.txt smb://192.168.1.100
```

---

### **26. Create a New Folder on an SMB Share**
Directly create a new folder using the interactive session or commands.

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME> -c "mkdir <NEW_FOLDER>"
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U admin -c "mkdir backups"
```

---

### **27. Mount SMB Share Temporarily (Single Session)**
Mount the share for temporary use without modifying the system.

#### Command:
```bash
sudo mount -t cifs //<SERVER_IP>/<SHARE_NAME> /mnt -o username=<USERNAME>,password=<PASSWORD>,uid=$(id -u),gid=$(id -g)
```

#### Example:
```bash
sudo mount -t cifs //192.168.1.100/shared_folder /mnt -o username=admin,password=1234,uid=$(id -u),gid=$(id -g)
```

---

### **28. Automate SMB Operations Using a Script**
Write a shell script to automate frequent tasks with `smbclient`.

#### Example Script:
```bash
#!/bin/bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME> -c "
ls;
put /path/to/local/file;
get remote_file;
exit
"
```

Save the script as `smb_automation.sh` and execute it:
```bash
bash smb_automation.sh
```

---

### **29. Transfer Large Files Efficiently**
For large file transfers, adjust buffer settings for better performance.

#### Command:
```bash
smbclient //<SERVER_IP>/<SHARE_NAME> -U <USERNAME> --socket-options='TCP_NODELAY IPTOS_LOWDELAY'
```

#### Example:
```bash
smbclient //192.168.1.100/shared_folder -U admin --socket-options='TCP_NODELAY IPTOS_LOWDELAY'
```

---

### **30. Combine with Nmap for SMB Enumeration**
Use Nmap to enumerate SMB shares before accessing them.

#### Command:
```bash
nmap --script smb-enum-shares.nse -p 139,445 <TARGET_IP>
```

#### Example:
```bash
nmap --script smb-enum-shares.nse -p 139,445 192.168.1.100
```

---

Let me know if you need **further examples**, **help with automation**, or **troubleshooting guidance**!
