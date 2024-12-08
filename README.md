# Linux

What is the boot process in linux?
The Linux boot process is a series of steps that a computer goes through when it is powered on to start the Linux operating system. It involves several key components and stages:   

BIOS/UEFI:

When the computer is powered on, the BIOS (Basic Input/Output System) or UEFI (Unified Extensible Firmware Interface) takes control.   
It performs basic hardware checks and initialization tasks.   
It then looks for a bootable device (usually a hard drive or SSD) and loads the boot loader from the MBR (Master Boot Record) or GPT (GUID Partition Table).   
Boot Loader:

The boot loader (commonly GRUB or LILO) is a small program that loads the Linux kernel into memory.   
It provides options for selecting the kernel to boot and any kernel parameters.
Kernel:

The kernel is the core of the Linux operating system.   
It initializes hardware devices, sets up memory management, and mounts the root file system.   
It then starts the init process, which is the first process to run in the system.
Init:

The init process is responsible for starting other system processes and services.
It reads configuration files to determine which services to start and in what order.   
It also sets up the runlevels or target states of the system.   
Runlevel Programs:

Runlevel programs are scripts or programs that are executed at different stages of the boot process or in response to system events.   
They can be used to configure hardware, start services, and set up the system environment.

2.What are soft-links and hard-links in linux?
Definition: A hard link is a direct pointer to a file's data on the disk. It's essentially an alternate name for the same file.   
Key Characteristics:
Same Inode: Hard links share the same inode (a data structure that stores information about a file), meaning they point to the exact same data on the disk.   
Cannot Point to Directories: You cannot create hard links to directories.   
Cannot Cross Filesystems: Hard links must reside within the same filesystem.   
Deletion: Deleting the original file does not affect the hard link, as the data remains accessible through the link.   
Soft Links (Symbolic Links)

Definition: A soft link (or symbolic link) is a special file that contains the path to another file or directory. It's like a shortcut.   
Key Characteristics:
Different Inode: Soft links have their own inode and do not share the same inode as the target file.   
Can Point to Anything: Soft links can point to files, directories, or even other symbolic links, and they can cross filesystems.   
Deletion: If the original file is deleted, the soft link becomes "broken" (it points to a non-existent file).

Hard Links: Useful for creating multiple access points to a file within the same filesystem, especially for frequently accessed files.   
Soft Links: More flexible for creating shortcuts to files and directories across different locations, including other filesystems.

 3.What are the ping,telnet,curl and wget commands in linux?
 -ping: Checks network reachability.
telnet: Provides basic remote access (insecure).   
curl: Versatile tool for data transfer and interaction with web services.   
wget: Primarily for downloading files from the web.

   
4.What is a mount in linux and how do you create one?
-In Linux, mounting is the process of making a file system accessible within the operating system's directory structure. This allows you to interact with files and directories on external devices (like USB drives, network shares), partitions, or other file systems as if they were part of your local storage.   
How to Create a Mount

Identify the Device or File System:

Physical Devices: Often identified by device names like /dev/sda1, /dev/sdb, etc.
Network Shares: Specified by their network address or hostname.
ISO Images: Mounted as loop devices.   
Choose a Mount Point:

Select an empty directory where you want to mount the file system. This directory will become the entry point to access the mounted content.   
Use the mount Command:

The basic syntax is:

Bash

mount <device> <mount_point>
Example:

To mount a USB drive at /media/usb:

Bash

mount /dev/sdb1 /media/usb

Options:

-t <type>: Specify the file system type (e.g., ext4, ntfs, vfat).
-o <options>: Set mount options (e.g., ro for read-only, rw for read-write, user to allow ordinary users to mount).

5.What is an inode in linux?
5.What is an inode in linux?
In Linux, an inode is a fundamental data structure that stores metadata about a file or directory within a file system.

 It's essentially a unique identifier and a central repository of information for each file.   


6.How do you troubleshoot live logs in linux?
1. Identify the Relevant Log Files

System Logs:
/var/log/messages: General system messages.
/var/log/syslog: Another common location for system messages.
/var/log/kern.log: Kernel-related messages.
/var/log/auth.log: Authentication logs (login/logout attempts).
/var/log/daemon.log: Messages from system daemons.
/var/log/mail.log: Mail server logs.
/var/log/secure: Security-related messages.
Application Logs:
Application-specific log files are usually located in the application's configuration directory or a subdirectory within /var/log.
Check the application's documentation for the location of its log files.
2. Use the tail Command for Live Monitoring

Basic Syntax:
Bash

tail -f <log_file>
   This command displays the last part of the specified log file and continuously updates as new lines are appended.   

Example:
Bash

tail -f /var/log/messages
3. Filter and Search Logs

grep: Filter log messages based on keywords.   

Bash

tail -f /var/log/messages | grep "error" 
awk: Extract specific fields from log messages.   

Bash

tail -f /var/log/apache2/error.log | awk '{print $4}' 
less: View log files with pagination and search capabilities.   

Bash

less /var/log/messages
4. Log Management Tools

journalctl: A powerful tool for managing and querying systemd journal logs.   

Bash

journalctl -f -u <service_name> 
Log Management Systems: For larger environments, consider using centralized log management systems like ELK (Elasticsearch, Logstash, Kibana) or Splunk.

5. Tips for Effective Troubleshooting

Focus on Recent Entries: Use tail to focus on the most recent log entries.
Search for Specific Error Messages: Use grep to search for keywords related to the issue you're investigating.
Check Timestamps: Pay attention to timestamps to correlate log entries with events.
Consult Documentation: Refer to the documentation for the specific software or service you're troubleshooting.
Use Log Rotation: Configure log rotation to manage log file size and prevent them from consuming excessive disk space.   

7.What are nice and renice commands in linux?
-In Linux, the nice and renice commands are used to adjust the scheduling priority of processes, influencing how the Linux kernel allocates CPU time among them.

nice Command   

Purpose: Used to start a new process with a specific priority.   
Syntax: nice [-n <increment>] <command>
Example: nice -n 10 sleep 60
This starts the sleep 60 command with a niceness value of 10, lowering its priority.
renice Command

Purpose: Modifies the priority of a running process.   
Syntax: renice <increment> -p <process_id>
Example: renice 5 -p 1234
This increases the priority of the process with PID 1234 by 5.   
Niceness Values

Niceness values range from -20 (highest priority) to 19 (lowest priority).   
A higher nice value lowers the process's priority, meaning it will receive less CPU time.   
A lower (negative) nice value increases its priority, giving it more CPU time.   
Key Points

Only root or users with the CAP_SYS_NICE capability can lower the priority of processes below their own.
Modifying process priorities should be done with caution, as it can impact system stability and performance.

8.What are grep and egrep commands in linux?
grep

Purpose: Searches for lines containing a specified pattern in one or more files.   
Basic Syntax: grep [options] pattern [files]
Pattern Matching: Uses basic regular expressions.   
Example:
grep "error" /var/log/messages: Searches the /var/log/messages file for lines containing the word "error."
egrep

Purpose: Similar to grep, but uses extended regular expressions.
Basic Syntax: egrep [options] pattern [files]
Pattern Matching: Supports a wider range of metacharacters (like +, ?, |) without the need for escaping, making it more concise for complex patterns.
Note: egrep is essentially equivalent to grep -E.

9.What is awk command in linux?
awk is a powerful pattern scanning and text processing language in Linux. It's often used for:

Extracting data from files: Parsing log files, CSV files, and other structured text.
Data manipulation: Transforming data, performing calculations, and generating reports.
Filtering data: Selecting specific lines or fields based on conditions.
Basic Syntax:

Bash

awk 'pattern { action }' input_file
pattern:
Can be a regular expression, a comparison operator (e.g., ==, !=, >, <), or a boolean expression.
If no pattern is specified, the action is performed on every line.
action:
A set of commands to be executed when the pattern matches.
Often involves printing fields using print statements.
Fields:

awk divides each line into fields by default using whitespace as the delimiter.
Fields are numbered starting from 1.
You can access fields using $1, $2, $3, etc.
Example:

Bash

awk '{print $1}' /etc/passwd 
This command extracts the first field (username) from each line of the /etc/passwd file and prints it to the console.
Built-in Variables:

$0: The entire current line.
NF: The number of fields in the current line.
NR: The current record (line) number.
FILENAME: The name of the current input file.
Example with Conditions:

Bash

awk '$2 == "root" {print $1}' /etc/passwd
This command prints the username (first field) only for lines where the second field (user ID) is "root."

10.What is sed command in linux?
sed (Stream Editor) is a powerful command-line utility in Linux used to process and transform text within files. It works by reading input, applying a set of editing commands, and then writing the modified output.

Key Uses:

Search and Replace:
Find and replace specific strings within a file.
Use regular expressions for complex pattern matching.
Delete Lines:
Remove lines based on patterns or line numbers.
Insert Lines:
Add new lines before or after specific patterns.
Change Lines:
Modify existing lines by inserting, deleting, or substituting text.
Basic Syntax:

Bash

sed [options] 'command' input_file(s)
options:
-e: Specify multiple editing commands.
-n: Suppress automatic printing of lines.
-i: Edit the file in-place (modify the original file directly).
command:
The editing command to be applied. Common commands include:
s/pattern/replacement/: Substitute pattern with replacement.
d: Delete the current line.
a\: Append text after the current line.
i\: Insert text before the current line.
p: Print the current line.
Examples:

Replace "old" with "new" in a file:

Bash

sed 's/old/new/g' myfile.txt 
g: Replace all occurrences of "old" on each line.
Delete lines containing "error" from a log file:

Bash

sed '/error/d' logfile.txt
Insert a line before lines starting with "keyword":

Bash

sed '/^keyword/i\This line is inserted before keyword lines.' myfile.txt

11.How do you kill a process in linux?
1. Find the Process ID (PID)

ps aux | grep <process_name>: This command lists all running processes and filters them by the name of the process you want to kill.   

Example: ps aux | grep firefox
top: This interactive command allows you to view a list of running processes, their resource usage (CPU, memory), and kill them directly from within the top interface.

2. Kill the Process

kill <process_id>: This sends a SIGTERM signal to the process, requesting it to terminate gracefully.

Example: kill 1234 (replace 1234 with the actual PID)
kill -9 <process_id>: This sends a SIGKILL signal, which forces the process to terminate immediately without any cleanup. Use this with caution as it can result in data loss.

Example: kill -9 1234
3. Alternative: pkill Command

pkill <process_name>: This command kills all processes matching the given name.
Example: pkill firefox

12.What is unmask in linux?
In Linux, umask (user file creation mask) is a command that controls the default permissions for newly created files and directories.

How it Works:

Permission Masking: The umask value represents a set of permissions that are not granted to new files and directories.
Octal Notation: umask values are typically expressed in octal notation (base-8). Each digit represents permissions for the owner, group, and others:
First digit: Owner permissions
Second digit: Group permissions
Third digit: Other users' permissions   
  
Permission Bits:
4: Read permission
2: Write permission   
1: Execute permission
Example:

umask 022:
Subtracts write permission from the group and others.
A file created with this umask would have permissions like -rw-r--r-- (owner can read/write, group and others can only read).
Setting the Umask:

Temporarily: umask 022 (sets the umask for the current session)
Permanently: Add the umask command to your shell's configuration files (e.g., .bashrc, .profile) to set it for each login.
Key Points:

umask is a security measure to restrict default permissions and prevent accidental sharing of files.
The umask value can be customized to suit your specific security needs.
Understanding umask is crucial for managing file permissions effectively in a Linux environment.

13.What is the prupose of export command in linux?
In Linux, the export command is used to mark variables and functions to be passed to child processes.

Here's a breakdown:

Environment Variables: When you set a variable using export, it becomes an environment variable. This means that the variable and its value are made available not only in the current shell session but also to any processes that are started from that session.   

Child Processes: Child processes are processes that are created by the current process. For example, if you run a script or execute another program from your current shell, that program becomes a child process.

Sharing Information: export allows you to share information between the parent process (your current shell) and its child processes. This is crucial for various reasons:

Configuration: You can set environment variables that configure how child processes behave. For example, you might export the PATH variable to specify where child processes should look for executable files.   
Script Parameters: You can pass values to scripts or programs through exported variables.
Consistent Settings: Ensure that child processes inherit specific settings or configurations.
Example:

Bash

export MY_VARIABLE="hello"
This command sets the MY_VARIABLE to "hello" and makes it available to any child processes started from the current shell.

Key Points:

export only affects child processes. It does not modify the environment of other running processes.   
To make exported variables persistent across sessions, you can add the export command to your shell's configuration files (e.g., .bashrc, .profile).

14. What is nohup command in linux?
In Linux, nohup is a command that allows you to run a command or script in the background and have it continue to run even after you log out or close the terminal.

15.How can you chcek the running ports in a linux machine?
1. Using netstat

Basic Syntax:

Bash

sudo netstat -tulpn | grep LISTEN
Explanation:

sudo: Executes the command with root privileges (required for some systems).
netstat: Displays network connections and routing tables.
-t: Show TCP connections.
-u: Show UDP connections.
-l: Show only listening ports.
-p: Display the PID (Process ID) of the process using the port.
-n: Display numerical addresses instead of resolving hostnames.
| grep LISTEN: Filters the output to show only lines containing "LISTEN," indicating listening ports.
2. Using ss (Socket Statistics)

Basic Syntax:

Bash

sudo ss -tulpn | grep LISTEN
Explanation:

ss: A newer command that provides more detailed socket information.
Options are similar to netstat, providing information about TCP, UDP, and listening ports.
3. Using lsof (List Open Files)
Bash

sudo lsof -i -P -n | grep LISTEN

16.How can you list only directories in linux?
1. Using ls

ls -d */
This is the most concise way.
-d: Tells ls to list directory entries themselves, not their contents.
*/: Matches only directories (the trailing / is crucial).
2. Using ls with grep

ls -l | grep "^d"
ls -l: Lists files in long format, including file type information.
grep "^d": Filters the output to show only lines that start with "d" (indicating a directory).
3. Using find

find . -type d
find .: Starts searching from the current directory (.).
-type d: Specifies that only directories should be found.
Example:

Let's say you want to list all directories in the current directory:

ls -d */ This will directly list the names of all directories in the current directory.




17.What is the purpose of export command in linux?
In Linux, the export command is crucial for managing environment variables and ensuring that they are accessible to child processes. Here's a breakdown of its purpose:

18.How do you send error logs and stdout logs to dfferent files in linux?
1. Using &> and 2>&1

&>: This operator redirects both standard output (stdout) and standard error (stderr) to the same file.

2>&1: This operator redirects stderr to stdout.

Example:

Bash

my_command &> output.log 
This command runs my_command and redirects both its standard output and standard error to the file output.log.

Bash

my_command > output.log 2> error.log
This command redirects standard output to output.log and standard error to error.log.

2. Using tee

tee reads from standard input and writes it to both standard output and a file simultaneously.
Example:

Bash

my_command | tee output.log > error.log
This command runs my_command, pipes its output to tee, which writes the output to both output.log and standard output. The > error.log then redirects the output (which now includes both stdout and stderr) to error.log.

3. Using nohup

nohup is often used to run commands in the background and prevent them from being terminated when you log out.
Example:

Bash

nohup my_command > output.log 2>&1 &
This command runs my_command in the background, redirects both stdout and stderr to output.log, and continues running even after you log out.

Explanation:

stdout: The standard output stream is typically used for displaying normal program output.
stderr: The standard error stream is used for displaying error messages.

19.What does the netstat command in linux do?
The netstat command in Linux is a powerful tool for displaying network connections, routing tables, and interface statistics.

Key Functions:

Displaying Network Connections:
Shows active TCP and UDP connections, including their states (ESTABLISHED, LISTEN, CLOSE_WAIT, etc.).   
Provides information about the local and remote addresses and ports involved in each connection.   
Identifying Listening Ports:
Reveals which ports on the system are currently listening for incoming connections.   
Examining Routing Tables:
Displays the routing table, showing how network traffic is directed to different destinations.   
Gathering Interface Statistics:
Provides information about network interfaces, such as the number of packets sent and received, bytes transmitted and received, and error counts.   
Common Uses:

Troubleshooting Network Problems: By examining network connections and listening ports, you can identify potential issues like blocked ports, connection failures, or unexpected connections.   
Monitoring Network Activity: netstat can help you monitor network traffic and identify potential security threats or performance bottlenecks.
Checking Server Status: You can use netstat to verify if a server is listening on the expected ports.
Basic Syntax:

Bash

netstat [options] 
Common Options:

-t: Display TCP connections.
-u: Display UDP connections.
-l: Show only listening ports.
-p: Display the process ID (PID) of the process using the port.
-n: Display numerical addresses instead of resolving hostnames.
-r: Display routing table information.
-i: Display interface statistics.
Example:

Bash

sudo netstat -tulpn | grep LISTEN 
This command displays a list of listening TCP and UDP ports along with the PIDs of the processes using them.

20.How do you run script at boot level in linux?
1. Using rc.local

Applicable to: Older Linux distributions and some modern ones.
Process:
Create/Edit: Create or edit the /etc/rc.local file using a text editor with root privileges (e.g., sudo nano /etc/rc.local).
Add Script: Add a line to the end of the file to execute your script. For example:
Bash

/path/to/your/script.sh
Save and Reboot: Save the file and reboot your system.
2. Using systemd (Modern Distributions)

Applicable to: Most modern Linux distributions (e.g., Ubuntu, Debian, Fedora, CentOS/RHEL).
Process:
Create a Systemd Unit File: Create a unit file (usually with a .service extension) in the /etc/systemd/system/ directory.
Example: /etc/systemd/system/my_script.service
Unit File Content:
[Unit]
Description=My Custom Script
After=network.target 

[Service]
ExecStart=/path/to/your/script.sh
User=root 
Group=root 

[Install]
WantedBy=multi-user.target
Enable and Start:
Enable the service: sudo systemctl enable my_script.service
Start the service: sudo systemctl start my_script.service
Verify: Check the service status: sudo systemctl status my_script.service
3. Using cron (For Scheduled Tasks)

Use Case: If you want to run the script at specific intervals (e.g., daily, weekly), you can use cron.
Process:
Edit Crontab: Edit the root crontab: sudo crontab -e
Add a Line: Add a line like this to schedule the script to run at boot:
@reboot /path/to/your/script.sh
Important Notes:

Permissions: Ensure your script is executable (chmod +x /path/to/your/script.sh).
Testing: Always test your script thoroughly before enabling it at boot.
Systemd is Preferred: In modern Linux distributions, systemd is generally the preferred method for managing system services.
Choosing the Right Method:

rc.local: Simple for basic scripts, but less flexible and less suitable for complex scenarios.
systemd: More powerful and flexible, recommended for most cases.   
cron: Suitable if you need to schedule the script to run at specific times or intervals, not just at boot.   

21.How do you chcek the cpu utilisation in linux?
1. top command

Most versatile: Provides a real-time, dynamic view of system resource usage, including CPU utilization.   

Key features:

Displays a continuously updated list of processes sorted by CPU usage.   
Shows overall CPU usage at the top of the screen.   
Interactive: Allows you to sort processes by different criteria, kill processes, and change update intervals.   
Example:

Bash

top
2. mpstat command

Focused on CPU statistics: Provides detailed CPU statistics, including utilization by core, user time, system time, idle time, and more.   
Example:
mpstat 1 5 (displays CPU statistics every 1 second for 5 iterations)
3. vmstat command   

Provides a snapshot of system activity: Includes CPU utilization, memory usage, disk I/O, and more.   
Example:
vmstat 1 5 (displays system statistics every 1 second for 5 iterations)
4. htop command

Enhanced top: An interactive process viewer with a more user-friendly interface, often considered an improvement over the standard top command.
5. sar command

System Activity Reporter: Collects and reports system activity data, including CPU utilization, memory usage, I/O, and network traffic.
sar -u ALL (displays CPU utilization statistics)
  
6. iostat command

Focuses on I/O statistics: Provides information about disk and CPU utilization, but the primary focus is on I/O activity.   
Tips for Checking CPU Utilization:

Observe Trends: Monitor CPU usage over time to identify potential bottlenecks or performance issues.   
Identify Resource-Intensive Processes: Use top or htop to identify processes that are consuming a significant amount of CPU resources.
Consider System Load: The system load average provides a measure of overall system activity and can be helpful in assessing CPU utilization.   

21.How can you chcek the sttaus of services in linux ?
1. Using systemctl

Most common method: Systemd is the default init system in most modern Linux distributions.   

Command:

Bash

sudo systemctl status <service_name>
Replace <service_name> with the actual name of the service (e.g., nginx, apache2, ssh, postgresql).

Output: Provides detailed information about the service's status, including whether it's running, stopped, or disabled.   

2. Using service (Older Systems)   

For older init systems: Some older systems might still use the service command.

Command:

Bash

sudo service <service_name> status
Note: The syntax and availability of the service command can vary between distributions.

3. Using chkconfig (Older Systems)   

For checking service startup configuration: This command checks if a service is set to start automatically at boot time.   
Command:
Bash

sudo chkconfig <service_name> --list
4. Using ps (To Check if a Process is Running)   

Identify the process associated with the service: Find the process ID (PID) of the service.   
Command:
Bash

ps aux | grep <service_name> 
If the process is running, it will be listed in the output.
Example

To check the status of the Apache web server:

Bash

sudo systemctl status apache2
This command will provide detailed information about the Apache service, including its current state (running, stopped, etc.).   

Remember:

Root privileges: You often need root privileges (using sudo) to check the status of system services.
Service names: The exact names of services may vary depending on the Linux distribution and the specific software installed.

22.How can you change the file permissions in linux?
You can change file permissions in Linux using the chmod command. Here's how:

1. Symbolic Mode

Syntax: chmod [ugoa][+-=][rwxX] file_or_directory

u: User (owner)   
g: Group   
o: Others   
a: All (user, group, and others)   
+: Add permissions   
-: Remove permissions   
=: Set permissions explicitly   
r: Read permission   
w: Write permission   
x: Execute permission   
X: Execute permission only if the file is a directory or already executable
Examples:

chmod u+x my_script.sh: Add execute permission for the owner of my_script.sh.
chmod go-r my_file.txt: Remove read permission for group and others from my_file.txt.
chmod a+rwX my_directory: Add read, write, and execute permissions for all users to my_directory.
2. Absolute Mode (Octal Notation)

Syntax: chmod [nnn] file_or_directory

nnn: A three-digit octal number representing permissions for user, group, and others.
Each digit represents permissions for one category:
4: Read permission   
2: Write permission   
1: Execute permission   
  
Examples:

chmod 755 my_file.txt:

Owner: Read, write, execute (7)
Group: Read and execute (5)
Others: Read and execute (5)
chmod 644 my_file.txt:

Owner: Read and write (6)   
Group: Read (4)   
Others: Read (4)   
Important Notes:

Root Privileges: You may need root privileges (using sudo) to change file permissions for files that you don't own.
Security: File permissions are crucial for system security. Be careful when changing file permissions to avoid unintended security risks.

23.How do you allow ports in linux?
1. Identify and Choose a Firewall

UFW (Uncomplicated Firewall): User-friendly, command-line interface. Popular on Ubuntu and other Debian-based systems.   
Firewalld: More advanced, offers graphical configuration options. Common on Fedora, CentOS, and RHEL.   
iptables: Powerful but more complex command-line tool. Provides fine-grained control over firewall rules.   
2. Open the Port (UFW Example)

Open a Single Port:

Bash

sudo ufw allow <port_number>/<protocol> 
Replace <port_number> with the port you want to open (e.g., 80 for HTTP, 22 for SSH).

Replace <protocol> with tcp or udp.

Example: sudo ufw allow 80/tcp (opens port 80 for TCP connections)

Open a Range of Ports:

Bash

sudo ufw allow <start_port>-<end_port>/<protocol>
Example: sudo ufw allow 22-25/tcp (opens ports 22 to 25 for TCP connections)
Allow Connections from a Specific IP Address:

Bash

sudo ufw allow from <ip_address> to any port <port_number>
Example: sudo ufw allow from 192.168.1.100 to any port 22 (allows connections to port 22 only from the IP address 192.168.1.100)
3. Make Changes Persistent

UFW:

Bash

sudo ufw enable 
Firewalld:

Bash

sudo firewall-cmd --permanent --add-port=<port_number>/<protocol> 
sudo firewall-cmd --reload
4. Verify the Changes

UFW:

Bash

sudo ufw status 
Firewalld:

Bash

sudo firewall-cmd --list-all 

24.What are the differences b/w top and htop commands in linux?
The top and htop commands are both used to monitor system resource usage in Linux, but they have some key differences:

top

Basic: A standard, text-based command that provides a real-time view of system processes.   
Interface:
Plain text output.
Uses bold text to highlight information.
No mouse support.
Limited scrolling capabilities.
Features:
Shows a list of processes sorted by CPU usage.   
Displays overall system statistics (CPU, memory, load average).   
Allows you to sort processes by different criteria (CPU, memory, etc.).   
Provides commands to interact with processes (kill, rename, etc.).   
htop

Enhanced: An interactive process viewer with a more user-friendly interface.   
Interface:
Color-coded display for better readability.   
Supports mouse interaction for navigation and process selection.   
Allows scrolling both horizontally and vertically.
Provides a tree view to visualize the process hierarchy.   
Features:
All the features of top.
Easier navigation and process selection.   
Customizable display options.   
Supports filtering and searching processes.   
Provides a more intuitive interface for interacting with processes

25.1. What are the main networking tools in Linux?

ifconfig: Used to configure and display network interfaces. Deprecated, but still widely used.
ip: More modern tool for networking configuration (replaces ifconfig).
netstat: Displays network connections, routing tables, and interface statistics. Deprecated, replaced by ss in most cases.
ss: Utility to investigate sockets, often faster and more efficient than netstat.
ping: Tests connectivity to another system by sending ICMP packets.
traceroute: Traces the route packets take to reach a destination.
nslookup: Query DNS servers for information about domain names.
dig: A more advanced DNS query tool than nslookup.
nmap: Network exploration tool and security scanner.
iptables: Tool for managing firewall rules.
tcpdump: Network packet analyzer.
route: Used to view and manipulate the IP routing table.
hostname: Displays or sets the system’s hostname.


2. What are iptables chains and how do they work?

Answer: iptables uses different chains to process network packets. The three default chains are:
INPUT: For incoming network traffic to the system.
OUTPUT: For outgoing network traffic from the system.
FORWARD: For packets that are routed through the system (not intended for the system itself but forwarded to another destination).

3. What are the common network troubleshooting commands in Linux?

ping: Tests the connectivity to a host.
traceroute: Traces the route packets take to a network host.
netstat or ss: Shows active network connections and listening ports.
curl: Tests network services, e.g., HTTP requests.
dig or nslookup: Queries DNS records.
tcpdump: Captures network packets to analyze network traffic

4. What is the purpose of systemctl in Linux?

Start a service: sudo systemctl start <service>
Stop a service: sudo systemctl stop <service>
Enable a service to start at boot: sudo systemctl enable <service>
Check the status of a service: sudo systemctl status <service>
Reload systemd configuration: sudo systemctl daemon-reload

5. How do you configure a static IP on a RedHat-based system (e.g., CentOS)?

For a static IP configuration, you need to modify the interface configuration file in /etc/sysconfig/network-scripts/ifcfg-<interface>.

6. What is a network bridge in Linux?

sudo brctl addbr br0 
sudo brctl addif br0 eth0 
sudo ip addr add IP dev br0 
sudo ip linkset br0 up

7. How do you restart networking services on a Linux system?

sudo systemctl restart networking
sudo systemctl restart network
sudo systemctl restart NetworkManager

📍 Register here for Free Linux MasterClass https://lnkd.in/gMEA9PhC

📍 Checkout the Free DevOps Projects 
https://lnkd.in/gkB27ZDF


ls -R:list all files in sub-directories as well.
ls -a:shows hidden files
ls -al:lists files and directories with detailed info
find / -name filename: finds a file or a directory by its nam
file filename:determines the file type
less filename: views the file content page by page
head filename: views the last ten lines of a file
tail filename: views the last ten lines 
du -h --max-depth=1 shows the size of each dir

cp -r source directory:copies dir recursively
mov oldir newdir: renames directory
find / -type -d -name directoryname: finds a directory starting from root
pkills name: kills the process with the given name
bg: resumes suspeneded jobs without bringing them to foreground
fg: Brings the most recent job to foreground.
1>filename: redirects the std output to file
2>filename: redirect stderr to file 

chown owner filename:chnage file owner
chgrp groupname filename: Change group owner

ping host: Ping a host and outputs result
netstat -pnltu: displays various n/w related info
ssh user@host: Remoteb login into the host as user
wget: donwload files from the web
curl url: sends a equest to a url and returns the response

tar cf file.tar files: Create a tar named file.tar containing files.
tar xf file.tar: extract the files from file.tar
gzip file:Compreses file and renames it to file.gz
gzip -d file.gz: Decompresses file.gz back to file
zip -r file.zip files: Create a zip archieve named file.ip
unzip file.zip: extract the contents of a zip file

grep pattern files: Search for pattern in files
grep -r pattern dir: Search recursively for pattern in directory
echo 'text':Prints text
di file1 file2: compares two files
wc filename: Count,lines,words,and characters in a file

df: shows disk usage
du:shows directory usage space
free: shows memory and swap usage
utpime: current uptime
uname -a:shows kernel info

locate filename: find a file by its name
tar -xvf archieve.tar: Extract a tar file

port 22: ssh
port 80:http
port 443: https
port 3000: Grafana
port 3100: Loki
port 9090: Elasticsearch
port 9100: Node exporter
port 53: DNS
port 9090: Prometheus
port 25: SMTP
Port 5601: Kibana
port 3306: mysql
port 6379: Redis
port 8080: tomcat
port 5432: postgresql

1. **Explain the Linux boot process.** 

 The BIOS loads the bootloader (like GRUB), which loads the kernel. The kernel initializes hardware, mounts the root filesystem, and starts `init` or `systemd`, loading system services and setting the default runlevel or target.

2. **How would you troubleshoot a slow server?** 

 Check system resources (`top`, `vmstat`, `free`) for CPU, memory, or I/O issues. Review disk usage (`df`, `du`) and network traffic (`netstat`, `ss`). Identify resource-heavy processes and adjust configurations, terminate processes, or consider hardware upgrades.

3. **Describe Linux file permissions and how to change them.** 

 Permissions include read, write, and execute for the owner, group, and others. Use `chmod` to modify permissions (e.g., `chmod 755 filename`), `chown` to change ownership, and `chgrp` to change the group.

4. **What is LVM, and how do you manage it?** 

 LVM (Logical Volume Manager) enables flexible disk management across physical volumes. Commands include `pvcreate` (create physical volume), `vgcreate` (create volume group), `lvcreate` (create logical volume), and `lvextend`/`lvreduce` for resizing.

5. **How do you secure a Linux server?** 

 Disable unnecessary services, configure `iptables`/`firewalld`, enforce SSH security (disable root login, use SSH keys), enable SELinux/AppArmor, apply patches, monitor logs, and use Fail2ban for brute-force prevention.

6. **How do you manage services in Linux?** 

 Use `systemctl` for `systemd` services (`systemctl start service`, `systemctl enable service`). On older systems, use `service` or `init.d` scripts.

7. **How do you add a user and manage permissions?** 

 Use `useradd username` and `passwd username` to add users. Add users to groups with `usermod -aG groupname username`. Adjust file permissions with `chmod` and `chown`.

8. **How do you monitor server performance?** 

 Use `top` or `htop` for real-time monitoring, `sar` for historical data, `iostat` for I/O stats, and `netstat` or `ss` for network connections. Monitor load average, keeping it below the number of CPU cores.

9. **What steps would you take for filesystem corruption recovery?** 

 Boot into single-user mode or use a live CD, run `fsck` to repair, and restore from backups if needed. Regular backups are essential for data protection.

10. **How do you automate tasks in Linux?** 

 Use `cron` for scheduled tasks (`crontab -e`). For complex automation, use shell scripts and tools like `Ansible` or `Puppet` for consistent deployments across servers.

