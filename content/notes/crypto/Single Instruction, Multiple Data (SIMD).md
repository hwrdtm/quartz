---
title: Single Instruction, Multiple Data (SIMD)
---
SIMD is a type of parallel processing, allowing machines to exploit data level parallelism, but not concurrency. There are simultaneous, parallel computations, but each unit performs the exact same instruction at any given moment, just with different data.

SIMD is particularly applicable to common tasks such as adjusting the contrast in a digital image or adjusting the volume of digital audio.

Performance
- Most modern CPU designs include SIMD instructions for performance
	- For example, if you have a SIMD instruction that adds two vectors of numbers, the processor can add corresponding elements of the vectors simultaneously.
- **Vectorization**: SIMD instructions often work with vectors of data, allowing the processor to perform operations on multiple elements of a vector with a single instruction. This is known as vectorization. Vectorized operations can significantly improve throughput by processing multiple data elements in a single clock cycle.
- **Specialized Registers**: SIMD-capable processors have specialized registers, called SIMD registers, that can hold multiple data elements at the same time. These registers are wider than traditional scalar registers, allowing for the storage of multiple values.

# Resources

https://en.wikipedia.org/wiki/Single_instruction,_multiple_data