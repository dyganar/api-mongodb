# Bancos não relacionais
    NoSQL - Not Only SQL (Structed query Language)
    Criados em 1960 teve popularidade a partir do século 21

    Classe de banco de dados que fornecem um mecanismo para armazenamento e recuperação de dados que são modelados de formas diferentes das relações tabulares usadas nos bancos de dados relacionais.

    Vantagens:
        Performance
        Escalabilidade
        Flexibilidade
        Agilidade de desenvolvimento.

## Classes de bancos NoSQL
    Chave/valor (Key-Value) redis
    Colunas (Column Family) cassandra
    Documento (Document model) mongoDB
    Grafos (Graph) neo4j

## MongoDB
    Document Model/Multi-model
    Escrito em C++
    OpenSource
    Multi-plataforma
    Armazena dados em formato BSON

    Relacional DB      MongoDB
    Base de dados     Base de dados
    Tabela            Coleção
    Registro          Documento
    Coluna            Atributo

    Standalone atende aplicações que não necessitam de escabalidade e alta disponibilidade. Possui apenas um mongod em execução.

    **Replicaset** é um conjunto de mongod que armazena os mesmos dados
    A replicação fornece redundância e aumenta a disponibilidade dos dados.
    Fornece um nível de tolerância a falhas contra a perda de um único servidor de banco de dados
    Recomendado para a maioria dos ambientes produtivos
    Alguns deploys podem ser configurados para aumentar a capacidade de leitura.
                        primary
                replica
        secondary     -Heartbeat-    secondary
    
    Em caso de erro no primary o  heartbeat define quem será o novo primário

    Na ConnectionSring deve ser identificado todos ip's das replicas.

    **Modelagem - Embedado - BJSON
    {
        _id: <ObjectId1>,
        username: "x",
        Contact: {
            phone: "rsjkrhs"
        },
        Access: {
            level: 5,
            group: "dev"
        }
    }

    Comandos:
        Insert (Insert INTO do sql)
        Find (SELECT do sql)

    MongoDB Atlas server/gerenciador.

## Criar projeto:

    1. data>Collections>infectado (representação da collection no banco)
    2. Instalar pacoteMongoDB.Driver
    3. data>Collections>MongoDB
        Iconfiguration possui todas as configurações carregadas pelo Program. Carrega as propriedades add em appsettings.
        Existem 2 maneiras de mapear o BD:
            DataAnotations;
            FluentMap (cria um método onde é mapeado o BD)
            SetIgnoreExtraElements evita quebra pela falta de alguma propriedade nova no bd que não foi implementada na classe.
    4. Models>InfectadoDto -- model de retorno
        Pra cada endpoint é interessante ter um Dto (view model)
    
    5. Controllers>InfectadoController
        o mesmo que routes em node.
    
    Injeção de dependência (dependence Injection) acontece quando o sistema identifica o controller através da rota enviada e carrega no sistema. Assim, não é preciso instanciar manualmente com o new.

    6. configurar Startup para identificar o MongoDB
        services.AddSingleton<Data.MongoDB>();
        o services.AddScoped a cada request instancia na memória matando o anterior.
        o services.Transient a cada request instancia na memória mantendo todos.
        o services.AddSingleton mantêm uma instância na memória enquanto o app está na memória. //não muito recomendado pois não desaloca a memória.

    
