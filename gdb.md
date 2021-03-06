## Using GDB

GDB is GNU Debugger. To debug a C program. First we need to compile with -g flag so that the compiled version will provide debug information. See the example below.

Source code:
```
# hello.c
#include<stdio.h>

void printMessage(char msg[]) {
  printf("Hello %s\n", msg);
}

int main() {
  char msg[] = "jon";
  printMessage(msg);
  char goodbye[] = "bye";
  printf("Program is completed, %s\n", goodbye);
}
```

Let's compile with gcc -g:
```
gcc -g hello.c
```

Then start gdb and pass the program in the gdb arguments:
```
gdb a.out # a.out is the compiled hello.c
```

gdb will start, printing the license information and a message about symbol table and ends with `(gdb)` prompt that indicates gdb interactive session prompt:
```
Reading symbols from /home/lamida/ss/a.out...done.
(gdb)
```

The most obvious command in gdb is to just run the probram by typing run:
```
(gdb) run
Starting program: /home/lamida/ss/a.out 
Hello jon
Program is completed, bye
[Inferior 1 (process 2781) exited with code 032]
(gdb) 
```

To set a break point use break with file name and line argument. If we run the program again it will stop in that break point:
```
(gdb) break hello.c:8
Breakpoint 1 at 0x8048465: file hello.c, line 8.
(gdb) run
Starting program: /home/lamida/ss/a.out 

Breakpoint 1, main () at hello.c:8
8	  char msg[] = "jon";
(gdb)
```

We can either continue:
```
(gdb) continue
Continuing.
Hello jon
Program is completed, bye
[Inferior 1 (process 2849) exited with code 032]
(gdb)
```

Or step (we need to run the program again):
```
(gdb) run
Starting program: /home/lamida/ss/a.out 

Breakpoint 1, main () at hello.c:8
8	  char msg[] = "jon";
(gdb) step
9	  printMessage(msg);
(gdb) step
printMessage (msg=0xbffff334 "jon") at hello.c:4
4	  printf("Hello %s\n", msg);
(gdb) step
Hello jon
5	}
(gdb) step
main () at hello.c:10
10	  char goodbye[] = "bye";
(gdb) step
11	  printf("Program is completed, %s\n", goodbye);
(gdb) step
Program is completed, bye
12	}
(gdb) step
0xb7e394e3 in __libc_start_main () from /lib/i386-linux-gnu/libc.so.6
(gdb)
```

Alternatively, we also can set breakpoint using filename and function name:
```
(gdb) break hello.c:printMessage
Breakpoint 3 at 0x804843a: file hello.c, line 4.
(gdb)
```

Or just function name:
```
(gdb) break printMessage
Breakpoint 4 at 0x804843a: file hello.c, line 4.
(gdb)
```

To delete breakpoint, we can use clear command and the argument that we use to set the breakpoint, e.g. either of filename:line, filename:function, function.
```
(gdb) clear printMessage
Deleted breakpoints 4 5 
(gdb)
```

With breakpoint set we can inspect variables value during breakpoint using print.
```
(gdb) run
Starting program: /home/lamida/ss/a.out 

Breakpoint 1, main () at hello.c:8
8	  char msg[] = "jon";
(gdb) print msg
$1 = "\000\000\000"
(gdb) next
9	  printMessage(msg);
(gdb) print msg
$2 = "jon"
(gdb)
```

To inspect stack frame, we can use these commands:
* info frame: info about the frame
* info args: info about arguments
* info locals: info about local variables

To demonstrate stack frame inspection, let's restart the gdb session and set breakpoint in the printMessage function:
```
(gdb) break printMessage
Breakpoint 1 at 0x804843a: file hello.c, line 4.
(gdb) run
Starting program: /home/lamida/ss/a.out 

Breakpoint 1, printMessage (msg=0xbffff334 "jon") at hello.c:4
4	  printf("Hello %s\n", msg);
(gdb) info frame
Stack level 0, frame at 0xbffff320:
 eip = 0x804843a in printMessage (hello.c:4); saved eip 0x8048479
 called by frame at 0xbffff350
 source language c.
 Arglist at 0xbffff318, args: msg=0xbffff334 "jon"
 Locals at 0xbffff318, Previous frame's sp is 0xbffff320
 Saved registers:
  ebp at 0xbffff318, eip at 0xbffff31c
(gdb) info args
msg = 0xbffff334 "jon"
(gdb) info locals
No locals.
(gdb)
```
