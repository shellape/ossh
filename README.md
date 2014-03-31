
ossh manager
=============

The ossh manager shows open ssh connections and the user can establish a further based on the information.

Features
-------

* show open ssh connection
* open new ssh connections
* increase v4 ip address

Walkthrough
-------

* open a new ssh connection to [01]
```
# ossh
[01] ssh 192.168.10.12
[02] ssh -l root 192.168.10.13
Enter connection id: 1
```

* open a new ssh connection to a different server [02]+2 will open a connection to 192.168.10.15
```
# ossh
[01] ssh 192.168.10.12
[02] ssh -l root 192.168.10.13
Enter connection id: 2+2
```

Known Problems
-------

* increasing ip with v6 is not working

Author
-------

* VD <vd@ghostshell.de>

