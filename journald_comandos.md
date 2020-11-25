Filtrar log com base no serviço
```console
user@modernlinuxguide:~$ journalctl -u nginx.service
```

Filtrar o log com base no serviço a partir de um período
```console
user@modernlinuxguide:~$ journalctl -u nginx.service --since today
```

É possível consultar os logs para mais de um processo
```console
user@modernlinuxguide:~$ journalctl -u nginx.service -u php-fpm.service
```
Também é possível verificar o log com base no ID de um processo, ou para um grupo de processos pode-se usar o UID e o GID (use o comando id -u <nome do serviço> para consultar o _UID ou _GID)
```console
user@modernlinuxguide:~$ journalctl _PID=70605
```
e
```console
user@modernlinuxguide:~$ journalctl _UID=342
```

Para mostrar as mensagens de log do Kernel
```console
user@modernlinuxguide:~$ journalctl -k
```

