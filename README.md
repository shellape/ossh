
# ossh - a ssh connection manager

ossh shows open ssh connections and the user can establish a connection based on the shown information.

## Features

* show open ssh connections
* show recently used ssh connections (via ossh history file)
* open new ssh connection
* increase/decrease ip v4 address you see in ossh overview
  to be used as new ssh host to connect to

## Builtin help
```
$> ossh -h
Usage: ossh [-l|--list] [-a|--auto] [-r|--rev] [-c|--conf <file>] [-h|--help] [index]

List or establish ssh connections.

Options:
 -l|--list         only list connections, do not a ask for a connection id
                   (mutually exclusive with "index", supersedes "-a")
 -a|--auto         auto login (or ping) if there is only one unique current connection
                   (superseded by "index")
 -r|--rev          show output in reverse order, first history then current connections
 -c|--conf <file>  specify path to custom config file
                   (by default ossh looks for ~/.ossh.conf)
 -h|--help         show this help
 index             specify a numeric index to use from the overview, e.g. "2" or "4"
                   using +/- modifies ip's last octett of the choosen index, e.g. "+3" or "4-2"
                   (appending "p" to "index" will just ping the ip, e.g. "2p" or "4+6p")

```

## Walkthrough

* open a new ssh connection to [01]
```
# ossh
[01] ssh 192.168.10.12
[02] ssh -l root 192.168.10.13
[-b]
[03] ssh 172.16.20.14
>id: 1
```

* open a new ssh connection to a different server [02]+2 will open a connection to 192.168.10.15
```
# ossh
[01] ssh 192.168.10.12
[02] ssh -l root 192.168.10.13
[-b]
[03] ssh 172.16.20.14
>id: 2+2
```

## Hints

* For choosing the first entry from the overview you can simply hit enter.
* "[-b]" in the overview implies that all entries below come from the history file.
* Passing the parameter "[-l|--list]" just lists the connection overview without asking for a connection id.
* Passing the parameter "[-a|--auto]" provides the possibility to auto login if there is only
  one unique current connection instead of printing the overview and asking for a connection id.
* Passing the parameter "[-r|--rev]" will output first history then current connections.
  The history indicator changes then from "[-b]" to "[-a]" to show history is above.
  This is useful if you have quite a lot of history connections and your terminal window is small.
* If you know what the overview looks like you can pass the id directly, e.g. "ossh 1" or "ossh 4+2"
* Passing a trailing "p" to the "index" will just ping the ip, e.g. "2p" or "8p-2" or "6+2p".
* If there is a FQDN in the ossh overview a name lookup will be performed when increasing/decreasing.
* There are global variables in the script header.

  **It is generally recommended to put your modified variables in ~/.ossh.conf to avoid conflicts on ossh updates.**
  **Simply execute this command to generate the include config:**

```
ossh/bin/gen-include.sh -w > ~/.ossh.conf
```

  The default values and short explanations:

```
HIST_FILE=~/.ossh_history
MAX_HIST_LINES=16
# Optional bash compatible regex for ssh connections which
# should not appear in the connection overview at all.
# Exclude is applied on active connections only, not on history.
CONN_EXCL_RE='sshfs|sftp|scp| -fnN '
# Optional sed compatible expression to strip off a part of the ssh command
# in the connection overview. e.g. SSH_STRIP_EXPR='s/ .*foobar//'
SSH_STRIP_EXPR=''
# I you're using a wrapper to call ssh you can specify it here.
SSH_BIN=''
# command parameters
PING_PARAM='-c3'
HOST_PARAM='-4 -t A'
# Skip the output of current connections, thus show only history.
SKIP_CURR_CONN=no
```

## Known Problems

* increasing/decreasing an ip v6 address is not supported

## Author

* Vladimir

## License

ossh is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, version 2 of the License.

ossh is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with ossh.  If not, see <http://www.gnu.org/licenses/>.

