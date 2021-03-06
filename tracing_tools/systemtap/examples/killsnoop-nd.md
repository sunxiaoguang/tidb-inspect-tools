### Usage
```
$ sudo stap killsnoop-nd.stp
```

killsnoop-nd.stp traces signals, including those sent by the kill(1) command.
For example:

```
$ sudo stap killsnoop-nd.stp
FROM   COMMAND      SIG   TO     RESULT
14163  w            0     11962       0
14163  w            0     12040       0
14163  w            0     14152       0
14152  bash         9     12345      -3
14152  bash         9     14152       0
^C13914  killsnoop-nd.st 15    14147       0
```

The output begins by showing the w(1) command sending three signal 0's to
different processes: signal 0, and the return value, is used as an aliveness
check. Then bash sends a signal 9 (SIGKILL) to PID 12345, which doesn't exist,
and returns an error (-3). This is followed by a successful signal 9. These two
were issued using "kill -9".

Finally, I hit Ctrl-C to end this example, and this was caught and shown after
the "^C". Signal 15 (SIGTERM)? I thought Ctrl-C issued signal 2 (SIGINT)...

For a quick lookup of signal numbers to names, you can use the kill(1) bash
builtin with -l. Eg:

```
$ kill -l
 1) SIGHUP	 2) SIGINT	 3) SIGQUIT	 4) SIGILL	 5) SIGTRAP
 6) SIGABRT	 7) SIGBUS	 8) SIGFPE	 9) SIGKILL	10) SIGUSR1
11) SIGSEGV	12) SIGUSR2	13) SIGPIPE	14) SIGALRM	15) SIGTERM
16) SIGSTKFLT	17) SIGCHLD	18) SIGCONT	19) SIGSTOP	20) SIGTSTP
21) SIGTTIN	22) SIGTTOU	23) SIGURG	24) SIGXCPU	25) SIGXFSZ
26) SIGVTALRM	27) SIGPROF	28) SIGWINCH	29) SIGIO	30) SIGPWR
31) SIGSYS	34) SIGRTMIN	35) SIGRTMIN+1	36) SIGRTMIN+2	37) SIGRTMIN+3
38) SIGRTMIN+4	39) SIGRTMIN+5	40) SIGRTMIN+6	41) SIGRTMIN+7	42) SIGRTMIN+8
43) SIGRTMIN+9	44) SIGRTMIN+10	45) SIGRTMIN+11	46) SIGRTMIN+12	47) SIGRTMIN+13
48) SIGRTMIN+14	49) SIGRTMIN+15	50) SIGRTMAX-14	51) SIGRTMAX-13	52) SIGRTMAX-12
53) SIGRTMAX-11	54) SIGRTMAX-10	55) SIGRTMAX-9	56) SIGRTMAX-8	57) SIGRTMAX-7
58) SIGRTMAX-6	59) SIGRTMAX-5	60) SIGRTMAX-4	61) SIGRTMAX-3	62) SIGRTMAX-2
63) SIGRTMAX-1	64) SIGRTMAX
```
