# java_debugging

* `strace -ttf -p <pid> # trace a running process and show time to the microsecond (-tt) - and also trace child processes as they are created  by currently traced processes as  a  result of  the  fork, vfork and clone system  calls. Note that -p PID -f (which is the same as the now obsolete -F) will attach all threads of process PID  if  it is  multi-threaded,  not  only thread with thread_id = PID.`

* `strace -f -p <pid> 2>&1|grep -v clock_gettime # attach to PID of running process and grep stdout/err for occurrence of "clock_gettime" and limit output to this string.`
* `strace -p <pid> -e open -o processExecute.txt # attach to PID and limit output to opens and create and send this to the processExecute.txt file.`

* `strace -p 22254 -s 80 -o /tmp/debug.lighttpd.txt # attach to PID and include 80 characters strsize instead of default 32. Send this to a file.`
* `strace -e trace=open,read -p 22254 -s 80 -o debug.webserver.txt # limit same trace as above to the open, read system calls.`
* `strace $(pidof apache2 |sed 's/\([0-9]*\)/\-p \1/g') # strace multiple pid's of running procs.`


Some other useful options and examples

* -c – See elapsed time and where this was spent (combine with -S for sorting).
* -P /tmp – Track a process when interacting with a path
* -T – Display syscall duration in the output

### Track by specific system call group

* -e trace=ipc – Track communication between processes (IPC)
* -e trace=memory – Track memory syscalls
* -e trace=network – Track memory syscalls
* -e trace=process – Track process calls (like fork, exec)
* -e trace=signal – Track process signal handling (like HUP, exit)
* -e trace=file – Track file related syscalls


For example w/ Java, you could trace the interaction between the JVM and the linux kernel with:
```
strace -f -o strace.log -tt -T -s 1024 java -jar socket-timeouts*.jar 127.0.0.1 1234 0 0 
```
This will run the JVM and record all of the syscall activity of the JVM and all of its child processes and write them in a human-readable format in strace.log ./strace.log.
