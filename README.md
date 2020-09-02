## Monitoramento

Docker-compose para subir ferramentas de monitoramento: Prometheus, Grafana, Cadvisor, Alertmanager, Redis

<!-- - Instalação e configuração do Alertmanager;
- Configuração do Prometheus para falar com o Alertmanager;
- Criação das regras de alerta no Prometheus.
- Configuração de autenticação básica no Grafana
- Configuração de criptografia TLS Grafana
!-->

### Pré-requisitos

* Docker
* Docker compose


### Prometheus

O Prometheus extrai métricas de trabalhos instrumentados, diretamente ou por meio de um gateway intermediário para trabalhos de curta duração. Ele armazena todas as amostras coletadas localmente e executa regras sobre esses dados para agregar e registrar novas séries temporais de dados existentes ou gerar alertas.

Arquivo de configuração: **prometheus/prometheus.yml**
Acesso: **http://localhost:9090**
prometheus metrics: **http://localhost:9090/metrics**

#### - Alertas Prometheus
Alertas com Prometheus são separados em duas partes:

* Regras de alerta no servidor Prometheus que enviam para o Alertmanager;

* Alertmanager então gerencia esses alertas, incluindo silenciamento, inibição, agregação e enviando notificações através de métodos tais como: e-mail, slack, telegram, etc.

#### - Alert Rules
A regra de alerta está definida em /prometheus/alert.rules e o path do arquivo foi adicionado em rule_files no prometheus.yml


### Cadvisor
O cAdvisor (Container Advisor) fornece aos usuários de contêiner uma compreensão do uso de recursos e das características de desempenho de seus contêineres em execução. É um daemon em execução que coleta, agrega, processa e exporta informações sobre a execução de contêineres. Especificamente, para cada contêiner, ele mantém parâmetros de isolamento de recursos, uso de recursos históricos, histogramas de uso de recursos históricos completos e estatísticas de rede. Esses dados são exportados por contêiner e por toda a máquina.

### Node Exporter
Coleta as métricas do sistema operacional, tais como: disco, memória, cpu, etc.


### Alertmanager
O Alertmanager lida com alertas enviados por aplicativos clientes como o Prometheus. Ele cuida de desduplicação, de agrupamento e do roteamento para a integração correta do receptor, como email, PagerDuty ou OpsGenie. Também cuida do silenciamento e inibição de alertas.

O arquivo de configuração do alertmanager está em **/alertmanager/alertmanager.yml** e também foi adicionado no **prometheus.yml**

### Grafana
O Grafana permite consultar, visualizar, alertar e entender suas métricas, independentemente de onde elas estejam armazenadas. Crie, explore e compartilhe painéis com sua equipe e promova uma cultura orientada por dados.

Acesso: **http://localhost:3000**
Usuário: admin

#### - Criar data source: 
* Add data source -> Prometheus
* Inserir a URL do servidor do prometheus(http://prometheus:9090)
* Clicar em "Test & Save"
#### - Criar dashboard:
* Create dashboard -> add new panel
* Ir em Panel -> visualization -> selecionar Graph
* ir em Query -> metrics -> adicionar a query **node_memory_MemFree_bytes** (apenas exemplo)
* Clicar em "Save" -> escolher um nome para sua dashboars -> Save
* Veja a dashboards criada, clicando no icone a esquerda do painel.

<!-- ### Autenticação Basica
O Prometheus não suporta diretamente a autenticação básica para conexões com o navegador de expressões do Prometheus e a API HTTP. Para impor a autenticação básica para essas conexões, vamos usar o Prometheus em conjunto com um proxy reverso e aplicar a autenticação na camada de proxy.
!-->

<!-- ### Persistencia de dados
!-->