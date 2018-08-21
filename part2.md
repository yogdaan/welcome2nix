# first minute on a nix server

1.history
2.w, who
3.htop
4.df
5.netstat

## History

its a very usefull command but can be used to check what was done on server last time 

i like to use it in 

```bash
history | less	
```

create a histignore file cause too many time ls ,date,pwd like commands can add unwanted stuff to history

``` bash
export HISTIGNORE='ls -l:pwd:date:'	
```

### get history of anyother user 

to see command history executed by a specific user. Bash keeps records of history in a ‘~/.bash_history’ file. We can view or open file to see the command history.
this can change with the shell

```bash
less /home/<some user>/.bash_history
```

## w

## htop/top

## df

## netstat

