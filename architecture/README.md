# Arquitetura

## Resumo

Para definir as previsões de data de vacinação dos motoristas, a cada semana o **Serviço de Qualidade de Vida do Motorista (DriverQoLService)** é executado em lotes de 10000 motoristas separados por pelo menos uma hora. Durante a execução de cada lote o *DriverQoLService* obtem os dados do motorista de estrutura pré-sincronizada dos dados do motorista e das informações do site [Quando vou ser vacinado](https://quandovouservacinado.com/).
Tais previções são, então, lidas pelo  **Serviço de Notificação (NotificationService)** e processadas em notificações que são posteriormente enviadas, através do **Proxy do Firebase Cloud Messaging [FCMProxy]** para cada dispositivo do motorista

Para uma visualização completa da arquitetura, ver [diagrama](diagram.md)

## Introdução

Levando em consideração o volume de possíveis estimativas necessárias por semana e os possíveis bloqueios de recursos que um acúmulo de processamentos pode causar na infraestrutura de dados dos motoristas, foi definido que as principais características arquiteturais do Sistema seriam Custo/Mantenabilidade e Modularidade. Adicionalmente, deseja-se que o Sistema integre-se facilmente com a estrutura existente e possa ser reutilizado para outros fins, de modo que almeja-se também as características de extensibilidade e agilidade

Na seção seguinte, define-se como cada característica foi inserida na arquitetura inicial do projeto.

## Características

### Custo/Mantenabilidade

Para minimizar os custos de operação do Sistema, definiu-se uma estrutura de mensageria e processamento de estimativas assíncrono o que possibilita o consumo de uma quantidade pré-estabelicida de dados em intervalos bem definidos e que disposnibiliza os resultados em formato de Push Notification. 
O consumo das informações do motorista e definição da data prevista de vacinação são feitos em serviço separado, denomidado de **Serviço de Qualidade de Vida do Motorista (DriverQoLService)**, e disponibilizados através de mensagem enviada pela Mensageria.

### Modularidade
Para garantir a segregação da responsabilidade de definir a previsão de vacinação e de notificar o usuário, definiu-se o **Serviço de Notificação (NotificationService)**, cuja responsabilidade é ouvir mensagens de interesse, neste caso mensagens do *DriverQoLService* do usuário e criar textos informativos para este, denominados de *notificações*. 
Além disso, para garantir a independência do *DriverQoLService* de requisições externas optou-se por utilizar uma estrutura de BD de leitura para as informações do motorista, seguindo modelo de CQRS. Este BD de leitura tem uma consistência eventual garantida por um *background worker* que é executado em intervalos pré-estabelecidos <sup>[1](#note-1)</sup>.
As notificações são disponibilizadas através de API e de mensagens enviada a mensageria. 

A partir das mensages do *NotificationService*, o **Proxy do Firebase Cloud Messaging [FCMProxy]** enviará uma mensagem para o grupo de dispositivos do usuário

### Extensibilidade
A decisão de segregar a responsabilidade de notificar o usuário (*NotificationServie*), da de processar as informações (*DriverQoLService*) e da de mostrar as informações (*App*) levou em conta também a extensibilidade de cada uma dessas partes. Ao separar estas responsabilidades, tem-se a garantia de que será possível adicionar novas notificações e novos consumidores para estas noticações

### Agilidade
A separação citada também garante o desenvolvimento de cada funcionalidade por times distintos, o que garante a agilidade do sistema. 
A separação da infraestrutura destes serviços também contribui para esta característica

## Detalhamento

### Serviço de Qualidade de Vida do Motorista (DriverQoLService)

O *DriverQoLService* é o responsável pela definição da previsão de vacinação de cada motorista bem como notificar outros serviços quando novas previsões são geradas

#### **Obtenção de dados**
O *DriverQoLService* utiliza um **Web Crawler** para obter as informações de estimativa de vacinação de cada estado. Desejável: separar execução deste da execução do processamento de vacinação

Ele também utiliza um **BackgroundWorker (denominado DbSync)** para sincronizar os dados do [motorista](../resources/driver_resources.json). Desejável: separar execução deste da execução do processamento de vacinação

#### **Mensagens**

O *DriverQoLService* deve enviar mensagem a *Mensageria (Message Broker)* toda vez que uma previsão de vacinação diferente para o motorista é gerada

Desejável: Não persistir previsão a menos que esta difira da previsão atual para o motorista

> Notas: Para poupar custos, decidiu-se que não é necessário que previsões antigas se mantenham persistidas. 

### Serviço de Notificação (NotificationService)

É o responsável por gerar mensagens para o usuário (denominadas **notificações**) e disponibilizá-las para consumo bem como notificar outros serviços quando novas notificações são geradas

#### **Obtenção de dados**
O *NotificationService* deve ler novas previsões de vacinação através da mensageria.
Desejável: abstrair leitura de mensagens para que outros tipos de eventos de interesse do usuário também sejam lidos

#### **Mensagens**

O *NotificationService* deve enviar mensagem a *Mensageria (Message Broker)* toda vez que uma nova notificação a usuário é gerada

Desejável: Persistir status de leitura da mensagem

### Proxy do Firebase Cloud Messaging [FCMProxy]

É o responsável por ouvir as notificações para os usuários e enviar para o grupo correspondente do [*Firebase Cloud Messaging*](https://firebase.google.com/docs/cloud-messaging/android/first-message)

#### **Obtenção de dados**
O *FCMProxy* deve ler novas notificações através da mensageria.


## Tecnologias Sugeridas

- DriverQoLService - Pod de Kubernetes (com AKS) + MongoDb (com CosmoDB)
- DbSync - Azure Function
- NotificationService - Pod de Kubernetes (com AKS) + MongoDb (com CosmoDB)
- ProxyFCM - Azure Function
- Message Broker - Kafka ou RabbitMQ

<br>
<br>
<br>


###### <a name="note-1">1</a>:  Como não espera-se que os dados de cadastro sejam alterados com frequencia pode-se utilziar o intervalo de uma semana
