# Dynamic Memory Allocator
A simple explict allocator package based on implicit list.

It's an application for learning about ***Virtual Memory*** and ***Dynamic memory Allocation***.

## Overview
A dynamic memory allocator maintains an area of a process's virtual memory known as ***heap***. It's used to acquire additional virtual memory at run time.

## Implementation issues
1. **Block format**
    - A block consists of a one-word header, the payload, possibly some additional padding and a one-word boundary-tag (footer). The minimum block size is 16 bytes. The header encodes the block size as well as whether the block is allocated or not.
2. **Free list format**
    - The allocator maintains an ***implicit free list*** to keep track of free blocks. The first word of the free list is an unused padding word aligned to a double-word boundary. The padding is followed by a special 8-bytes-allocated ***prologue*** block, followed by a zero or more regular blocks that are created by calls to ***malloc*** or ***free***. The heap always ends with a special ***epilogue*** block, which is a zero-size allocated block that consists of only a header.
3. **Placement policy**
    - The allocator searches the free list for a free block that is large enough to hold the requested block using ***Next fit*** algorithm.
4. **Splitting policy**
    - After placing the requested block in some free block, The allocator splits the block if the remainder would be equal to or greater than the ***minimum block size***.
5. **Coalescing policy**
    - The allocator uses ***immediate boundary-tag*** coalescing, that it merges next and previous free blocks with the current block each time an applications calls ***free()*** on this current block.

## Files
- `mm.{c,h}`: The package implementation
- `memlib.{c,h}`: A module that simulates the memory system

## Thoughts
- The project helped me understand different memory allocation techniques and how memory allocators work.
- I learned about virtual memory, and how virtual memory is mapped to physical memory (Address Translation).
