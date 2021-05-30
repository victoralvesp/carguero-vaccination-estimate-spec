# Serviço de Notificação (NotificationService)

## Introdução

Serviço responsável por criar notificações e enviar mensagens alertando serviços interessados. 
Possui um auxiliar:
- *FCMProxy*
    Responsável por realizar a comunicação das notificações com o serviço externo Firebase Cloud Messaging


## Requisitos

### NotificationService
1. Deve disponibilizar API para visualizar notificações do motorista.  
   - Desejável: filtro para novas notificações
   - Desejável: API para marcar notificações como lidas
1. Deve receber mensagens da *Mensageria* (seja em lotes ou individualmente) que interessem ao usuário (neste caso, novas previsões de vacinação)
1. Deve gerar notificação com um texto informativo para o motorista informando a possível data de visualização
    - Desejável: deve remover notificações antigas (30 dias ou mais) de tempos em tempos
1. Deve emitir mensagens sempre que um motorista tiver novas notificações para visualizar
 - Desejável: Preparar estrutura para possível inclusão de notificações para embarcadoras e outras entidades que consomem os serviços do Carguero (ou seja, na implementação abstrair o conceito de [usuário/ente notificado] que neste caso concreto é representado pelo motorista)

### Proxy do Firebase Cloud Messaging (FCMProxy)
1. Deve mensagens da *Mensageria* de eventos de novas notificações
2. Deve enviar notificações recebidas para o Firebase Cloud Messaging


### Esforço estimado
- NotificationService: G
  - API Visualização notificasõesNoti: M
  - Receber mensagens da Mensageria: M
  - Gerar notificação: P
  - Envio de mensagem: M
- FCMProxy: M
  - Receber mensagens da Mensageria: M
  - Enviar notificações para FCM: M

<br>
> Legenda: Esforços: [P]  pequeno - ~ 2h - 3h;
>                    [M]  médio - ~ 2h - 4h;
>                    [M+] acima da média - ~ 3h - 8h;
>                    [G]  grande - ~ 2d - 3d;
>    