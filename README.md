# financial-microservices
Projeto de estudo de arquitetura de microserviços utilizando Java, Spring Boot, Docker, PostgreSQL e RabbitMQ para gerenciamento financeiro.
# Payment System

Projeto de estudo desenvolvido para praticar conceitos de **arquitetura de microserviços**, utilizando Java e Spring Boot.

A aplicação tem como objetivo simular um fluxo de processamento de pagamentos, desde a solicitação até a aprovação ou rejeição, com geração de um código de acesso após a confirmação do pagamento.

## Objetivos

- Aprender os fundamentos de microserviços.
- Implementar comunicação entre serviços utilizando REST.
- Utilizar Nginx como API Gateway.
- Trabalhar com persistência de dados utilizando PostgreSQL.
- Containerizar aplicações com Docker.
- Aplicar conceitos de organização e separação de responsabilidades.

## Arquitetura

```text
                    CLIENTE
                       |
                       v
                +-------------+
                |    NGINX    |
                | API GATEWAY |
                +-------------+
                       |
             +---------+---------+
             |                   |
             v                   v
     +---------------+   +------------------+
     | PAYMENT       |-->| PROCESSOR        |
     | SERVICE       |   | SERVICE          |
     +---------------+   +------------------+
             |                   |
             v                   v
        PostgreSQL          PostgreSQL
```

## Tecnologias

| Tecnologia | Finalidade |
|---|---|
| Java 21 | Linguagem principal |
| Spring Boot | Desenvolvimento dos serviços |
| Spring Data JPA | Persistência de dados |
| PostgreSQL | Banco de dados |
| Nginx | API Gateway / Reverse Proxy |
| Docker | Containerização |
| Docker Compose | Orquestração local |

## Microserviços

### Payment Service

Responsável pelo gerenciamento dos pagamentos.

Funcionalidades previstas:
- Registrar solicitações de pagamento.
- Consultar pagamentos.
- Controlar status das transações.
- Solicitar processamento ao Processor Service.
- Gerar código de acesso após aprovação.

### Processor Service

Responsável por simular o processamento das transações.

Funcionalidades previstas:
- Receber solicitações de processamento.
- Simular aprovação ou rejeição.
- Retornar o resultado ao Payment Service.

### Nginx

Responsável por centralizar as requisições HTTP e direcioná-las aos respectivos microserviços.

## Fluxo de processamento

1. O cliente solicita um pagamento.
2. O Nginx encaminha a requisição ao Payment Service.
3. O pagamento é registrado com status `PENDING`.
4. O Payment Service solicita o processamento.
5. O Processor Service simula a operação.
6. O resultado retorna ao Payment Service.
7. Se aprovado, um código de acesso é gerado.
8. O cliente pode consultar o resultado do pagamento.

### Estados do pagamento

```text
PENDING
   |
   v
PROCESSING
   |
   +------> APPROVED
   |
   +------> REJECTED
```

## Estrutura do projeto

```text
payment-system/
│
├── nginx/
│   └── nginx.conf
│
├── payment-service/
│
├── processor-service/
│
├── docker-compose.yml
│
└── README.md
```

## Execução

A aplicação será executada utilizando Docker Compose, centralizando a inicialização dos serviços e da infraestrutura necessária.

```bash
docker compose up -d --build
```

## Status do projeto

🚧 Em desenvolvimento.

Este projeto possui finalidade exclusivamente educacional. O processamento de pagamentos será simulado, sem integração com instituições financeiras ou movimentação de dinheiro real.

---

**Projeto desenvolvido para fins de estudo e evolução profissional em Java, Spring Boot e arquitetura de microserviços.**
