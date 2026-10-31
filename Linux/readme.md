# Linux Terminal Cheat Sheet

Essential Linux commands for everyday terminal use (Bash / Ubuntu).

## File Management & Navigation

-   `pwd` --- Show the current directory.
-   `ls` --- List files and directories.
-   `ls -la` --- List all files, including hidden files, with details.
-   `cd <directory>` --- Change directory.
-   `cd ..` --- Move one directory up.
-   `cd ~` --- Go to the home directory.
-   `mkdir <directory>` --- Create a directory.
-   `mkdir -p <path>` --- Create nested directories.
-   `touch <file>` --- Create an empty file.
-   `cp <source> <destination>` --- Copy a file.
-   `cp -r <source> <destination>` --- Copy a directory.
-   `mv <source> <destination>` --- Move or rename files.
-   `rm <file>` / `rm -r <directory>` --- Remove files or directories.
-   `find <path> -name "<pattern>"` --- Search for files by name.
-   `locate <filename>` --- Search indexed file locations.
-   `file <filename>` --- Identify a file type.

## Text Manipulation

-   `cat <file>` --- Display file contents.
-   `less <file>` --- View a file page by page (`q` to quit).
-   `nano <file>` / `vim <file>` --- Edit a file in the terminal.
-   `grep "<pattern>" <file>` --- Search text inside a file.
-   `grep -r "<pattern>" <directory>` --- Search recursively.
-   `head <file>` --- Show the first 10 lines.
-   `tail <file>` --- Show the last 10 lines.
-   `tail -f <file>` --- Follow a file as it updates.
-   `wc -l <file>` --- Count lines.
-   `sort <file>` --- Sort lines.
-   `diff <file1> <file2>` --- Compare two files.
-   `awk '{print $1}' <file>` --- Print the first field.
-   `sed 's/old/new/g' <file>` --- Replace text in command output.

## System Monitoring

-   `uname -a` --- Show system and kernel information.
-   `whoami` --- Show the current username.
-   `uptime` --- Show system uptime.
-   `top` / `htop` --- Monitor running processes.
-   `ps aux` --- List running processes.
-   `kill <PID>` --- Terminate a process.
-   `kill -9 <PID>` --- Forcefully terminate a process.
-   `free -h` --- Check RAM and swap usage.
-   `df -h` --- Check disk space.
-   `du -sh <directory>` --- Show directory size.
-   `lscpu` --- Display CPU information.
-   `lsblk` --- List storage devices and partitions.

## Process & Job Control

-   `jobs` --- List background and suspended jobs.
-   `bg` --- Resume a suspended job in the background.
-   `fg` --- Bring a job to the foreground.
-   `pgrep <name>` --- Find a process by name.
-   `pkill <name>` --- Terminate processes by name.
-   `nohup <command> &` --- Run a command that can continue after
    logout.

## Networking

-   `ping <hostname>` --- Test network connectivity.
-   `curl <URL>` --- Transfer data from or to a URL.
-   `wget <URL>` --- Download a file.
-   `ip addr` --- Show network interfaces and IP addresses.
-   `ip route` --- Show the routing table.
-   `ss -tuln` --- Show listening network ports.
-   `nslookup <domain>` / `dig <domain>` --- Look up DNS information.
-   `ssh user@host` --- Connect to a remote machine.
-   `scp <source> user@host:<path>` --- Securely copy files to a remote
    machine.

## File Permissions

-   `ls -l` --- View file permissions and ownership.
-   `chmod <permissions> <file>` --- Change file permissions.
-   `chmod +x <file>` --- Make a file executable.
-   `chmod 755 <file>` --- Owner: full access; others: read and execute.
-   `chmod 644 <file>` --- Owner: read/write; others: read-only.
-   `chown <user>:<group> <file>` --- Change file owner and group.
-   `sudo <command>` --- Run a command with elevated privileges.

**Permission values:** `r` = read (4), `w` = write (2), `x` = execute
(1).\
`755` = `rwxr-xr-x` · `644` = `rw-r--r--`

## Package Management (Ubuntu / Debian)

-   `sudo apt update` --- Refresh package lists.
-   `sudo apt upgrade` --- Upgrade installed packages.
-   `sudo apt install <package>` --- Install a package.
-   `sudo apt remove <package>` --- Remove a package.
-   `sudo apt purge <package>` --- Remove a package and its
    configuration.
-   `sudo apt autoremove` --- Remove unused dependencies.
-   `apt search <package>` --- Search for packages.
-   `apt show <package>` --- Show package information.
-   `dpkg -l` --- List installed packages.

## Compression & Archives

-   `tar -czvf archive.tar.gz <files>` --- Create a compressed TAR
    archive.
-   `tar -xzvf archive.tar.gz` --- Extract a TAR.GZ archive.
-   `tar -tzf archive.tar.gz` --- List archive contents.
-   `zip archive.zip <files>` --- Create a ZIP archive.
-   `unzip archive.zip` --- Extract a ZIP archive.
-   `gzip <file>` / `gunzip <file.gz>` --- Compress / decompress a file.

## Pipes, Redirection & Utilities

-   `>` --- Redirect output to a file (overwrite).
-   `>>` --- Append output to a file.
-   `<` --- Read input from a file.
-   `|` --- Pass output from one command to another.
-   `2>` --- Redirect error output.
-   `echo <text>` --- Print text.
-   `clear` --- Clear the terminal screen.
-   `man <command>` --- Open the command manual.
-   `history` --- Show previously executed commands.
-   `alias ll='ls -lah'` --- Create a command shortcut.
-   `unalias ll` --- Remove an alias.
-   `env` --- Display environment variables.
-   `export NAME=value` --- Set an environment variable.
-   `which <command>` --- Show the executable's location.

## Task Scheduling

-   `crontab -l` --- List scheduled cron jobs.
-   `crontab -e` --- Edit scheduled cron jobs.
-   `crontab -r` --- Remove the current user's cron jobs.
-   `at <time>` --- Schedule a one-time task (if installed and enabled).

## Useful Examples

``` bash
# Find all text files under the current directory
find . -name "*.txt"

# Search for a word in files recursively
grep -Rni "keyword" .

# Check disk space and memory
df -h
free -h

# Find a running process
pgrep -a firefox

# Make and run a script
chmod +x script.sh
./script.sh

# Update packages
sudo apt update && sudo apt upgrade
```

## Terminal Shortcuts

### Cursor Movement & Navigation

-   `Ctrl + A` --- Move to the beginning of the line.
-   `Ctrl + E` --- Move to the end of the line.
-   `Alt + B` --- Move backward one word.
-   `Alt + F` --- Move forward one word.
-   `Home` / `End` --- Move to the beginning / end of the line.
-   `Tab` --- Autocomplete commands, filenames, and paths.
-   `Tab` twice --- Show available completions.

### Editing & Deleting

-   `Ctrl + U` --- Delete from the cursor to the beginning of the line.
-   `Ctrl + K` --- Delete from the cursor to the end of the line.
-   `Ctrl + W` --- Delete the word before the cursor.
-   `Alt + D` --- Delete the word after the cursor.
-   `Ctrl + H` --- Delete the character before the cursor.
-   `Ctrl + D` --- Delete the character under the cursor; on an empty
    prompt, send EOF.
-   `Ctrl + T` --- Swap the two characters before the cursor.
-   `Ctrl + Y` --- Paste the text most recently removed with a Readline
    shortcut.

### History & Process Control

-   `Up Arrow` / `Down Arrow` --- Browse command history.
-   `Ctrl + R` --- Search command history.
-   `!!` --- Run the previous command again.
-   `!$` --- Reuse the last argument of the previous command.
-   `Ctrl + L` --- Clear the terminal screen.
-   `Ctrl + C` --- Interrupt the running command.
-   `Ctrl + Z` --- Suspend the foreground process.
-   `Ctrl + D` --- Send EOF; may exit the shell if the prompt is empty.

> **Notes:** Shortcuts can vary by shell and terminal. Be careful with
> `rm -r`, especially `rm -rf`, and always check the target path before
> deleting files. Prefer `kill <PID>` before using `kill -9 <PID>`.
