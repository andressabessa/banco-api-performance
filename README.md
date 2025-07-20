
# Testes de Performance da API do Banco com K6

Este repositório contém scripts de testes de performance desenvolvidos com o [Grafana K6](https://k6.io/) e JavaScript, com o objetivo de avaliar o desempenho e a estabilidade de uma API simulando diferentes cargas de usuários.


## Repositório

Acesse o repositório completo em:  
[https://github.com/andressabessa/banco-api-performance](https://github.com/andressabessa/banco-api-performance)

---

## Introdução

Testes de performance são fundamentais para identificar gargalos, validar a escalabilidade e garantir a confiabilidade de sistemas sob carga. Neste projeto, utilizamos o K6 para criar cenários que simulam o comportamento de usuários reais em diferentes níveis de intensidade.

---

## Tecnologias utilizadas

- [K6](https://k6.io/) – Ferramenta open source de testes de carga e performance.
- JavaScript (ES6)
- [GJSON](https://github.com/tidwall/gjson) – Para extração de dados em respostas JSON.
- Variáveis de ambiente para configuração dinâmica (ex: `BASE_URL`).


---

## Estrutura do Repositório

```
banco-api-performance/
├── tests/         #Casos de teste organizados por módulo da API
│   ├── login.test.js
│   ├── transferencias.test.js
├── config/
│   └── config.local.json    #Arquivo de configuração de variáveis de ambiente 
├── utils/            #Funções utilitárias reutilizáveis
│   └── variaveis.js
├── fixtures/       #Dados de entrada para os testes (ex:usuários, payloads) 
│   └── postLogin.json
├── helpers/       #Funções utilitárias reutilizáveis para interação com a API
│   └── autenticacao.js
├── README.md
```

---

## Objetivo de cada grupo de arquivos

- `tests/`: Casos de teste organizados por módulo da API.
- `config/`: Arquivo de configuração de variáveis de ambiente.
- `utils/`: Funções utilitárias reutilizáveis.
- `fixtures/`: Dados de entrada para os testes (ex:usuários, payloads).
- `helpers/`:Funções utilitárias reutilizáveis para interação com a API.


---

## Instalação e execução do projeto

### 1. Pré-requisitos

- Ter o [Node.js](https://nodejs.org/) e o [K6](https://k6.io/docs/getting-started/installation) instalados na máquina.

### 2. Clonar o repositório

```bash
git clone https://github.com/andressabessa/banco-api-performance.git
cd banco-api-performance
```

### 3. Configure as variáveis de ambiente 

Altere o arquivo `config.local.json`e defina a URL base da API a ser testada.

```json
{
    "baseUrl": "http://localhost:3000"

}
```
> Essas variáveis serão usadas dinamicamente nos testes para montar as requisições. 

### 4. Executar um teste

```bash
k6 run tests/login.test.js
```

Certifique-se de passar a variável de ambiente `BASE_URL`, caso não esteja usando um `config.local.json` ou uma abordagem de carregamento automático: 

```bash

k6 run tests/autenticacao/login.test.js -e BASE_URL=http://localhost:3000

```

### 5. Acompanhamento em tempo real 

Você pode ativar o modo dashboard do K6 e exportar o relatório ao final do teste:

```bash
K6_WEB_DASHBOARD=true \
K6_WEB_DASHBOARD_EXPORT=html-report.html \
k6 run tests/autenticacao/login.test.js -e BASE_URL=http://localhost:3000
```

Após a execução, o relatório estará salvo como `html-report.html`.

