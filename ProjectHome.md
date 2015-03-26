# PCMSIM #

A block device driver for Linux that simulates the presence of a Phase Change Memory (PCM), a type of a non-volatile (persistent) byte-addressable memory (NVBM), in the system installed in one of the DIMM slots on the motherboard. The simulator is implemented as a kernel module for Linux that creates `/dev/pcm0` when it is loaded - a ramdisk-backed block devices with latencies that of PCM.

We have designed pcmsim to have minimal overhead, so that the users can run benchmarks in real time. pcmsim accounts for the differences between read and write latencies, and the effects of CPU caches, but it is by no means a complete system simulation. The current implementation only partially accounts for prefetching in the CPU and for memory-level parallelism.

Please beware that a bunch of configuration is currently hard-coded in memory.c and module.c, separately for 32-bit and 64-bit systems (separated using the LP64 macro). Please refer to README.txt about what you need to change, so that you get meaningful results. I would also recommend that you run your benchmarks with disabled swap, so that your simulated PCM device would not be swapped out while you are using it.

Lastly, the pcmsim kernel module has been tested only on selected 2.6.x kernels; it still needs to be ported to 3.x kernels. If you fix any of these issues, please send me your patches, and I'll be happy to merge them!