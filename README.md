# pytrace

This utility allowing you to trace wall time during program execution. Sometimes you wonder where time is spent 
during execution. The *Trace* class is awrapper where call data is gathered, filename, linenumber, and time.
It is however not collected automatically, you have to instrument your code where you like to collect
time stamps. 

You can initialize the class in verbose mode, then you will collect filename and line number where 
the data is collected. For this you pay an overhead that is relatively large 14-16 usec per 
collected entry. The plain mode is significantly more efficient.

The class has a dump method that prints the collected information, like

```
===================== Verbose Mode ============================
Trace init 08:33:40.395 file: /home/bertilsson/source/pytrace/trace.py lineno: 88
    [1] time: 42 (usec) tag: "calling a       " file: trace.py         lineno: 82 (42 usec)
    [2] time: 24 (usec) tag: "calling b       " file: trace.py         lineno: 77 (66 usec)
    [3] time: 19 (usec) tag: "calling c       " file: trace.py         lineno: 73 (85 usec)
    [4] time: 19 (usec) tag: "at the end      " file: trace.py         lineno: 90 (104 usec)

===================== Plain Mode ============================
Trace init 08:33:40.395
    [1] time:        3 tag: "calling a       "(3 usec)
    [2] time:        0 tag: "calling b       "(3 usec)
    [3] time:        0 tag: "calling c       "(3 usec)
    [4] time:        2 tag: "at the end      "(5 usec)

```