# DevOps

Será necessária organização junto com a squad de DevOps para alinhamento dos elementos de infraestrutura necessários para a nova funcionalidade.

Os tópicos a serem discutidos são:
- Infraestrutura do Serviço de Qualidade de Vida do Motorista [DriverQoLService]
- Infraestrutura do Serviço de Notificação [NotificationService]
- Infraestrutura para Web Crawler
- Infraestrutura da Mensageria
- Configuração do Firebase Cloud Messaging [FCM]


## Requisitos de infraestrutura para o Serviço de Qualidade de Vida do Motorista [DriverQoLService]

O Serviço de Qualidade de Vida do Motorista [DriverQoLService] necessita de uma estrutura de persistência e de servidores para receber as requisições e consumir as mensagens da Mensageria

### Persistencia
Para a persistencia do serviço se faz necessária uma estrutura (preferencialmente em NoSql) para previsão de vacinação seguindo os modelos de [VaccinationEstimateResource](resources/vaccination_estimate_resources.json) ver [sugestão](#note_1).
Para garantir a publicação correta em produção é necessário criar um processo automatizado para a publicação dessa estrutura.


### Servidor
Necessário definição estrutura de parâmetros para Kubernetes [k8s] para subir um serviço com API Rest
Para garantir a publicação correta em produção é necessário criar um processo automatizado para a publicação dessa estrutura.

### Integração contínua (Continuos integration)
Necessário a definição e criação de processo de integração de código e execução de testes automátizados  exclusivo para este serviço

### Entrega contínua (Continuos delivery)
Necessário a definicão e criação de processo automatizado para compilar e publicar o código de um repositório exclusivo para este serviço


Esforço estimado
- Persistência 
  -  Implementação: M
  -  Automatização: M+
  -  Teste: P

- Servidor
  -  Implementação: P
  -  Automatização: P
  -  Teste: P

- Integração contínua (Continuos integration)
  - Implementação: M
  - Publicação: P
  
- Entrega contínua (Continuos delivery) 
  - Implementação: M
  - Publicação: P


## Requisitos de infraestrutura para o Serviço de Notificação [NotificationService]

O Serviço de Notificação [NotificationService] necessita de uma estrutura de persistência e de servidores para receber as requisições e consumir as mensagens da Mensageria

### Persistencia
Para a persistencia do serviço se faz necessária uma estrutura (preferencialmente em NoSql) para notificações seguindo o [NotificationsResource](resources/notifications_resources.json)
Para garantir a publicação correta em produção é necessário criar um processo automatizado para a publicação dessa estrutura.

### Servidor
Necessário definição estrutura de parâmetros para Kubernetes [k8s] para subir um serviço com API Rest
Para garantir a publicação correta em produção é necessário criar um processo automatizado para a publicação dessa estrutura.

### Integração contínua (Continuos integration)
Necessário a definição e criação de processo de integração de código e execução de testes automátizados  exclusivo para este serviço

### Entrega contínua (Continuos delivery)
Necessário a definicão e criação de processo automatizado para compilar e publicar o código de um repositório exclusivo para este serviço


Esforço estimado
- Persistência 
  -  Implementação M
  -  Automatização M+
  -  Teste P

- Servidor
  -  Implementação P
  -  Automatização P
  -  Teste P

- Integração contínua (Continuos integration)
  - Implementação: M
  - Publicação: P
  
- Entrega contínua (Continuos delivery) 
  - Implementação: M
  - Publicação: P
  

## Requisitos de infraestrutura para o Web Crawler

### Servidor
Necessário definição estrutura de parâmetros para Kubernetes [k8s] para subir um serviço com API Rest
Para garantir a publicação correta em produção é necessário criar um processo automatizado para a publicação dessa estrutura.

### Integração contínua (Continuos integration)
Necessário a definição e criação de processo de integração de código e execução de testes automátizados  exclusivo para este serviço

### Entrega contínua (Continuos delivery)
Necessário a definicão e criação de processo automatizado para compilar e publicar o código de um repositório exclusivo para este serviço

- Servidor
  -  Implementação P
  -  Automatização P
  -  Teste P

- Integração contínua (Continuos integration)
  - Implementação: M
  - Publicação: P
  
- Entrega contínua (Continuos delivery) 
  - Implementação: M
  - Publicação: P


## Requisitos de infraestrutura para Mensageria

Necessário serviço de mensageria com garantia de pelo menos uma entrega (At-least-once delivery).


Esforço estimado
- Implementação M+
- Publicação M
 

## Requisitos para o Firebase Cloud Messaging [FCM]

Necessário configurar o serviço do Google [Firebase Cloud Messaging - FCM](https://firebase.google.com/docs/cloud-messaging/) para envio de mensagens para grupos de dispositivos (os dispositivos configurados para o Motorista).

Esforço estimado
- Implementação M+




> ##### <a name="note_1"></a> Sugestão: para o modelo [state_vaccination_estimates] utilizar tabela em NoSql com entradas por estado com arrays com as previsões, em meses, para cada uma das idades. Ex: 
> `{
        {
            "state":"SC",
            "predictions": [
                ...
                {
                    "age":"29",
                    "prediction":"12:10:00:00:00.000"
                },
                {
                    "age":"30",
                    "prediction":"12:00:00:00:00.000"
                },
                {
                    "age":"31",
                    "prediction":"11:20:00:00:00.000"
                },
                ...
            ]
        },
        {
            "state":"SP",
            "predictions": [
                ...,
                {
                    "age":"29",
                    "prediction":"6:24:00:00:00.000"
                },
                {
                    "age":"30",
                    "prediction":"6:16:00:00:00.000"
                },
                {
                    "age":"31",
                    "prediction":"6:08:00:00:00.000"
                },
                ...
            ]
        },
        ...
    ]
}`

> Legenda: Esforços: [P]  pequeno - ~ 2h - 3h;
>                    [M]  médio - ~ 2h - 4h;
>                    [M+] acima da média - ~ 3h - 8h;
>                    [G]  grande - ~ 2d - 3d;
>                    [G+] muito grande - + 3d estudar subdividir o trabalho
  