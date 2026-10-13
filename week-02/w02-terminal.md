# Terminal: grep

## Preparing a test file (in the sandbox)

"cd ~/sandbox"
"printf "INFO start\nERROR login failed\nINFO done\nERROR timeout\n" > app.log"  

*We created a file named app.log consisting of four lines:*  
INFO start  
ERROR login failed  
INFO done  
ERROR timeout  

---

## Commands and what they do  

"grep "ERROR" app.log"  

*Displays only the lines that contain the word ERROR (two lines).*

---

"grep -n -i "error" app.log"

*-n adds line numbers; -i ignores case (will find ERROR, error, and Error).*

---

"grep -c "ERROR" app.log"

*-c (count) displays the number of lines found, not the lines themselves. Answer: 2.*

---

"grep -v "INFO" app.log"

*-v (invert) does the opposite: it displays all lines except those containing “INFO.”*

---

"grep -rn "timeout" ."

*-r (recursive) searches all files within the folder and its subfolders. A period (.) means “current folder.”*

---

# Terminal: chmod (access permissions)

In Linux, every file has permissions that specify who can do what with it. This is a security measure: an unauthorized user should not be able to read passwords that do not belong to them or modify system files. The `chmod` (change mode) command changes these permissions.  

"ls -l app.log":

| Position  | Meaning | 
| --- | --- | 
| 1st character | Type: - regular file, d - directory |
2–4 (rw-)  |  Owner's permissions |
5–7 (r--) | Group permissions |
8–10 (r--) |  Permissions for everyone else |

---

Each triplet consists of three letters: r (read), w (write), x (execute). If a letter is replaced by a dash (-), that permission is denied. So, rw-r--r-- means “you can read and write, while others can only read.”

---

### Permissions by Numbers

Each permission corresponds to a number: r = 4, w = 2, x = 1. Add the appropriate numbers together to get a single digit for each of the three groups (owner, group, others):

| Number | Calculation | Permissions |
| --- | --- | --- |
7 | 4+2+1 | rwx (all) |
6 | 4+2 | rw- (read and write) |
5 | 4+1 | r-x (read and execute) |
4 | 4 | r-- (read only) |
0 | none | --- |

---

Therefore:
* 644 = rw-r--r-- (the owner can read and write; others can only read); typical permissions for a regular file.
* 755 = rwxr-xr-x (the owner has full access; others can read and execute); typical permissions for a program or script.
* 600 = rw------- (owner only; suitable for private items, such as an SSH key).

### Commands

---

"chmod 600 app.log"  

*"Now only you can access the file".*

---

"printf '#!/bin/bash\necho hi\n' > script.sh
chmod +x script.sh"
./script.sh"

*We created a script file, granted it execute permission (+x adds the x permission), and ran it. Without chmod +x, the terminal would have returned “Permission denied.”*

---

