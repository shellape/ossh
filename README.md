
ossh manager
=============

The ossh manager shows open ssh connections and the user can establish a further based on the information.

Features
-------

* show open ssh connections
* show recent used connections via ossh (history)
* open new ssh connections
* increase v4 ip address

Walkthrough
-------

* open a new ssh connection to [01]
```
# ossh
[01] ssh 192.168.10.12
[02] ssh -l root 192.168.10.13
[--]
[03] ssh 172.16.20.14
>id: 1
```

* open a new ssh connection to a different server [02]+2 will open a connection to 192.168.10.15
```
# ossh
[01] ssh 192.168.10.12
[02] ssh -l root 192.168.10.13
[--]
[03] ssh 172.16.20.14
>id: 2+2
```

Hints
-------

* For choosing the first entry from the overview you can simply hit enter.
* "[--]" in the overview implies that all following entries come from the history file.
* If you know what the overview looks like you can pass the id direclty, e.g. "ossh 1" or "ossh 4"
* Passing the parameter [-a|--auto] provides the possibility to auto login if
  there is only one unique current connection instead of printing the overview.
* There are global variables in the script header. Here are their default values:
```
  HIST_FILE=~/.ossh_history
  MAX_HIST_LINES=6
  EXCLUDE_RE=
```
  Read the script's comment about the variable $EXCLUDE_RE for further information.

Known Problems
-------

* increasing ip with v6 is not working

Author
-------

* vd <vd@ghostshell.de>

License
-------

ossh is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, version 2 of the License.

ossh is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with ossh.  If not, see <http://www.gnu.org/licenses/>.

