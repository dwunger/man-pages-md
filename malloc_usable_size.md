# `malloc_usable_size(3)` GNU Linux Programmer's Manual
## NAME
`malloc_usable_size` - obtain size of block of memory allocated from heap
## SYNOPSIS
```c
#include <malloc.h>

size_t malloc_usable_size(void *ptr);
```
## DESCRIPTION
The `malloc_usable_size()` function returns the number of usable bytes in the block pointed to by `ptr`, a pointer to a block of memory allocated by `malloc(3)` or a related function.
## RETURN VALUE
`malloc_usable_size()` returns the number of usable bytes in the block of allocated memory pointed to by `ptr`. If `ptr` is NULL, 0 is returned.
## ATTRIBUTES
For an explanation of the terms used in this section, see [attributes(7)](http://man7.org/linux/man-pages/man7/attributes.7.html).
```plaintext
Interface            Attribute     Value
malloc_usable_size() Thread safety MT-Safe
```
## CONFORMING TO
This function is a GNU extension.
## NOTES
The value returned by `malloc_usable_size()` may be greater than the requested size of the allocation because of alignment and minimum size constraints. Although the excess bytes can be overwritten by the application without ill effects, this is not good programming practice: the number of excess bytes in an allocation depends on the underlying implementation.

The main use of this function is for debugging and introspection.
## SEE ALSO
- [`malloc(3)`](http://man7.org/linux/man-pages/man3/malloc.3.html)
