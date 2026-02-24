# Mini-LSM

This is a study log following the [mini-lsm](https://skyzh.github.io/mini-lsm/00-preface.html) course written in [Rust](https://rust-lang.org/). However, I'm doing it in Kotlin — without any external libraries, purely from scratch.
Anyway, this is what we'll be building.

![mini-lsm-overview](/images/20260222SUN/mini-lsm-overview.png)

Regretting it already? You'll probably dip your toes in and give up, right?

## LSM Overview

LSM storage generally consists of the following three parts:

- Write-Ahead Log (WAL), which writes temporary data to disk for crash recovery
- SSTs that maintain the LSM tree structure on disk
- Memtable, an in-memory structure that batches small writes

The provided interface is as follows:

- `Put(key, value)`: Store a key-value pair in the LSM tree
- `Delete(key)`: Delete a key and its corresponding value
- `Get(key)`: Look up the value for a given key
- `Scan(range)`: Retrieve key-value pairs within a range

Durability interface:

- `Sync()`: Guarantees that all operations before Sync have been written to disk

## Write Path

![mini-lsm-overview](/images/20260222SUN/write-path.png)

The LSM write path consists of four stages:
1. Write the key-value pair to the WAL so the storage engine can recover after a crash.
2. Write the key-value pair to the memtable. Once (1) and (2) are complete, we can acknowledge the write to the user.
3. (Background task) When the memtable is full, freeze it as an immutable memtable and flush it to disk as an SST file.
4. (Background task) Compact files from some levels into lower levels to maintain the LSM tree shape and reduce read amplification.

Here, read amplification refers to how many actual disk/memory accesses are needed to perform a single logical read (`Get(key)`). Obviously, fewer is better.

## Read Path

![mini-lsm-overview](/images/20260222SUN/read-path.png)

When reading a key:
- First, probe all memtables from newest to oldest
- If the key is not found there, search the entire LSM tree composed of SSTs

There are two types of reads:
- Lookup: Finding a single key in the LSM tree
- Scan: Iterating over all key-value pairs within a given range in the storage engine
