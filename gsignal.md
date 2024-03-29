---
title: GSIGNAL 3
section: 3
date: 2021-03-22
source: Linux Programmer's Manual
---

# NAME

**gsignal**, **ssignal** - software signal facility

# SYNOPSIS

```c
#include <signal.h>

typedef void (*sighandler_t)(int);

int gsignal(int signum);
sighandler_t ssignal(int signum, sighandler_t action);
```

# DESCRIPTION

Don't use these functions under Linux. Due to a historical mistake, under Linux these functions are aliases for **raise(3)** and **signal(2)**, respectively.

Elsewhere, on System V-like systems, these functions implement software signaling, entirely independent of the classical **signal(2)** and **kill(2)** functions.

The function **ssignal()** defines the action to take when the software signal with number **signum** is raised using the function **gsignal()**, and returns the previous such action or **SIG_DFL**. The function **gsignal()** does the following: if no action (or the action **SIG_DFL**) was specified for **signum**, then it does nothing and returns 0. If the action **SIG_IGN** was specified for **signum**, then it does nothing and returns 1. Otherwise, it resets the action to **SIG_DFL** and calls the action function with argument **signum**, and returns the value returned by that function. The range of possible values **signum** varies (often 1 to 15 or 1 to 17).

# ATTRIBUTES

In the above table, **sigintr** in **MT-Safe sigintr** signifies that these functions implement a software signal facility.

# CONFORMING TO

These functions are available under AIX, DG/UX, HP-UX, SCO, Solaris, Tru64. They are called obsolete under most of these systems and are broken under glibc.

# SEE ALSO

**kill(2)**, **signal(2)**, **raise(3)**
