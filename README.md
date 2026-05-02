# Diagrama de Contexto - Sistema Integrado de Monitoramento e Gestão de Configuração para Máquinas Agrícolas

## 1. Visão geral do sistema

O sistema proposto é uma plataforma central para monitoramento, controle e gestão de configuração de máquinas agrícolas conectadas. Ele permite que operadores acompanhem, em tempo real, o desempenho e a saúde das máquinas, enquanto administradores podem consultar, alterar e aplicar configurações nos equipamentos da frota. Além disso, o sistema se integra a serviços externos, como dados meteorológicos, para apoiar decisões operacionais e manutenção preventiva.

No C4 Model, este é um **Diagrama de Contexto**, ou seja, ele mostra o sistema principal em relação aos usuários, dispositivos e sistemas externos com os quais ele interage, sem detalhar ainda sua arquitetura interna.

## 2. Atores e sistemas externos
### Atores:
- **Operador Agrícola**: é o usuário que utiliza o sistema no dia a dia para acompanhar o funcionamento das máquinas, visualizar alertas, consultar dados de desempenho e tomar decisões operacionais no campo. Ele interage com o sistema por meio de uma interface web ou mobile.

- **Administrador de Configuração**: é o usuário responsável por gerenciar parâmetros técnicos e operacionais das máquinas. Ele utiliza o sistema para criar, alterar, validar e aplicar configurações, garantindo que os equipamentos estejam funcionando de acordo com os padrões definidos pela empresa.

### Sistemas externos:
- **Máquinas Agrícolas com IoT**: são os equipamentos monitorados pelo sistema. Elas enviam dados de telemetria, como localização, velocidade, consumo, temperatura, falhas, status de sensores e condições de operação. Também podem receber comandos ou atualizações de configuração enviados pelo sistema.

- **Plataforma de Integração / Middleware**: funciona como uma ponte entre as máquinas IoT e o sistema central. Ela é responsável por receber os dados enviados pelas máquinas, tratar protocolos de comunicação e encaminhar essas informações ao sistema. Também pode enviar comandos do sistema de volta para os equipamentos.

- **Serviço de Dados Meteorológicos**: é um sistema externo que fornece informações sobre clima, previsão do tempo, chuva, temperatura, vento e outras variáveis ambientais. Esses dados ajudam o sistema a apoiar decisões agrícolas e ações de manutenção preventiva.

- O **Banco de Dados Central** é o local onde são armazenadas as informações principais do sistema, como histórico de telemetria, configurações das máquinas, registros de eventos, alertas, logs e dados operacionais. Neste contexto, ele faz parte da infraestrutura do próprio sistema, mas foi representado no diagrama para deixar claro onde os dados ficam persistidos.

## 3. Fronteiras do sistema

A fronteira do **Sistema Integrado de Monitoramento e Gestão de Configuração** inclui as funcionalidades de monitoramento em tempo real, visualização de dados, emissão de alertas, gestão de configurações, registro histórico das informações e integração com dados meteorológicos. O sistema é responsável por transformar os dados recebidos das máquinas em informações úteis para operadores e administradores.

Ficam fora da fronteira do sistema as responsabilidades específicas de comunicação física com sensores, firmware embarcado das máquinas, coleta direta dos sinais dos dispositivos IoT e fornecimento dos dados climáticos. Essas funções são executadas pelas máquinas agrícolas, pela plataforma de integração e pelo serviço meteorológico externo. O sistema central consome essas informações e as utiliza para monitoramento, análise e configuração.

## 4. Diagrama de Contexto em Mermaid
![Diagrama-C4-Miro](image.png)
```mermaid
flowchart LR

    Operador["Operador Agrícola"]
    Admin["Administrador de Configuração"]

    Maquinas["Máquinas Agrícolas com IoT"]
    Middleware["Plataforma de Integração / Middleware"]
    Clima["Serviço de Dados Meteorológicos"]

    subgraph Sistema["Fronteira do Sistema Integrado de Monitoramento e Gestão de Configuração"]
        App["Sistema Central<br/>Monitoramento, alertas e gestão de configurações"]
        DB["Banco de Dados Central<br/>Telemetria, configurações, eventos e histórico"]
        App <--> DB
    end

    Operador -->|"Consulta status, desempenho, alertas e saúde das máquinas"| App
    App -->|"Exibe dashboards, alertas e informações operacionais"| Operador

    Admin -->|"Cria, altera e aplica configurações"| App
    App -->|"Mostra histórico, validações e status das configurações"| Admin

    Maquinas -->|"Enviam telemetria, sensores, falhas e localização"| Middleware
    Middleware -->|"Encaminha dados tratados das máquinas"| App

    App -->|"Envia comandos e novas configurações"| Middleware
    Middleware -->|"Entrega comandos e configurações"| Maquinas

    App -->|"Consulta previsão do tempo e condições climáticas"| Clima
    Clima -->|"Retorna dados meteorológicos"| App
````

## 5. Explicação do diagrama

O diagrama mostra que o sistema central é o núcleo da solução. Ele recebe dados das máquinas agrícolas por meio da plataforma de integração, armazena essas informações no banco de dados central e apresenta os dados aos usuários por meio de telas de monitoramento, alertas e relatórios.

O Operador Agrícola usa o sistema principalmente para acompanhar o funcionamento da frota e tomar decisões rápidas no campo. Já o Administrador de Configuração utiliza o sistema para manter os equipamentos corretamente parametrizados, enviando configurações para as máquinas quando necessário.

As máquinas agrícolas não se comunicam diretamente com os usuários. Elas enviam dados para o middleware, que atua como intermediário técnico entre os dispositivos IoT e o sistema central. Isso torna a arquitetura mais organizada, pois o sistema central não precisa lidar diretamente com todos os protocolos e detalhes de comunicação dos equipamentos.

A integração com o serviço meteorológico permite que o sistema complemente os dados das máquinas com informações externas de clima. Com isso, é possível apoiar decisões como manutenção preventiva, ajuste de operação, planejamento de atividades agrícolas e redução de riscos operacionais.

## 6. Conclusão

O Diagrama de Contexto deixa claro que o sistema atua como uma camada central de inteligência, conectando operadores, administradores, máquinas agrícolas, middleware, banco de dados e serviços externos. Sua principal responsabilidade é transformar dados operacionais e climáticos em informações úteis para monitoramento, controle, configuração e tomada de decisão no ambiente agrícola.
