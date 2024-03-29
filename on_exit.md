# `on_exit(3)` Linux Programmer's Manual
## NAME
`on_exit` - register a function to be called at normal process termination
## SYNOPSIS
```c
#include <stdlib.h>

int on_exit(void (*function)(int, void *), void *arg);
```
## DESCRIPTION
The `on_exit()` function registers the given `function` to be called at normal process termination, whether via `exit(3)` or via return from the program's `main()`. The `function` is passed the status argument given to the last call to `exit(3)` and the `arg` argument from `on_exit()`.

The same function may be registered multiple times: it is called once for each registration.

When a child process is created via `fork(2)`, it inherits copies of its parent's registrations. Upon a successful call to one of the `exec(3)` functions, all registrations are removed.
## RETURN VALUE
The `on_exit()` function returns the value 0 if successful; otherwise, it returns a nonzero value.
## ATTRIBUTES
For an explanation of the terms used in this section, see [attributes(7)](http://man7.org/linux/man-pages/man7/attributes.7.html).
## CONFORMING TO
This function comes from SunOS 4 but is also present in glibc. It no longer occurs in Solaris (SunOS 5). Portable applications should avoid this function and use the standard `atexit(3)` instead.
## NOTES
By the time `function` is executed, stack (auto) variables may already have gone out of scope. Therefore, `arg` should not be a pointer to a stack variable; it may, however, be a pointer to a heap variable or a global variable.
## SEE ALSO
- [_exit(2)](http://man7.org/linux/man-pages/man2/_exit.2.html)
- [atexit(3)](http://man7.org/linux/man-pages/man3/atexit.3.html)
- [exit(3)](http://man7.org/linux/man-pages/man3/exit.3.html)
