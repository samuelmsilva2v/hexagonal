# Hexagonal Architecture
[🇺🇸 Read in English](#hexagonal-architecture-1)

Estudo de **arquitetura hexagonal** (ports & adapters) em Spring Boot, usando o cadastro de clientes como caso de uso.

## Estrutura
```
application/
├── core/     # regras de negócio (domínio)
└── ports/    # interfaces (portas de entrada e saída)
adapters/
├── in/       # controller REST, consumer Kafka
└── out/      # persistência (MongoDB), cliente Feign, produtor Kafka
```

## Tecnologias
Java 21, Spring Boot 3.5.0, Spring Data MongoDB, Spring Cloud OpenFeign, Spring Kafka, MapStruct

## Caso de uso
CRUD de clientes (`InsertCustomerAdapter`, `FindCustomerByIdAdapter`, `UpdateCustomerAdapter`, `DeleteCustomerByIdAdapter`), persistido no MongoDB. Ao cadastrar, o endereço é buscado por CEP via um cliente Feign (`FindAddressByZipCodeAdapter`) e a validação do CPF é enviada de forma assíncrona pelo Kafka (`SendCpfValidationAdapter` / consumer).

## Como executar
```bash
./gradlew bootRun
```
Requer uma instância de MongoDB e um broker Kafka disponíveis (configuráveis em `application.properties`).

---

# Hexagonal Architecture
[🇧🇷 Leia em Português](#hexagonal-architecture)

A study of **hexagonal architecture** (ports & adapters) in Spring Boot, using customer registration as the use case.

## Structure
```
application/
├── core/     # business rules (domain)
└── ports/    # interfaces (inbound and outbound ports)
adapters/
├── in/       # REST controller, Kafka consumer
└── out/      # persistence (MongoDB), Feign client, Kafka producer
```

## Technologies
Java 21, Spring Boot 3.5.0, Spring Data MongoDB, Spring Cloud OpenFeign, Spring Kafka, MapStruct

## Use case
Customer CRUD (`InsertCustomerAdapter`, `FindCustomerByIdAdapter`, `UpdateCustomerAdapter`, `DeleteCustomerByIdAdapter`), persisted in MongoDB. On registration, the address is looked up by ZIP code through a Feign client (`FindAddressByZipCodeAdapter`) and CPF (Brazilian tax ID) validation is sent asynchronously via Kafka (`SendCpfValidationAdapter` / consumer).

## How to run
```bash
./gradlew bootRun
```
Requires a running MongoDB instance and a Kafka broker (configurable in `application.properties`).
