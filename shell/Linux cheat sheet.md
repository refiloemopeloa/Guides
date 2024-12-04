# Terminal Cheat Sheet

## File and Directory Operations

### List files and directories

```bash
ls -options
```

#### options

-   `-l` : long format listing
-   `-a` : include hidden files
-   `-h` : human readable file sizes

---

### Change directory

```bash
cd path/to/directory
```

---

### Print working directory

```bash
pwd
```

---

### Make directory

```bash
mkdir directory
```

---

### Remove files and directories

```bash
rm -options file
```

#### options

-   `-r` : remove directories recursively
-   `-f` : force remove without confirmation

---

### Copy files and directories

```bash
cp -options source_file destination
```

#### options

-   `-r` : copies directories recursively

---

### Move or rename files and directories

```bash
mv old new
```

if `old` directory == `new` directory: rename

---

### Create new file or update file timestamp

```bash
touch file
```

---

### View contents of a file

```bash
cat file
```

---

### Display the first few lines of a file

```bash
head -options file
```

#### options

-   `-n` : specify number of lines to display

---

### Display the last few lines of a file

```bash
tail -options file
```

#### options

-   `-n` : specify number of lines to display

---

### Create links between files

```bash
ln -options source_file link_name
```

#### options

-   `-s` : create soft link. think windows shortcut

---

### Search for files and directories

```bash
find directory -options file
```

#### options

-   `-name` : search by filename
-   `-type` : search by file type

## File Permissions

### Change file permissions

```bash
chmod options file
```

#### options

-   `u` : user
-   `g` : group
-   `o` : other
-   `+` : add permissions
-   `-` : remove permissions
-   `=` : set permissions explicitly

## File compression

### Create or extract archive files

```bash
tar -options file
```

#### options

-   `-c` : Create a new archive
-   `-x` : Extract files from an archive
-   `-f` : Specify the archive file name
-   `-v` : Verbose mode
-   `-z` : Compress the archive with gzip
-   `-j` : Compress the archive with bzip2

---

### Compress files

```bash
gzip -options file
```

#### options

-   `-d` : Decompress files.

---

### Create zip files

```bash
zip -options destination [files]
```

#### options

-   `-r` : Recursively include directories.

## Grep

Grep is its own command and has a separate file dedicated to it. You can check out this [grep](https://www.geeksforgeeks.org/grep-command-in-unixlinux/) guide on [GeeksForGeeks](https://www.geeksforgeeks.org/).

## Network commands

### Download files from the web

```bash
wget url
```

---

### Transfer data to or from a server

```bash
curl url
```

## IO Redirection

### Send file contents to command as input

```bash
command < file
```

---

### Send command output (`stdout`) to file

```bash
command > file
```

---

### Send command2 output (`stdout`) to command1 input

```bash
command1 < (command2)
```

---

### Send every command output (`stdout`) to file

```bash
command &> file
```

---

### Appends command output (`stdout`) to file

```bash
command >> file
```

---

## Processes

### View running processes

```shell
ps -e
```

### Kill a process

```shell
kill -9 pid
```

You get the `pid` of a process from the command above.
# References

1. [Linux Commands Cheat Sheet: Beginner to Advanced (geeksforgeeks.org)](https://www.geeksforgeeks.org/linux-commands-cheat-sheet/)
2. 