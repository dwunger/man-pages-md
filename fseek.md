---
title: FSEEK 3
section: 3
date: 2021-03-22
source: GNU
manual: Linux Programmer's Manual
---

# NAME

**fgetpos**, **fseek**, **fsetpos**, **ftell**, **rewind** - reposition a stream

# SYNOPSIS

```c
#include <stdio.h>

int fseek(FILE *stream, long offset, int whence);
long ftell(FILE *stream);
void rewind(FILE *stream);
int fgetpos(FILE *restrict stream, fpos_t *restrict pos);
int fsetpos(FILE *stream, const fpos_t *pos);
```

# DESCRIPTION

The **fseek()** function sets the file position indicator for the stream pointed to by **stream**. The new position, measured in bytes, is obtained by adding **offset** bytes to the position specified by **whence**. If **whence** is set to **SEEK_SET**, **SEEK_CUR**, or **SEEK_END**, the offset is relative to the start of the file, the current position indicator, or end-of-file, respectively. A successful call to the **fseek()** function clears the end-of-file indicator for the stream and undoes any effects of the **ungetc(3)** function on the same stream.

The **ftell()** function obtains the current value of the file position indicator for the stream pointed to by **stream**.

The **rewind()** function sets the file position indicator for the stream pointed to by **stream** to the beginning of the file. It is equivalent to:

```c
(void) fseek(stream, 0L, SEEK_SET)
```

except that the error indicator for the stream is also cleared (see **clearerr(3)**).

The **fgetpos()** and **fsetpos()** functions are alternate interfaces equivalent to **ftell()** and **fseek()** (with **whence** set to **SEEK_SET**), setting and storing the current value of the file offset into or from the object referenced by **pos**. On some non-UNIX systems, an **fpos_t** object may be a complex object and these routines may be the only way to portably reposition a text stream.

# RETURN VALUE

The **rewind()** function returns no value. Upon successful completion, **fgetpos()**, **fseek()**, **fsetpos()** return 0, and **ftell()** returns the current offset. Otherwise, -1 is returned, and **errno** is set to indicate the error.

# ERRORS

- **EINVAL**: The **whence** argument to **fseek()** was not **SEEK_SET**, **SEEK_END**, or **SEEK_CUR**. Or: the resulting file offset would be negative.
- **ESPIPE**: The file descriptor underlying **stream** is not seekable (e.g., it refers to a pipe, FIFO, or socket).

The functions **fgetpos()**, **fseek()**, **fsetpos()**, and **ftell()** may also fail and set **errno** for any of the errors specified for the routines **fflush(3)**, **fstat(2)**, **lseek(2)**, and **malloc(3)**.

# ATTRIBUTES

- Interface: MT-Safe

# CONFORMING TO

POSIX.1-2001, POSIX.1-2008, C89, C99.

# SEE ALSO

**lseek(2)**, **fseeko(3)**