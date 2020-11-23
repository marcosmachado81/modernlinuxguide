
Comandos mais úteis para o systemd

Listar os serviços instalados no host (similar ao chkconfig --list)
```console
user@modernlinuxguide:~$ systemctl -l -t service
```

Verificar os serviços que falharam
```console
user@modernlinuxguide:~$ systemctl --failed
```

Iniciar e habilitar um serviço
```console
user@modernlinuxguide:~$ systemctl enable --now [nome do serviço]
```
É possível executar comandos remotos
```console
user@modernlinuxguide:~$ systemctl -H [host] restart [nome do serviço]
```
Depois de alterar ou criar arquivos de configuração de serviços (/etc/systemd/system e /lib/systemd/system) é necessário dar um reload no systemd
```console
user@modernlinuxguide:~$ systemctl  daemon-reload
```
Para verificar a configuração de um serviço
```console
user@modernlinuxguide:~$ systemctl cat [serviço]
```
Listar as propriedades de uma unit
```console
user@modernlinuxguide:~$ systemctl show --all [serviço]
```
Ou é possível procurar um parâmetro em específico
```console
user@modernlinuxguide:~$ systemctl show -p Restart [serviço]
```
Mostrar informações do boot
```console
user@modernlinuxguide:~$ systemctl status
```
