pthread_atfork - register fork handlers

# SYNOPSIS
```c
#include <pthread.h>

int pthread_atfork(void (*prepare)(void), void (*parent)(void),
                   void (*child)(void));
```

Link with `-pthread`.

# DESCRIPTION
The `pthread_atfork()` function registers fork handlers that are to be executed when `fork(2)` is called by this thread. The handlers are executed in the context of the thread that calls `fork(2)`.

Three kinds of handler can be registered:
- `prepare` specifies a handler that is executed before `fork(2)` processing starts.
- `parent` specifies a handler that is executed in the parent process after `fork(2)` processing completes.
- `child` specifies a handler that is executed in the child process after `fork(2)` processing completes.

Any of the three arguments may be NULL if no handler is needed in the corresponding phase of `fork(2)` processing.

# RETURN VALUE
On success, `pthread_atfork()` returns zero. On error, it returns an error number. `pthread_atfork()` may be called multiple times by a thread to register multiple handlers for each phase. The handlers for each phase are called in a specified order: the `prepare` handlers are called in reverse order of registration; the `parent` and `child` handlers are called in the order of registration.

# ERRORS
- `ENOMEM`: Could not allocate memory to record the form handler entry.

# CONFORMING TO
POSIX.1-2001, POSIX.1-2008.

# NOTES
When `fork(2)` is called in a multithreaded process, only the calling thread is duplicated in the child process. The original intention of `pthread_atfork()` was to allow the calling thread to be returned to a consistent state. For example, at the time of the call to `fork(2)`, other threads may have locked mutexes that are visible in the user-space memory duplicated in the child. Such mutexes would never be unlocked, since the threads that placed the locks are not duplicated in the child. The intent of `pthread_atfork()` was to provide a mechanism whereby the application (or a library) could ensure that mutexes and other process and thread state would be restored to a consistent state. In practice, this task is generally too difficult to be practicable.

After a `fork(2)` in a multithreaded process returns in the child, the child should call only async-signal-safe functions (see [signal-safety(7)](https://man7.org/linux/man-pages/man7/signal-safety.7.html)) until such time as it calls `execve(2)` to execute a new program.

POSIX.1 specifies that `pthread_atfork()` shall not fail with the error `EINTR`.

# SEE ALSO
- [fork(2)](https://man7.org/linux/man-pages/man2/fork.2.html)
- [atexit(3)](https://man7.org/linux/man-pages/man3/atexit.3.html)
- [pthreads(7)](https://man7.org/linux/man-pages/man7/pthreads.7.html)
