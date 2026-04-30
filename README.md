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

🧪 Simulação do projeto no Wokwi:
[Acessar projeto no Wokwi](https://wokwi.com/projects/462694220214405121)

## 👥 Integrantes

- Cauã Pereira da Silva — RM568143
- Felipe Estevo Santos — RM567780
- Igor Grave Teixeira — RM567663
- Renan dos Reis Santos — RM568540
