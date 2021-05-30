# App
- [App](#app)
  - [Introdução](#introdução)
  - [Requisitos](#requisitos)
    - [Firebase Cloud Messaging](#firebase-cloud-messaging)
    - [Alertar usuário](#alertar-usuário)
    - [Esforço estimado](#esforço-estimado)
          - [<a name="note-1"><sup>1</sup></a>: para receber mensagens é necessário registrar o dispositivo junto (https://firebase.google.com/docs/cloud-messaging/android/client)](#sup1sup-para-receber-mensagens-é-necessário-registrar-o-dispositivo-junto-httpsfirebasegooglecomdocscloud-messagingandroidclient)

## Introdução

Serão necessárias alterações no App para adequar ao push de mensagens vindos do *Firebase Cloud Messaging*

## Requisitos

O *App* deve receber mensagens vindas do *Firebase Cloud Messaging (FCM)* e salvá-las em memória interna.

### Firebase Cloud Messaging
1. Necessário configuração no console do *Firebase Cloud Messaging*
2. Necessário registro do dispositivo no grupo de dispositivos do usuário após login
3. Necessário implementação do *Firebase Cloud Messaging SDK*

### Alertar usuário
1. Ao entrar no *App*, usuário deve conseguir ver que há uma nova previsão de vacinação
1. Desejável: Deve disponibilizar uma área para visualização de notificações

### Esforço estimado
- Configurar FCM : M
- Registrar dispositivo no FCM : M
- Implementação FCM SDK : M
- Alertar Usuário: M




###### <a name="note-1"><sup>1</sup></a>: para receber mensagens é necessário registrar o dispositivo junto (https://firebase.google.com/docs/cloud-messaging/android/client)

<br>
> Legenda: Esforços: [P]  pequeno - ~ 2h - 3h;
>                    [M]  médio - ~ 2h - 4h;
>                    [M+] acima da média - ~ 3h - 8h;
>                    [G]  grande - ~ 2d - 3d;
>                    [G+] muito grande - + 3d estudar subdividir o trabalho
  