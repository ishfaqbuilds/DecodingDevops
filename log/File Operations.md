### Linux File Operations Note

#### Core Concept: Everything is a File  
In Linux, everything is treated as a file, text files, directories, hardware devices, even processes. This simplifies how the system interacts with resources.

---

#### File Types

| Symbol | Type            | Description                                |
|--------|-----------------|--------------------------------------------|
| -      | Regular file    | Text, binary, or executable files          |
| d      | Directory       | Folders containing other files             |
| l      | Symbolic link   | Pointer/shortcut to another file           |
| c      | Character device| Streaming devices (keyboard, terminal)     |
| b      | Block device    | Storage devices (hard disk, SSD)           |
| s      | Socket          | Network communication endpoints            |
| p      | Named pipe      | Inter-process communication                |

View file types: `ls -l` (first character shows type)

---

#### Directory Operations

| Command | Purpose | Example |
|---------|---------|---------|
| mkdir <dir> | Create single directory | mkdir projects |
| mkdir -p <path> | Create nested directories | mkdir -p a/b/c/d |
| rmdir <dir> | Remove empty directory | rmdir empty_folder |
| rm -r <dir> | Remove directory and contents | rm -rf practice/ |

---

#### File Operations

| Command | Purpose | Key Options |
|---------|---------|-------------|
| touch <file> | Create empty file or update timestamp | touch file{1..5}.txt |
| cp <src> <dest> | Copy files | -r for directories, -i interactive |
| mv <src> <dest> | Move or rename | No -r needed for directories |
| rm <file> | Remove files | -r recursive, -f force, DANGEROUS |
| cat <file> | Display file contents | Concatenates multiple files |

---

#### Links (Shortcuts)

| Command | Purpose |
|---------|---------|
| ln -s <target> <linkname> | Create symbolic (soft) link |
| rm <link> or unlink <link> | Remove link (target stays intact) |

Dead link: Link pointing to moved/deleted target.

---

#### Listing and Sorting

| Command | Result |
|---------|--------|
| ls | Basic list |
| ls -l | Long format with permissions, size, date |
| ls -la | Include hidden files (dotfiles) |
| ls -lt | Sort by time, newest first |
| ls -ltr | Sort by time, reverse (oldest first) |
| ls -lh | Human-readable sizes (KB, MB, GB) |

---

#### Wildcards (Pattern Matching)

| Pattern | Matches | Example |
|---------|---------|---------|
| * | Any characters | *.txt → all .txt files |
| ? | Single character | file?.txt → file1.txt, fileA.txt |
| {a,b,c} | Brace expansion | file{1..5}.txt → file1.txt to file5.txt |
| [abc] | Any character in brackets | file[0-9].txt → file0.txt to file9.txt |

---

#### Quick Reference

##### Create structure
```
mkdir -p practice/{projects/{web,api},archive,logs}
```
##### Create files
```
touch practice/projects/web/{index.html,style.css,app.js}
```
##### Copy with wildcard
```
cp practice/logs/access-log-*.txt practice/archive/
```
##### Move directory
```
mv practice/projects/web/app.js practice/projects/api/
```
##### Safe removal workflow
```
pwd && ls          # Verify location and targets
rm -rf practice/   # Then delete
```
