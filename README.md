# Trabalho Conteinerização

## Requisitos
Para este projeto, é necessário que as ferramentas abaixo estjam instaladas.

- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Docker](https://docs.docker.com/engine/install/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Introdução
Este trabalho tem como objetivo criar uma infraestrutura em Docker com:
- Uma aplicação frontend em React juntamente com um NGINX;
- Um backend em Python com Flask;
- Um banco de dados PostgreSQL.

## Estrutura de arquivos e pastas
```shell
.
├── README.md # O arquivo que você está lendo agora
├── backend
│   └── Dockerfile # Arquivo do container backend
├── database # Pasta onde o Postgres salvará os dados
├── docker-compose.yaml # Arquivo compose com configurações dos conteiners
└── frontend
    ├── Dockerfile # Arquivo do container frontend
    └── nginx.conf # Arquivo de configuração do NGINX
```

## Opções de design
### Volumes
Os dados do banco de dados estão sendo armazenados na pasta `database`, onde as seguintes linhas do `docker-compose.yaml` define isto:
```yaml
...
    PGDATA: /var/lib/postgresql/data/pgdata
volumes:
    - ./database/:/var/lib/postgresql/data
...
```

### Balanceamento de carga
Para o balanceamento de carga com o NGINX, foram utilizadas configurações de upstream, conforme mostra abaixo:
```
upstream backend-upstream {
  server backend:5000;
}
...

location /api {
    proxy_pass http://backend-upstream/;
    ...
```

## Instruções
### Clonar repositório
1. Vá até o diretório onde deseja clonar o repositório.
2. Execute o comando `git clone https://github.com/luizpaese/TrabalhoConteinerizacao.git`
3. Entre no repositório e siga os passos abaixo.

### Gerenciando os conteiners
Para gerenciar os conteiners existem alguns comandos do Docker Compose, eles estão listados abaixo.
```shell
docker compose up -d --build # Para buildar e iniciar os conteiners.

docker compose down # Para parar todos os conteiners.

docker compose up -d --build --scale servico=3 # Escala os conteiners conforme especificação do serviço e o número de conteiners.
```

Caso queira fazer alguma modificação, como alterar a imagem, utilize os comandos acima para parar os conteiners e então inicia-los novamente com os parâmetros/configurações alteradas.