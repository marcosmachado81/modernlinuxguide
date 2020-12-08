# Componentes de um Processo
Os componentes que nos interessam aqui são aqueles que possamos utilizar para identificar um processo.

- **PID**: Número do processo. É o identificador único do processo. com ele é possível executar comandos direcionados para o processo específico, em alguns casos você precisa saber esse número.
- **PPID**: Número do processo pai. Esta é uma referência ao processo anterior ao processo atual. É uma forma de traçar a linha do tempo de um processo. Usado quando não se sabe ao certo sobre o processo e se desaja descobrir como ele foi inicializado. Lembrando que o Linux não possuí uma system call de criação de processo do nada, todo processo precisa de um pai (o init seria o processo pai do sistema). O PPID é importante em casos como o processo zumbi, que apesar de morto continua consumindo recursos. As vezes para acabar com o processo é preciso parar o processo pai.
- **UID e EUID**: O UID é a identificação do usuário responsável por iniciar o processo. O EUID é o UID efetivo do processo, que determina quais recursos o processo pode acessar. Normalmente o UID e o EID são iguais.
- **GID e EGID**: O mesmo acontece com o grupo do processo. O GID é a identificação do grupo do usuário que criou o processo e o EGID indica o grupo do processo.

Como comentado acima, o **init** é o processo inicial do sistema. Todos os demais processos nascem do **init**.

