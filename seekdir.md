# SEEKDIR(3) Linux Programmer's Manual
## NAME
`seekdir` - set the position of the next `readdir()` call in the directory stream.
## SYNOPSIS
```c
#include <dirent.h>

void seekdir(DIR *dirp, long loc);
```
## DESCRIPTION
The `seekdir()` function sets the location in the directory stream from which the next `readdir()` call will start. The `loc` argument should be a value returned by a previous call to `telldir(3)`.

## RETURN VALUE
The `seekdir()` function returns no value.

## ATTRIBUTES
For an explanation of the terms used in this section, see [attributes(7)](attributes.7.html).

- Thread safety: MT-Safe

## CONFORMING TO
POSIX.1-2001, POSIX.1-2008, 4.3BSD.

## NOTES
In glibc up to version 2.1.1, the type of the `loc` argument was `off_t`. POSIX.1-2001 specifies `long`, and this is the type used since glibc 2.1.2. See `telldir(3)` for information on why you should be careful in making any assumptions about the value in this argument.

## SEE ALSO
`lseek(2)`, `closedir(3)`, `opendir(3)`, `readdir(3)`, `rewinddir(3)`, `scandir(3)`, `telldir(3)`
