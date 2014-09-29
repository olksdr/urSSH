urSSH - Your SSH Client
========================

## Description

This simple script gives a possibility to connect over SSH to remote host and to take all your
config files with you. It depends on only one perl package *Net::OpenSSH*, which  should be installed. 
All you need to do is to place all the configs and other files you want to take with you 
over ssh to *$HOME/.ursshrc.d* and then edit config file for for modified bash *$HOME/.urbashrc.d/urbashrc*
in order to use those configs and files.
You should remember the more things (the bigger they will be), the longer you will need to wait until connection 
will get opened.

```bash
Example:
    $> echo "PGHOST=10.10.10.1" >> $HOME/.ursshrc.d/urbashrc
    $> urssh 10.10.10.2
```

There is a possibility to specify login and password with hostname/IP in the connection string. In order 
to support this the perl package *IO::Pty* should be installed. Then one can use next connection string:

```bash
Example:
    $> urssh user:p@sw00RD@10.10.10.2
```
