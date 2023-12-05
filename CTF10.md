# CTF 10 Weak Encryption

## Setup

- Antes de iniciarmos o desafio, tivemos de ativar a vpn e fazer download do cipherspec.py onde é revelada o algoritmo que utilizam para encriptar e 
desencriptar. 
Correr este codigo para obter a ciphertext e a nounce aqui está cifrada a nossa flag
![Alt text](imageCTF10-4.png)

## Análise
- Após analisar o cipherspec.py descobrimos que a geração da chave apenas cria as 3 bytes menos significantes de maneira aleatória mantendo as restante 0x00 assim ficando vulneravel a bruteforce uma vez que existem apenas 2^(8*3) = 16777216
combinações 
![Alt text](imageCTF10-5.png)

## Exploit

- Para realizar o bruteforce attack criamos uma função para criar chaves gendif(val) de maneira não aleatória
```python
def gen_dif(val):
	offset = 3 # Hotfix to make Crypto blazing fast!!
	key = bytearray(b'\x00'*(KEYLEN-offset)) 
	key.extend(val.to_bytes(3, byteorder='big'))
	return bytes(key)
```
- E corremos este for loop que vai tentar desencriptar com todas as chaves possiveis e se alcançar algum valor válido vai imprimir na consola assim revelando a flag.
```python

m_in_string=""
for i in range(0,16777216):
	m_in_bytes=dec(gen_dif(i),bytes.fromhex("0501b24ea0e61bb2676ad4388f8a524c85caf3bd3592c93c7ed37591252a6390b48d9580e7a6d8"),bytes.fromhex("564db29a35b84d5430e56351b96f842c"))

	try:
		m_in_string=m_in_bytes.decode('utf-8')
	except UnicodeDecodeError as e:
		continue
	else:
		print(m_in_string)

```

![Alt text](imageCTF10-6.png)