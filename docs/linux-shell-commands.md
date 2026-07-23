# devops-notes

> Personal DevOps learning notes covering Linux, networking, SSH, backend deployment practices and others as needed.

Basic linux shell command that I use regularly.

---

### Note: `<value>` represents a variable to be replaced with actual value

## Directory Operations

---


```bash
ls                                                                    # List files and directories.

ls -la                                                                # List files and directories with attributes

pwd                                                                   # Show current directory path.

cd <directory-name>                                                   # Change directory


cd ..                                                                 # Navigate to parent directory

cd ~                                                                  # Navigate to current user's home directory

cd /                                                                  # Navigate to root directory

mkdir <directory-name>                                                # Create a directory

rm -rf <directory-name>                                               # Delete a directory

mv <old-name> <new-name>                                              # Rename a directory

cp -r </path/from/directory-name> </path/to/>                         # Copy a directory to another location

cp -r </path/from/directory-name> </path/to/new-directory-name>       # Copy a directory with new name
```


## File Operations

---


```bash
touch <filename>                                                    # Create a file

rm <filename>                                                       # Delete a file

mv <old-filename> <new-filename>                                    # Rename a file

cp -p </path/from/filename> </path/to/>                             # Copy a file to different directory
                                                                    # Note: -p flag preserves file ownership, permissions, timestamps


cp -p </path/from/filename> </path/to/new-filename>                 # Copy a file to with different name
```


## File Viewing and Editing

---


```bash
cat <filename>                              # Read file content

cat <file1> <file2> <file2> <.....>         # Concatenate multiple files


less <filename>                             # Read file less


head <filename> -n 5                        # Read first 5 lines


tail <filename> -n 5                        # Read last 5 lines

echo <"some text"> > <filename>             # Overwrite existing

echo <"some text"> >> <filename>            # Append a file
```

## Search and Find



```bash
grep <"text"> <filename>                      # Search for occurrences of "text" in a filename

grep <"text"> <directory-name/>               # Recursively search "text" in a directory

find . -name "*.txt"                          # Find all .txt extension files in current directory

find </directory-name/*> -name "*.txt"        # Find all .txt files in a directory and it's subdirectories
```



## Process Management

---



```bash
ps aux                                  # Show all processes

ps aux | grep "java-test file"          # Search for a process that contains name "java-test file"

kill <pid>                              # Kill a process by pid
```


## User

---

```bash
sudo adduser <username>     # Create a new user
```



## Permissions

---

```bash
chown <user> <filename>     # Change file ownership

chmod 761 <filename>        # Change file privilege
```
`Structure: chmod <owner><group><others> <filename>`

Breakdown of 761:

- Owner: Can Read (r) - Can Write (w) - Can Execute (x)
- Group: Can Read (r) - Can Write (w) - Cannot Execute (x)
- Others: Cannot Read (r) - Cannot Write (w) - Can Execute (x)



<table>
    <tr>
        <th>Role</th>
        <th>Permission</th>
        <th>Binary</th>
        <th>Octal</th>
    </tr>
    <tr>
        <td>Owner</td>
        <td>rwx</td>
        <td>111</td>
        <td>7</td>
    </tr>
    <tr>
        <td>Group</td>
        <td>rw-</td>
        <td>110</td>
        <td>6</td>
    </tr>
    <tr>
        <td>Others</td>
        <td>--x</td>
        <td>001</td>
        <td>1</td>
    </tr>
</table>




## SSH and Remote Access

---



```bash
scp <local-filename> <user@server>:</path/to/>        # Copy a file from local machine to remote server

scp -r <local-directory> <user@server>:</path/to/>    # Copy a directory from local machine to remote server
```