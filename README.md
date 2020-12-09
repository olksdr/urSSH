urSSH - Your SSH Client
========================

This simple script gives a possibility to connect over SSH to remote host and to take all your
config files with you. It depends on only one perl package **Net::OpenSSH**, which  should be installed. 
All you need to do is to place all the configs and other files you want to take with you 
over ssh to **$HOME/.ursshrc.d** and then edit config file for for modified bash **$HOME/.urbashrc.d/urbashrc**
in order to use those configs and files.
You should remember the more things (the bigger they will be), the longer you will need to wait until connection 
will get opened:

```bash
    echo "PGHOST=10.10.10.1" >> $HOME/.ursshrc.d/urbashrc
    urssh 10.10.10.2
```
In the config files you can use next variables:
* *$URSSHRC_D* - which points to  **.urbashrc.d** of temporary home (see below) on the remote host
* *$URSSH_HOME* - which points to temporary home on the remote host

#### Example
Let's say you want to create a custom environment for a specific host, so we can create next folder/files structure

```
$HOME/.ursshrc.d/
                \
                 \_urbashrc
                 |_server1rc
                 |_screenrc
```

with next contents:

###### urbashrc

```bash
# reading exteranl config file for Server1
source $URSSHRC_D/server1rc

```

###### server1rc

```bash
# here can be some useful information
if [ -e /etc/motd ]; then cat /etc/motd; fi

# extend the $PATH variable 
export PATH=/bin:/usr/bin:/sbin:/usr/sbin:/usr/local/bin:/usr/local/sbin

# get rid of all aliases set up before 
unalias -a

# set up my own aliases 
alias ls="ls --color=auto"
alias grep="grep --color=auto"
alias egrep="egrep --color=auto"
alias screen="screen -c $URSSHRC_D/screenrc -s $URSSH_HOME/urbash"
```

and **screenrc** file is a regular config for GNU Screen
After connection the environment will be set up reding all this files.

There is a possibility to specify login and password with hostname/IP in the connection string. In order 
to support this the perl package **IO::Pty** should be installed. Then one can use next connection string:

```bash
    urssh user:p@sw00RD@10.10.10.2
```

Script supports single commands mode as well:

```bash
    urssh 10.10.10.2 "ls -la"
```

which will list your $HOME directory

#### Dependencies 

For Ubuntu/Debian in order to install dependencies you can use apt-get/aptitude:

```bash
    apt-get install libnet-openssh-perl libio-pty-perl
```

or you can use cpan/cpanm:

```bash
    cpanm Net::OpenSSH
    cpanm IO::Pty
```
