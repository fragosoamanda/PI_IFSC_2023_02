<!-- PROJECT LOGO -->
<div align="center">
  <h3 align="center">Sistema de Monitoramento de Vazamento de Gás de Cozinha</h3>

  <p align="center">
    <strong>(Conceive)</strong>
    <br />
</div>

## Índice

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#introdução">Introdução</a>
    </li>
    <li>
      <a href="#objetivos">Objetivos</a>
    </li>
    <li>
      <a href="#requisitos-principais">Requisitos Principais</a>
    </li>
    <li>
      <a href="#requisitos-extras">Requisitos Extras</a>
    </li>
    <li>
      <a href="#componentes-utilizados">Componentes Utilizados</a>
      <ul>
        <li><a href="#hardware">Hardware</a></li>
        <li><a href="#software">Software</a></li>
      </ul>
    </li>
    <li>
      <a href="#arquitetura-do-sistema">Arquitetura do Sistema</a>
    </li>
    <li>
      <a href="#desenvolvimento">Desenvolvimento</a>
      <ul>
        <li><a href="#configuração-inicial">Configuração Inicial</a></li>
        <li><a href="#programação">Programação</a></li>
        <li><a href="#testes">Testes</a></li>
      </ul>
    </li>
    <li>
      <a href="#pontos-chaves-do-sistema">Pontos Chaves do Sistema</a>
      <ul>
        <li><a href="#monitoramento">Monitoramento</a></li>
        <li><a href="#controle">Controle</a></li>
        <li><a href="#ações">Ações</a></li>
        <li><a href="#visualização-e-feedback">Visualização / Feedback</a></li>
      </ul>
    </li>
    <li>
      <a href="#plano-de-ação-para-implementação-de-projeto-piloto">Plano de Ação para Implementação de Projeto Piloto</a>
    </li>
  </ol>
</details>


---

## Introdução

Este documento detalha a concepção de um sistema integrado de monitoramento de vazamento de gás de cozinha, projetado para aumentar a segurança e o bem-estar dos usuários em ambientes residenciais.

## Objetivos

- Detectar vazamentos de gás de cozinha de forma eficiente.
- Acionar alarmes e sistemas de segurança em casos de vazamento.
- Fornecer uma interface de monitoramento e controle ao usuário (Extra).

## Requisitos Principais

1. **Detecção de Vazamento**: Utilizar sensores de gás MQ-5 para detectar vazamentos de gás de cozinha.
2. **Sirene de Emergência**: Ativar uma sirene de emergência no caso de detecção de vazamento.
3. **Corte de Gás**: Interromper automaticamente o fornecimento de gás através de uma válvula solenoide.
4. **Ventilação**: Ligar um sistema de ventilação para dissipar o gás acumulado.
5. **Corte de Energia Elétrica**: Desligar a energia elétrica da residência para prevenir possíveis acidentes.
6. **Alimentação por Bateria**: Manter o sistema alimentado mesmo em caso de falta de energia elétrica ou durante o corte de energia principal.

## Requisitos Extras

1. **Servidor de Logs**: Desenvolver um servidor para armazenar logs de concentração de gás.
2. **Aplicativo Móvel**: Desenvolver um aplicativo móvel para monitoramento em tempo real e configurações do sistema.
3. **Notificações**: Enviar notificações para o celular do usuário em casos de vazamento de gás.

## Componentes Utilizados

### Hardware

- **Microcontrolador ESP32 com Wi-Fi**: Atua como cérebro do sistema, lê dados dos sensores e controla os atuadores.
- **Sensor de Gás MQ-5**: Utilizado para detecção de vazamento de gás.
- **Relés**: Utilizados para controle de atuadores como ventiladores e válvulas.
- **Buzzer (Sirene)**: Para alerta audível em caso de vazamento.
- **Ventilador**: Para ventilação do ambiente em caso de vazamento.
- **Fonte de Alimentação**: Para alimentação elétrica do sistema.
- **Válvula Solenoide**: Para corte da alimentação de gás.
- **Contatora Residencial**: Para corte da energia elétrica da residência.
- **Sistema de carregamento/balanceamento**: Para alimentação do sistema em caso de falta de energia elétrica.
- **Células de lítio**: Para armazenamento de energia em caso de falta de energia elétrica.

### Software

- Código desenvolvido em C/C++ para o microcontrolador Esp32.

#### Extras

- Servidor para armazenamento e monitoramento (ThingSpeak).
- Aplicativo móvel de monitoramento.

## Arquitetura do Sistema

A arquitetura consiste em sensores espalhados pela cozinha para detectar possíveis vazamentos de gás conectados ao Esp32, que por sua vez está conectado a relés que controlam a sirene, o ventilador, a válvula solenoide e a energia da casa. Além disso o sistema possui uma bateria para manter o funcionamento em caso de falta de energia elétrica.

## Desenvolvimento

### Configuração Inicial

1. **Conexão dos Sensores**: Conectar a rede de sensores MQ-5 ao Esp32.
2. **Conexão dos Atuadores**: Conectar a sirene, o ventilador, e a válvula solenoide aos relés, que são controlados pelo Esp32.

### Programação

1. **Algorítmo de Detecção**: Implementar o algoritmo que analisa os dados dos sensores MQ-5.
2. **Acionamento de Atuadores**: Programar o Esp32 para acionar os atuadores conforme necessário.

### Testes

1. **Teste de Detecção**: Certificar que o sistema detecta com precisão vazamentos.
2. **Teste de Atuadores**: Verificar o correto funcionamento dos atuadores.

## Pontos chaves do sistema

### Monitoramento

#### O que o sistema possui de Monitoramento:

- **Sensores de Gás (MQ-5)**: O sistema utiliza múltiplos sensores MQ-5 para detectar a presença de gás.

### Controle

#### O que o sistema performa de Controle:

- **Corte de Alimentação de Gás**: Uma válvula solenoide é ativada para cortar o fornecimento de gás em caso de vazamento.
- **Corte de Energia Elétrica**: Um contatora residencial ou uma adaptação em 3D de um disjuntor é utilizado para cortar o fornecimento elétrico da residência em caso de vazamento de gás.

### Ações

#### Quais Ações o sistema performa:

- **Disparo de Sirene de Emergência**: Um buzzer (sirene) é acionado para alertar os moradores e vizinhos sobre o vazamento.
- **Acionamento de Ventilação**: Um ventilador é ligado para dispersar o gás acumulado no ambiente onde o vazamento foi detectado.

### Visualização e Feedback

#### Quais formas de Visualização/Feedback principal ou extra o sistema oferece:

- **Logs de Concentração de Gás (Extra)**: Um servidor armazena os dados dos logs de concentração de gás para monitoramento.
- **Aplicativo de Monitoramento (Extra)**: Desenvolvimento de um app para monitoramento em tempo real e configuração do sistema.
- **Notificações (Extra)**: Sistema de envio de notificações para o celular do usuário em casos de vazamento de gás.

## Plano de Ação para Implementação de Projeto Piloto

1. **Pesquisa e Aquisição / Compra de Componentes**: Adquirir todos os componentes necessários listados acima.
2. **Montagem do Protótipo**: Realizar a montagem inicial dos componentes.
3. **Desenvolvimento de Software**: Implementar o código em C/C++ para ESP32.
4. **Testes de Detecção de Gás**: Calibrar os sensores MQ-5 e testar a detecção de gás.
5. **Testes de Atuadores**: Verificar o funcionamento de relés, buzzer, ventilador, válvula solenoide e contatora.
6. **Integração do Sistema**: Integrar todas as partes e realizar testes funcionais.
7. **Desenvolvimento de Extras**: Se necessário, desenvolver o servidor e aplicativo para monitoramento e armazenamento de logs.
8. **Testes Finais e Ajustes**: Realizar testes finais e fazer ajustes conforme necessário.
