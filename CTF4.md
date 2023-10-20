# CTF 2 - Semana 4

## Reconhecimento

Ao entrarmos no port 4006 do host ctf-fsi.fe.up.pt, usando o comando nc ctf-fsi.fe.up.pt 4006 com o vpn da FEUP ativado, fizemos o ls -l para verificar o conteúdo da pasta onde estávamos.

![ls](/Images/lsl.png)

Após analisar o conteúdo do admin_note.txt , usando o `cat admin_note.txt`

```
flag_reader,

I locked you out of the temp folders.
Told you before they are not to be used as permanent storage!
Hackers stole the flag by reading the files you left there!!!!!!
Finish your damn program ASAP!!!!!
Tired of waiting for you to lock them out for good, you lazy !@%#

- The Admin
```

