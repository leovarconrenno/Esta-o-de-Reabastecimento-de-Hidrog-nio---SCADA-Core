# Insumos do Sistema Lógico (Entradas e Saídas)

Para o desenvolvimento da lógica de controle e intertravamento da Estação de Reabastecimento de Hidrogênio, os dados mapeados foram classificados em variáveis de **Entrada** (Insumos de leitura/sensoriamento) e **Saída** (Atuadores e sinalizações).

## Entradas (Sensores e Comandos)
Estas são as proposições lógicas que o sistema SCADA irá ler do campo (valores discretos 0 ou 1):

* **Setor 100:**
  * $p_1$: Pressão do Banco > 900 bar (PT-101)
  * $t_1$: Temperatura do Banco > 85°C (TT-101)
  * $g_1$: Vazamento de $H_2$ detectado > 25% LIE (AT-101)
  * $e_1$: Parada de emergência acionada (ESD-100)
* **Setor 200:**
  * $p_2$: Pressão de descarga do compressor > 950 bar (PT-201)
  * $t_2$: Temperatura do cabeçote > 120°C (TT-201)
  * $vb_1$: Vibração acima do limite de trip (VS-201)
  * $f_1$: Vazão fora da faixa nominal (FT-201)
* **Setor 300:**
  * $t_3$: Temperatura de pré-resfriamento adequada, $T \leq -40^\circ C$ (TT-301)
  * $p_3$: Pressão do buffer dentro da faixa (PT-301)
* **Setor 400:**
  * $h_1$: Botão de início de abastecimento acionado (HS-401)
  * $c_1$: Comunicação estabelecida com o veículo (COM-401)
  * $bv_1$: Acoplamento do bico conectado e íntegro (BV-401)
  * $p_4$: Pressão de enchimento atinge o setpoint (PT-401)
  * $t_4$: Temperatura no receptáculo do veículo > 85°C (TT-401)
  * $g_2$: Vazamento de $H_2$ no dispenser (AT-401)

## Saídas (Atuadores e Alarmes)
Estas são as proposições que determinam as ações tomadas pelo sistema de controle com base nas entradas:

* **Setor 100:**
  * $v_1$: Válvula de saída do banco ABERTA (XV-101)
  * $r_1$: Válvula de alívio ATUADA (PSV-101)
  * $a_1$: Alarme geral ATIVADO (ALM-101)
* **Setor 200:**
  * $m_1$: Motor do compressor LIGADO (M-201)
* **Setor 300:**
  * $m_2$: Chiller LIGADO (M-301)
* **Setor 400:**
  * $v_2$: Válvula de dispensação ABERTA (XV-401)
