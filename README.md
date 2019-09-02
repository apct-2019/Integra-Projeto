# Integra-Projeto
Este bloco tem como objetivo realizar a integração dos dispositivos da cadeia de recepção para um rádio VHF 108-137MHz, para comunicação aeronáutica, empregando modulação AM.

O projeto deve seguir as seguintes especificações:
![Especificações do Projeto](specs.png)

As instruções detalhadas sobre o projeto são estabelecidas [nesta apresentação](Trabalhos.pdf)

## Descrição do projeto
A cadeia de recepção terá sua arquitetura baseada em receptores super-heteródinos e deve ser capaz de detectar sinais de voz a partir de 0dBu (equivalente a -106.5dBm em potência) na faixa de 108 a 137MHz. Com uma frequência intermediária de 455kHz, o usuário será capaz de selecionar entre bandas de largura 3kHz, com um espaçamento de 8.33kHz, ou bandas de 7.5kHz com espaçamentos de 25kHz.

O sinal será entregue a um microcontrolador STM32F407VGT6 para demodulação e, em seguida, envio para as saídas de áudio. A potência de entrada do sinal será ajustada através de um controlador PID, implementado no mesmo microncontrolador, que se comunicará através de protocolo SPI com um atenuador e 3 amplificadores de ganho variável, podendo variar o ganho do circuito em até 91dB. A malha de ajuste do ganho deve garantir uma potência de 10dBm para a entrada do Mixer.

O microcontrolador também fará o ajuste da potência de saída do sintetizador, através de protocolo SPI, e deve ter a frequência de amostragem do seu conversor A/D configurada para um valor que atenda ao critério de Nyquist para a demodulação (>=2FI). O ajuste da potência deve garantir que o sintetizador entregue 13dBm para o Mixer.

## Divisão de tarefas
As descrições detalhadas de cada bloco do projeto pode ser vistas nos seguintes repositórios:

1 - Antena: [Mariana](https://github.com/apct-2019/Mariana)

2 - Filtros: [Nicolas Oliveira](https://github.com/apct-2019/Nicolas)

3 - Atenuadores: [Mendes](https://github.com/apct-2019/Mendes)

4 - LNA/Gain Block: [Arturo](https://github.com/apct-2019/Arturo)

5 - Mixer: [Sampaio](https://github.com/apct-2019/Sampaio)

6 - Oscilador Local: [Bacelar](https://github.com/apct-2019/Bacelar)

7 - Conversor A/D e Firmware: [Aquino](https://github.com/apct-2019/Aquino)

8 - Integração do Projeto: João Carvalho

9 - Layout e Componentes de Características Distribuídas: [Onias](https://github.com/apct-2019/Onias)

## Diagrama de Blocos Preliminar
![Diagrama de Blocos com Especificações de Projeto](RX-APCT.png)

## Parâmetros Críticos
* O Mixer selecionado apresenta uma boa operação para as potências de entrada: RF=+10dBm e LO=+13dBm. Por isto, as potências do sintetizador e dos blocos de ganho devem ser ajustadas para atender tais valores.
* A FI foi selecionada para 455kHz para atender a capacidade de amostragem do microcontrolador e reduzir os efeitos dos acoplamentos indesejados do Mixer.
* Com o ajuste da potência de entrada do Mixer, ajusta-se também a potência de entrada no microcontrolador, que pode ter seu pico em até 20.9dBm (2.5V, para Z=50ohms). Para isto, utiliza-se um circuito elevador de tensão para gerando um offset de 1.25V. 
