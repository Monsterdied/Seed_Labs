# LogBook4

## Identificação
### Taks 1

- Usar printenv permite listar todas as variaveis de ambiente
- Usar export adicionar variaveis de ambiente e unset remove variaveis de ambiente
### **Terminal**
![terminal_of_print_env](/Images/printenv.png)

### Task 2
- Começamos por compilar e rodar o código que nos dá as variaveis do child process e guardamos num ficheiro

![dependencies](/Images/week4-task2-0.png)

- De Seguida modificamos o codigo para nos dar as variaveis do Parent process e guardamos num ficheiro diferente

![dependencies](/Images/week4-task2-1.png)

- Por fim comparamos os dois ficheiros com o codigo diff

![dependencies](/Images/week4-task2-2.png)

- Como observamos os ficheiros são iguais assim as variaveis de ambiente do child são herdadas do pai

### Task 3

- envp é um array de pointers para string , convencionalmente da forma chave = value, que são passados como ambiente do novo programa. Se envp é null as variaveis de ambiente do programa anterior não serão passadas para o excve não tendo variaveis de ambiente para representar quando o comando correr.
#### **myenv**
```c
#include <unistd.h>
extern char **environ;
int main()
{
char *argv[2];
argv[0] = "/usr/bin/env";
argv[1] = NULL;
execve("/usr/bin/env", argv, environ); ➀
retur
```

#### **Terminal**
![diferences_of_execev](/Images/diference_from_execev.png)
### Task 4

- quando executamos o codigo mysyms.c verificamos que são passadas as variaveis de ambiente do processo anterior pois o system cria um novo processo que vai buscar as variaveis a execução do system difere da execução do mesmo comando com o excve.
- ja a task anterior utiliza o para executar excve() utiliza as variaveis de anbiente do processo atual se forem fornecidas como argumento na sua execução.
#### **mysyms.c**
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    system("/usr/bin/env");
    return 0 ;
}

```
#### **Terminal**
![dependencies](/Images/terminal_mysysms.png)



### Task 5 

-  Quando se altera o PATH variable, a maior parte das funcões do terminal para de funcionar ate que se volte a dar set do PATH correto.

![dependencies](/Images/print1.png)


- Depois de repor as variáveis de ambiente, as funções do terminal 
voltaram a funcionar


![dependencies](/Images/print2.png)

![dependencies](/Images/Captura_de_ecrã_2023-10-11_232522.png)

-   Quando se adicionam as variáveis de ambiente ANY e quando se altera a variável de ambiente PATH elas aparecem quando nós utilizamos o código da task2 mas quando se adiciona a variável LD_LIBRABRY_PATH ela não aparece, mas quando se utiliza o codigo printenv encontra-se a variável que criamos com o respetivo path. 


![dependencies](/Images/Captura_de_ecrã_2023-10-11_232303.png)

- Pois o printenv roda no processo em que criamos a nova variável de ambiente enquanto que o cdigo da task2 roda num child da root que vai buscar as variaveis de ambiente ao root e no root não se pode adicionar/alterar esta variável de ambiente LD_LIBRABRY_PATH pois esta variavel de ambiente é utilizada para apontar para bibliotecas dinamicas partilhadas o que iria possibilitar a execução de um programa malizioso com a sua alteração

![dependencies](/Images/print3.png)


### Task6

![dependencies](/Images/print4.png)

- Para fazer a função correr a minha função ls, nós alteramos o path para Desktop/new_env onde criei um código em c que dá print hacked depois de compilado com o nome ls.

![dependencies](/Images/print5.png)

- Depois de executado ele utiliza o meu ls pois o linux procura a função ls e encontra a minha antes da outra devido à prioridade do path que nós colocamos.



