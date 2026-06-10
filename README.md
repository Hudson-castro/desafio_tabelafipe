# Consulta Tabela FIPE

## Sobre o Projeto

Aplicação desenvolvida em Java com o objetivo de consumir a API da Tabela FIPE e consultar informações de veículos, como carros, motos e caminhões.

O sistema permite ao usuário selecionar uma categoria de veículo, pesquisar modelos disponíveis e visualizar informações detalhadas, incluindo valor de mercado, marca, modelo, ano e tipo de combustível.

---

## Tecnologias Utilizadas

- Java 21
- Maven
- Jackson Databind
- HttpClient (Java HTTP Client)
- API Tabela FIPE

---

## Conceitos Aplicados

Durante o desenvolvimento foram praticados conceitos importantes do ecossistema Java:

- Consumo de APIs REST
- Requisições HTTP
- Desserialização de JSON
- Programação Orientada a Objetos
- Records
- Generics
- Interfaces
- Collections (List)
- Streams
- Tratamento de Exceções
- Organização em Camadas

---

## Estrutura do Projeto

### ConsumoApi

Responsável por realizar as requisições HTTP para a API da Tabela FIPE e retornar os dados em formato JSON.

### IConverteDados

Interface responsável por definir o contrato para conversão de JSON em objetos Java.

### ConverteDados

Implementação da interface utilizando a biblioteca Jackson para converter JSON em objetos Java.

### Dados

Record utilizado para representar informações básicas retornadas pela API, como código e nome.

Exemplo:

```java
public record Dados(String codigo, String nome) {
}
```

### Modelos

Record utilizado para representar a lista de modelos de uma determinada marca.

```java
public record Modelos(List<Dados> modelos) {
}
```

### Veiculos

Record responsável por representar os detalhes completos de um veículo.

```java
public record Veiculos(
        String valor,
        String marca,
        String modelo,
        Integer ano,
        String tipoCombustivel
) {
}
```

### Principal

Classe responsável pela interação com o usuário e controle do fluxo da aplicação.

---

## Fluxo da Aplicação

1. O usuário escolhe a categoria:

- Carros
- Motos
- Caminhões

2. A aplicação consulta as marcas disponíveis.

3. O usuário seleciona uma marca.

4. A aplicação exibe os modelos disponíveis.

5. O usuário informa o modelo desejado.

6. O sistema consulta os anos disponíveis.

7. Os dados de cada versão são exibidos ao usuário.

---

## Exemplo de Uso

```text
Digite o tipo de veículo:

Carros

Toyota

Digite o modelo desejado:

Corolla
```

Resultado:

```text
Marca: Toyota
Modelo: Corolla XEi
Ano: 2024
Combustível: Gasolina
Valor: R$ 154.890,00
```

---

## Exemplo de Endpoint Consumido

Consulta de marcas:

```http
GET https://parallelum.com.br/fipe/api/v1/carros/marcas
```

Resposta:

```json
[
  {
    "codigo": "59",
    "nome": "Toyota"
  }
]
```

Consulta de veículo:

```http
GET https://parallelum.com.br/fipe/api/v1/carros/marcas/59/modelos/8032/anos/2024-1
```

Resposta simplificada:

```json
{
  "Valor": "R$ 154.890,00",
  "Marca": "Toyota",
  "Modelo": "Corolla XEi",
  "AnoModelo": 2024,
  "Combustivel": "Gasolina"
}
```

---

## Aprendizados

Este projeto foi fundamental para compreender:

- Como consumir APIs REST utilizando Java.
- Como converter JSON em objetos Java utilizando Jackson.
- Como utilizar Records para modelagem de dados.
- Como trabalhar com listas retornadas por APIs.
- Como utilizar Generics para criar conversores reutilizáveis.
- Como estruturar aplicações Java em múltiplas camadas.

---

## Possíveis Melhorias

- Interface gráfica utilizando JavaFX.
- Persistência dos dados em banco de dados.
- Criação de uma API própria utilizando Spring Boot.
- Cache de consultas.
- Testes unitários utilizando JUnit e Mockito.

---

## Autor

Desenvolvido como projeto de estudos para aprofundamento em Java, consumo de APIs e desenvolvimento Backend.
