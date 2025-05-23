# Purpose
This C header file, `xmalloc.h`, provides declarations for a set of memory management and string manipulation functions that enhance standard library functions by incorporating error checking and handling. The functions, such as `xmalloc`, `xcalloc`, `xrealloc`, and their variants, are designed to never return a failure; instead, they invoke a fatal error handler if an error occurs, ensuring robust memory allocation. Additionally, the file includes safer string duplication and formatted output functions like `xstrdup`, `xasprintf`, and `xsnprintf`, which include attributes for format checking and non-null constraints to prevent common errors. This header is part of a larger software project, likely related to secure shell (SSH) development, as indicated by the author's note on usage and compatibility with protocol descriptions.
# Global Variables

---
### xmalloc
- **Type**: `function pointer`
- **Description**: `xmalloc` is a function that acts as a safer version of the standard `malloc` function. It allocates a specified amount of memory and checks the result to ensure that the allocation was successful. If the allocation fails, it calls a fatal error handler instead of returning a null pointer.
- **Use**: `xmalloc` is used to allocate memory dynamically while ensuring that any allocation failure is handled by terminating the program.


---
### xcalloc
- **Type**: `function pointer`
- **Description**: `xcalloc` is a function pointer that represents a custom implementation of the standard `calloc` function. It is designed to allocate memory for an array of elements, each of a specified size, and initializes all bytes in the allocated storage to zero. This function is part of a set of memory allocation functions that ensure memory allocation errors are handled by calling a fatal error function instead of returning failure.
- **Use**: `xcalloc` is used to allocate and zero-initialize memory for an array, ensuring that allocation errors are handled by terminating the program.


---
### xrealloc
- **Type**: `function pointer`
- **Description**: `xrealloc` is a function pointer that points to a function designed to reallocate memory blocks. It takes a pointer to the existing memory block and a size_t value representing the new size of the memory block. This function is part of a set of memory management functions that ensure memory allocation operations do not fail silently, as they call a fatal error handler if an error occurs.
- **Use**: `xrealloc` is used to resize an existing memory block, ensuring that the operation is checked for errors and handled safely.


---
### xreallocarray
- **Type**: `function pointer`
- **Description**: `xreallocarray` is a function pointer that points to a function designed to reallocate memory for an array. It takes three parameters: a pointer to the existing memory block, and two size_t values representing the number of elements and the size of each element, respectively.
- **Use**: This function is used to safely resize an array by reallocating memory, ensuring that the operation does not fail silently.


---
### xrecallocarray
- **Type**: `function pointer`
- **Description**: `xrecallocarray` is a function pointer that points to a function designed to reallocate memory for an array, with the added functionality of zeroing out the newly allocated memory. It takes four parameters: a pointer to the existing memory block, the old number of elements, the new number of elements, and the size of each element.
- **Use**: This function is used to safely resize an array while ensuring that any newly allocated memory is initialized to zero.


---
### xstrdup
- **Type**: `function pointer`
- **Description**: `xstrdup` is a function that duplicates a string by allocating memory for the new string and copying the content of the given string into it. It is a safer version of the standard `strdup` function, as it is part of a set of memory allocation functions that check their results and handle errors by calling a fatal error function if necessary.
- **Use**: This function is used to create a duplicate of a given string with error checking for memory allocation.


---
### xstrndup
- **Type**: `function`
- **Description**: `xstrndup` is a function that duplicates a specified number of characters from a given string, returning a pointer to the newly allocated string. It is similar to the standard `strndup` function but is part of a custom memory management library that ensures memory allocation errors are handled gracefully.
- **Use**: This function is used to safely duplicate a portion of a string, ensuring that memory allocation is successful or handled appropriately.


