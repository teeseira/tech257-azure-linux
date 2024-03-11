# Linux Tasks

## [1] Managing file ownership

### Why is managing file ownership important?

For security and access control. It determines who has the authority to read, write, or execute files and directories on a system.

### What is the command to view file ownership?

ls -l

### What permissions are set when a user creates a file or directory? Who does file or directory belong to?

When a user creates a file or directory, the permissions set are typically read and write permissions for the user who created it, and no permissions for others. The file or directory initially belongs to the user who created it.

### Why does the owner, by default, not receive X permissions when they create a file?

The owner, by default, does not receive execute (X) permissions when they create a file for security reasons. This prevents accidentally running potentially harmful scripts or programs.

### What command is used to change the owner of a file or directory?

chown

For example, the following command changes the owner of the file "filename" to "newowner":
```
sudo chown newowner filename
```

## [2] Managing file permissions

### Does being the owner of a file mean you have full permissions on that file? Explain.

No, the owner may have read, write, or execute permissions based on how the file's permissions are set.

### If you give permissions to the User entity, what does this mean?

It means granting access rights to the owner of the file or directory.

### If you give permissions to the Group entity, what does this mean?

It means granting access rights to a specific group of users that have been assigned to the file or directory.

### If you give permissions to the Other entity, what does this mean?

It means granting access rights to all users on the system who are not the owner or part of the group associated with the file or directory.

### You give the following permissions to a file: User permissions are read-only, Group permissions are read and write, Other permissions are read, write and execute. You are logged in as the user which is owner of the file. What permissions will you have on this file? Explain.

I will have read-only permissions on the file. This means I can view the contents of the file but cannot modify or execute it.

**Example output from `ls -l`**:

`-rwxr-xr-- 1 tcboony staff  123 Nov 25 18:36 keeprunning.sh`


- The `-` at the beginning indicates that it's a file.
- Owner has read, write, and execute permissions - `rwx`.
- Group has read and execute permissions (`r-x`).
- Others have only read permission (`r--`).

- `tcboony` is the owner of the file.
- `staff` is the group associated with the file.

## [3] Managing  file permissions using numeric values

### What numeric values are assigned to each permission?

Read: 4

Write: 2

Execute: 1

### What value would assign read + write permissions?

Read + write = 4 + 2 = 6

So with the value 6 you can read and write the file.

### What value would assign read, write and execute permissions?

Read + write + execute = 4 + 2 + 1 = 7

So with the value 7 you can read, write and execute the file.

### What value would assign read and execute permissions?

Read + write + execute = 4 + 1 = 5

So with the value 5 you can read and execute the file.

### Often, a file or directory's mode/permissions are represented by 3 numbers. What do you think 644 would mean?

- The owner has read and write permissions (6).
- The group has read permissions (4).
- Others have read permissions (4).

## [4] Changing File Permissions

### What command changes file permissions?

chmod

### To change permissions on a file what must the end user be? (2 answers)

- The file owner
- A superuser (having root access).

### Give examples of some different ways/syntaxes to set permissions on a new file (named testfile.txt) to:



- **Set User to read, Group to read + write + execute, and Other to read and write only**
   
    ```
    chmod u=r,g=rwx,o=rw testfile.txt
    ```
    ```
    chmod 754 testfile.txt
    ```
    ```
    chmod u=r--,g=rwx,o=rw- testfile.txt
    ```


- **Add execute permissions (to all entities)**

    ```
    chmod +x testfile.txt
    ```

- **Take write permissions away from Group**
  
  ```
  chmod g-w testfile.txt
  ```

- **Use numeric values to give read + write access to User, read access to Group, and no access to Other.**

    ```
    chmod 640 testfile.txt
    ```

## Key takeaways

Usually for a private key you set the permsisison has 400, where the User gets to read and the group/others get no permissions.
