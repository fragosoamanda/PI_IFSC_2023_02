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
      <a href="#diagrama-de-funcionamento">Diagrama de Funcionameto</a>
    </li>
    <li>
      <a href="#componentes-utilizados">Componentes Utilizados</a>
      <ul>
        <li><a href="#hardware">Hardware</a></li>
        <li><a href="#software">Software</a></li>
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

Este documento detalha a concepção de um sistema integrado de monitoramento de vazamento de gás de cozinha, monóxido de carbono e Gás natural, projetado para aumentar a segurança e o bem-estar dos usuários em ambientes residenciais.
A finalidade do projeto é, através do sistema de monitoramento de gases específicos, prevenir a ocorrência de potenciais incidentes causados principalmente em ambientes domésticos que podem resultar em um sinistro ou até fatalidades.

Visando a autonomia do usuário, os sensores estarão embutidos em uma placa com comunicação com o módulo central e poderão ser dispostos dentro de uma determinada área que esteja no alcance da ocorrência de vazamento. Assim, o usuário poderá escolher quais pontos da residência deseja monitorar, como nas proximidades de um fogão, botijão, lareira, aquecedor, etc.

## Objetivos

- Detectar vazamentos de certos gases de forma eficiente.
- Acionar alarmes e sistemas de segurança em casos de vazamento.
- Fornecer uma interface de monitoramento e controle ao usuário (Extra).

## Requisitos Principais

1. **Detecção de Vazamento**: Utilizar sensores de gás MQ-5, MQ-6 e MQ-7 (para detectar vazamentos de gás natural, gás de cozinha e  monóxido de carbono, respectivamente).
2. **Sirene de Emergência**: Ativar uma sirene de emergência no caso de detecção de vazamento.
3. **Corte de Gás**: Interromper automaticamente o fornecimento de gás através de uma válvula solenoide (Para o projeto atual será utilizado uma solenoide simples de demonstração, sendo necessário uma solenoide apropriada em um ambiente real).
4. **Ventilação**: Ligar um sistema de ventilação para dissipar o gás acumulado.
5. **Corte de Energia Elétrica**: Desligar a energia elétrica da residência para prevenir possíveis acidentes (Mantendo apenas os canais dos atuadores alimentados diretamente pela central).
6. **Alimentação por Bateria**: Os modulos de sensoriamento estarão distribuídos pela casa utilizando uma alimentação por bateria, esta por sua vez será removível e de tempos em tempos será de cargo do usuário retirar a bateria e carregar, mantendo os módulos de sensoriamento ativos e carregados.

## Requisitos Extras

1. **Servidor de Logs**: Desenvolver um servidor para armazenar logs de concentração de gás (ThingSpeak).
2. **Aplicativo Móvel**: Desenvolver um aplicativo móvel para monitoramento em tempo real e configurações do sistema.
3. **Notificações**: Enviar notificações para o celular do usuário em casos de vazamento de gás.
4. **Sistema de proteção**: Desenvlver um sistema de proteção pull-up/pull-down que irá proteger o sistema.


## Diagrama de Funcionamento

<div style="display: flex; width: 100%; align-items: center; justify-content: space-around; gap: 20px;">

<img src="./WhatsApp Image 2023-09-26 at 20.05.40.jpeg" alt="Diagrama de Funcionamento" height="300px"/>

</div>
<br />

Haverão placas de sensoriamento, cada uma possuindo três sensores distintos, uma bateria de lítio e um ESP-32. A quantidade de placas é equivalente ao número de pontos monitorados (para os testes, necessitaremos de apenas duas). 

Essas placas de sensoriamento se comunicarão ao ESP-32 central via ferramenta "ESPNOW", que por sua vez ficará localizado na caixa de energia geral da residência e acionará os atuadores que irão fazer o controle externo dos relés e bobinas que ativam a sirene, o ventilador, a válvula solenoide de corte da válvula geral de gás e o disjuntor geral da casa.

O projeto será composto por dois tipos de dispositivos: O sistema de sensoriamento será composto de dispositivos pequenos que estarão dispostos pelo ambiente a ser monitorado e transmitirão de tempo em tempo os dados para a central, esta por sua vez estará no quadro de eneriga da casa conectada diretamente na rede e será responsável por receber os dados dos dispositivos de sensoriamento bem como fazer o controle dos atuadores a serem controlados. No projeto atual a central será responsável por controlar 4 canais do quadro, um deles será a própria energia do quadro geral da casa, sendo responsável por desligar a distribuição de energia para o ambiente no caso de detecção de algum gás inflamável, os outros canais serão distribuídos para um sistema de feedback sonoro que será uma sirene, um sistema de ventilação e um sistema de controle de fluxo de gás da residência. Esses atuadores terão cabeamento comum que será levado da central até a localidade onde estarão instalados na residência e serão responsáveis por suprir o usuário com feedback de um possível sinistro bem como cortar o fornecimento de gás utilizando uma válvula solenoide e iniciar a ventilação da casa caso seja detectado um possível vazamento na casa.

Esse módulo central também enviará logs em tempo real a um sistema de monitoramento (ThingSpeak), possibilitando o usuário a acompanhar as medições.

## Componentes Utilizados

### Hardware

- **Microcontrolador ESP32 com Wi-Fi**: Atua como cérebro do sistema, utilizado em ambos, módulos de sensoriamento e central de controle.
- **Sensores de Gás MQ-5, MQ-6 e MQ-7**: Utilizado para detecção de vazamento de gás.
- **Relés**: Utilizados para controle de atuadores como ventiladores, válvula e controle do corte de energia da casa (Apenas posicionados na central de controle).
- **Buzzer (Sirene)**: Para alerta audível em caso de vazamento.
- **Ventilador**: Para ventilação do ambiente em caso de vazamento.
- **Fonte de Alimentação**: Para alimentação elétrica da central de controle (Deriva sua fonte de energia direto da entrada principal de energia da casa).
- **Válvula Solenoide**: Para corte da alimentação de gás (No projeto atual apenas uma solenóide comum, para viés comercial precisa ser uma apropriada para gases).
- **Sistema de carregamento/balanceamento**: Para alimentação do sistema em caso de falta de energia elétrica.
- **Contatora Elétromecânica**: Utilizada para fazer o corte de energia da casa (No projeto atual apenas será utilizado um relé para demonstrar, em um cenário real devido a carga necessária ser suportada pela contatora, deverá ser utilizado uma contatora adequada, sendo esta apenas acionada pelo relé da central)
- **Células de lítio**: Para servir de fonte de alimentação para os módulos de sensoriamento.

### Software

- Código desenvolvido em C/C++ para o microcontrolador Esp32, sendo dividido em duas codebases, uma para os módulos de sensoriamento e outra para o módulo central. O código dos módulos de sensoriamento será responsável por realizar uma medição dos sensores de tempos em tempos e transmitir um log desses dados para a central. Por sua vez a central deverá receber estes dados e fazer o controle necessário dos atuadores bem como restrasmitir esses dados para a nuvem.

#### Extras

- Servidor para armazenamento e monitoramento (ThingSpeak).
- Aplicativo móvel de monitoramento.


## Pontos chaves do sistema

### Monitoramento

#### O que o sistema possui de Monitoramento:

- **Sensores de Gás**: O sistema utiliza múltiplos sensores MQ-5, MQ-6 e MQ-7 para detectar a presença de certos gases.

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
