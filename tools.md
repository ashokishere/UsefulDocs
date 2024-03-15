**jstack:** This is a command-line utility included with the Java Development Kit (JDK). It's used for collecting thread information from a Java process. 
When you run jstack against a Java process ID (PID) or a core file, it prints the stack traces of all threads 
that are part of that process. This can be useful for diagnosing deadlocks, performance issues, or understanding what the application is doing at a given moment.

**jmap:** This is another command-line utility included with the JDK. It's used for generating memory-related information about a Java process. 
jmap can be used to obtain heap dumps, which are snapshots of the Java heap memory at a particular moment. Heap dumps are helpful for diagnosing
memory-related issues such as memory leaks or excessive memory consumption.

Combining these tools, you can analyze both the thread and heap states of a Java process to diagnose and troubleshoot various issues. 
For instance, if you suspect a deadlock, you might use jstack to examine the thread states, while if you're investigating a memory leak, 
you might use jmap to obtain a heap dump for further analysis.
