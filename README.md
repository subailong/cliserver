cliserver
---------
A libevent-driven server that handles simple commands from multiple clients.
Created while learning to use libevent, this is intended to help alleviate the
relative dearth of libevent sample code.  See the reasonably-well-commented
source code for additional information.

Note that evbuffer_readline() is a potential source of denial of service, as
once data exists in a buffer, that buffer's read event will continue triggering
until a newline is received and the buffer is cleared.  Additionally,
evbuffer_readline() does an O(n) scan for a newline character each time it is
called.  One solution would be checking the length of the buffer and dropping
the connection if the buffer exceeds some limit (dropping the data is less
desirable, as the client is clearly not speaking our protocol anyway).

Clients connect to the server on port 14310, allowing them to run the following
commands:

 * echo:	Print the command line.
 * help:	Print a list of commands and their descriptions.
 * info:	Print connection information.
 * quit:	Disconnect from the server.
 * kill:	Shut down the server.

Compile the server with `make`, run it with `./cliserver`.  Connect to the
server using netcat: `nc localhost 14310`.

You will need libevent 1.x (I'm using 1.4.2 from Ubuntu 10.10), gcc, and GNU
make to compile this code.  It should, in theory, be easily portable to libevent
2.x.

(C)2010 Mike Bourgeous, licensed under 2-clause BSD

