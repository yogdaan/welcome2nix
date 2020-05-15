# welcome2nix

## ls 

List directory contents

### too many posibilites go and read man pages lol
```ls [-ABCFGHLOPRSTUW@abcdefghiklmnopqrstuwx1%] [file ...]```

### simple example
```ls /some/dir```

it will list files and folder on that path if your terminal support colors you may see some different colors too

### How to see hidden files ?
```ls -a``` if you are confused with `.` and `..` then use ```ls -A```

### file search using ls 
i am searching for file that ends with x ``` ls *x```\
```ls s*``` will search all files starting with s on current path\
```ls x??``` this will display chars with x and any two letters\
what if I have multiple folders at my current path and want to chek them too\
```ls -R */x```\
if you know what pipe is (will cover later) you can try using grep

### my terminal shows color and I know what color means what if its dosent support color how can I differinciate between files dirs or symbolic links etc etc
```ls -F```

* ```/ indicates a directory```
* ```@ indicates a symbolic link```
* ```| indicates a FIFO```
* ```= indicates a socket```
* ```> indicates a door```
* ```nothing is shown for regular files```

##### we will look at above things later what they mean

### to display one directory content per line (it might be useful in some case )
```ls -1```
ls -2 will not work lol

### what if I want to look inside folders too but I dont want to run ls one by one ?

```ls -R``` i personally prefer tree

### lets see long listing
```ls -l```
oooo too much information but what do that means ?
* 1st column is permissions (we will see it later <sometimes you can find a . too its intresting>)

In some permission systems additional symbols in the ls -l display represent additional permission features:

> + (plus) suffix indicates an access control list that can control additional permissions.\
> . (dot) suffix indicates an SELinux context is present. Details may be listed with the command ls -Z.
> @ suffix indicates extended file attributes are present.

* 2nd column tells about how many link to this file
* 3rd column tells about the owner of the file
* 4th column tells about the group owner of the file
* 5th column tells about the size of the file in bytes unit. 
  * Except for directories, the size will always count as 4096 bytes
  * long listing with size displayed using human readable units (KB, MB, GB):
    * ```ls -lh```
* 6th column tells about the last time and date the file is modified
* 7th column tells the filename (I knew this)

# some example commands for ls -l
* long listing (permissions, ownership, size and modification date) of all files:
  * ```ls -la```
* long listing with size displayed using human readable units (KB, MB, GB):
  * ```ls -lh```
* long format list sorted by size (descending):
  * ```ls -lS```
* long listing of all files, sorted by modification date (oldest first):
  * ```ls -ltr```
