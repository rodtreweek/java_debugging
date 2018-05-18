# java_debugging


strace -F -p <pid> 2>&1|grep -v clock_gettime
  sudo strace -p <pid> -e open -o processExecute.txt

$ strace -p 22254 -s 80 -o /tmp/debug.lighttpd.txt

To see only a trace of the open, read system calls, enter :
$ strace -e trace=open,read -p 22254 -s 80 -o debug.webserver.txt

Useful options and examples

-c – See what time is spend and where (combine with -S for sorting)
-f – Track process including forked child processes
-o my-process-trace.txt – Log strace output to a file
-p 1234 – Track a process by PID
-P /tmp – Track a process when interacting with a path
-T – Display syscall duration in the output
Track by specific system call group

-e trace=ipc – Track communication between processes (IPC)
-e trace=memory – Track memory syscalls
-e trace=network – Track memory syscalls
-e trace=process – Track process calls (like fork, exec)
-e trace=signal – Track process signal handling (like HUP, exit)
-e trace=file – Track file related syscalls
Trace multiple syscalls

strace -e open,close
