
### Linux File Operations Note
**Core Concept: Everything is a File**  
In Linux, everything is treated as a file—text files, directories, hardware devices, even processes. This simplifies how the system interacts with resources.
---
### File Types
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
### Identifying File Contents
```bash
file <path>          # Reveals actual file type regardless of extension
```
Examples:
    file /bin/pwd → ELF 64-bit LSB executable
    file script.sh → Bourne-Again shell script, ASCII text executable
### Directory Operations
| Command | Purpose | Example |
|---------|---------|---------|
| mkdir <dir> | Create single directory | mkdir projects |
| mkdir -p <path> | Create nested directories | mkdir -p a/b/c/d |
| rmdir <dir> | Remove empty directory | rmdir empty_folder |
| rm -r <dir> | Remove directory and contents | rm -rf practice/ |

### File Operations
| Command | Purpose | Key Options |
|---------|---------|-------------|
| touch <file> | Create empty file or update timestamp | touch file{1..5}.txt |
| cp <src> <dest> | Copy files | -r for directories, -i interactive |
| mv <src> <dest> | Move or rename | No -r needed for directories |
| rm <file> | Remove files | -r recursive, -f force, DANGEROUS |
| cat <file> | Display file contents | Concatenates multiple files |

### Links (Shortcuts)
| Command | Purpose |
|---------|---------|
| ln -s <target> <linkname> | Create symbolic (soft) link |
| rm <link> or unlink <link> | Remove link (target stays intact) |
Dead link: Link pointing to moved/deleted target.

### Listing and Sorting
| Command | Result |
|---------|--------|
| ls | Basic list |
| ls -l | Long format with permissions, size, date |
| ls -la | Include hidden files (dotfiles) |
| ls -lt | Sort by time, newest first |
| ls -ltr | Sort by time, reverse (oldest first) |
| ls -lh | Human-readable sizes (KB, MB, GB) |

### Wildcards (Pattern Matching)
| Pattern | Matches | Example |
|---------|---------|---------|
| * | Any characters | *.txt → all .txt files |
| ? | Single character | file?.txt → file1.txt, fileA.txt |
| {a,b,c} | Brace expansion | file{1..5}.txt → file1.txt to file5.txt |
| [abc] | Any character in brackets | file[0-9].txt → file0.txt to file9.txt |

### Critical Safety Rules
    Always pwd before rm -rf * — Know where you are
    Use ls before wildcards — Verify what matches
    cp -r for directories, mv without — Different behaviors
    No trash/recycle bin — Deleted files are gone forever
    Quote paths with spaces — "my file.txt" not my file.txt

### Common Mistakes
| Mistake | Why It Fails | Correct |
|---------|-------------|---------|
| mkdir a/b/c when a doesn't exist | Parent missing | mkdir -p a/b/c |
| cp dir1 dir2 | Directory needs -r | cp -r dir1 dir2 |
| web{file1,file2} | Missing / separator | web/{file1,file2} |
| rm -rf * in wrong directory | Deletes everything | pwd first, then ls |

### Quick Reference
```bash
# Create structure
mkdir -p practice/{projects/{web,api},archive,logs}
# Create files
touch practice/projects/web/{index.html,style.css,app.js}
# Copy with wildcard
cp practice/logs/access-log-*.txt practice/archive/
# Move directory
mv practice/projects/web/app.js practice/projects/api/
# Safe removal workflow
pwd && ls          # Verify location and targets
rm -rf practice/   # Then delete
```

### Key Takeaways
    Linux treats everything as a file—understand file types
    mkdir -p is your friend for nested directories
    cp needs -r for directories; mv doesn't
    Brace expansion saves time but requires careful syntax
    There is no undo—verify before destructive operations
    file command reveals true content type, not extension