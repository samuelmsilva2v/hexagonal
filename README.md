# Hexagonal Architecture

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
