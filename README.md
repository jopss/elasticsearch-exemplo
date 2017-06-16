# elasticsearch-exemplo
Arquivos e dados de exemplos de uso do ElasticSearch para o post http://blog.caelum.com.br/?p=9020&preview=true.

# Configuracoes Iniciais

+ É necessário ter o Java instalado na sua máquina.
+ Baixar o Elasticsearch: "curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.4.1.tar.gz"
+ Descompactar: "tar -zxvf elasticsearch-5.4.1.tar.gz"
+ Dentro da pasta bin, suba: "./elasticsearch -Ecluster.name=search-cluster-exemplo -Enode.name=search-node-exemplo"

# Banco

+ No arquivo zipado há um arquivo SQL contendo os dados a serem importados no PostgreSQL. Use o pgAdmin para isso.
+ Para importar no Elasticsearch, será necessário o uso do LogStash.

# Importando no Elasticsearch

Baixe o LogStash

+ É necessário ter o Elasticsearch instalado e no ar.
+ Baixar o LogStash: "curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.4.1.tar.gz"
+ Descompactar: "tar -zxvf logstash-5.4.1.tar.gz"

Crie um arquivo de importação e configure a importação do CSV para o seu Node.

input {
    file {
        path => ["/[seu-path]/backup_pessoas.csv"]
        start_position => "beginning"
    }
}

filter {
    csv {
        columns => ["id", "datacriacao", "nome", "tipopessoa"]
        separator => ","
    }
}

output {
    stdout { codec => rubydebug }
    elasticsearch {
        action => "index"
        hosts => ["127.0.0.1:9200"]
        index => "pessoas_idx"
        document_type => "pessoas_type"
        workers => 1
    }
}

Entre na pasta bim e suba o LogStash ./logstash -f [seu-path]/importacao.conf
Aguarde bastante, são quase 1.5mi registros :)



