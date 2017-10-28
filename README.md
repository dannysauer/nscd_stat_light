# nscd_stat_light
Gather stats from the Name Service Cache Daemon using the nscd socket rather than exec'ing `nscd -g`

I wanted a reason to learn Go, and I wanted to gather stats on nscd.  The other tools I've seen run "nscd -g" and parse that output.  While it does provide some level of abstraction, I generally dislike the idea of `fork()`/`exec()` if it can be avoided.  So, this tool reads directly from the nscd socket (which is exactly what "nscd -g" does) opened by the daemon.  That means stats can be gathered at tighter intervals without as much overhead, and stats don't necessarily stop being gathered if something happens on the system which prevents spawning new processes.  It's a stretch, I know, but the main reason is to lean Go. :)
