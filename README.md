# elasticsearch-exemplo
Arquivos e dados de exemplos de uso do ElasticSearch para o post http://blog.caelum.com.br/buscas-eficientes-com-elasticsearch

São quase 1.5mi de dados para testes.

# Configuracoes Iniciais

+ É necessário ter o Java instalado na sua máquina.
+ Baixar o Elasticsearch ```curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.4.1.tar.gz```
+ Descompactar ```tar -zxvf elasticsearch-5.4.1.tar.gz```
+ Dentro da pasta bin, suba ```./elasticsearch -Ecluster.name=search-cluster-exemplo -Enode.name=search-node-exemplo```

# Banco

+ No arquivo zipado há um arquivo SQL contendo os dados a serem importados no PostgreSQL. Basta executar no pgAdmin.
+ Para importar no Elasticsearch, será necessário o uso do LogStash.

# Importando no Elasticsearch

Baixe o LogStash

+ É necessário ter o Elasticsearch instalado e no ar.
+ Baixar o LogStash ```curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.4.1.tar.gz```
+ Descompactar ```tar -zxvf logstash-5.4.1.tar.gz```

Veja o arquivo aqui versionado chamado importacao.conf. Ele contem o caminho do arquivo de importação e os dados do seu Node. Altere o que achar necessário. Entre na pasta bin e suba o LogStash apontando para esse arquivo de configuração.

```./logstash -f [seu-path]/importacao.conf```

Aguarde bastante :)

# Testando

No navegador, acesse aos URLs abaixo.

+ Verificar se o nó foi criado: ```http://127.0.0.1:9200/_cat/indices?v```
+ Buscar todas as pessoas: ```http://127.0.0.1:9200/pessoas_idx/_search?pretty -d '{"query": {"match_all": {}}'```





