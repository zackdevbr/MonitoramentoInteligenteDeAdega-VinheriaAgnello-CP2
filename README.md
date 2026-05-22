# 🍷 Smart Solutions — Sistema Inteligente para Vinheria Agnello
<img width="544" height="535" alt="image" src="https://github.com/user-attachments/assets/5facb4d3-da17-4360-9cc7-2cb27ebea6d7" />

## 📌 Sobre o Projeto

Este projeto foi desenvolvido para a disciplina de **Edge Computing & Computer Systems** da FIAP com o objetivo de criar uma solução inteligente de monitoramento para a **Vinheria Agnello**.

A proposta consiste em simular um sistema embarcado capaz de monitorar as condições ideais de armazenamento dos vinhos, garantindo qualidade e preservação do produto através da análise de:

- 🌡️ Temperatura
- 💧 Umidade
- ☀️ Luminosidade

Além disso, o projeto busca aproximar a experiência digital da vinheria física, oferecendo uma interface intuitiva e interativa através do display LCD.

---

# 🧠 Funcionalidades do Sistema

✅ Monitoramento em tempo real  
✅ Leitura de temperatura e umidade com DHT11  
✅ Leitura de luminosidade com LDR  
✅ Calibração automática do sensor LDR  
✅ Média das leituras para maior estabilidade  
✅ Display LCD I2C 16x2  
✅ Relógio em tempo real com RTC DS1307  
✅ Sistema de alertas visuais e sonoros  
✅ Armazenamento de logs na EEPROM  
✅ Alternância de idioma (Português/Inglês)  
✅ Interface UX personalizada  
✅ Sistema de classificação do ambiente  
✅ Monitor Serial para debug e monitoramento  

---

# ⚙️ Tecnologias e Componentes Utilizados

## Hardware

- Arduino Uno
- Sensor DHT11
- Sensor LDR
- RTC DS1307
- Display LCD I2C 16x2
- LEDs
- Buzzer
- Push Button
- Protoboard
- Resistores

---

## Bibliotecas

```cpp
Wire.h
LiquidCrystal_I2C.h
RTClib.h
EEPROM.h
DHT.h
```

---

# 🔌 Pinagem do Projeto

| Componente | Porta Arduino |
|---|---|
| DHT11 | D2 |
| Botão Idioma | D3 |
| Buzzer | D9 |
| LED Crítico | D10 |
| LED Alerta | D11 |
| LED OK | D12 |
| LDR | A0 |
| LCD SDA | SDA |
| LCD SCL | SCL |
| RTC SDA | A4 |
| RTC SCL | A5 |

---

# 🌡️ Controle Inteligente do Ambiente

## Temperatura

Faixa ideal:

```txt
10°C até 16°C
```

Faixa crítica:

```txt
Abaixo de 7°C ou acima de 19°C
```

---

## Umidade

Faixa ideal:

```txt
60% até 80%
```

Faixa crítica:

```txt
Abaixo de 50% ou acima de 90%
```

---

## Luminosidade

O sistema utiliza o sensor LDR com calibração automática e conversão utilizando a função `map()`.

Classificação:

| Luminosidade | Estado |
|---|---|
| 0% - 30% | Ideal |
| 31% - 60% | Alerta |
| 61% - 100% | Crítico |

---

# 🚦 Sistema de Alertas

## LEDs

🟢 Verde → Ambiente ideal  
🟡 Amarelo → Ambiente em alerta  
🔴 Vermelho → Ambiente crítico  

---

## Buzzer

O buzzer emite alertas sonoros a cada 5 segundos:

- Alerta → som moderado
- Crítico → som intenso

---

# 🖥️ Interface LCD

O display LCD apresenta:

- Data
- Hora
- Temperatura
- Umidade
- Luminosidade
- Status geral da adega

Além disso, o projeto possui:

✅ Tela de boas-vindas  
✅ Animação inicial  
✅ Ícones personalizados  
✅ Interface bilíngue  

---

# 🌐 Sistema Bilíngue

O botão conectado ao pino D3 permite alternar entre:

- 🇧🇷 Português
- 🇺🇸 English

---

# 💾 EEPROM — Registro de Logs

O sistema registra automaticamente situações de alerta e criticidade na EEPROM.

São armazenados:

- Data
- Hora
- Temperatura
- Umidade
- Luminosidade
- Tipo de erro detectado

Os logs são gravados a cada 60 segundos enquanto houver alguma anomalia no ambiente.

---

# 🧮 Funcionamento da Luminosidade

O LDR realiza leituras analógicas entre:

```txt
0 até 1023
```

Após a calibração automática, os valores são convertidos para porcentagem:

```cpp
map(raw, ldrMin, ldrMax, 100, 0)
```

Isso garante:

✅ Mais luz → maior porcentagem  
✅ Menos luz → menor porcentagem  

---

# 📟 Monitor Serial

O Serial Monitor exibe informações completas do sistema:

```txt
Leitura 22/05/2026 14:32:10
Temp: 13.2C
Umid: 72%
Luz: 18%
Status: IDEAL
```

---

# 🎨 Diferenciais do Projeto

## UX e Interface

- Sistema visual intuitivo
- Interface dinâmica
- Ícones personalizados
- Navegação automática entre telas
- Animação de inicialização

---

## Edge Computing

O sistema realiza:

- processamento local
- tomada de decisão embarcada
- armazenamento local
- monitoramento em tempo real

---

# ⚠️ Dificuldades Encontradas

- Inicialmente, o sensor LDR apresentava os valores invertidos. O problema foi resolvido ajustando a lógica da função `map()` para que ambientes mais iluminados apresentassem porcentagens maiores.

- O sensor DHT11 apresentou instabilidade em leituras muito rápidas. Para resolver isso, foi reduzida a frequência de leitura e adicionada validação utilizando `isnan()`.

- Durante a montagem física do projeto, alguns componentes e conexões apresentaram mau contato na protoboard, principalmente nos jumpers e no display LCD, causando falhas temporárias de comunicação. O problema foi resolvido reorganizando a montagem e substituindo conexões defeituosas.

- O LCD possui limitação de caracteres personalizados. Para resolver isso, foi feita uma otimização dos ícones utilizados na interface.

---

# ▶️ Simulação Wokwi

https://wokwi.com/projects/464730953131805697

---

# 📂 Estrutura do Repositório

```txt
📁 projeto-edge-vinheria
 ┣ 📄 README.md
 ┗ 📄 código do arduino
```

---

# 👨‍💻 Integrantes — Smart Solutions

| Nome | RM |
|---|---|
| Eduarda Soares | RM569369 |
| Isac Nilton Fernandes de Oliveira | RM573282 |
| João Benedito de Oliveira Simplicio | RM570206 |
| Julia Souza Matarazzo | RM571340 |
| Mariana Malagutti | RM570290 |

---

# 🎓 FIAP — Edge Computing & Computer Systems

Projeto acadêmico desenvolvido para fins educacionais utilizando conceitos de:

- Edge Computing
- Sistemas Embarcados
- IoT
- Monitoramento Inteligente
- UX em dispositivos embarcados
- Automação
