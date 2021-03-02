# CM Dev Academy - Java

Fala, galera!!! 

Gostaríamos de agradecer sua presença no  **CM Dev Academy - Java**. Abaixo vamos explicar os detalhes do desafio proposto. 


## O que vamos avaliar? O que buscamos?

O principal objetivo do desafio é analisarmos como entende, modela, resolve o problema e testa, de maneira clara e objetiva, adotando boas práticas de programação. Seja criativo!! Seja ousado!!!!

Enviar uma aplicação funcionando é o ideal, mas mesmo que não esteja 100 % envie o código para que possamos analisar até onde você chegou.

O problema que vamos apresentar não tem uma lógica complexa, mas implemente seu código pensando em um sistema extensível e de alta concorrência no uso, é muito importante que você aplique SOLID em tudo que fizer.

Seja criativo!



## Tecnologias

1. Nossa stack de desenvolvimento é Java, então nossa sugestão é que você utilize Spring.

2. Teste seu código, crie Unit tests e/ou Integration tests.

3. A aplicação deve ser self contained, use um database em memória, por exemplo o H2.

## O Desafio

O desafio proposto é de construir uma API que terá dois endpoints:
  
### Endpoint – Pedido de Venda

  Sua aplicação deve expor em `http://localhost:{porta}/api/v1/pedidos` uma API RESTful. (GET, POST, PUT, DELETE)

O conteúdo de um Pedido de Venda possui o seguinte payload:

```json
{
"pedido":"123456",
"nomeCliente":"JOSE FRANCISCO",
"endereco":"Rua A, 500",
"telefone":"8532795578",
"valorTotalProdutos":13.50,
"taxa":2.50,
"valorTotal":16.00,
"itens": 
    [{
        "descricao": "Refri",
        "precoUnitario": 5.5,
        "quantidade": 1
   },
   {
        "descricao": "Coxinha",
        "precoUnitario": 3.00,
        "quantidade": 1
   },
   {
        "descricao": "Batatinha",
        "precoUnitario": 5.00,
        "quantidade": 1
   }]
}
```

O conteúdo desse Pedido de Venda e seus Itens deverão ser persistidos em banco de dados. Fique à vontade para criar as validações que você considerar necessárias.

O pedido de venda poderá ter os seguintes status:

 - PENDENTE
 - PREPARANDO
 - PRONTO
 - EM_ROTA
 - ENTREGUE
 - CANCELADO

### Regra de Negócio

Todo novo pedido de venda terá que ter o status inicial **PENDENTE**. A cada novo pedido deverá ser feito o cálculo do **valor total dos produtos** e do **valor total** (valor total dos produtos+ taxa de entrega).

O endpoint não deve permitir:

 - pedido de venda sem produtos
 - produtos sem quantidade
 - produtos sem valor
 - produtos sem nome
 - alterar o status
 
### Endpoint – Mudança de Status de Pedido de Venda

Sua aplicação deve receber um POST em `http://localhost:{porta}/api/v1/pedidos/{id}/status` com o seguinte payload, onde {id} contido no path será o código do pedido e body o status que o pedido irá receber:

```json
{
"status": "PREPARANDO"
}
```  

A função desse endpoint é alterar o status do pedido de venda a medida em que ele for passando pelo seu ciclo de vida

O endpoint **não** deve permitir:

 - alterar o status para CANCELADO caso o status atual seja EM_ROTA, ENTREGUE ou CANCELADO
 - alterar o status para EM_ROTA caso o status atual não seja PRONTO
 - alterar o status para ENTREGUE caso o status atual não seja EM_ROTA

Para cada ação de sucesso de alteração do status a API deve de retornar a seguinte resposta:

```log
 HTTP 200 OK
```

Em caso de alguma regra de negócio não antendida, API deve de retornar a seguinte resposta:
```log
HTTP 422 - Unprocessable Entity
```
```
{
"mesagem": "status não pode ser alterado...."
}
```


#### Informações finais

Uma tentativa de mudança de status deverá passar por todas essas regras descritas e a API deverá retornar todos os status gerados, observe que as validações são compartilhadas entre as regras, reutilize código.

  Observe que:

  1. O valor total do pedido é composto pela somatória do valor calculado de cada item (precoUnitario * quantidade).

  2. A quantidade total de itens do pedido é composta pela somatória da quantidade de cada item.

## Entrega

Crie um arquivo chamado `stepbystep.md` com tudo o que é preciso para executar sua aplicação.

Para enviar seu código, você pode:

* Enviar a URL do seu repositório para a pessoa responsável pelo seu processo seletivo dentro do CM Dev Academy Java.
