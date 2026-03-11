+++
title = "Tiered-Latency DRAM"
[extra]
bio = """ """
[[extra.authors]]
name = "Brian Castellon Rosales"
[[extra.authors]]
name = "Jared Ho"
[[extra.authors]]
name = "Samuel Shaaban"
+++

# Introduction
Modern computing systems frequently face tradeoffs between available memory capacity and CPU resources. When memory becomes scarce, operating systems often resort to swapping pages to disk, which can significantly degrade performance due to high latency of disk I/O. As a result, reducing or delaying swap activity is an important goal for maintaining system performance under memory pressure.

One approach to improve this issue is compressed memory, where pages are compressed and stored in RAM rather than being immediately written to disk. Linux provides this capability through zswap, a compressed cache that stores swapped pages in memory before they reach disk. By compressing memory pages, zswap can effectively increase the usable memory capacity of the system and reduce the number of disk accesses.

The goal of our project was to explore whether compression settings could be adaptively adjusted based on system conditions to improve performance during periods of high memory pressure. In particular, we focused on the tradeoff between CPU utilization and compression effectiveness. Compression can reduce memory usage and delay swapping, but it also consumes CPU resources. Determining how to balance these competing demands is a key systems design challenge.

We developed a controller that monitors system metrics such as CPU usage, memory pressure, and swap activity, and dynamically adjusts compression behavior in response to changing conditions. Through controlled experiments using synthetic memory workloads, we evaluated how compression affects system behavior and how effectively it can reduce swap activity while managing CPU overhead.

# Background
When a system experiences memory pressure, the OS may move memory pages to disk through a process called swapping. While swapping allows programs to continue running when RAM is exhausted, it introduces significant performance overhead because disk access is much slower than memory access. To improve this, modern OS employ techniques designed to reduce the amount of memory written to disk.

One such mechanism in Linux is zswap, a compressed cache that sits in front of the swap device. Instead of immediately writing pages to disk, zswap first compresses them and stores them in a compressed memory pool in RAM. If the compressed pool becomes full, only then are pages written to disk. By compressing pages in memory, zswap can effectively increase the usable capacity of RAM and reduce the frequency of disk swaps

However, compression introduces its own tradeoffs. Compressing and decompressing memory pages consumes CPU time, and different compression algorithms offer different balances between speed and compression effectiveness. Fast algorithms such as LZO minimize CPU overhead but provide lower compression ratios, while algorithms such as ZSTD achieve higher compression ratios at the cost of greater CPU usage.

The challenge is determining when and how aggressively compression should be applied. If compression starts too late, the system may still resort to disk swapping. If compression is too aggressive, it may consume excessive CPU resources and degrade overall performance. Our project explores how system metrics such as CPU utilization and memory pressure can be used to guide compression decisions in order to reduce swap activity while maintaining efficient CPU usage.

# Design and Implementation


# Evaulation


# Challenges


# Future Work

# Conclusion

# References
*  https://www.kernel.org/doc/html/latest/admin-guide/mm/zswap.html
*  https://facebook.github.io/zstd/
*  https://www.oberhumer.com/opensource/lzo/
*  https://lz4.org/
*  https://man7.org/linux/man-pages/man7/cgroups.7.html
