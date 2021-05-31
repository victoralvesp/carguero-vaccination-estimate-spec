# Especificação Notificação de vacinação - Carguero
- [Especificação Notificação de vacinação - Carguero](#especificação-notificação-de-vacinação---carguero)
  - [Objetivo](#objetivo)
  - [Estratégia e arquitetura](#estratégia-e-arquitetura)
  - [Definição da API](#definição-da-api)
  - [Escopo e desenvolvimento](#escopo-e-desenvolvimento)

## Objetivo
Este projeto visa introduzir um alerta no app Carguero com um indicativo de uma data provável para a vacinação dos motoristas.

## Estratégia e arquitetura

A estratégia adotada foi dividir o problema em duas partes, cálculo da data provável de vacinação e alerta ao usuário, e realizá-las de forma assíncrona. Para isso optou-se por utilizar um *Message Broker* em conjunto com o *Firebase Cloud Messaging* para enviar notificações do tipo *Push Notification* para o app.

Definições e diagramação da arquitetura podem ser encontrados em [Arquitetura](arquitetura/)

## Definição da API

As definições dos modelos, operações e mensagens das api podem ser encontrados em [API](api/)

## Escopo e desenvolvimento
A divisão do problema e modularização permitem que o processo de desenvolvimento ocorra, em sua grande parte, em paralelo e permite que a solução seja implementada de forma robusta em aproximadamente uma *Sprint*.

Mais detalhes em [Escopo](escopo/)

