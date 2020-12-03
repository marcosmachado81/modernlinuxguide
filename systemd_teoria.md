O systemd padroniza a forma como controlamos os processos no Linux. Ele apresenta uma nova abordagem para a gestão de processos/programas e trás compatibilidade com o SysV e o LSB. Por este motivo ele foi amplamente adotado (apesar da controvérsia inicial)

Todo o conjunto do systemd vai além de apenas permitir que iniciemos processos/programas no Linux. Ele trás um conjunto de componentes como journal do sistema, agendar jobs, e etc. Abaixo uma imagem que ilustra os componentes do Systemd.


![Systemd: Fonte Wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/3/35/Systemd_components.svg/440px-Systemd_components.svg.png "Systemd")  
*componentes do Systemd: Fonte Wikipedia*


**Units e Arquivo Unit**
O systemd gerencia entidades que são conhecidas pelo nome genérico <i>Unit</i>. Essa <i>Unit</i> pode ser um serviço, um socket, um device, um ponto de montagem, partição, arquivo swap, entre outros.

Dentro do systemd o comportamento de cada unidade é definido atravez de um arquivo de configuração. É este arquivo que descreve o comportamento da <i>Unit</i>, como iniciar e parar por exemplo. Abaixo um exemplo do arquivo do rsync.service:

```text
[Unit]
Description=fast remote file copy program daemon ConditionPathExists=/etc/rsyncd.conf
[Service]
ExecStart=/usr/bin/rsync --daemon --no-detach
[Install] WantedBy=multi-user.target
```
Estes arquivos de configuração podem ser encontrados em mais de um local. Normalmente eles ficam em /usr/lib/systemd/system, em algumas distros em /lib/systemd/system. Um ponto importante, e comum, é que independente do local original você pode redefinir o arquivo colocando-o em /etc/systemd/system. Isto é, se você quiser mudar o comportamento de algum <i>Unit</i> pode adicionar o arquivo em /etc/systemd/system.

Para verificar qual arquivo o systemd está utilizando você pode usar o command do systemctl para verificar:
```console
user@modernlinuxguide:~$ systemctl status mysqld
● mysqld.service - MySQL 8.0 database server
   Loaded: loaded (/usr/lib/systemd/system/mysqld.service; enabled; vendor preset: disabled)
   Active: active (running) since Thu 2020-08-27 03:18:21 EDT; 1 months 28 days ago
 Main PID: 1071 (mysqld)
   Status: "Server is operational"
    Tasks: 47 (limit: 5025)
   Memory: 154.6M
   CGroup: /system.slice/mysqld.service
           └─1071 /usr/libexec/mysqld --basedir=/usr
```
No caso acima o serviço do MySQL está usando o arquivo em /usr/lib/systemd/mysqld.service. Caso você precise alterar o arquivo, faça-o dentro de /etc/systemd/system e depois execute o comando <i>systemctl daemon-reload</i> para que o systemd releia os arquivos dos <i>Unit</i>.

Abaixo um exemplo de configuração do serviço nginx, usando parâmetros mais complexos que no arquivo anterior.
```text
[Unit]
Description=The nginx HTTP and reverse proxy server 
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/run/nginx.pid 
ExecStartPre=/usr/bin/rm -f /run/nginx.pid 
ExecStartPre=/usr/sbin/nginx -t 
ExecStart=/usr/sbin/nginx 
ExecReload=/bin/kill -s HUP $MAINPID 
KillMode=process
KillSignal=SIGQUIT
TimeoutStopSec=5
PrivateTmp=true

[Install] 
WantedBy=multi-user.target
```
