# CarePlus Health Tracker (ESP32)

## 📌 Visão geral

Este projeto simula um dispositivo vestível (Smartwatch/Health Tracker) utilizando ESP32, com envio de dados via protocolo MQTT para a nuvem (HiveMQ) e visualização no Node-RED.

A proposta segue o conceito de uma solução digital para saúde baseada em:

- coleta passiva de dados
- microinterações simples
- feedback em tempo real
- gamificação (metas e pontuação)

---

## 🧠 Ideia do projeto

O dispositivo monitora métricas simuladas do usuário e avalia se ele está cumprindo metas diárias de bem-estar.

Diferente de soluções invasivas ou complexas, o sistema foi pensado para:

- reduzir fricção
- evitar necessidade de interação constante
- entregar feedback simples e direto

- ## 🔧 Componentes utilizados

- ESP32
- 2 potenciômetros
- 1 botão (pushbutton)
- LED verde
- LED amarelo
- LED vermelho
- buzzer

---

## ⚙️ Funcionamento do sistema

### Entrada de dados

O sistema utiliza entradas simples para simular métricas reais de saúde:

- Potenciômetro 1 → simula nível de atividade (movimento/passos)
- Potenciômetro 2 → simula qualidade do sono
- Botão → representa um check-in rápido de hidratação

---

### Processamento

O ESP32 analisa os dados coletados e:

- verifica se metas diárias foram atingidas
- calcula a pontuação do usuário
- define o status geral (normal, progresso ou atenção)

---

### Feedback ao usuário

O sistema fornece feedback físico imediato:

- 🟢 LED verde → meta atingida
- 🟡 LED amarelo → progresso parcial
- 🔴 LED vermelho → precisa melhorar
- 🔊 buzzer → recompensa ao atingir meta

---

## 🧠 Interpretação do sistema

O projeto simula um dispositivo vestível moderno, onde:

- dados são coletados automaticamente (sem esforço do usuário)
- o sistema interpreta o comportamento
- o usuário recebe feedback simples e contínuo

Essa abordagem reduz a fricção e aumenta a aderência ao uso diário.

## ☁️ Comunicação MQTT

Os dados gerados pelo ESP32 são enviados em tempo real para a nuvem utilizando o protocolo MQTT.

Foi utilizado o broker HiveMQ Cloud com conexão segura (TLS).

---

### 📡 Tópico utilizado

```txt
fiap/careplus/healthtracker
```

---

## 🔗 Fluxo de dados

O fluxo completo do sistema é:

ESP32 → HiveMQ Cloud → Node-RED

---

## 📊 Integração com Node-RED

O Node-RED é utilizado para consumir e visualizar os dados enviados pelo dispositivo.

Configuração do nó MQTT:

- Broker: HiveMQ Cloud
- Porta: 8883
- TLS: ativado
- Autenticação: usuário e senha
- Tópico: fiap/careplus/healthtracker

---

## 📦 Exemplo de payload enviado

```json
{
  "device": "careplus_health_tracker",
  "meta_movimento": "batida",
  "meta_sono": "nao_batida",
  "hidratacao_check": false,
  "pontos": 10,
  "status": "progresso_parcial",
  "streak": 0,
  "timestamp": 45699
}
```

---

## 🧠 Interpretação dos dados

- `meta_movimento` → indica se a meta de atividade foi atingida
- `meta_sono` → indica se o descanso foi adequado
- `hidratacao_check` → registro rápido do usuário
- `pontos` → sistema de gamificação
- `status` → estado geral do usuário
- `streak` → sequência de metas atingidas

- ## 🔄 Arquitetura do sistema

O projeto segue uma arquitetura típica de soluções IoT:

ESP32 → MQTT → HiveMQ Cloud → Node-RED

- O ESP32 coleta e processa os dados
- O protocolo MQTT faz a comunicação
- O HiveMQ atua como broker na nuvem
- O Node-RED consome e exibe os dados em tempo real

---

## 🛠 Tecnologias utilizadas

- ESP32
- Linguagem C/C++ (Arduino)
- MQTT
- HiveMQ Cloud
- Node-RED
- Wokwi (simulação)

---

# CarePlus Health Tracker (ESP32 Físico)

Este repositório contém a documentação técnica, códigos e scripts do ecossistema **Health Tracker** desenvolvido para a **Care Plus**. O projeto consiste em uma solução de Internet das Coisas (IoT) integrada de ponta a ponta, coletando dados críticos de bem-estar a partir de um dispositivo físico de borda e disponibilizando os dados em tempo real em um painel gerencial executivo.

---

## 🏗️ Arquitetura do Sistema
O ecossistema segue a arquitetura clássica e enxuta de soluções corporativas de IoT, dividida em três camadas:

1. **Camada Edge (Borda):** O microcontrolador **ESP32** realiza a leitura analógica dos sinais dos sensores na protoboard física. Os sinais são digitalizados, normalizados para uma escala percentual estável (0 a 100) e encapsulados em uma estrutura de dados padronizada em formato **JSON**.
2. **Camada de Transporte (Nuvem):** Utilização do protocolo **MQTT** para comunicação assíncrona orientada a tópicos. Os dados são transmitidos com **Criptografia TLS (Transport Layer Security)** ativa através da porta segura **8883** para o broker em nuvem **HiveMQ Cloud**.
3. **Camada de Aplicação (Tratamento e UI):** O **Node-RED** atua como o motor de processamento local. Ele subscreve o tópico na nuvem, realiza o *parsing* do objeto JSON recebido e injeta as variáveis dinamicamente no **Node-RED Dashboard** para monitoramento em tempo real.

---

## 🎛️ Componentes Utilizados (Hardware)
* **1 ESP32** (NodeMCU)
* **2 Potenciômetros** de precisão (Simulando a telemetria analógica dos sensores de saúde)
* **1 Protoboard** e cabos jumpers de conexão

---

## ⚙️ Funcionamento do Sistema & Interpretação de Dados

### Entrada de Dados (Payload JSON)
O dispositivo físico de borda realiza as leituras estruturadas e envia periodicamente o pacote JSON abaixo para o tópico `fiap/careplus/healthtracker`:

```json
{
  "device": "careplus_tracker_fisico_real",
  "movimento": 79,
  "sono": 100,
  "hidratacao": 0,
  "pontos": 20
}
```
---

## 🎯 Objetivo do projeto

Este projeto tem como objetivo demonstrar um sistema IoT funcional que representa um Health Tracker moderno, com foco em:

- simplicidade de uso
- baixo atrito para o usuário
- coleta passiva de dados
- feedback imediato
- engajamento por gamificação

---

## 📌 Considerações finais

O protótipo foi desenvolvido com foco em representar uma solução realista de mercado, alinhada com tendências atuais de dispositivos vestíveis e saúde digital.

Mesmo sendo uma simulação, o sistema demonstra conceitos importantes como:

- comunicação em tempo real
- processamento local (edge computing)
- integração com serviços em nuvem
- experiência do usuário baseada em feedback contínuo

## 🎥 Demonstração do Projeto

📺 Vídeo demonstrando o funcionamento completo do sistema:
[Assista no YouTube](https://youtu.be/4JgOYw4e4tY?si=wmjduRjW2SbO0Q4w)

📺 Assista à validação em runtime de todo o ecossistema integrado (Hardware Real, MQTT Cloud e Dashboard):
[Assista no YouTube](https://youtu.be/rdVtUcSX1VU)

🧪 Simulação do projeto no Wokwi:
[Acessar projeto no Wokwi](https://wokwi.com/projects/462694220214405121)


## 👥 Integrantes

- Cauã Pereira da Silva — RM568143
- Felipe Estevo Santos — RM567780
- Igor Grave Teixeira — RM567663
- Renan dos Reis Santos — RM568540
