# Desafio Pipeline CI/CD

Projeto desenvolvido como parte do desafio prático de pipeline CI/CD.

Foi criada uma aplicação utilizando FastAPI, com testes automatizados, containerização com Docker e pipelines de CI e CD utilizando GitHub Actions.

## Tecnologias utilizadas

- Python
- FastAPI
- Uvicorn
- Pytest
- Semgrep
- Docker
- Git
- GitHub
- GitHub Actions
- Docker Hub

## Estrutura do projeto

```text
desafio-pipeline/
├── .github/
│   └── workflows/
│       ├── ci.yml
│       └── cd.yml
├── app/
│   └── main.py
├── tests/
│   └── test_main.py
├── .dockerignore
├── .gitignore
├── Dockerfile
├── README.md
└── requirements.txt
```

## Executando o projeto localmente

### Instalar as dependências

```powershell
python -m pip install -r requirements.txt
```

### Executar a aplicação

```powershell
python -m uvicorn app.main:app --reload
```

A aplicação ficará disponível em:

```text
http://localhost:8000
```

### Endpoints

Endpoint principal:

```text
GET /
```

Health check:

```text
GET /health
```

## Testes

Os testes automatizados foram implementados utilizando Pytest.

Para executar os testes:

```powershell
python -m pytest tests/ -v
```

Os testes verificam o status code e o conteúdo retornado pelos endpoints da aplicação.

## Docker

A aplicação foi containerizada utilizando Docker.

### Build da imagem

```powershell
docker buildx build --load -t cloudops-api:local .
```

### Executar o container

```powershell
docker run --rm -p 8000:8000 --name cloudops-api cloudops-api:local
```

Com o container em execução, a aplicação pode ser acessada em:

```text
http://localhost:8000
```

E o health check em:

```text
http://localhost:8000/health
```

## CI - Integração Contínua

O workflow de CI está localizado em:

```text
.github/workflows/ci.yml
```

O CI é executado em Pull Requests destinados às branches `develop` e `main`.

Durante a execução são realizados:

- testes automatizados com Pytest;
- análise estática de segurança com Semgrep.

## CD - Entrega Contínua

O workflow de CD está localizado em:

```text
.github/workflows/cd.yml
```

O CD é executado quando o código entra na branch `main`.

O workflow realiza o build da imagem Docker e publica a imagem no Docker Hub.

As credenciais do Docker Hub foram configuradas utilizando GitHub Secrets:

```text
DOCKERHUB_USERNAME
DOCKERHUB_TOKEN
```

A imagem é publicada no Docker Hub com duas tags:

```text
latest
SHA do commit
```

Imagem:

```text
gracekely/cloudops-api
```

## GitFlow

Durante o desenvolvimento foram utilizadas as branches:

```text
main
develop
feature/docker
feature/ci
feature/cd
feature/readme
```

O fluxo utilizado para integração das alterações foi:

```text
feature/* → develop → main
```

As alterações foram integradas utilizando Pull Requests.

## Docker Hub

A imagem Docker gerada pelo pipeline de CD está disponível no repositório:

```text
gracekely/cloudops-api
```