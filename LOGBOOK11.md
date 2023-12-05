# LOGBOOK 8 Public-Key Infrastructure (PKI)
## Setup
- Começando o setup na pasta do lab, vamos mudar de pasta para a pasta "LabSetup" e executamos os codigos para dar build ao servidor  local e para colocar o servidor a rodar, utilizando os seguintes codigos

```shell
$ docker-compose build # Build the container image
$ docker-compose up # Start the container
```

- abrindo outro terminal e depois de executado o comando 

```shell
$ dockps // Alias for: docker ps --format "{{.ID}} {{.Names}}"
```

- para sabes os containers que estão a ser utilizados dando este resultado
![Alt text](Images/image11.png)

## Task 1
- Usando este codigo nos copiamos a openssl.conf presente na presente em `/usr/lib/ssl/openssl.cnf` para a directory atual que estou com o nome myopenssl.conf pois nos vamos fazer mudanças deste ficheiro

```shell
cp /usr/lib/ssl/openssl.cnf  myopenssl.conf
```
- Para permitir criar certificados digitais nos descomentamos esta linha do ficheiro `unique_subject	=   no` ficando com o ficheiro assim
```
[ CA_default ]

dir		= ./demoCA		# Where everything is kept
certs		= $dir/certs		# Where the issued certs are kept
crl_dir		= $dir/crl		# Where the issued crl are kept
database	= $dir/index.txt	# database index file.
unique_subject	= no			# Set to 'no' to allow creation of
```

- Now to create a Certificate Authority (CA) we ran this code
```
openssl req -x509 -newkey rsa:4096 -sha256 -days 3650 \
-keyout ca.key -out ca.crt

```
 - We filled the certificate with the following data

 ```
 PEM Pass Phrase : 1234
 Country: Pt
 State: Mirandela
 City: Mirandela
 Organization: Mira-papel
 Unit: Mira_1
 Name: MiraCorps
 Email: Mira@example.com
 
 ```
- Using this command we can see the information of the public key `openssl x509 -in ca.crt -text -noout
` e utilizando este codigo `openssl rsa -in ca.key -text -noout` podemos ver a chave privada rsa utilizando estes dois outputs podemos tirar algumas conclusões
- Atraves deste output podemos saber que é um AC valido 'CA: TRUE'
![Alt text](Images/image-111.png)
- Sabemos que este certificado foi utilizado por si proprio e porque tanto o signature algorithm como o subject são os mesmos.
![Alt text](Images/image-112.png)
- Cheking the rsa files we can see that
- The public expoent is this
![Alt text](Images/image-113.png)
- The 