# Purpose
This C header file, `xmalloc.h`, provides declarations for a set of memory management and string manipulation functions that enhance standard library functions by incorporating error checking and handling. The functions, such as `xmalloc`, `xcalloc`, `xrealloc`, and `xstrdup`, are designed to never return a failure; instead, they invoke a fatal error handler if an error occurs, ensuring robust memory allocation. Additionally, the file includes functions like `xasprintf` and `xsnprintf`, which are safer versions of their standard counterparts, with added format string checking and non-null attribute enforcement to prevent common errors. The header is part of a larger software project, likely related to secure communications, as indicated by the author's note on usage and compatibility with the SSH protocol.
# Global Variables

---
### xmalloc
- **Type**: `function pointer`
- **Description**: `xmalloc` is a function that allocates memory of a specified size and returns a pointer to the allocated memory. It is a safer version of the standard `malloc` function, as it checks the result of the allocation and does not return a null pointer on failure, instead calling a fatal error handler.
- **Use**: `xmalloc` is used to allocate memory dynamically, ensuring that the program handles allocation failures gracefully by terminating execution.


---
### xcalloc
- **Type**: `function pointer`
- **Description**: `xcalloc` is a function pointer that represents a custom implementation of the standard `calloc` function. It is designed to allocate memory for an array of elements, initializing all bytes to zero, and is part of a set of memory allocation functions that ensure memory allocation errors are handled by terminating the program.
- **Use**: This variable is used to allocate zero-initialized memory for an array, ensuring that allocation errors are handled by calling a fatal error function.


---
### xrealloc
- **Type**: `function pointer`
- **Description**: `xrealloc` is a function pointer that points to a function designed to reallocate memory blocks. It takes a pointer to the existing memory block and a size_t value representing the new size of the memory block.
- **Use**: This function is used to resize an existing memory allocation, ensuring that the operation does not fail silently by incorporating error checking.


---
### xreallocarray
- **Type**: `function pointer`
- **Description**: `xreallocarray` is a function pointer that points to a function designed to reallocate memory for an array. It takes three parameters: a pointer to the existing memory block, the number of elements, and the size of each element.
- **Use**: This function is used to safely resize an array by reallocating memory, ensuring that the operation does not fail silently.


---
### xrecallocarray
- **Type**: `function pointer`
- **Description**: `xrecallocarray` is a function pointer that points to a function designed to reallocate memory for an array, with the added functionality of zeroing out the newly allocated memory. It takes four parameters: a pointer to the existing memory block, the old number of elements, the new number of elements, and the size of each element.
- **Use**: This function is used to safely resize an array while ensuring that any newly allocated memory is initialized to zero.


---
### xstrdup
- **Type**: `function pointer`
- **Description**: `xstrdup` is a function that duplicates a given string by allocating memory for the new string and copying the content of the original string into it. It is similar to the standard `strdup` function but is part of a custom memory management library that ensures memory allocation errors are handled gracefully.
- **Use**: `xstrdup` is used to create a duplicate of a string with memory allocation that is checked for errors, ensuring robust memory management.


---
### xstrndup
- **Type**: `function`
- **Description**: `xstrndup` is a function that duplicates a specified number of characters from a given string, returning a pointer to the newly allocated string. It is similar to `strndup`, but is part of a custom memory management library that ensures memory allocation errors are handled gracefully.
- **Use**: This function is used to safely duplicate a portion of a string, ensuring that memory allocation is successful or handled appropriately.


