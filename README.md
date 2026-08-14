# InnovaBank API

> Projeto Django + Django REST Framework para Governança de Portfólio de TI.

![Python](https://img.shields.io/badge/Python-3.13-8EC5F0?style=flat-square&logo=python&logoColor=1a1a1a)
![Django](https://img.shields.io/badge/Django-5.0+-9DD89A?style=flat-square&logo=django&logoColor=1a1a1a)
![DRF](https://img.shields.io/badge/DRF-3.15-F0A8B8?style=flat-square&logo=django&logoColor=1a1a1a)
![Poetry](https://img.shields.io/badge/Poetry-Latest-C7B8E8?style=flat-square&logo=poetry&logoColor=1a1a1a)
---

## Orientador

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Claudio%20Ulisse-8EC5F0?style=flat-square&logo=linkedin&logoColor=000000)](https://linkedin.com/in/claudio-ulisse)
[![GitHub](https://img.shields.io/badge/GitHub-claulis-C7B8E8?style=flat-square&logo=github&logoColor=000000)](https://github.com/claulis)
[![Lattes](https://img.shields.io/badge/Lattes-Claudio%20Ulisse-9DD89A?style=flat-square&logoColor=000000)](http://lattes.cnpq.br/)
---

## Sumário

- [Visão Geral](#visão-geral)
- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)
- [Rodando o Servidor](#rodando-o-servidor)

## Visão Geral

Este repositório contém uma API construída com **Django (>= 5.0)** e **Django REST Framework**, voltada para o gerenciamento de portfólio do **InnovaBank**. O projeto utiliza **SQLite** por padrão para facilitar o desenvolvimento.

### Principais dependências

Definidas em `pyproject.toml`:

* `django (>=5.0,<6.0.0)`
* `djangorestframework (>=3.15,<4.0.0)`
* `drf-yasg` — Documentação Swagger
* `django-filter`

---

## Pré-requisitos

* Python **3.13** ou superior
* Git
* **Poetry** (gerenciador de dependências)

---

## Instalação

### Instalar o Poetry

Caso ainda não tenha o Poetry instalado, siga a [documentação oficial](https://python-poetry.org/docs/#installation):

```bash
curl -sSL https://install.python-poetry.org | python3 -
```

Após a instalação, adicione o Poetry ao PATH:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

Verifique a instalação:

```bash
poetry --version
```

---

### Clonar o projeto

```bash
git clone https://github.com/AdrianaAGSilva/projeto-integrador-python.git
```

---

### Instalar dependências

O Poetry cria automaticamente o ambiente virtual e instala todas as dependências:

```bash
poetry install
```
---

### Configuração de variáveis de ambiente

Copie o arquivo de exemplo e gere sua própria SECRET_KEY:

```bash
cp .env.example .env
```

Gere uma nova chave e cole no arquivo `.env`:

```bash
poetry run python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
```
---

### Ativar o ambiente virtual (opcional)

Você pode executar comandos diretamente com:

```bash
poetry run <comando>
```

Ou entrar em um shell interativo:

```bash
poetry shell
```

---

## Configuração do Banco de Dados

O projeto já vem configurado para usar **SQLite** (`db.sqlite3`). Para preparar o banco:

```bash
poetry run python manage.py migrate
```

Criar um usuário administrador (opcional):

```bash
poetry run python manage.py createsuperuser
```

> Para usar outro banco (PostgreSQL, MySQL etc.), edite `setup/settings.py` na seção `DATABASES` e instale o driver apropriado.

---

## Rodando o Servidor

```bash
poetry run python manage.py runserver
```

* API (ambiente local): [http://127.0.0.1:8000/admin](http://127.0.0.1:8000/admin)
* Endpoints (ambiente local): [http://127.0.0.1:8000/api/](http://127.0.0.1:8000/api/)
* Swagger (ambiente local): [http://127.0.0.1:8000/swagger/](http://127.0.0.1:8000/swagger/)

>  **Observação:** os links acima funcionam apenas com o servidor Django em execução localmente (`python manage.py runserver`).

---

## Diagrama de Banco de Dados

O diagrama abaixo representa o **modelo relacional** utilizado na aplicação, evidenciando as entidades **Departamento**, **Projeto** e **Tecnologia**, bem como seus relacionamentos.

![Diagrama de Banco de Dados](docs/diagrama_banco.png)

---

## Endpoints da API

**Base URL (desenvolvimento):**

```
http://127.0.0.1:8000/api/
```

* Django 5.0 + DRF 3.15
* Permissões atuais: `AllowAny` (aberta para testes)

---

### 1. Departamentos (`/departamentos/`)

| Método | Endpoint                   | Descrição                    | Campos obrigatórios |
| ------ | -------------------------- | ---------------------------- | ------------------- |
| GET    | `/api/departamentos/`      | Lista todos os departamentos | —                   |
| GET    | `/api/departamentos/{id}/` | Detalhe de um departamento   | —                   |
| POST   | `/api/departamentos/`      | Cria novo departamento       | `nome`, `gestor`    |
| PUT    | `/api/departamentos/{id}/` | Atualiza todos os campos     | `nome`, `gestor`    |
| PATCH  | `/api/departamentos/{id}/` | Atualiza campos parciais     | —                   |
| DELETE | `/api/departamentos/{id}/` | Remove departamento          | —                   |

**Exemplo (POST / PUT):**

```json
{
  "nome": "Segurança da Informação",
  "gestor": "Adriana Silva",
  "ativo": true
}
```

---

### 2. Tecnologias (`/tecnologias/`)

| Método | Endpoint                 | Descrição                  | Campos obrigatórios |
| ------ | ------------------------ | -------------------------- | ------------------- |
| GET    | `/api/tecnologias/`      | Lista todas as tecnologias | —                   |
| GET    | `/api/tecnologias/{id}/` | Detalhe da tecnologia      | —                   |
| POST   | `/api/tecnologias/`      | Cria nova tecnologia       | `nome`              |
| DELETE | `/api/tecnologias/{id}/` | Remove tecnologia          | —                   |

**Exemplo:**

```json
{
  "nome": "Django Framework",
  "acronimo": "DJ",
  "versao_padrao": "5.0"
}
```

---

### 3. Projetos (`/projetos/`)

| Método | Endpoint              | Descrição                    | Campos obrigatórios    |
| ------ | --------------------- | ---------------------------- | ---------------------- |
| GET    | `/api/projetos/`      | Lista projetos (com filtros) | —                      |
| GET    | `/api/projetos/{id}/` | Detalhe do projeto           | —                      |
| POST   | `/api/projetos/`      | Cria novo projeto            | `nome`, `departamento` |
| PUT    | `/api/projetos/{id}/` | Atualiza projeto completo    | `nome`, `departamento` |
| PATCH  | `/api/projetos/{id}/` | Atualização parcial          | —                      |
| DELETE | `/api/projetos/{id}/` | Remove projeto               | —                      |

**Exemplo (POST):**

```json
{
  "nome": "Migração Nuvem 2025",
  "descricao": "Migração dos servidores locais para AWS",
  "departamento": 1,
  "tecnologias": [1, 2],
  "data_inicio": "2025-10-20",
  "status": "em_andamento"
}
```

**Observações:**

* `departamento`: ID do departamento
* `tecnologias`: lista de IDs

Status possíveis:

```json
"planejamento" | "em_andamento" | "concluido" | "cancelado"
```

---

## Fluxo Típico de Testes

```bash
# 1. Criar departamento
POST http://127.0.0.1:8000/api/departamentos/

# 2. Criar tecnologia
POST http://127.0.0.1:8000/api/tecnologias/

# 3. Criar projeto
POST http://127.0.0.1:8000/api/projetos/

# 4. Listar projetos
GET  http://127.0.0.1:8000/api/projetos/
```

---

## Dicas e Troubleshooting

### Poetry não encontrado

```bash
export PATH="$HOME/.local/bin:$PATH"
```

### Problemas no `poetry install`

Verifique a versão do Python:

```bash
python --version
```

Definir versão específica:

```bash
poetry env use python3.13
```

### Limpar cache do Poetry

```bash
poetry cache clear . --all
poetry install
```

### Gerenciar dependências

Adicionar:

```bash
poetry add requests
```

Remover:

```bash
poetry remove requests
```

---

## Como Contribuir

1. Abra uma issue descrevendo o bug ou feature
2. Faça um fork do projeto
3. Crie uma branch (`feature/` ou `fix/`)
4. Implemente a alteração
5. Envie um Pull Request para a branch `main`
