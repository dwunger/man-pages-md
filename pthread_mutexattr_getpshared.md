```markdown
---
title: pthread_mutexattr_getpshared, pthread_mutexattr_setpshared - Linux Programmer's Manual
date: 2021-03-22
categories: [Linux, Manual]
---

# NAME

pthread_mutexattr_getpshared, pthread_mutexattr_setpshared - get/set process-shared mutex attribute

# SYNOPSIS

```c
#include <pthread.h>

int pthread_mutexattr_getpshared(const pthread_mutexattr_t *restrict attr, int *restrict pshared);
int pthread_mutexattr_setpshared(pthread_mutexattr_t *attr, int pshared);
```

# DESCRIPTION

These functions get and set the process-shared attribute in a mutex attributes object. This attribute must be appropriately set to ensure correct, efficient operation of a mutex created using this attributes object.

The process-shared attribute can have one of the following values:

- PTHREAD_PROCESS_PRIVATE: Mutexes created with this attributes object are to be shared only among threads in the same process that initialized the mutex. This is the default value for the process-shared mutex attribute.

- PTHREAD_PROCESS_SHARED: Mutexes created with this attributes object can be shared between any threads that have access to the memory containing the object, including threads in different processes.

pthread_mutexattr_getpshared() places the value of the process-shared attribute of the mutex attributes object referred to by attr in the location pointed to by pshared.

pthread_mutexattr_setpshared() sets the value of the process-shared attribute of the mutex attributes object referred to by attr to the value specified in pshared.

If attr does not refer to an initialized mutex attributes object, the behavior is undefined.

# RETURN VALUE

On success, these functions return 0. On error, they return a positive error number.

# ERRORS

pthread_mutexattr_setpshared() can fail with the following errors:

- EINVAL: The value specified in pshared is invalid.

- ENOTSUP: pshared is PTHREAD_PROCESS_SHARED but the implementation does not support process-shared mutexes.

# CONFORMING TO

POSIX.1-2001, POSIX.1-2008.

# SEE ALSO

- pthread_mutexattr_init(3)
- pthreads(7)
```