# Instalação

### Você precisa ter o ambiente docker/docker-compose instalado em sua máquina.

# Rodando

## Você só precisa executar
$ docker-compose up -d

# Grafana

O data source pode se conectar através da web, ex: http://host.docker.internal:8080/api_jsonrpc.php, lembrese que está sendo execultado dentro de um container, por isso foi utilizado "host.docker.internal" para o container poder encontrar a máquina principal.

# Zabbix

Para configurar o Agent de monitoramento do docker você precisa criar um novo host, o campo "Host name" deve ser o mesmo "Hostname" do arquivo zabbix_agent2.config, deve possuir uma interface do tipo "Agent" com o "DNS name" com o mesmo nome do servico do arquivo "docker-compose" e deve utilizar o template "docker".

# Arquivo Docker-compose 

Dentro do serviço "zabbix-agent" deve utilizar o "user: root" para o Agent poder ler o arquivo "docker.sock", foram cridos 2 volumes, uma para compartilhar o arquivo "docker.sock" da maquina principal com o container, e outro para o arquivo de configuração do Agent.

# Arquivo zabbix_agent2.conf

### Server: Deve conter o nome do servico do zabbix server
### ServerActive: Deve conter o nome e a porta do servico zabbix server
### Hostname: Deve conter o nome do host utilizado na web
### Plugins.Docker.Endpoint: Deve conter o caminha para o arquivo "docker.sock"