# ipserver.mnd
Monitoramento ativo e execução de comandos, para servidores Unix-like.

A ferramenta IPSERVER.mnd, vem como um complemento a outras soluções de monitoramento, como NAGIOS, ZABBIX, CACTI, MONIT, etc. Agregando mais recursos ao NetAdmin/SysAdmin;

O sistema funciona invocando comandos e informações diretamente ao servidor de gerenciamento, que controla cliente ativo ou não, senha de acesso, trabalhando de forma dinâmica. Assim como a sequencia dos comandos sendo realizada pelo IPSERVER (WEB).

No cliente script "ipserver.mnd", deve estar salvo em "/sbin";
- Necessário NMAP, dos2unix, PING, resolv.conf e MySQL Cli;
- Script deve ser adicionado na CRON, como segue:
      * Ativo no modo DAEMON, podendo ser ajustado como necessário;
      * Devido a controle interno, o ipserver.mnd não corre riscos de executar de forma duplicada;
      * Podendo ser adicionado ao rc.local;

            0-59/1 * * * * /sbin/ipserverd.mnd &

No servidor script "ipmonitor.php", responsável pelo monitoramento e envio de alertas, via e-mail, SMS e pagina de monitoramento;
- Necessário SendMAIL, NMAP, PHP, MySQL Srv;

      Script deve ser adicionado na CRON, como exemplo abaixo:
      0-59/1 * * * * /usr/bin/php /opt/ipmonitor.php

No servidor, pagina padrão de acesso ao painel do IPSERVER, salva em:

      "/<diretorio padrão www servidor apache, raiz>/ipserver/index.php"
      Pagina utilizada para validar os comandos a serem realizados;

No servidor, pagina padrão de acesso ao painel do IPMONITOR, salva em:

      "/<diretório padrão www servidor apache, raiz>/ipmonitor/index.php"
      Pagina utilizada para monitoramento dos equipamentos;

- AJUSTE BASE DE DADOS:

      - my.cnf: under [mysqld] section.

            innodb_file_per_table
            innodb_file_format = Barracuda

      - ALTER the table:

            ALTER TABLE nombre_tabla
                  ENGINE=InnoDB
                  ROW_FORMAT=COMPRESSED
                  KEY_BLOCK_SIZE=8;
