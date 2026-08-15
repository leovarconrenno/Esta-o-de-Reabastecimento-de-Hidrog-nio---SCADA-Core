# Mapeamento de Variáveis de Processo para Proposições Lógicas

Na automação industrial (norma ISA-5.1), instrumentos e atuadores emitem e recebem sinais discretos (binários: $0$ = Falso / $1$ = Verdadeiro). 

![Estação de reabastecimento](/Etapa-01-Logica/Projeto_2.png)

## Setor 100: Armazenamento de Hidrogênio (Banco de Cilindros de Alta Pressão)
 
| Tag Instrumento | Tipo de Dispositivo    | Variável Física                     | Proposição Lógica | Estado 1                                                             |
| ---------------- | ----------------------- | ------------------------------------ | ------------------ | ---------------------------------------------------------------------- |
| **PT-101**       | Transmissor Pressão     | Pressão do tanque de Armazenamento de baixa pressão   | $p\_1\_1$              | Pressão excede o limite máximo de armazenamento ($P > 400\text{ bar}$) |
| **TT-101**       | Transmissor Temp.       | Temp. do tanque de Armazenamento de baixa pressão      | $t\_1\_1$              | Temperatura excede o limite seguro do vaso ($T > 85^\circ\text{C}$)    |
| **AT-101**       | Detector de Gás H₂      | Concentração de H₂ na área do tanque de Armazenamento de baixa pressão          | $g\_1\_1$              | Vazamento de hidrogênio detectado ($C > 1\text{% vol, } 25\text{% LIE}$) |                            |                                   |
| **PSV-101**      | Válvula de Alívio       | Proteção contra sobrepressão         | $r\_1\_1$              | Válvula de alívio de pressão ATUADA
| **XV-101**       | Válvula Corte Rápido    | entrada do tanque de Armazenamento de baixa pressão      | $v\_1\_1$              | Válvula de segurança de entrada ABERTA
| **SL-101**       | Sinalizador / luz    | alarme do tanque de baixa pressão     | $s\_1\_1$              | Luz ACESSA                                    
| **PT-102**       | Transmissor Pressão     | Pressão do tanque de Armazenamento de média pressão   | $p\_1\_2$              | Pressão excede o limite máximo de armazenamento ($P > 700\text{ bar}$) |
| **TT-102**       | Transmissor Temp.       | Temp. do tanque de Armazenamento de média pressão      | $t\_1\_2$              | Temperatura excede o limite seguro do vaso ($T > 85^\circ\text{C}$)    |
| **AT-102**       | Detector de Gás H₂      | Concentração de H₂ na área do tanque de Armazenamento de média pressão          | $g\_1\_2$              | Vazamento de hidrogênio detectado ($C > 1\text{% vol, } 25\text{% LIE}$) |                            |                                   |
| **PSV-102**      | Válvula de Alívio       | Proteção contra sobrepressão         | $r\_1\_2$              | Válvula de alívio de pressão ATUADA
| **XV-102**       | Válvula Corte Rápido    | entrada do tanque de Armazenamento de média pressão      | $v\_1\_2$              | Válvula de segurança de entrada ABERTA
| **SL-102**       | Sinalizador / luz    | alarme do tanque de média pressão     | $s\_1\_2$              | Luz ACESSA                                     
| **PT-103**       | Transmissor Pressão     | Pressão do tanque de Armazenamento de alta pressão   | $p\_1\_3$              | Pressão excede o limite máximo de armazenamento ($P > 1000\text{ bar}$) |
| **TT-103**       | Transmissor Temp.       | Temp. do tanque de Armazenamento de alta pressão      | $t\_1\_3$              | Temperatura excede o limite seguro do vaso ($T > 85^\circ\text{C}$)    |
| **AT-103**       | Detector de Gás H₂      | Concentração de H₂ na área do tanque de Armazenamento de alta pressão          | $g\_1\_3$              | Vazamento de hidrogênio detectado ($C > 1\text{% vol, } 25\text{% LIE}$) |                            |                                   |
| **PSV-103**      | Válvula de Alívio       | Proteção contra sobrepressão         | $r\_1\_3$              | Válvula de alívio de pressão ATUADA
| **XV-103**       | Válvula Corte Rápido    | entrada do tanque de Armazenamento de alta pressão      | $v\_1\_3$              | Válvula de segurança de entrada ABERTA
| **SL-103**       | Sinalizador / luz    | alarme do tanque de alta pressão     | $s\_1\_3$              | Luz ACESSA
| **XV-104**       | 	Válvula Direcional 4/3 vias (duplo solenoide, retorno por mola)   | Posição de seleção do tanque     | $v\_4$              | quando ambas as bobinas não ligadas seleciona media pressão
| **YV-104A**       | Bobina Solenoide (lado A)    | Comando elétrico de acionamento A     | $y\_a$              | Bobina A energizada → seleciona tanque de baixa pressão
| **YV-104B**       | Bobina Solenoide (lado B)    | Comando elétrico de acionamento B     | $y\_b$              | Bobina B energizada → seleciona tanque de alta pressão                                  
| **ALM-101**      | Sinaleiro / Buzzer      | Alarme Geral                         | $a\_1\_1$              | Sistema de alarme e evacuação ATIVADO  
| **ESD-100**      | Botão Físico            | Segurança Manual                     | $e\_1\_1$              | Parada de emergência acionada pelo operador                                |
 
 
## Setor 200: Condicionamento (Pré-resfriamento)
 
| Tag Instrumento | Tipo de Dispositivo    | Variável Física                  | Proposição Lógica | Estado 1                                                       |
| ---------------- | ----------------------- | ---------------------------------- | ------------------ | ------------------------------------------------------------------ |
| **TT-201**       | Transmissor Temp.       | Temp. de Saída do Pré-resfriador   | $t\_2\_1$              | Temperatura de pré-resfriamento adequada ($T \leq -40^\circ\text{C}$) |
| **PT-201**       | Transmissor Pressão     | Pressão do Buffer de Condicionamento| $p\_2\_1$             | Pressão do buffer dentro da faixa de operação                      |
| **M-201**        | Contator do Motor       | Unidade de Refrigeração (Chiller)  | $m\_2\_1$              | Chiller LIGADO e operacional  
| **XV-201**        | Válvula Corte Rápido      | valvula de entrada do chiller  | $v\_2\_1$              | Válvula de segurança de entrada ABERTA                                       |
 
## Setor 300: Dispensador e Transferência para o Veículo
 
| Tag Instrumento | Tipo de Dispositivo    | Variável Física                              | Proposição Lógica | Estado 1                                                        |
| ---------------- | ----------------------- | ---------------------------------------------- | ------------------ | -------------------------------------------------------------------- |
| **HS-301**       | Chave Manual            | Comando de Início de Abastecimento             | $h\_3\_1$              | Botão de início de abastecimento acionado pelo operador              |
| **COM-301**      | Comunicação IR          | Protocolo de Comunicação com o Veículo (J2799) | $c\_3\_1$              | Comunicação estabelecida com o veículo                               |
| **BV-301**       | Válvula de Ruptura      | Acoplamento do Bico Dispensador (Breakaway)    | $bv\_3\_1$             | Acoplamento do bico conectado e íntegro                              |
| **XV-301**       | Válvula Solenoide       | Alimentação do Bico Dispensador                | $v\_3\_1$              | Válvula de dispensação ABERTA                                        |
| **PT-301**       | Transmissor Pressão     | Pressão no Bico (Nozzle)                       | $p\_3\_1$              | Pressão de enchimento atinge o setpoint do veículo ($P \approx 700\text{ bar}$) |
| **TT-301**       | Transmissor Temp.       | Temp. no Ponto de Recepção do Veículo          | $t\_3\_1$              | Temperatura no ponto de recepção excede o limite ($T > 85^\circ\text{C}$) |
| **AT-301**       | Detector de Gás H₂      | Concentração de H₂ na Área do Dispensador      | $g\_3\_1$              | Vazamento de hidrogênio detectado na área de abastecimento           |
