## Monitoramento

Docker-compose para subir ferramentas de monitoramento: Prometheus, Grafana, Cadvisor, alertmanager, redis, influx

- Instalação e configuração do Alertmanager;
- Configuração do Prometheus para falar com o Alertmanager;
- Criação das regras de alerta no Prometheus.

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
Grafana é um criador de Dashboard, que te permite consultar, visualizar, alertar e entender suas métricas, independentemente de onde elas estejam armazenadas.