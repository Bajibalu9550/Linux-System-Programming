# 🛠️ System I/O Calls in Linux (Low-Level I/O)

System I/O calls are **unbuffered, low-level input/output** functions provided by the Linux operating system. These calls work directly with file descriptors and are defined in headers like `<unistd.h>` and `<fcntl.h>`.

They are **closer to the OS kernel**, used in systems programming, device drivers, and performance-critical tasks.

---

## 📄 Key Characteristics

- **Unbuffered**: Each read/write goes directly to hardware or OS.
- **File Descriptor-based**: Uses `int` instead of `FILE*`.
- **Faster** but **less convenient** than stdio.
- **Not portable** across all systems (POSIX/Linux specific).

---

## 🔧 System I/O Functions and Descriptions

| Function   | Header        | Description                                      |
|------------|---------------|--------------------------------------------------|
| `open()`   | `<fcntl.h>`   | Open or create a file, returns file descriptor  |
| `read()`   | `<unistd.h>`  | Reads data from a file descriptor               |
| `write()`  | `<unistd.h>`  | Writes data to a file descriptor                |
| `close()`  | `<unistd.h>`  | Closes a file descriptor                        |
| `lseek()`  | `<unistd.h>`  | Moves file offset (like file pointer)           |
| `dup()`    | `<unistd.h>`  | Duplicates a file descriptor                    |
| `dup2()`   | `<unistd.h>`  | Duplicates to a specific file descriptor        |
| `pipe()`   | `<unistd.h>`  | Creates a unidirectional pipe                   |
| `fcntl()`  | `<fcntl.h>`   | Performs operations on file descriptors         |

---



```c
📘 open()

#include <fcntl.h>


int fd = open("file.txt", O_RDONLY); // Read-only
int fd2 = open("new.txt", O_WRONLY | O_CREAT, 0644);

Returns -1 on failure
Third argument (permissions) needed if file is created

 📘 read()

#include <unistd.h>

char buf[100];
int bytes = read(fd, buf, sizeof(buf));
Reads up to sizeof(buf) bytes from fd into buf

Returns number of bytes read,
or -1 on error

📘 write()

#include <unistd.h>

write(fd, "Hello", 5);
Writes 5 bytes to file descriptor fd

📘 close()

#include <unistd.h>

close(fd);
Releases the file descriptor

Always close unused descriptors to prevent leaks

📘 lseek()

#include <unistd.h>

off_t pos = lseek(fd, 0, SEEK_END); // Move to end
Moves file offset

SEEK_SET, SEEK_CUR, SEEK_END used for positioning

🧪 Complete Example: Writing to File Using System I/O

#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>

int main() {
    int fd = open("example.txt", O_WRONLY | O_CREAT, 0644);
    if (fd < 0) {
        perror("open");
        return 1;
    }

    const char *msg = "System I/O Example\n";
    write(fd, msg, 20);
    close(fd);

    return 0;
}
