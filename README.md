# FAT File System Simulator

A C-based academic simulation of a **File Allocation Table (FAT)-style file system**. The program creates a small virtual memory space, divides it into fixed-size blocks, tracks occupied/free blocks, and lets the user create, load, inspect, print, and delete files through a command-line menu.

## Overview

The simulator allocates **500 bytes of virtual memory** and divides that memory into **10 blocks of 50 bytes each**. Files are mapped to one or more blocks, while in-memory tables track file names, sizes, block counts, and block addresses.

The project demonstrates operating-system concepts such as:

- File allocation
- Fixed-size memory blocks
- Free-space tracking
- File metadata
- Allocation/deallocation
- Logical-to-physical block mapping

## Features

The interactive menu supports:

1. **Open/load a text file** into simulated virtual memory
2. **Delete a file** and release its occupied blocks
3. **Print a stored file** from its allocated blocks
4. **Display the FAT/file table**
5. **Display block allocation details**
6. **Create a FAT file** and optionally write text into it
7. **Exit**

## How it works

```text
500-byte virtual memory
        │
        ▼
10 blocks × 50 bytes
        │
        ├── Block 1 ── free / occupied
        ├── Block 2 ── free / occupied
        ├── ...
        └── Block 10 ─ free / occupied

File metadata
  ├── filename
  ├── size
  ├── number of required blocks
  └── addresses of allocated blocks
```

When a file is loaded, the program:

1. Measures the file size.
2. Calculates the number of 50-byte blocks required.
3. Checks whether enough simulated memory remains.
4. Finds free blocks.
5. Copies the file contents into those blocks.
6. Stores the allocated block numbers in the file's address table.

Deleting the file marks those blocks as free again and returns the corresponding capacity to the available-memory counter.

## Repository structure

```text
FAT-File-System-/
├── file.c       # FAT / virtual-memory simulator
├── .gitignore
└── README.md
```

## Build and run

Using GCC:

```bash
gcc file.c -o fat-simulator
./fat-simulator
```

On Windows:

```bash
gcc file.c -o fat-simulator.exe
fat-simulator.exe
```

The program expects text files referenced through the CLI to exist in the working directory.

## Key implementation details

- Dynamic allocation creates the 500-byte memory buffer.
- `block[]` stores block starting addresses.
- `empty[]` tracks whether each block is free or occupied.
- `address[]` stores each file's allocated block list.
- `name[][]` and `s_b[][]` store basic file metadata.
- Allocation and deletion update the remaining-memory counter.

## Educational purpose

This project is a **simplified simulation**, not a disk-level implementation of Microsoft's FAT12/FAT16/FAT32 formats. It focuses on illustrating the idea behind block allocation and a file-allocation table within a small in-memory model.

## Limitations

- Fixed 500-byte simulated memory
- Fixed 50-byte block size
- Fixed maximum table sizes
- Command-line interface only
- No persistence of the simulated FAT between program runs
- Minimal input/error handling

## Possible improvements

- Use structs to model files and FAT entries explicitly
- Support configurable memory and block sizes
- Add fragmentation statistics
- Persist the virtual disk to a binary file
- Add file replacement and append operations
- Add unit tests for allocation/deallocation behavior
- Improve boundary and input validation

## Tech stack

- **Language:** C
- **Concepts:** operating systems, file allocation, memory management, dynamic memory, file I/O

---

Built as an Operating Systems project to demonstrate how files can be mapped onto fixed-size storage blocks and tracked through allocation metadata.
