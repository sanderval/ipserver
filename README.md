# ipserver
Monitoramento ativo e execucao de comandos, para servidores Unix-like.


#      +------+
#  +---| INFO |---------------------------------------------------------------+
#  |   +------+                                                               |
#  | A ferramenta IPSERVER, vem como um complemento a outras solucoes de      |
#  | monitoramento, como NAGIOS, ZABBIX, CACTI, MONIT, etc. Agregando mais    |
#  | recursos ao NetAdmin/SysAdmin;                                           |
#  |                                                                          |
#  | O sistema funciona de forma segura, invocando comandos e informacoes     |
#  | diretamente ao servidor de gerenciamento, que controla cliente ativo ou  |
#  | nao, senha de acesso, trabalhando de forma dinamica. Assim como a        |
#  | sequencia dos comandos sendo realizada pelo IPSERVER (WEB).              |
#  |                                                                          |
#  | No cliente, necessario NMAP, dos2unix, PING, resolv.conf e MySQL Cli;    |
#  |                                                                          |
#  | CONFIGS:                                                                 |
#  | --------                                                                 |
#  |                                                                          |
#  | No cliente script "ipserver.logic", deve estar salvo em "/sbin";         |
#  | - Script deve ser adicionado na CRON, como segue:                        |
#  |    * Ativo no modo DAEMON, podendo ser ajustado como necessario;         |
#  |    * Devido a controle interno, o ipserver nao corre riscos de executar  |
#  |      de forma duplicada ou algo do genero;                               |
#  |    * Podendo ser adicionado ao rc.local;                                 |
#  |                                                                          |
#  |    0-59/1 * * * * /sbin/ipserverd.logic &                                |
#  |                                                                          |
#  | No servidor, necessario SendMAIL, NMAP, PHP, MySQL Srv;                  |
#  |                                                                          |
#  | No servidor script "ipmonitor.php", responsavel pelo monitoramento e     |
#  | envio de alertas, via e-mail, SMS e pagina de monitoramento;             |
#  | - Script deve ser adicionado na CRON, como exemplo abaixo:               |
#  |      0-59/1 * * * * /usr/bin/php /opt/ipmonitor.php                      |
#  |                                                                          |
#  | No servidor, pagina padrao de acesso ao painel do IPSERVER, salva em:    |
#  |    "/<diretorio padrao www servidor apache, raiz>/ipserver/index.php"    |
#  | Pagina utilizada para validar os comandos a serem realizados;            |
#  |                                                                          |
#  | No servidor, pagina padrao de acesso ao painel do IPMONITOR, salva em:   |
#  |    "/<diretorio padrao www servidor apache, raiz>/ipmonitor/index.php"   |
#  | Pagina utilizada para monitoramento dos equipamentos;                    |
#  |                                                                          |
#  | AJUSTE BASE DE DADOS:                                                    |
#  | ---------------------                                                    |
#  |                                                                          |
#  |  - my.cnf: under [mysqld] section.                                       |
#  |                                                                          |
#  |  innodb_file_per_table                                                   |
#  |  innodb_file_format = Barracuda                                          |
#  |                                                                          |
#  |  - ALTER the table:                                                      |
#  |                                                                          |
#  |  ALTER TABLE nombre_tabla                                                |
#  |     ENGINE=InnoDB                                                        |
#  |     ROW_FORMAT=COMPRESSED                                                |
#  |     KEY_BLOCK_SIZE=8;                                                    |
#  |                                                                          |
#  +--------------------------------------------------------------------------+
