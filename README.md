# OS-Project-3

Ruben Osornio
CS3113

Producer-Consumer Problem Using Semaphores

Project Description
This program implements the Producer-Consumer Problem using threads and semaphores in C. It demonstrates how to safely share a limited-size circular buffer between two threads (producer and consumer) by ensuring proper synchronization and mutual exclusion.

The producer thread reads characters from an input file (mytest.dat) and places them into a circular buffer of size 15. The consumer thread reads characters from the buffer and prints them to the screen, one character at a time, with a 1-second delay between each read.

The program also ensures correct handling of the end-of-file (EOF) condition using a special marker (*).

How to Compile and Run
1. Prerequisites
A Linux-based system with gcc installed.
Access to the provided VM (for testing).
Ensure the input file mytest.dat exists in the same directory as the program.
2. File Setup
Place the following files in the same directory:
project3.c (this source code file).
mytest.dat (input file with characters to be processed).
Example content of mytest.dat:
kotlin
Copy code
Hello, this is a test for the producer-consumer problem!
3. Compile the Program
Use the following gcc command to compile the program:

gcc project3.c -lpthread -lrt -o project3

Flags:
-lpthread: Links the POSIX threading library.
-lrt: Links the real-time library for semaphore functions.
-o project3: Specifies the output executable name.
5. Run the Program
Execute the compiled program:
./project3
5. Expected Output
The program will read the characters from mytest.dat and print them to the screen, one by one, with a 1-second delay between each character. For example:
Hello, this is a test for the producer-consumer problem!
Program completed successfully.
Features
Circular Buffer:
A fixed-size buffer of 15 positions is used to share data between threads.
Synchronization:
Semaphores ensure safe sharing of the buffer between the producer and consumer threads.
End-of-File Marker:
The producer signals the end of data with a special character (*), ensuring the consumer stops correctly.
Consumer Delay:
The consumer thread runs slower than the producer by introducing a 1-second delay between reads.
Implementation Details
Semaphores
sem_items: Tracks the number of items in the buffer.
sem_space: Tracks available space in the buffer.
sem_mutex: Ensures mutual exclusion when accessing the buffer.
Threads
Producer Thread:
Reads characters from mytest.dat.
Writes each character to the circular buffer.
Signals EOF with the * marker.
Consumer Thread:
Reads characters from the buffer.
Prints each character to the screen with a 1-second delay.
Stops when the EOF marker is encountered.
Error Handling
The program checks if mytest.dat exists and handles the error gracefully:
if (!fp) {
    perror("Failed to open file");
    pthread_exit(NULL);
}

Performance Evaluation
Execution Time:
real	0m57.009s
user	0m0.000s
sys	0m0.006s

Behavior Analysis:

2. Verify that the producer finishes writing before the consumer completes reading.
Ensure no data loss or duplication occurs in the buffer.

Troubleshooting
Compilation Errors:

Ensure the gcc command includes the correct flags (-lpthread and -lrt).
Check for typos in the filename or function calls.
Runtime Errors:

Verify that mytest.dat exists and contains valid data.
Ensure permissions to read/write files in the directory.
No Output:

Confirm that the producer is writing to the buffer and the consumer is processing data.
Check semaphore initialization and thread creation.
<img width="524" alt="Screenshot 2024-11-22 at 5 14 07 PM" src="https://github.com/user-attachments/assets/62d59d1b-7807-47a2-9161-f53a87a7afac">
