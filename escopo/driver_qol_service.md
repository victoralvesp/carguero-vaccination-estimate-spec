# Serviço de Qualidade de Vida do Motorista (DriverQoLService)

- [Serviço de Qualidade de Vida do Motorista (DriverQoLService)](#serviço-de-qualidade-de-vida-do-motorista-driverqolservice)
  - [Introdução](#introdução)
  - [Requisitos](#requisitos)
    - [DriverQoLService](#driverqolservice)
    - [DbSync](#dbsync)
    - [Web Crawler](#web-crawler)
    - [Esforço estimado](#esforço-estimado)

## Introdução

Serviço responsável por definir previsão de vacinação para todos os motoristas cadastrados. 
Possui dois auxiliares: 
- *DbSync*
    Responsável por sincronizar os dados dos motoristas com a base do micro serviço 
- *Web Crawler*
    Responsável por obter os dados do site (Quando vou ser vacinado?)[https://quandovouservacinado.com]


## Requisitos

### DriverQoLService
1. Deve disponibilizar API para receber dados de estimativas dos estados.
1. Deve disponibilizar API para visualizar datas previstas por motorista.
1. Deve, a cada semana, buscar os dados dos motoristas e para cada um definir qual é a previsão de vacinação
1. Deve persistir as previsões calculadas
3. Deve enviar uma mensagem para a *Mensageria* todas as vezes que a previsão for distinta da atual

1. Desejável: não atualizar a base de dados caso a previsão seja a mesma.

### DbSync
1. Deve, a cada semana, buscar os dados definidos no modelo do [DriverResources](../api/driver_resources.json) e atualizar, caso necessário, os dados da estrutura de persistência local.

### Web Crawler
Deve, a intervalos regulares, buscar os dados do site (Quando vou ser vacinado?)[https://quandovouservacinado.com]

Desejável: Deve utilizar a API definida em operations de [VaccinationEstimateResources](../api/vaccination_estimate_resources.json) para inserir os dados obtidos

### Esforço estimado
- DriverQoLService: G
  - API Recebimento Estimativas: M
  - API Visualização Previsões: M
  - Calcular previsão: M
  - Envio de mensagem: M
- DbSync : M
  - Sincronizar BD: M
- WebCrawler : G
  - Interagir com site: M
  - Extrair informações: M

<br>
> Legenda: Esforços: [P]  pequeno - ~ 2h - 3h;
>                    [M]  médio - ~ 2h - 4h;
>                    [M+] acima da média - ~ 3h - 8h;
>                    [G]  grande - ~ 2d - 3d;
>                    [G+] muito grande - + 3d estudar subdividir o trabalho
  

