## lsof

### Introduction

lsof was created by Victor A. Abell and is a utility that lists open files. As everything in Linux can be considered a file, this means that lsof can gather information on the majority of activity on your machine, including network interfaces and network connections. lsof by default will output a list of all open files and the processes that opened them.

The two main drawbacks of lsof are that it can only display information about the local machine(localhost), and that it requires administrative privileges to print all available data.

### Examples

* Running lsof with -r option puts lsof in repeat mode.
> lsof -r 2

* Make lsof to output IPv4 network connections only.
> lsof -i4

* Output TCP connections of IPv4 protocol.
> lsof -i4 -a -i TCP

* Output UDP connection of IPv6 protocol.
> lsof -i6 -a -i UDP

* Logically ADD all options
> lsof -nPi -a -u work

* Using regular expressions.
> lsof -c /^.....$/

* Show all ESTABLISHED IPv4 connections.
> lsof -i4 -a -s TCP:ESTABLISHED

* Find network connections from or to an external host, or with a port range.
> lsof -i @example.host
> lsof -i @example.host:200-250

* Display open files under a given directory.
> lsof +D /etc

### Command Line Options

The lsof binary supports a large number of command line options, including the following:

| Option     | Description                                                  |
| ---------- | ------------------------------------------------------------ |
| -h         | This option present a help screen.                           |
| -a         | This option tells lsof to logically ADD all provided options. |
| -b         | This option tells lsof to avoid kernel functions that might block the returning of results. This is a very specialized option. |
| -l         | If converting a user ID to a login name is working improperly or slowly, you can disable it using the -l parameter. |
| -P         | The -P option prevents the conversion of port numbers to port names for network files. |
| -u list    | The -u option allows you to define a list of login names or user ID numbers whose files will be returned. The -u option supports the ^ character for excluding the matches from the output. |
| -c list    | The -c option selects the listing of files for processes executing the commands that begins with the characters in the list. This supports regular expressions, and also supports the ^ character for executing the matches from the output. |
| -p list    | The -p option allows you to select the files for the processes whose process IDs are in the list. The -p option supports the ^ character for excluding the matches from the output. |
| -g list    | The -g option allows you to select the files for the processes whose optional process group IDs are in the list. The -g option supports the ^ character for excluding the matches from the output. |
| -s         | The -s option allows you to select the network protocols and states that interest you. The -s option supports the ^ character for excluding the matches from the output. The correct form is PROTOCOL:STATE. Possible protocols are UDP and TCP. Some possible TCP states are: CLOSED, SYN-SENT, SYN-RECEIVED, ESTABLISHED, CLOSE-WAIT, LAST-ACK, FIN-WAIT-1, FIN-WAIT-2, CLOSING, and TIME-WAIT. Possible UDP states are Unbound and Idle. |
| +d s       | The +d option tells lsof to search for all open instances of directory s and the files and directories it contains at its top level. |
| +D d       | The +D option tells lsof to search for all optn instances of directory d and all the files and directories it contains to its complete depth. |
| -d list    | The -d option specifies the list of file descriptors to display. It supports the ^ character for excluding the matches from the output. -d 1,^2 means include fd 1, and exclude fd 2. |
| -i4        | This option is used for displaying IPv4 data only.           |
| -i6        | This option is used for displaying IPv6 data only.           |
| -i         | The -i option without any values to tell lsof to display network connections only. |
| -i ADDRESS | The -i option with a value will limit the displayed information to match that value. Some example values are TCP:25 for displaying TCP data that listens to port number 25, @google.com for displaying information related to google.com, :25 for displaying information related to port number 25, :POP3 for displaying information related to the port number that is associated to POP3 in the /etc/services file, etc. You can also combine hostnames and IP address with port numbers and protocols, for example, TCP:172.27.130.12:9001. |
| -t         | The -t option tells lsof to display process identifiers without a header line. This is particularly useful for feeding the output of lsof to the kill command or to a script. Notice that -t automatically selects the -w option. |
| +w/-w      | The +w/-w option enables or disables the supression of warming messages. |
| -r TIME    | The -r option causes the lsof command to repeat every TIME seconds until the command is manually terminated with an interrupt. |
| +r TIME    | The +r command, with the + prefix, acts the same as the -r command, but will exit its loop when it fails to find any open files. |
| -n         | The -n options inhibits the conversion of network numbers to host names for network files. |

<https://www.linode.com/docs/networking/diagnostics/lsof/>

<https://www.akadia.com/services/lsof_quickstart.txt>

<https://www.howtoforge.com/linux-lsof-command/>

<http://www.361way.com/lsof-ss-netstat/4351.html>

## ss

### Introduction

