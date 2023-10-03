# CTF 1 - Semana 4

## Reconhecimento

Ao navegar pela web http://ctf-fsi.fe.up.pt:5001 , começamos por investigar todas as páginas à procura de pistas, que acabou por não ser produtivo, decidimos analisar as páginas usando o elemento Inspect fornecido pelo Google, descobrimos as seguintes dependências:

- Wordpress 5.8.1
- Woocommerce plugin 5.7.1
- Booster for WooCommerce plugin 5.4.3

Após obtermos, apercebemo-nos que podiamos tê-los descobertos muito mais facilmente, pois estavam escondidas numa das secções da loja. Decidimos analisar melhor o comentário que um utilizador fez relativamente a um produto na qual a data era 2021.


## Pesquisa por vulnerabilidades

Sabendo que a data foi em 2021 e a vulnerabilidade permite fazer login como administrador num servidor wordpress, decidimos então começar a pesquisar vulnerabilidades relacionadas com as dependências referidas, neste [site](https://cve.mitre.org/).

## Escolha da vulnerabilidade

Após uma pesquisa exaustiva, chegamos à conclusão que se trata da vulnerabilidade CVE-2021-34646 (para mais informação: [link](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-34646)) e usamos a flag `flag[CVE-2021-34646]`.

## Encontrar um exploit

Agora que sabemos qual a vulnerabilidade que a web tem, decidimos ir à database (mais especificamente o https://www.exploit-db.com), e encontramos o seguinte exploit que usa um progama em python (https://www.exploit-db.com/exploits/50299).


## Explorar a vulnerabilidade

Abrimos então a Virtual Machine para executar Ubuntu, e executamos o ficheiro python usando a seguinte linha de comando.

````bash
$ python3 exploit.py http://ctf-fsi.fe.up.pt:5001 1
````

Isto gerou-nos 3 links, na qual apenas um deles funcionava:

````

````

Após abrimos o link correto tivemos acesso direto à página (http://ctf-fsi.fe.up.pt:5001/wp-admin/edit.php) sem precisarmos de fazer log-in, o que nos permitiu ter acesso à última flag `flag{please don't bother me}`.
