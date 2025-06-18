# Purpose
This C header file, `xmalloc.h`, provides declarations for a set of memory allocation and string manipulation functions that enhance standard C library functions by incorporating error checking and handling. The functions, such as [`xmalloc`](#xmalloc), [`xcalloc`](#xcalloc), [`xrealloc`](#xrealloc), and [`xstrdup`](#xstrdup), are designed to never return a failure; instead, they invoke a fatal error handler if an error occurs, ensuring robust memory management. Additionally, the file includes functions like [`xasprintf`](#xasprintf) and [`xsnprintf`](#xsnprintf), which are safer versions of their standard counterparts, with added format string checking and non-null attribute enforcement to prevent common programming errors. The header is part of a larger software project, likely related to secure shell (SSH) development, as indicated by the author's note on usage and compatibility with protocol descriptions.
# Function Declarations (Public API)

---
### xmalloc<!-- {{#callable_declaration:xmalloc}} -->
Allocate memory and handle allocation failures.
- **Description**: This function allocates a block of memory of the specified size and ensures that the allocation is successful. It is used when memory allocation is critical and failure is not an option, as it will terminate the program if the allocation fails or if a zero size is requested. This function is suitable for use in applications where memory allocation errors are considered fatal and should be avoided at all costs.
- **Inputs**:
    - `size`: The number of bytes to allocate. Must be greater than zero. If zero is passed, the function will terminate the program.
- **Output**: A pointer to the allocated memory block. The program will terminate if the allocation fails.
- **See also**: [`xmalloc`](xmalloc.c.driver.md#xmalloc)  (Implementation)


---
### xcalloc<!-- {{#callable_declaration:xcalloc}} -->
Allocate and zero-initialize an array.
- **Description**: This function allocates memory for an array of `nmemb` elements of `size` bytes each and initializes all bytes in the allocated storage to zero. It is designed to ensure that memory allocation is successful, and it will terminate the program if the allocation fails or if either `nmemb` or `size` is zero. This function should be used when you need a guaranteed allocation with zero-initialization, and you want the program to exit on allocation failure.
- **Inputs**:
    - `nmemb`: The number of elements to allocate. Must be greater than zero. If zero, the function will terminate the program.
    - `size`: The size in bytes of each element. Must be greater than zero. If zero, the function will terminate the program.
- **Output**: A pointer to the allocated memory, which is zero-initialized. The program will terminate if allocation fails.
- **See also**: [`xcalloc`](xmalloc.c.driver.md#xcalloc)  (Implementation)


---
### xrealloc<!-- {{#callable_declaration:xrealloc}} -->
Reallocate memory to a new size, ensuring success or terminating the program.
- **Description**: This function is used to resize a previously allocated memory block to a new size. It is particularly useful when the size of the data structure needs to change dynamically. The function guarantees that it will not return a null pointer; instead, it will terminate the program if memory allocation fails. This behavior makes it suitable for applications where memory allocation failures are considered fatal and should not be handled by the caller. It is important to ensure that the pointer passed to the function was obtained from a previous memory allocation function and that the new size is appropriate for the intended use.
- **Inputs**:
    - `ptr`: A pointer to the memory block to be reallocated. It must be a valid pointer obtained from a previous allocation function or null if a new allocation is desired. The caller retains ownership.
    - `size`: The new size for the memory block in bytes. It must be a positive value appropriate for the intended use. If the size is zero, the behavior is implementation-defined, but typically it may free the memory.
- **Output**: A pointer to the reallocated memory block, which is guaranteed to be non-null.
- **See also**: [`xrealloc`](xmalloc.c.driver.md#xrealloc)  (Implementation)


---
### xreallocarray<!-- {{#callable_declaration:xreallocarray}} -->
Reallocate memory for an array, ensuring allocation success.
- **Description**: This function reallocates memory for an array of elements, ensuring that the allocation is successful. It is used when you need to resize an existing memory block pointed to by `ptr` to hold `nmemb` elements, each of size `size`. The function will terminate the program if the allocation fails or if either `nmemb` or `size` is zero, ensuring that the caller does not need to handle these errors. This function is suitable for use in applications where memory allocation failures are considered fatal and should be avoided in contexts where such failures need to be handled gracefully.
- **Inputs**:
    - `ptr`: A pointer to the memory block to be reallocated. It can be NULL, in which case the function behaves like `malloc`. The caller retains ownership.
    - `nmemb`: The number of elements to allocate. Must be greater than zero. If zero, the function will terminate the program.
    - `size`: The size of each element. Must be greater than zero. If zero, the function will terminate the program.
- **Output**: A pointer to the newly allocated memory block, which is guaranteed to be non-NULL.
- **See also**: [`xreallocarray`](xmalloc.c.driver.md#xreallocarray)  (Implementation)


---
### xrecallocarray<!-- {{#callable_declaration:xrecallocarray}} -->
Reallocate and zero-initialize an array, ensuring allocation success.
- **Description**: This function reallocates an array to a new size, ensuring that any newly allocated memory is zero-initialized. It is designed to handle memory allocation failures by terminating the program with an error message, thus guaranteeing that it never returns a null pointer. This function should be used when you need to resize an array and want to ensure that any new elements are initialized to zero. It is important to note that both the number of elements and the size of each element must be non-zero, as the function will terminate the program if either is zero.
- **Inputs**:
    - `ptr`: A pointer to the existing memory block to be reallocated. If this is NULL, the function behaves like a call to calloc(). The caller retains ownership of the memory.
    - `oldnmemb`: The number of elements in the existing memory block. Must be a non-negative value.
    - `nmemb`: The desired number of elements in the new memory block. Must be greater than zero, otherwise the function will terminate the program.
    - `size`: The size of each element in bytes. Must be greater than zero, otherwise the function will terminate the program.
- **Output**: Returns a pointer to the newly allocated memory block, which is guaranteed to be non-null. The new memory block is zero-initialized for any additional space beyond the original size.
- **See also**: [`xrecallocarray`](xmalloc.c.driver.md#xrecallocarray)  (Implementation)


---
### xstrdup<!-- {{#callable_declaration:xstrdup}} -->
Duplicates a string with error handling.
- **Description**: This function creates a duplicate of the given string, ensuring that memory allocation is successful. It is used when a copy of a string is needed and the program cannot continue if memory allocation fails. The function will terminate the program with an error message if it cannot allocate the necessary memory, making it suitable for use in applications where such failures are considered fatal.
- **Inputs**:
    - `str`: A pointer to a null-terminated string that is to be duplicated. Must not be null, as passing a null pointer will result in undefined behavior.
- **Output**: A pointer to the newly allocated string that is a duplicate of the input string.
- **See also**: [`xstrdup`](xmalloc.c.driver.md#xstrdup)  (Implementation)


---
### xstrndup<!-- {{#callable_declaration:xstrndup}} -->
Duplicates a string up to a specified maximum length, ensuring successful allocation.
- **Description**: This function creates a duplicate of the input string, copying at most 'maxlen' characters, and ensures that memory allocation is successful. It is useful when you need a copy of a string with a limited length, and you want to handle allocation failures by terminating the program. The function should be used when the program cannot continue without successfully duplicating the string, as it will call a fatal error handler if memory allocation fails. The caller is responsible for freeing the returned string when it is no longer needed.
- **Inputs**:
    - `str`: The input string to be duplicated. Must not be null, as the function does not handle null pointers.
    - `maxlen`: The maximum number of characters to duplicate from the input string. Must be a non-negative value.
- **Output**: A pointer to the newly allocated string containing up to 'maxlen' characters from the input string, or the entire string if it is shorter than 'maxlen'. The program will terminate if memory allocation fails.
- **See also**: [`xstrndup`](xmalloc.c.driver.md#xstrndup)  (Implementation)


---
### xasprintf<!-- {{#callable_declaration:xasprintf}} -->
Formats a string and allocates memory for it.
- **Description**: This function formats a string according to the specified format and additional arguments, allocating memory to store the resulting string. It is useful when you need a formatted string but do not know the required buffer size in advance. The function ensures that memory allocation is successful, and it will not return a failure. The caller is responsible for freeing the allocated memory. This function must be called with a valid format string, and the format string must not be null.
- **Inputs**:
    - `ret`: A pointer to a char pointer where the address of the allocated string will be stored. Must not be null. The caller is responsible for freeing the allocated memory.
    - `fmt`: A format string as in printf. Must not be null. It specifies how subsequent arguments are converted for output.
    - `...`: Additional arguments that are formatted according to the format string. The number and types of these arguments must match the format specifiers in the format string.
- **Output**: Returns the number of characters printed, excluding the null byte used to end output to strings.
- **See also**: [`xasprintf`](xmalloc.c.driver.md#xasprintf)  (Implementation)


---
### xvasprintf<!-- {{#callable_declaration:xvasprintf}} -->
Formats a string and allocates memory for it, ensuring no failure occurs.
- **Description**: This function formats a string according to the specified format string and variable argument list, allocating memory for the resulting string. It is used when you need to create a formatted string with dynamic content, and it ensures that memory allocation failures are handled by terminating the program. This function should be used when you want to guarantee that a formatted string is created without handling allocation errors manually. It is important to note that the function will not return on failure, as it calls a fatal error handler instead.
- **Inputs**:
    - `ret`: A pointer to a char pointer where the address of the allocated string will be stored. Must not be null. The caller is responsible for freeing the allocated memory.
    - `fmt`: A format string that specifies how to format the variable arguments. Must not be null.
    - `ap`: A va_list representing the variable arguments to format according to the format string. It should be initialized before calling this function.
- **Output**: Returns the number of characters printed (excluding the null byte used to end output to strings) or a negative value if an error occurs. However, the function will terminate the program on allocation failure, so a negative return value is not expected.
- **See also**: [`xvasprintf`](xmalloc.c.driver.md#xvasprintf)  (Implementation)


---
### xsnprintf<!-- {{#callable_declaration:xsnprintf}} -->
Formats a string and stores it in a buffer with size checking.
- **Description**: This function formats a string according to the specified format string and stores the result in the provided buffer. It is similar to snprintf but includes additional safety checks. The function ensures that the formatted string does not exceed the specified buffer length, preventing buffer overflows. It must be called with a valid format string and a buffer that is large enough to hold the resulting formatted string. The function is designed to handle variable argument lists, making it flexible for various formatting needs.
- **Inputs**:
    - `str`: A pointer to the buffer where the formatted string will be stored. The buffer must be large enough to hold the resulting string, including the null terminator. The caller retains ownership and must ensure it is not null.
    - `len`: The size of the buffer pointed to by str. It defines the maximum number of characters to be written, including the null terminator.
    - `fmt`: A format string that specifies how to format the subsequent arguments. It must not be null and should follow printf-style formatting.
    - `...`: A variable number of arguments that are formatted according to the format string. The types and number of these arguments must match the format specifiers in fmt.
- **Output**: Returns the number of characters that would have been written if the buffer had been sufficiently large, not counting the terminating null character. If the return value is greater than or equal to len, the output was truncated.
- **See also**: [`xsnprintf`](xmalloc.c.driver.md#xsnprintf)  (Implementation)


---
### xvsnprintf<!-- {{#callable_declaration:xvsnprintf}} -->
Formats a string into a buffer using a variable argument list.
- **Description**: This function formats a string according to a specified format and stores the result in a provided buffer. It is used when you have a variable argument list that needs to be formatted into a string. The function ensures that the formatted string does not exceed the specified buffer length, and it will terminate the program if an overflow is detected or if the length exceeds INT_MAX. This function is useful in scenarios where you need to safely format strings with variable arguments, ensuring that buffer overflows are avoided.
- **Inputs**:
    - `str`: A pointer to the buffer where the formatted string will be stored. The buffer must be large enough to hold the resulting string, including the null terminator.
    - `len`: The maximum number of bytes to be written to the buffer, including the null terminator. Must not exceed INT_MAX.
    - `fmt`: A format string that specifies how to format the variable arguments. Must not be null.
    - `ap`: A va_list representing the variable arguments to be formatted according to the format string.
- **Output**: Returns the number of characters that would have been written if the buffer had been sufficiently large, not counting the terminating null character. If the return value is negative or greater than or equal to len, the function will terminate the program.
- **See also**: [`xvsnprintf`](xmalloc.c.driver.md#xvsnprintf)  (Implementation)


