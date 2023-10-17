# LogBook4

## Identificação
### Taks 1
```
    printenv
```

### Task 2
- começamos por compilar e rodar o código que nos dá as variaveis do child process e guardamos num ficheiro

- Os ficheir são iguais pois ambos os processos são executados no mesmo ambiente, pois as variaveis de ambiente são gerdadas do processo anterior.

### Task 3

- envp é um array de pointers para string , convencionalmente da forma chave = value, que são passados como ambiente do novo programa. Se envp é null não há variáveis de ambiente.

### Task 4

- Foi feito o que foi pedido.

### Task 5 

-  Quando se altera o PATH variable, a maior parte das funcões do terminal para de funcionar ate que se volte a dar set do PATH correto.

![dependencies](/Images/print1.png)


- Depois de repor as variáveis de ambiente, as funções do terminal 
voltaram a funcionar


![dependencies](/Images/print2.png)

![dependencies](/Images/Captura_de_ecrã_2023-10-11_232522.png)

-   Quando se adicionam as variáveis de ambiente ANY e quando se altera a variável de ambiente PATH elas aparecem quando nós utilizamos o código da task2 mas quando se adiciona a variável LD_LIBRABRY_PATH ela não aparece, mas quando se utiliza o codigo printenv encontra-se a variável que criamos com o respetivo path. 


![dependencies](/Images/Captura_de_ecrã_2023-10-11_232303.png)

- Pois o printenv roda no processo em que criamos a nova variável de ambiente enquanto que o cdigo da task2 roda num child da root que vai buscar as variaveis de ambiente ao root e no root não se pode adicionar/alterar esta variável de ambiente LD_LIBRABRY_PATH

![dependencies](/Images/print3.png)


### Task6

![dependencies](/Images/print4.png)

- Para fazer a função correr a minha função ls, nós alteramos o path para Desktop/new_env onde criei um código em c que dá print hacked depois de compilado com o nome ls.

![dependencies](/Images/print5.png)

- Depois de executado ele utiliza o meu ls pois o linux procura a função ls e encontra a minha antes da outra devido à prioridade do path que nós colocamos.



