# 📘 Standard I/O vs System I/O in C

---

## ✅ What is Standard I/O in C?

Standard I/O functions are part of the C Standard Library (`<stdio.h>`). These functions work with `FILE*` and provide **buffered** input/output. They are portable, easy to use, and high-level.

---

## 🔧 Standard I/O Function Table

| Function     | Description                                 | Example Use                  |
|--------------|---------------------------------------------|------------------------------|
| `fopen()`    | Opens a file                                | `FILE *fp = fopen("a.txt","r");` |
| `fclose()`   | Closes a file                               | `fclose(fp);`                |
| `fgetc()`    | Reads a single character from a file        | `ch = fgetc(fp);`            |
| `fputc()`    | Writes a character to a file                | `fputc('A', fp);`            |
| `fgets()`    | Reads a line from a file                    | `fgets(buf, 100, fp);`       |
| `fputs()`    | Writes a string to a file                   | `fputs("Hello", fp);`        |
| `fprintf()`  | Writes formatted data to a file             | `fprintf(fp, "%d", 10);`     |
| `fscanf()`   | Reads formatted data from a file            | `fscanf(fp, "%d", &n);`      |
| `fread()`    | Reads binary data                           | `fread(&x, sizeof(x), 1, fp);` |
| `fwrite()`   | Writes binary data                          | `fwrite(&x, sizeof(x), 1, fp);` |
| `fseek()`    | Sets the file position indicator            | `fseek(fp, 0, SEEK_END);`    |
| `ftell()`    | Returns the current file position           | `long pos = ftell(fp);`      |
| `rewind()`   | Sets position to beginning of file          | `rewind(fp);`                |
| `fflush()`   | Flushes output buffer to file               | `fflush(fp);`                |

---

## 🧪 Example: Standard I/O

```c
#include <stdio.h>

int main() {
    FILE *fp = fopen("test.txt", "w");
    if (fp == NULL) {
        perror("Error opening file");
        return 1;
    }

    fputs("Hello, Baji!\n", fp);
    fclose(fp);
    return 0;
}
