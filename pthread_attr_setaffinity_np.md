# NAME
pthread_attr_setaffinity_np, pthread_attr_getaffinity_np - set/get CPU affinity attribute in thread attributes object

# SYNOPSIS
```c
#define _GNU_SOURCE             /* See feature_test_macros(7) */
#include <pthread.h>

int pthread_attr_setaffinity_np(pthread_attr_t *attr, size_t cpusetsize, const cpu_set_t *cpuset);
int pthread_attr_getaffinity_np(const pthread_attr_t *attr, size_t cpusetsize, cpu_set_t *cpuset);
```

Compile and link with `-pthread`.

# DESCRIPTION
The `pthread_attr_setaffinity_np()` function sets the CPU affinity mask attribute of the thread attributes object referred to by `attr` to the value specified in `cpuset`. This attribute determines the CPU affinity mask of a thread created using the thread attributes object `attr`.

The `pthread_attr_getaffinity_np()` function returns the CPU affinity mask attribute of the thread attributes object referred to by `attr` in the buffer pointed to by `cpuset`.

The argument `cpusetsize` is the length (in bytes) of the buffer pointed to by `cpuset`. Typically, this argument would be specified as `sizeof(cpu_set_t)`.

For more details on CPU affinity masks, see [sched_setaffinity(2)](https://man7.org/linux/man-pages/man2/sched_setaffinity.2.html). For a description of a set of macros that can be used to manipulate and inspect CPU sets, see [CPU_SET(3)](https://man7.org/linux/man-pages/man3/CPU_SET.3.html).

# RETURN VALUE
On success, these functions return 0; on error, they return a nonzero error number.

# ERRORS
- **EINVAL (pthread_attr_setaffinity_np()):** `cpuset` specified a CPU that was outside the set supported by the kernel. The kernel configuration option `CONFIG_NR_CPUS` defines the range of the set supported by the kernel data type used to represent CPU sets.

- **EINVAL (pthread_attr_getaffinity_np()):** A CPU in the affinity mask of the thread attributes object referred to by `attr` lies outside the range specified by `cpusetsize` (i.e., `cpuset / cpusetsize` is too small).

- **ENOMEM (pthread_attr_setaffinity_np()):** Could not allocate memory.

# VERSIONS
These functions are provided by glibc since version 2.3.4.

# ATTRIBUTES
For an explanation of the terms used in this section, see [attributes(7)](https://man7.org/linux/man-pages/man7/attributes.7.html).

- Thread safety: MT-Safe

# CONFORMING TO
These functions are nonstandard GNU extensions; hence the suffix "_np" (nonportable) in the names.

# NOTES
In glibc 2.3.3 only, versions of these functions were provided that did not have a `cpusetsize` argument. Instead, the CPU set size given to the underlying system calls was always `sizeof(cpu_set_t)`.

# SEE ALSO
- [sched_setaffinity(2)](https://man7.org/linux/man-pages/man2/sched_setaffinity.2.html)
- [pthread_attr_init(3)](https://man7.org/linux/man-pages/man3/pthread_attr_init.3.html)
- [pthread_setaffinity_np(3)](https://man7.org/linux/man-pages/man3/pthread_setaffinity_np.3.html)
- [cpuset(7)](https://man7.org/linux/man-pages/man7/cpuset.7.html)
- [pthreads(7)](https://man7.org/linux/man-pages/man7/pthreads.7.html)
