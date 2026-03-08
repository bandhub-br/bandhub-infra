<div align="center">

# 🎸 BandHub — Infraestrutura

**Guia de configuração e inicialização dos containers locais com Docker**

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)
![Kafka](https://img.shields.io/badge/Apache_Kafka-231F20?style=for-the-badge&logo=apache-kafka&logoColor=white)

</div>

---

## 📋 Visão Geral

Este repositório contém a configuração de infraestrutura da aplicação **BandHub**. Ele provisiona, via Docker Compose, todos os serviços necessários para o funcionamento do backend, incluindo **PostgreSQL**, **Redis** e **Kafka**.

---

## ✅ Pré-requisitos

Certifique-se de ter as seguintes ferramentas instaladas na sua máquina:

| Ferramenta | Download |
|---|---|
| 🐳 Docker Desktop | [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop) |
| 🔧 Git | [git-scm.com](https://git-scm.com) |
| 💻 Terminal | PowerShell, bash ou similar |

---

## 🔍 Verificando a Instalação do Docker

Confirme que o Docker está instalado executando:

```bash
docker --version
```

Em seguida, verifique se o Docker está em execução:

```bash
docker ps
```

---

## 📥 Clonando o Repositório

Clone o repositório que contém as configurações Docker:

```bash
git clone <url-do-repositorio>
cd bandhub-infra
```

---

## 📁 Estrutura do Projeto

```
bandhub-infra/
├── docker/
│   ├── docker-compose.yml
│   ├── init/
│   └── data/
└── scripts/
```

O arquivo `docker-compose.yml` sobe os seguintes serviços:

- 🐘 **PostgreSQL** — banco de dados relacional
- ⚡ **Redis** — cache e filas em memória
- 📨 **Kafka** — mensageria e streaming de eventos
- 🖥️ **Kafka UI** — interface web para inspeção do Kafka

---

## 🚀 Iniciando a Infraestrutura

Na raiz do repositório, execute:

```bash
docker compose up -d
```

> Este comando inicia todos os containers necessários em segundo plano.

---

## 🔎 Verificando os Containers

Após a inicialização, execute:

```bash
docker ps
```

Você deverá ver containers semelhantes a:

| Container | Descrição |
|---|---|
| `bandhub-postgres` | Banco de dados PostgreSQL |
| `bandhub-redis` | Servidor Redis |
| `bandhub-kafka` | Broker Kafka |
| `bandhub-zookeeper` | Coordenador do Kafka |
| `bandhub-kafka-ui` | Interface web do Kafka |

---

## 🖥️ Kafka UI

Acesse a interface do Kafka no navegador em:

```
http://localhost:8085
```

> Permite inspecionar tópicos e mensagens do Kafka de forma visual.

---

## 🐘 Conexão com o PostgreSQL

| Parâmetro | Valor |
|---|---|
| **Host** | `localhost:5432` |
| **Usuário** | `bandhub` |
| **Senha** | `bandhub` |

**Bancos de dados disponíveis:**

- `events_db`
- `notifications_db`
- `users_db`

```
localhost:5432
```

### Testando a conexão

```bash
docker exec -it bandhub-postgres psql -U bandhub -d postgres
```

---

## ⚡ Testando o Redis

Verifique se o Redis está respondendo:

```bash
docker exec -it bandhub-redis redis-cli ping
```

**Resposta esperada:**

```
PONG
```

---

## 🛑 Parando a Infraestrutura

Para parar todos os containers:

```bash
docker compose down
```

---

## 🔄 Resetando o Ambiente

Caso precise recriar tudo do zero:

```bash
docker compose down -v
docker compose up -d
```

> ⚠️ **Atenção:** o flag `-v` remove os volumes, apagando todos os dados persistidos.

---

## 🛠️ Problemas Comuns

| Problema | Solução |
|---|---|
| Docker não está rodando | Abra o **Docker Desktop** e aguarde a inicialização |
| Conflito de portas | Verifique se as portas `5432`, `6379`, `9092` e `8085` estão livres |
| Containers não iniciam | Consulte os logs com `docker logs <nome-do-container>` |

---

<div align="center">

Feito com ❤️ pelo time **BandHub**

</div>
