## Laboratórios Pós Go Expert - Corrida Distribuída e Span

Este sistema em Go recebe um CEP, identifica a cidade correspondente e retorna o clima atual (temperatura em graus Celsius, Fahrenheit e Kelvin), juntamente com o nome da cidade. Além disso, este sistema implementa OTEL (Open Telemetry) e Zipkin.

Baseado no cenário conhecido "Sistema de temperatura por CEP" referido como Serviço B, será incluído um novo projeto denominado Serviço A.

## Requisitos - Serviço A (responsável pela entrada):
O sistema deve receber um input de 8 dígitos via POST, utilizando o seguinte esquema: { "cep": "29902555" }
O sistema deve validar se o input é válido (contém 8 dígitos) e é uma STRING. Caso seja válido, será encaminhado para o Serviço B via HTTP.
Caso não seja válido, deve retornar:
Código HTTP: 422
Mensagem: CEP inválido

## Requisitos - Serviço B (responsável pela orquestração):

O sistema deve receber um CEP válido de 8 dígitos.
O sistema deve realizar a pesquisa do CEP e encontrar o nome da localização. A partir disso, deve retornar as temperaturas formatadas em Celsius, Fahrenheit e Kelvin, juntamente com o nome da localização.
O sistema deve responder adequadamente nos seguintes cenários:
Em caso de sucesso:
Código HTTP: 200
Corpo da resposta: { "city: "São Paulo", "temp_C": 28.5, "temp_F": 28.5, "temp_K": 28.5 }
Em caso de falha, caso o CEP não seja válido (com formato correto):
Código HTTP: 422
Mensagem: CEP inválido
Em caso de falha, caso o CEP não seja encontrado:
Código HTTP: 404
Mensagem: CEP não encontrado

## Após a implementação dos serviços, adicione a implementação do OTEL + Zipkin:

Implementar rastreamento distribuído entre o Serviço A e o Serviço B.
Utilizar spans para medir o tempo de resposta do serviço de busca de CEP e do serviço de busca de temperatura.

## Rodar o sistema em ambiente de DESENVOLVIMENTO
- Execute o comando docker-compose up -d --build

# Observações
O Sistema A rodará na porta 8080.
O Sistema B rodará na porta 8081.
Para visualizar o rastreamento, acesse o navegador e digite: http://localhost:9411
