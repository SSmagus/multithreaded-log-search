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

## Benchmark (200MB log)
Threads: 1 | Matches: 678690 | Time: 3481 ms
Threads: 2 | Matches: 678690 | Time: 2288 ms
Threads: 4 | Matches: 678690 | Time: 1320 ms
Threads: 8 | Matches: 678690 | Time: 1057 ms

## Notes
Speedup plateaus after 4–8 threads due to disk I/O bottlenecks.
