# Demo Sodium C hello world

Demonstration of:

  * [Sodium](https://libsodium.org): The Sodium crypto library
  * [C programming language](https://en.wikipedia.org/wiki/C_(programming_language)): a simple program that uses sodium
  * [GCC](https://gcc.gnu.org/): the GNU Compiler Collection


## Get Sodium

Visit https://download.libsodium.org/libsodium/releases/

We prefer getting the latest version.

Download:

```sh
curl -O https://download.libsodium.org/libsodium/releases/LATEST.tar.gz
tar xvzf LATEST.tar.gz
cd libsodium-stable
```

Install:

```sh
./configure
make && make check
sudo make install
```

## Write the demo

Create a file `demo.c` with this C code:

```c
#include <sodium.h>

int main(void)
{
    if (sodium_init() < 0) {
      puts("Sodium library couldn't be initialized, it is not safe to use.");
      exit(1);
    }
    puts("Sodium library is initialized.");
    exit(0);
}
```


## Run the demo

Compile:

```sh
gcc -lsodium demo.c -o demo
```

Run:

```sh
./demo
```

Output:

```sh
Sodium library is initialized.
```


## Generate random data

The `randombytes_buf()` function fills size bytes starting at buf with an unpredictable sequence of bytes.

```c
unsigned int buf_len = 16;
unsigned char buf[buf_len];
randombytes_buf(buf, buf_len);
```

## Format a hexadecimal string

The `sodium_bin2hex()` function converts a byte array into a hexadecimal string with a nul byte (\0) terminator.

```c
unsigned int hex_len = buf_len * 2 + 1;
char hex[hex_len];
sodium_bin2hex(hex, hex_len, buf, buf_len);
puts(hex);
```
