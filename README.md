# Multithreaded Log Search Engine (C++)

A multithreaded log search tool for large log files (100MB+), inspired by grep.

## Features
- Byte-range chunked file scanning
- Correct handling of line boundaries
- Parallel scanning with 1–8 worker threads
- Thread-local result aggregation
- Benchmarking support

## How it works
- File is split into byte ranges
- Each range is scanned independently
- Chunk reads overlap slightly to avoid missing boundary lines
- Lines are emitted only by their owning chunk to avoid duplicates

## Build & Run
g++ -O2 main.cpp -o logsearch
./logsearch

## Benchmark Results (200MB log)

| Threads | Time (ms) |
|--------:|----------:|
| 1       | 3481      |
| 2       | 2288      |
| 4       | 1320      |
| 8       | 1057      |

Observed diminishing returns beyond 4 threads due to disk I/O limits.


## Notes
Speedup plateaus after 4–8 threads due to disk I/O bottlenecks.
