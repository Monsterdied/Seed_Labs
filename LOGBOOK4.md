# LogBook4

## Identificação

## task 2
- os ficheiros são iguais
    pois a diferença do codigo é se o codigo é utilizado pelo processo principal (pai)
    ou pelo filho (child) e as variaveis de ambiente tanto do pai como do filho são as mesmas

## task 3
- envp is an array of pointers to strings, conventionally of the
       form key=value, which are passed as the environment of the new
       program.
       if envp is null there are no ambient variables
## task 4

 done what he asks

## task 5 


-  quando se altera o path a maior parte das funcoes do terminal para de funcionar ate que se volte a dar set do PATH correto

![dependencies](/Images/print1.png)


- depois de repor as variaveis de ambiente as funçoes do terminal 
a maior parte voltou a funcionar


![dependencies](/Images/print2.png)

![dependencies](/Images/Captura_de_ecrã_2023-10-11_232522.png)

-   quando se adicionam as variaveis de ambiente ANY e quando se altera a variavel de ambiente PATH elas aparecem quando nos utilizamos o codigo da task2 mas quando se adiciona a variavel LD_LIBRABRY_PATH ela não aparece mas quando se utiliza o codigo printenv encontra-se a variavel que criamos com o respetivo path 


![dependencies](/Images/Captura_de_ecrã_2023-10-11_232303.png)

- pois o printenv roda no processo em que criamos a nova variavel de ambiente enquanto que o codigo da task2 roda num child da root que vai buscar as variaveis de ambiente ao root e no root não se pode adicionar/alterar esta variavel de ambiente LD_LIBRABRY_PATH

![dependencies](/Images/print3.png)


## task6

- para 

![dependencies](/Images/print5.png)

![dependencies](/Images/print4.png)

