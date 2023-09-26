# Spectre

## Identificação

- Spectre, também conhecido por CVE 2017-5753 ou Spectre Variant 1, é uma vulnerabilidade que aproveita como vantagem a execução especulativa de instruções que seguem uma branch condicional.
- Esta vulnerabilidade afeta quase todos os microprocessadores mais recentes que usam “speculative execution”, tais como os da AMD , INTEL… (e não estão limitados a um sistema operativo)
- Os ataques “Spectre” envolvem “enganar” o processador em executar especulativamente um conjunto de instruções que não deviam ser executadas.
-  Dar “exploit” a “Spectre” requer técnicas sofisticadas, tornando-o um desafio para a comunidade de segurança, mas mesmo assim , ainda continua a ser um problema complexo.

## Catalogação

- Spectre foi descoberto independentemente por duas pessoas Jann Horn (Google Project Zero) e Paul Kocher em colaboração com várias pessoas depois dos fornecedores de hardware afetados serem notificados da vulnerabilidade em 1 de junho 2017 foi reportado ao público em 3 de janeiro 2018.
- De acordo com a NVD (National Vulnerability Database) o nivel de gravidade desta vulnerabilidade é medio tendo uma pontuação de 5.6 em 10


## Exploit

- As previsões especulativas melhoram o desempenho se estiverem corretas, mas levam ao abandono do trabalho se o processador seguir o caminho errado.
- Durante a execução especulativa, o processador adivinha o resultado provável das instruções de desvio.
- Um exemplo de previsão especulativa que uma CPU usa é quando há uma ramificação que compara dois valores, mas um deles não está no cache, para não deixar a CPU ociosa, a CPU usa a previsão de ramificação economizando tempo se estiver correta.
- Se o trabalho for abandonado, há vestígios do trabalho e podem ser lidos ignorando as verificações de segurança nas filiais ou permitindo o acesso a dados fora do limite, permitindo que um invasor tenha acesso aos dados
- A execução especulativa em CPUs modernas pode executar várias centenas de instruções à frente, tendo um enorme potencial para executar muitas instruções antes que a previsão seja comprovada ou não.

## Ataques

- Até à data, não há registo de ataques usando Spectre , visto que foi descoberta durante testes (e também porque não deixa “resíduos” nas ficheiros log).
- Um ataque Spectre pode ter grande impacto,  já que permite que programas maliciosos induzam um hipervisor (VM) para transmitir ao sistema “guest” .

