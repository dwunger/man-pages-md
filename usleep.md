# USLEEP(3) Linux Programmer's Manual USLEEP(3)

## NAME

**usleep** - suspend execution for microsecond intervals

## SYNOPSIS

```c
#include <unistd.h>

int usleep(useconds_t usec);
```

## DESCRIPTION

The **usleep()** function suspends execution of the calling thread for (at least) **usec** microseconds. The sleep may be lengthened slightly by any system activity or by the time spent processing the call or by the granularity of system timers.

## RETURN VALUE

The **usleep()** function returns 0 on success. On error, -1 is returned, with **errno** set to indicate the error.

## ERRORS

- **EINTR**: Interrupted by a signal; see **signal(7)**.
- **EINVAL**: **usec** is greater than or equal to 1000000 (on systems where that is considered an error).

## ATTRIBUTES

For an explanation of the terms used in this section, see **attributes(7)**.

- **Thread safety**: MT-Safe

## CONFORMING TO

4.3BSD, POSIX.1-2001. POSIX.1-2001 declares this function obsolete; use **nanosleep(2)** instead. POSIX.1-2008 removes the specification of **usleep()**.

Only the **EINVAL** error return is documented by SUSv2 and POSIX.1-2001.

## NOTES

The type **useconds_t** is an unsigned integer type capable of holding integers in the range [0,1000000]. Programs will be more portable if they never mention this type explicitly.

The interaction of this function with the **SIGALRM** signal, and with other timer functions such as **alarm(2)**, **sleep(3)**, **nanosleep(2)**, **setitimer(2)**, **timer_create(2)**, **timer_delete(2)**, **timer_getoverrun(2)**, **timer_gettime(2)**, **timer_settime(2)**, **ualarm(3)** is unspecified.

## SEE ALSO

**alarm(2)**, **getitimer(2)**, **nanosleep(2)**, **select(2)**, **setitimer(2)**, **sleep(3)**, **ualarm(3)**, **time(7)**
