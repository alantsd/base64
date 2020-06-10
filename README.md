# Base64

Base64 is a C library to convert from plain to base64 and vice versa suitable for embedded systems.
Optimized for less ROM usage for microcontroller.

Typical size of using gcc version 6.3.1 20170215 (release) [ARM/embedded-6-branch revision 245512] (GNU Tools for ARM Embedded Processors (Build 17.0)) 

```C
text    data     bss     dec     hex filename
 521       0       0     521     209 arm_build\base64_lib.o
 ```

# API

 * Get size required for encoding base64 null-terminated string.
 * @param size Size in bytes of source binary memory block.
 * @return A size of required for result of base64 encoding 

```C
int bintob64_size(int size);
```

 * Get size required for decoding base64 null-terminated string.
 * @param size Size in bytes of source base64 memory block.
 * @return A size of required for result of base64 decoding 

```C
int b64tobin_size(int size);
```
* The parameter 'src' is the source memory block to be converted.
* The parameter 'size' is the size in bytes of the source memory block.
* The parameter 'dest' is the destination buffer where the translation to base64 is stored. Also a null character is added at the end to become a null-terminated string.
* The return value is a pointer to the null character.

To convert from base64 to plain the following function is used:
```C
void* b64tobin( void* dest, char const* src );
```
* The parameter 'src' is the source base64 string. It must be terminated in a non base64-digit. A null-terminated string is OK.
* The parameter 'dest' is the destination memory block where the result of convertion is stroed.
* The return value is a null pointer if the base64 string has bad format. If the convertion is successfully the return value is a pointer to the end of the convertion. With this pointer you can get the length of the result.

Convert from base64 to plain in the same memory block is possible using the previous function by setting the same pointer for the destination and source. Or just use the following wrapper function:
```C
static inline void* b64decode( void* p ) {
    return b64tobin( p, (char*)p );
}
```
