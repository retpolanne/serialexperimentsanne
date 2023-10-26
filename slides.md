---
title: Serial Experiments Anne
subtitle: Ou como me tornei uma hardware hacker
author: Anne/Anya/Annie 2023
theme:
  # Otherwise specify the path for it
  path: themes/hackerbutcute.yaml
---
# Lain's NAVI
---
![](images/lainmac.jpg)
<!-- end_slide -->
# whoami
---
![](images/anya.png)

Anne / Anya / Anne

Head of gambiarra

Cat girl hacker

[https://github.com/retpolanne](https://github.com/retpolanne)

[https://blog.retpolanne.com](https://blog.retpolanne.com)
<!-- end_slide -->
# O que vem por aí
---

- Serial Experiments Anne - o incrível mundo do UART

- The PHYnal Countdown

- Miscelânea
<!-- end_slide -->
# Serial Experiments Anne - o incrível mundo do UART
---
![](images/lainio.jpg)
<!-- end_slide -->
# Baud Rate, UART, TTL e RS232
---
- baud /bɔːd/ é a medida de pulsos por segundo ou sinais que um equipamento transmite
- quando conseguimos dar match entre o baud rate de dois dispositivos, eles podem conversar entre si!
- o mais comum é utilizarmos sinais TTL (0v == 0, 5v == 1), e existem dispositivos que interpretam esses sinais em série (como bits, e aí ASCII)
- UART é um circuito que faz transmissão (Tx) e recepção (Rx) de sinais 

![](images/ftdi-scale.jpg)

<!-- end_slide -->
# Curious Annie finds an opportunity to hack 🤔
---
- Eu costumo usar o Linux headless, via SSH
- Porém, não sei quando o sistema operacional está up ou se houve uma falha durante o boot
- Por que não ler o console serial do Linux via UART? 
<!-- end_slide -->

# Olhando pra placa mãe
---
Normalmente, placas com UART possuem três pinos: Rx, Tx e GND.

Porém, placas mãe possuem um header COM. 

![](images/comport-scale.jpg)

Aparentemente, NSIN == Rx, NSOUT == Tx, e temos um GND também.
<!-- end_slide -->

Porém, quando tentei ligar tudo num FTDI, garbage!

![](images/mambojambo.jpg)
<!-- end_slide -->
# Annie ur breaking the board!!!!
---
Aparemente, placas mãe operam em RS232 (-12V, +12V), e não TTL (0v, 5v)! Eu poderia ter fritado tudo! 

Mas! Eu não sabia de um detalhe muito importante...

![](images/ttl-to-rs232-scale.jpg)
<!-- end_slide -->
Gambiarra um: tentativa de reduzir a voltagem 

![](images/voltage.jpg)

Não deu bom :c
<!-- end_slide -->

Depois de um dia inteiro rebootando o computador (e bloqueando meu TPM...), eu decidi usar um Logic Analyzer

![](images/50khz.png)

Nada fazia sentido :c
Até que corrigi o baud rate e inverti os bits:

![](images/asus-scale.jpg)

DEU BOM! Os bits estavam invertidos.
<!-- end_slide -->

Conversando com um pessoal do grupo de Hardware Hacking, eu descobri que o sinal de RS232 é diferente do TTL! 

![](images/ttl-to-rs232-scale-2.jpg)

Eu precisava de algo para converter RS232 em TTL e vice-versa

Behold: MAX232!

![](images/max232-scale.jpg)
<!-- end_slide -->

![](images/max232-circuit-scale.jpg)
<!-- end_slide -->

![](images/max232circuit.jpg)
<!-- end_slide -->

![](images/logs.jpg)
<!-- end_slide -->
# The PHYnal Countdown
---
![](images/orangepi.png)
<!-- end_slide -->
# Orange Pi One Plus no fundo da gaveta
---
O que fazer com ela? Buildar Linux usando Yocto, oras! 
![](images/orangepi.png)

Configura uns layers aqui e ali, roda o bitbake e voilá! Uma imagem prontinha pra ser flasheada pro SD card.
<!-- end_slide -->
# Tudo funcionando, só que não
---
A placa de rede simplesmente não funcionava :c sequer acendia a luz. 

Depois de conferir a device tree source, eu percebi que o suporte upstream a DHCP na Orange Pi One Plus não existia.

Fui besta de corrigir isso no u-boot ao invés de corrigir no upstream kernel 🤡
![](images/upstream.png)

Tive que olhar alguns datasheets e testar várias coisas pra descobrir o problema: 

[Embedded systems from ground up: PHYnal Fantasy](https://blog.retpolanne.com/hardware/embedded/2023/07/07/embedded-phy.html)

Eu descobri uma ferramenta muito massa também pra rodar testes de pytest em dispositivos conversando via TTY! 

[](https://blog.retpolanne.com/hardware/embedded/test-automation/2023/07/09/uboot-automation.html)
<!-- end_slide -->
![](images/orangepidhcp.jpg)
<!-- end_slide -->
# Miscelânea
---
![](images/devboard.jpg)
<!-- end_slide -->
![](images/soic8.jpg)
[](https://blog.retpolanne.com/kernel-dev/renesas/2023/06/20/renesas.html)
<!-- end_slide -->
![](images/xiaomiuart.jpg)
<!-- end_slide -->
# Thank you

![](images/anya-scale-30.jpg)

[https://github.com/retpolanne](https://github.com/retpolanne)

[https://blog.retpolanne.com](https://blog.retpolanne.com)

**Me pergunte sobre meu username**

<!-- end_slide -->
# Presented in glorious Presenterm
Direto do terminal, escrito em Rust.
## Presenterm by Matias Fontanini

[https://github.com/mfontanini/presenterm](https://github.com/mfontanini/presenterm)
<!-- end_slide -->
