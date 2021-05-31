# Escopo da funcionalidade Previsão de Vacinação
- [Escopo da funcionalidade Previsão de Vacinação](#escopo-da-funcionalidade-previsão-de-vacinação)
  - [Resumo](#resumo)
  - [Desenvolvimento](#desenvolvimento)
    - [Esforço](#esforço)
    - [Agenda e prazo](#agenda-e-prazo)

## Resumo
- MVP
  - [App](app.md)
    - Configurar FCM 
    - Registrar dispositivo no FCM 
    - Implementação FCM SDK 
    - Alertar Usuário
  - [DriverQoLService](driver_qol_service.md)
    - API Recebimento Estimativas
    - API Visualização Previsões
    - Calcular previsão
    - Envio de mensagem
    - Interagir com site
    - Extrair informações do site
    - Sincronizar dados do motorista
  - [NotificationService](notification_service.md)
  - [Infraestrutura](infraestrutura.md)
    - Persistência
    - Publicação de servidores
    - Integração contínua
    - Entrega contínua

- Desejável
  - App
    - Área de notificações
  - NotificationService
    - Remoção de notifações antigas

## Desenvolvimento

Para garantir a agilidade do processo de desenvolvimento, cada parte do sistema deve evoluir seguindo as informações definidas em [API](../api)
O processo de desenvolvimento será dividido em 7 partes sendo uma delas executada pela squad de DevOps. Cada parte do desenvolvimento pode ser executada independentemente e deve seguir a estrutura Agile. Cada serviço deve ser publicado em ambiente de desenvolvimento e testado e publicado em ambiente UAT antes de ser publicado em produção. 

### Esforço
O esforço estimado para cada serviço é:
- [DriverQoLService](driver_qol_service.md) 
  - Desenvolvimento
    - MVP: 2 DD ~ 4 DD
  - Testes: 2 DD ~ 6 DD
- [NotificationService](notification_service.md)
  - Desenvolvimento
    - MVP: 1.5 DD ~ 2.5 DD  
    - Desejável: ~ 0.5 DD
  - Testes: 2 DD ~ 4 DD
- [App](app.md)
  - Desenvolvimento
    - MVP: 1 DD ~ 2 DD
  - Desejável: 2 DD ~ 3 DD
  - Testes: 2 DD
- [Infraestrutura](infraestrutura.md)
  - Persistência: 2 DD ~ 3 DD
  - Servidores: 2 DD ~ 3 DD
  - Integração contínua: 1 DD ~ 2 DD
  - Entrega contínua: 1 DD ~ 2 DD

> Legenda: DD: desenvolvedor-dia

### Agenda e prazo

Considerando dois desenvolvolvedores para os serviços e o aplicativo, dois QAs e um desenvolvedor do squad de DevOps a estimativa de prazo é de 9 dias 

Mais detalhes em [Agenda desenvolvimento](diagrama-desenvolvimento.svg)

