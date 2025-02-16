# Projeto de Visualização de Intensidade Sonora com Matriz de LEDs

## Descrição

Este projeto foi desenvolvido para visualizar a intensidade sonora captada por um microfone em uma matriz de LEDs NeoPixel. O código foi baseado em um repositório de aplicações Pico SDK para o BitDogLab, mas sofreu modificações significativas na lógica de exibição dos LEDs, nas cores utilizadas e nos parâmetros de níveis sonoros.

O sistema capta amostras de áudio através de um microfone conectado ao ADC (Conversor Analógico-Digital) de um Raspberry Pi Pico, processa essas amostras para calcular a potência média do sinal e, com base nessa potência, acende os LEDs da matriz em diferentes padrões e cores, representando a intensidade do som.

---

## Repositório Base

Este código foi inspirado e adaptado a partir do repositório de estudos [BitDogLab-C](https://github.com/BitDogLab/BitDogLab-C).

---

## Mudanças Realizadas

### 1. **Exibição dos LEDs**
- A lógica de exibição dos LEDs foi modificada para criar um efeito visual mais intuitivo e organizado.
- Agora, os LEDs são acesos em "níveis", onde cada nível corresponde a uma intensidade sonora específica.
- A matriz de LEDs foi dividida em seções, e cada seção é acesa conforme o volume do som aumenta.

### 2. **Cores dos LEDs**
- As cores dos LEDs foram ajustadas para melhor representar a intensidade sonora:
  - **Nível 1 (Saudável)**: Verde.
  - **Nível 2 (Médio-Saudável)**: Verde com tons esverdeados.
  - **Nível 3 (Estado de Alerta)**: Amarelo.
  - **Nível 4 (Perigoso)**: Vermelho.
- Essa mudança proporciona uma visualização mais clara e esteticamente agradável.

### 3. **Parâmetros de Níveis Sonoros**
- Os parâmetros de níveis sonoros foram ajustados para melhor se adequar ao ambiente de teste:
  - **Nível 0**: Som muito baixo (abaixo de 0.2V).
  - **Nível 1**: Baixa intensidade (0.2V a 0.6V).
  - **Nível 2**: Média intensidade (0.6V a 1.2V).
  - **Nível 3**: Alta intensidade (1.2V a 2.0V).
  - **Nível 4**: Som muito alto (acima de 2.0V).

---

## Funcionalidades

- Captura de amostras de áudio através do ADC.
- Cálculo da potência média do sinal (valor RMS).
- Visualização da intensidade sonora em uma matriz de LEDs NeoPixel.
- Saída serial da intensidade e da média das leituras do ADC.

---

## Como Usar

### Pré-requisitos

- Placa BitDogLab (melhor caso), ou:
- Raspberry Pi Pico.
- Microfone conectado ao pino ADC (pino 26 + canal 2).
- Matriz de LEDs NeoPixel (25 LEDs).
- Ambiente de desenvolvimento configurado para o Raspberry Pi Pico (SDK e compilador).

### Instalação

1. Clone este repositório:
   ```bash
   git clone https://github.com/seu-usuario/seu-repositorio.git
   ```
2. Compile o código usando o SDK do Raspberry Pi Pico:
   ```bash
   mkdir build
   cd build
   cmake ..
   make
   ```
3. Carregue o arquivo `.uf2` gerado no Raspberry Pi Pico.

### Executando o Projeto

Após carregar o código no Raspberry Pi Pico, o sistema começará a capturar amostras de áudio e a exibir a intensidade sonora na matriz de LEDs. A intensidade e a média das leituras do ADC também serão enviadas para o monitor serial.

---

## Estrutura do Código

- **`main.c`**: Contém a lógica principal do projeto, incluindo a configuração do ADC, DMA e NeoPixel, além do loop de leitura e exibição.
- **`neopixel.c`**: Biblioteca para controle da matriz de LEDs NeoPixel.
- **`pico/stdlib.h`**, **`hardware/adc.h`**, **`hardware/dma.h`**: Bibliotecas do SDK do Raspberry Pi Pico para manipulação de GPIO, ADC e DMA.

---

## Explicação das Funções Principais

1. **`sample_mic()`**:
   - Realiza a leitura do microfone usando o ADC e armazena as amostras em um buffer.
   - Utiliza DMA para transferir os dados do ADC para o buffer de forma eficiente.

2. **`mic_power()`**:
   - Calcula a potência média do sinal (valor RMS) a partir das amostras capturadas.

3. **`get_intensity(float v)`**:
   - Determina a intensidade do som com base na tensão calculada.
   - Retorna um valor de 0 a 4, correspondente aos níveis de intensidade.

4. **Loop Principal**:
   - Realiza a leitura do microfone, calcula a intensidade e atualiza a matriz de LEDs conforme o nível de intensidade.

---

## Agradecimentos

- Agradeço ao repositório [BitDogLab-C](link_para_o_repositório_original) por fornecer a base para este projeto.
- Agradeço ao professor Antônio Santos por nos incentivar e dar suporte durante essa fase do EmbarcaTech.

---