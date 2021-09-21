# rewriter

## Write-up
chall とsrc.cがもらえる
<details><summary>src.c</summary><div>

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <fcntl.h>
#include <unistd.h>
#include <err.h>

#define BUFF_SIZE 0x20

void win() {
    execve("/bin/cat", (char*[3]){"/bin/cat", "flag.txt", NULL}, NULL);
}

void show_stack(unsigned long *stack);

int main() {
    unsigned long target = 0, value = 0;
    char buf[BUFF_SIZE] = {0};
    show_stack(buf);
    printf("Where would you like to rewrite it?\n> ");
    buf[read(STDIN_FILENO, buf, BUFF_SIZE-1)] = 0;
    target = strtol(buf, NULL, 0);
    printf("0x%016lx = ", target);
    buf[read(STDIN_FILENO, buf, BUFF_SIZE-1)] = 0;
    value = strtol(buf, NULL, 0);
    *(long*)target = value;
}

void show_stack(unsigned long *stack) {
    printf("\n%-20s|%-20s\n", "[Addr]", "[Value]");
    puts("====================+===================");
    for (int i = 0; i < 10; i++) {
        printf(" 0x%016lx | 0x%016lx ", &stack[i], stack[i]);
        if (&stack[i] == stack)
            printf(" <- buf");
        if (&stack[i] == ((unsigned long)stack + BUFF_SIZE))
            printf(" <- target");
        if (&stack[i] == ((unsigned long)stack + BUFF_SIZE + 0x8))
            printf(" <- value");
        if (&stack[i] == ((unsigned long)stack + BUFF_SIZE + 0x10))
            printf(" <- saved rbp");
        if (&stack[i] == ((unsigned long)stack + BUFF_SIZE + 0x18))
            printf(" <- saved ret addr");
        puts("");
    }
    puts("");
}

__attribute__((constructor))
void init() {
    setvbuf(stdin, NULL, _IONBF, 0);
    setvbuf(stdout, NULL, _IONBF, 0);
    alarm(60);
}
```
</div></details>

<details><summary>chall</summary><div>

```
./cahll
```

```
[Addr]              |[Value]             
====================+===================
 0x00007ffcfa9148b0 | 0x0000000000000000  <- buf
 0x00007ffcfa9148b8 | 0x0000000000000000 
 0x00007ffcfa9148c0 | 0x0000000000000000 
 0x00007ffcfa9148c8 | 0x0000000000000000 
 0x00007ffcfa9148d0 | 0x0000000000000000  <- target
 0x00007ffcfa9148d8 | 0x0000000000000000  <- value
 0x00007ffcfa9148e0 | 0x0000000000401520  <- saved rbp
 0x00007ffcfa9148e8 | 0x00007f0435c38d0a  <- saved ret addr
 0x00007ffcfa9148f0 | 0x00007ffcfa9149d8 
 0x00007ffcfa9148f8 | 0x0000000100000000 
 ```
</div></details>

challを実行すると、stackの情報が可視化される。
src.cには、win関数がありフラグを表示させている。

ret addrをwin関数のアドレスに書き換えれば、フラグを表示できる。
