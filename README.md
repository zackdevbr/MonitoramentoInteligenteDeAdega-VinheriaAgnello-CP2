# 🍷 Vinheria Agnello - Monitoramento Inteligente de Adega
<img width="544" height="535" alt="image" src="https://github.com/user-attachments/assets/5facb4d3-da17-4360-9cc7-2cb27ebea6d7" />


## 📌 Descrição

Este projeto foi desenvolvido pelo grupo **AdegaSense** para a disciplina de **Edge Computing da FIAP**, com o objetivo de criar uma solução inteligente para a **Vinheria Agnello**, uma vinheria tradicional que deseja expandir sua atuação para o ambiente digital sem perder a experiência personalizada do atendimento presencial.

A proposta consiste em um sistema de monitoramento ambiental para adegas, capaz de acompanhar fatores que influenciam diretamente a qualidade dos vinhos: **temperatura, umidade e luminosidade**.

O sistema utiliza sensores conectados ao Arduino para analisar o ambiente em tempo real, exibir as informações em um display LCD, emitir alertas visuais e sonoros e registrar situações críticas em memória.

---

## 🎯 Objetivo do Projeto

O objetivo principal é garantir que os vinhos estejam armazenados em condições adequadas, evitando problemas como:

- Exposição excessiva à luz;
- Temperatura inadequada;
- Baixa ou alta umidade;
- Risco de oxidação;
- Perda de qualidade do vinho;
- Danos aos rótulos e às rolhas.

Além disso, o projeto busca entregar uma experiência de usuário mais clara, intuitiva e próxima do atendimento presencial de uma vinheria.

---

## 🍇 Contexto do Problema

A qualidade do vinho pode ser afetada por diversos fatores ambientais.

A **luminosidade** em excesso pode causar alterações químicas no vinho, principalmente em vinhos brancos e espumantes, que são mais sensíveis à luz.

A **temperatura** também é um fator essencial. O calor excessivo pode prejudicar a conservação do vinho, enquanto grandes variações térmicas podem alterar aroma, sabor e qualidade.

A **umidade** influencia diretamente na conservação da rolha e do rótulo. Um ambiente muito seco pode ressecar o vedante, aumentando o risco de oxidação. Já a umidade excessiva pode danificar rótulos e favorecer a proliferação de fungos.

Por isso, foi desenvolvido um sistema capaz de monitorar esses três fatores e alertar quando algum deles estiver fora dos limites adequados.

---

## ⚙️ Tecnologias e Componentes

- Arduino Uno
- Sensor DHT11
- Sensor LDR
- Display LCD 16x2 com módulo I2C
- RTC DS1307
- EEPROM interna do Arduino
- LEDs verde, amarelo e vermelho
- Buzzer
- Push button para alteração de idioma
- Resistores
- Protoboard
- Jumpers
- Simulador Wokwi
- Linguagem C/C++ para Arduino

---

## 🧠 Funcionamento do Sistema

O sistema realiza a leitura dos sensores e interpreta as condições do ambiente da adega.

O **DHT11** mede a temperatura e a umidade.  
O **LDR** mede a luminosidade do ambiente.  
O **RTC DS1307** fornece data e hora em tempo real.  
O **LCD I2C** exibe as informações para o usuário.  
A **EEPROM** armazena logs sempre que uma situação crítica é detectada.

Para melhorar a estabilidade das leituras, o sistema realiza múltiplas medições e calcula uma média dos valores.

A luminosidade passa por um processo de calibração automática, utilizando os valores mínimo e máximo captados pelo LDR. Depois disso, a função `map()` converte a leitura analógica para uma escala percentual de **0% a 100%**, facilitando a interpretação.

---

## 🌡️ Parâmetros Monitorados

### Temperatura

A temperatura ideal para conservação dos vinhos fica próxima de **13°C**.

No projeto, foi definida uma faixa aceitável entre:

| Faixa | Estado |
|---|---|
| Abaixo de 10°C | Temperatura baixa |
| 10°C a 16°C | Condição adequada |
| Acima de 16°C | Temperatura alta |

---

### Umidade

A umidade ideal para armazenamento de vinhos fica próxima de **70%**, com faixa aceitável entre **60% e 80%**.

| Faixa | Estado |
|---|---|
| Abaixo de 60% | Umidade baixa |
| 60% a 80% | Condição adequada |
| Acima de 80% | Umidade alta |

---

### Luminosidade

A luminosidade deve ser baixa, pois a exposição excessiva à luz pode prejudicar a qualidade do vinho.

| Faixa | Estado |
|---|---|
| Baixa luminosidade | Ambiente ideal |
| Luminosidade média | Estado de atenção |
| Luminosidade alta | Estado crítico |

---

## 🚦 Estados do Sistema

O projeto utiliza LEDs e buzzer para indicar o estado atual da adega.

| Estado | Condição | Indicação |
|---|---|---|
| 🟢 Ideal | Temperatura, umidade e luminosidade adequadas | LED verde |
| 🟡 Atenção | Luminosidade em nível intermediário | LED amarelo + buzzer curto |
| 🔴 Crítico | Temperatura, umidade ou luminosidade fora do limite | LED vermelho + buzzer |

---

## 🖥️ Interface do Usuário

O display LCD 16x2 exibe as informações em telas alternadas, facilitando a leitura dos dados.

As telas exibidas são:

- Data e hora;
- Temperatura atual;
- Umidade atual;
- Luminosidade em porcentagem;
- Status geral da adega.

Também foram adicionados ícones personalizados no LCD, como:

- Taça de vinho;
- Gota para umidade;
- Símbolo de luminosidade.

---

## 🌐 Diferencial UX

Como diferencial de experiência do usuário, o projeto possui:

- Tela inicial personalizada com o nome **Vinheria Agnello**;
- Ícones visuais no LCD;
- Mensagens simples e intuitivas;
- Botão para alternar idioma entre **Português** e **Inglês**;
- Status geral da adega;
- Alertas visuais e sonoros;
- Registro automático de situações críticas.

Esses recursos tornam o sistema mais amigável, visual e próximo de uma experiência de atendimento personalizado.

---

## 🕒 RTC - Data e Hora

O projeto utiliza o módulo **RTC DS1307** para manter o controle de data e hora.

Essas informações são exibidas no LCD e também utilizadas nos registros de logs armazenados na EEPROM.

O LCD I2C e o RTC compartilham o barramento I2C do Arduino:

| Função | Porta Arduino Uno |
|---|---|
| SDA | A4 |
| SCL | A5 |

---

## 💾 Armazenamento de Logs na EEPROM

Sempre que uma condição crítica é detectada, o sistema registra um log na EEPROM contendo:

- Data e hora;
- Temperatura;
- Umidade;
- Luminosidade;
- Tipo de alerta detectado.

Os tipos de alerta são classificados da seguinte forma:

| Código | Alerta |
|---|---|
| 1 | Temperatura crítica |
| 2 | Umidade crítica |
| 4 | Luminosidade crítica |

Caso mais de um problema ocorra ao mesmo tempo, os códigos são somados.

Exemplo:

```txt
Código 5 = Temperatura crítica + Luminosidade crítica
