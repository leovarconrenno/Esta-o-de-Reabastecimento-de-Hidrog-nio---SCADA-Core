# Mapeamento de Variáveis de Processo para Proposições Lógicas

Na automação industrial (norma ISA-5.1), instrumentos e atuadores emitem e recebem sinais discretos (binários: $0$ = Falso / $1$ = Verdadeiro). 

![Estação de reabastecimento](/Etapa-01-Logica/Projeto 2.png)

## Setor 100: Armazenamento de Hidrogênio (Banco de Cilindros de Alta Pressão)
 
| Tag Instrumento | Tipo de Dispositivo    | Variável Física                     | Proposição Lógica | Estado 1                                                             |
| ---------------- | ----------------------- | ------------------------------------ | ------------------ | ---------------------------------------------------------------------- |
| **PT-101**       | Transmissor Pressão     | Pressão do tanque de Armazenamento de baixa pressão   | $p\_1$              | Pressão excede o limite máximo de armazenamento ($P > 400\text{ bar}$) |
| **TT-101**       | Transmissor Temp.       | Temp. do tanque de Armazenamento de baixa pressão      | $t\_1$              | Temperatura excede o limite seguro do vaso ($T > 85^\circ\text{C}$)    |
| **AT-101**       | Detector de Gás H₂      | Concentração de H₂ na área do tanque de Armazenamento de baixa pressão          | $g\_1$              | Vazamento de hidrogênio detectado ($C > 1\text{% vol, } 25\text{% LIE}$) |                            |                                   |
| **PSV-101**      | Válvula de Alívio       | Proteção contra sobrepressão         | $r\_1$              | Válvula de alívio de pressão ATUADA
| **XV-101**       | Válvula Corte Rápido    | entrada do tanque de Armazenamento de baixa pressão      | $v\_1$              | Válvula de segurança de saída ABERTA
| **SL-101**       | Sinalizador / luz    | alarme do tanque de baixa pressãp     | $s\_1$              | Luz ACESSA                                    
| **ALM-101**      | Sinaleiro / Buzzer      | Alarme Geral                         | $a\_1$              | Sistema de alarme e evacuação ATIVADO  
| **ESD-100**      | Botão Físico            | Segurança Manual                     | $e\_1$              | Parada de emergência acionada pelo operador                                |
 
## Setor 200: Compressão e Pressurização
 
| Tag Instrumento | Tipo de Dispositivo    | Variável Física                  | Proposição Lógica | Estado 1                                                     |
| ---------------- | ----------------------- | ---------------------------------- | ------------------ | --------------------------------------------------------------- |
| **PT-201**       | Transmissor Pressão     | Pressão de Descarga do Compressor  | $p\_2$              | Pressão de descarga excede o limite ($P > 950\text{ bar}$)      |
| **TT-201**       | Transmissor Temp.       | Temp. do Cabeçote do Compressor    | $t\_2$              | Temperatura do compressor excede o limite ($T > 120^\circ\text{C}$) |
| **VS-201**       | Chave de Vibração       | Vibração do Compressor             | $vb\_1$             | Vibração acima do limite de disparo (trip)                      |
| **FT-201**       | Transmissor de Vazão    | Vazão de H₂ Comprimido             | $f\_1$              | Vazão fora da faixa nominal de operação                         |
| **M-201**        | Contator do Motor       | Motor do Compressor                | $m\_1$              | Motor do compressor LIGADO e em operação nominal                |
 
## Setor 300: Condicionamento (Pré-resfriamento)
 
| Tag Instrumento | Tipo de Dispositivo    | Variável Física                  | Proposição Lógica | Estado 1                                                       |
| ---------------- | ----------------------- | ---------------------------------- | ------------------ | ------------------------------------------------------------------ |
| **TT-301**       | Transmissor Temp.       | Temp. de Saída do Pré-resfriador   | $t\_3$              | Temperatura de pré-resfriamento adequada ($T \leq -40^\circ\text{C}$) |
| **PT-301**       | Transmissor Pressão     | Pressão do Buffer de Condicionamento| $p\_3$             | Pressão do buffer dentro da faixa de operação                      |
| **M-301**        | Contator do Motor       | Unidade de Refrigeração (Chiller)  | $m\_2$              | Chiller LIGADO e operacional                                       |
 
## Setor 400: Dispensador e Transferência para o Veículo
 
| Tag Instrumento | Tipo de Dispositivo    | Variável Física                              | Proposição Lógica | Estado 1                                                        |
| ---------------- | ----------------------- | ---------------------------------------------- | ------------------ | -------------------------------------------------------------------- |
| **HS-401**       | Chave Manual            | Comando de Início de Abastecimento             | $h\_1$              | Botão de início de abastecimento acionado pelo operador              |
| **COM-401**      | Comunicação IR          | Protocolo de Comunicação com o Veículo (J2799) | $c\_1$              | Comunicação estabelecida com o veículo                               |
| **BV-401**       | Válvula de Ruptura      | Acoplamento do Bico Dispensador (Breakaway)    | $bv\_1$             | Acoplamento do bico conectado e íntegro                              |
| **XV-401**       | Válvula Solenoide       | Alimentação do Bico Dispensador                | $v\_2$              | Válvula de dispensação ABERTA                                        |
| **PT-401**       | Transmissor Pressão     | Pressão no Bico (Nozzle)                       | $p\_4$              | Pressão de enchimento atinge o setpoint do veículo ($P \approx 700\text{ bar}$) |
| **TT-401**       | Transmissor Temp.       | Temp. no Ponto de Recepção do Veículo          | $t\_4$              | Temperatura no ponto de recepção excede o limite ($T > 85^\circ\text{C}$) |
| **AT-401**       | Detector de Gás H₂      | Concentração de H₂ na Área do Dispensador      | $g\_2$              | Vazamento de hidrogênio detectado na área de abastecimento           |