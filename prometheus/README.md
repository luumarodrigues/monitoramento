###Configurando o Prometheus

A configuração do Prometheus é YAML. O Prometheus vem com um exemplo de configuração no arquivo prometheus.yml que é um bom lugar para começar.

Comentário, são linhas começadas com um  #

```
global:
  scrape_interval:     15s
  evaluation_interval: 15s
 
rule_files:
  # - "first.rules"
  # - "second.rules"
 
scrape_configs:
  - job_name: prometheus
    static_configs:
      - targets: ['localhost:9090']
```

Há três blocos de configuração no arquivo: 'global', 'rule_files'  e  'scrape_configs'.


O bloco  'global'  controla as configurações globais do servidor prometheus. No exemplo temos duas opções:

- A primeira, 'scrape_interval', controla como o prometheus irá consultar (scrape) os alvos (targert). É possível sobrescrever esta configuração por alvos individuais. No caso a configuraçao é para consultar a cada 15 segundos.

- A opção  'evaluation_interval' controla com que frequencia o prometheus irá avaliar as regras. O Prometheus usa regras para criar novos time series  para gerar alertas.



O bloco 'rule_files' especifica o local de qualquer regra para que o Prometheus tenha que carregar. Neste momento não foi criado regras.


O ultimo bloco, 'scrape_configs', controla qual recursos o Prometheus monitora.  Como o Prometheus também expõe dados sobre si mesmo como um endpoint HTTP, ele pode raspar (scrape) e monitorar sua própria saúde.  Por padrão o arquivo de configuraçao possui um unico job, chamado 'prometheus', o qual realiza o scrapes de time series data expostos pelo Prometheus server. O job contem uma configuração estática de target, o 'localhost' na porta '9090'. O Prometheus espera que as métricas estejam disponíveis nos destinos em um caminho de '/metrics'. Então, esse job está consultando a URL: http://localhost:9090/metrics.

Os time series data retornarão o estado de desempenho do Prometheus server.

Referência: 
https://prometheus.io/docs/introduction/first_steps/