# Mapeamento de Insumos: Matérias-Primas e Variáveis Lógicas

Este documento descreve os insumos físicos (matérias-primas e utilidades) que alimentam a Estação de Reabastecimento de Hidrogênio, bem como o mapeamento completo dos insumos lógicos (entradas e saídas discretas) utilizados nas equações de intertravamento do sistema SCADA.

## 1. Matérias-Primas Primárias e Utilidades Físicas

Antes da abstração lógica, o sistema depende de insumos físicos fundamentais para a sua operação. Eles representam a massa e a energia transformadas ou controladas pela planta:

* **Gás Hidrogênio ($H_2$):** A matéria-prima principal do processo. É recebido em baixa/média pressão, comprimido, armazenado em alta pressão e, por fim, dispensado no veículo.
* **Energia Elétrica (Potência Motriz e Controle):** Insumo utilitário crítico que alimenta os motores dos compressores, as bombas do chiller e todo o painel de automação (CLP, SCADA, instrumentação).
* **Fluido Refrigerante / Glicol:** Insumo utilitário circulante no sistema do Chiller (Setor 300), vital para o pré-resfriamento do hidrogênio ($T \leq -40^\circ C$) antes da dispensação.
* **Ar Comprimido / Gás Nitrogênio ($N_2$):** Insumo utilitário frequentemente utilizado para atuação de válvulas pneumáticas ou rotinas de purga de segurança nas tubulações.

---

## 2. Insumos Lógicos de Entrada (Sensoriamento e Comandos)

Estas são as proposições lógicas lidas do campo (valores discretos Verdadeiro/Falso) que atuam como as premissas nas equações lógicas de permissivo e trip.

### Setor 100: Banco de Armazenamento
* $p_1$: Pressão do Banco excede o limite de segurança (PT-101)
* $t_1$: Temperatura do Banco excede o limite de segurança (TT-101)
* $g_1$: Vazamento de $H_2$ detectado no armazenamento (AT-101)
* $e_1$: Parada de emergência (ESD-100) acionada pelo operador

### Setor 200: Compressão
* $p_2$: Pressão de descarga do compressor excede o limite (PT-201)
* $t_2$: Temperatura do cabeçote do compressor excede o limite (TT-201)
* $vb_1$: Vibração do compressor atinge o limiar de trip (VS-201)

### Setor 300: Condicionamento e Resfriamento
* $t_3$: Temperatura de pré-resfriamento adequada, alcançando $T \leq -40^\circ C$ (TT-301)
* $p_3$: Pressão do tanque de buffer operacional e dentro da faixa (PT-301)

### Setor 400: Dispensador (Abastecimento)
* $h_1$: Botão de comando para início de abastecimento acionado (HS-401)
* $c_1$: Comunicação de dados (IR) estabelecida com o veículo (COM-401)
* $bv_1$: Acoplamento mecânico (*breakaway* valve) conectado e íntegro (BV-401)
* $t_4$: Temperatura no receptáculo do veículo excede o limite (TT-401)
* $g_2$: Vazamento de $H_2$ detectado na área de dispensação (AT-401)

---

## 3. Insumos Lógicos de Saída (Atuadores e Alarmes)

Estas são as proposições que representam os estados de comando enviados pelo controlador (CLP) para o campo, resultado do processamento das equações lógicas (ex: $F_1 \rightarrow \neg v_1$).

### Atuadores de Bloqueio e Alívio
* $v_1$: Válvula de corte rápido do armazenamento (XV-101) no estado ABERTA
* $v_2$: Válvula de dispensação do bico (XV-401) no estado ABERTA
* $r_1$: Válvula de alívio de pressão (PSV-101) ATUADA

### Atuadores de Força Motriz
* $m_1$: Contator do Motor do Compressor (M-201) no estado LIGADO
* $m_2$: Comando do sistema de resfriamento / Chiller (M-301) no estado LIGADO

### Sinalização
* $a_1$: Sirene / Alarme geral da planta (ALM-101) ATIVADO
