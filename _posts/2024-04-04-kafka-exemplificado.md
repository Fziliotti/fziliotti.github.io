---
title: "Kafka - exemplo prático"
author: fziliotti
date: 2024-04-04 04:33:00 +0800
categories: ["Desenvolvimento"]
tags: [backend]
---

## O que é Kafka?

Kafka é uma plataforma de streaming distribuída desenvolvida inicialmente pelo LinkedIn e posteriormente tornada um projeto de código aberto pela Apache Software Foundation. Ele fornece uma infraestrutura escalável e de alto desempenho para o processamento de fluxos de dados em tempo real.

Em termos simples, Kafka é um sistema de mensagens distribuído que permite que você publique, armazene, processe e consuma streams de dados em tempo real de maneira confiável e eficiente. Ele é altamente escalável, tolerante a falhas e oferece recursos robustos para lidar com grandes volumes de dados.

A arquitetura do Kafka é composta por vários componentes principais:

- Producer (Produtor): É responsável por publicar mensagens em tópicos específicos do Kafka. Os produtores podem ser aplicativos ou sistemas que geram dados em tempo real.

- Broker: São os servidores do Kafka que armazenam os dados publicados pelos produtores em tópicos específicos. Cada tópico é particionado e replicado em vários brokers para garantir a tolerância a falhas e a escalabilidade.

- Topic (Tópico): É uma categoria de fluxo de dados no Kafka. Os dados publicados pelos produtores são organizados em tópicos, que podem ter vários partições para distribuir a carga de trabalho e permitir o processamento paralelo.

- Consumer (Consumidor): São os aplicativos ou sistemas que consomem os dados dos tópicos do Kafka. Eles podem ler dados de um ou mais tópicos e processá-los de acordo com a lógica de negócios específica.

- ZooKeeper: Kafka depende do ZooKeeper para coordenação e gerenciamento de brokers, detectar falhas e eleger líderes de partições.


## Exemplo prático

### Cenário:
Uma empresa de transporte de mercadorias precisa rastrear em tempo real a localização de seus veículos em uma frota para otimizar rotas, monitorar o desempenho dos motoristas e fornecer atualizações em tempo real aos clientes sobre o status de suas entregas.

Como Kafka pode ser usado neste cenário:

### Produção de dados:

Cada veículo na frota está equipado com um dispositivo de rastreamento que envia periodicamente sua localização (latitude e longitude) para um tópico no Kafka chamado "localização-veículos".

### Processamento em tempo real:

Os consumidores de dados Kafka são configurados para monitorar o tópico "localização-veículos". Esses consumidores podem estar executando diferentes tipos de processamento em tempo real, como calcular a velocidade média dos veículos, detectar desvios de rota ou identificar atrasos nas entregas com base na localização atual dos veículos.

### Armazenamento persistente:

Além do processamento em tempo real, as informações de localização dos veículos também são armazenadas de forma persistente no Kafka. Isso permite que a empresa tenha um histórico completo das localizações dos veículos ao longo do tempo, útil para análises retrospectivas, investigação de incidentes ou para cumprir requisitos regulatórios.

### Integração com outros sistemas:

As informações de localização dos veículos podem ser consumidas por outros sistemas da empresa. Por exemplo, um sistema de logística pode utilizar esses dados para calcular rotas otimizadas, um sistema de gerenciamento de frota pode monitorar o desempenho dos motoristas em tempo real e um sistema de atendimento ao cliente pode fornecer atualizações automáticas aos clientes sobre o status de suas entregas com base nas informações de localização em tempo real.

### Resumo:

Neste exemplo, Kafka é utilizado para rastrear em tempo real a localização dos veículos em uma frota de transporte de mercadorias. Ele facilita a produção, processamento, armazenamento e integração de dados de localização em tempo real, permitindo que a empresa otimize rotas, monitore o desempenho dos motoristas e forneça atualizações em tempo real aos clientes sobre o status de suas entregas.