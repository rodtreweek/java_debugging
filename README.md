# java_debugging

* strace -ttfF -p <pid>
* strace -F -p <pid> 2>&1|grep -v clock_gettime
* strace -p <pid> -e open -o processExecute.txt

* $ strace -p 22254 -s 80 -o /tmp/debug.lighttpd.txt

* strace multiple pid's:
```
strace $(pidof apache2 |sed 's/\([0-9]*\)/\-p \1/g')
```

To see only a trace of the open, read system calls, enter :
$ strace -e trace=open,read -p 22254 -s 80 -o debug.webserver.txt

Useful options and examples

* -c – See what time is spend and where (combine with -S for sorting)
* -f – Track process including forked child processes
* -o my-process-trace.txt – Log strace output to a file
* -p 1234 – Track a process by PID
* -P /tmp – Track a process when interacting with a path
* -T – Display syscall duration in the output

###Track by specific system call group

* -e trace=ipc – Track communication between processes (IPC)
* -e trace=memory – Track memory syscalls
* -e trace=network – Track memory syscalls
* -e trace=process – Track process calls (like fork, exec)
* -e trace=signal – Track process signal handling (like HUP, exit)
* -e trace=file – Track file related syscalls


You can trace the interaction between the JVM and the linux kernel using strace. For example the call 
```
strace -f -o strace.log -tt -T -s 1024 java -jar socket-timeouts*.jar 127.0.0.1 1234 0 0 
```
will run the JVM and record all of the syscall activity of the JVM and all of its child processes and write them in a human-readable format in strace.log 
