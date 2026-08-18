
# Representação Simbólica das Regras de Processo e Intertravamentos

No contexto do controle lógico de processos da Estação de Reabastecimento de Hidrogênio, a análise de tautologias e contradições garante que as equações booleanas dos intertravamentos (SIS) sejam consistentes e seguras.

## A. Intertrava de Trip de Emergência do Banco de Armazenamento (Setor 100)

A válvula de corte rápido do banco de armazenamento ($v_{1,X}$, XV-10X) deve ser imediatamente FECHADA ($\neg v_1$) e o alarme geral acionado ($a_1$)e a respectiva sinalização ($s\_{1,X}$ ,SL-10X) caso haja sobrepressão, sobretemperatura, vazamento de gás ou acionamento manual de emergência.

* **Condição de Falha / Evento Crítico ($F_1$):**

$$F_1 \equiv s\_{1,x} \equiv p_{1,X} \lor t_{1,X} \lor g_{1,X} \lor e_1$$

* **Equação Lógica de Intertravamento:**

$$F_1 \rightarrow (\neg v_1 \land a_1)$$

Adicionalmente, a válvula de alívio ($r_1$, PSV-101) atua especificamente em caso de sobrepressão, de forma independente do fechamento de $v_1$:

$$p_1 \rightarrow r_1$$

## B. Permissivo de Partida do Compressor (Setor 200)

O motor do compressor ($m_1$) SÓ PODE partir se houver suprimento de gás disponível (válvula de saída do armazenamento aberta, $v_1$) e não houver nenhuma condição de falha ativa no armazenamento nem no próprio compressor.

* **Condição de Permissivo de Partida ($P_{comp}$):**

$$P_{comp} \equiv v_1 \land \neg p_1 \land \neg t_1 \land \neg g_1 \land \neg e_1 \land \neg p_2 \land \neg t_2 \land \neg vb_1$$

* **Regra Operacional:**

$$m_1 \rightarrow P_{comp}$$

## C. Proteção do Compressor contra Sobrepressão, Sobretemperatura e Vibração (Setor 200)

O motor do compressor ($m_1$) deve ser desligado ($\neg m_1$) caso a pressão de descarga ultrapasse o limite, a temperatura do cabeçote exceda o valor seguro, ou a vibração ultrapasse o limiar de disparo (trip).

* **Condição de Falha do Compressor ($F_2$):**

$$F_2 \equiv p_2 \lor t_2 \lor vb_1$$

* **Regra de Desligamento:**

$$F_2 \rightarrow \neg m_1$$

## D. Permissivo de Abertura do Dispensador / Início de Abastecimento (Setor 400)

A válvula de dispensação ($v_2$, XV-401) só pode abrir se: o operador tiver acionado o comando de início ($h_1$), a comunicação com o veículo estiver estabelecida ($c_1$), o acoplamento *breakaway* estiver íntegro ($bv_1$), o condicionamento do gás estiver adequado (pré-resfriamento $t_3$, pressão de buffer $p_3$ e chiller operacional $m_2$), e não houver vazamento de H₂ em nenhuma das duas zonas de detecção ($g_1$, $g_2$) nem parada de emergência ativa ($e_1$).

* **Condição de Permissivo de Abertura ($P_{disp}$):**

$$P_{disp} \equiv h_1 \land c_1 \land bv_1 \land t_3 \land p_3 \land m_2 \land \neg g_1 \land \neg g_2 \land \neg e_1$$

* **Regra Operacional:**

$$v_2 \rightarrow P_{disp}$$

## E. Trip de Abastecimento — Fechamento Imediato do Dispensador (Setor 400)

A válvula de dispensação ($v_2$) deve ser imediatamente fechada ($\neg v_2$) se a temperatura no ponto de recepção do veículo exceder o limite, se houver vazamento de H₂ detectado na área do dispensador, se o *breakaway* se desconectar, ou se a parada de emergência for acionada.

* **Condição de Falha de Abastecimento ($F_3$):**

$$F_3 \equiv t_4 \lor g_2 \lor \neg bv_1 \lor e_1$$

* **Regra de Bloqueio:**

$$F_3 \rightarrow \neg v_2$$

---

# Validação Formal por Prova Lógica (Tautologia de Segurança)

## Prova 1 — Segurança do Banco de Armazenamento

Para demonstrar ao motor do SCADA-Core que a planta nunca entrará em estado de risco de explosão por sobrepressão mantendo a válvula de saída do armazenamento aberta, constrói-se a prova formal do teorema de segurança.

* **Afirmação de Segurança:** "Não é possível ter sobrepressão no armazenamento ($p_1$) E manter a válvula de saída $v_1$ aberta."
* **Proposição do Estado de Risco ($S_{risco,1}$):**

$$S_{risco,1} \equiv p_1 \land v_1$$

Da regra de intertravamento A, sabe-se que $F_1 \rightarrow (\neg v_1 \land a_1)$, e que $p_1 \rightarrow F_1$ (pois $p_1$ é um dos disjuntos de $F_1$). Por silogismo hipotético, obtém-se a regra derivada implementada no controlador:

$$p_1 \rightarrow \neg v_1$$

Aplica-se a equivalência lógica do condicional ($\mathbf{A} \rightarrow \mathbf{B} \equiv \neg \mathbf{A} \lor \mathbf{B}$):

$$p_1 \rightarrow \neg v_1 \equiv \neg p_1 \lor \neg v_1$$

Substituindo o estado de risco sob a premissa de que a regra $p_1 \rightarrow \neg v_1$ é estritamente VERDADEIRA (restringindo o espaço de estados):

$$S_{risco,1} \land (\neg p_1 \lor \neg v_1)$$

$$(p_1 \land v_1) \land (\neg p_1 \lor \neg v_1)$$

Distribuindo $(p_1 \land v_1)$:

$$\big((p_1 \land v_1) \land \neg p_1\big) \lor \big((p_1 \land v_1) \land \neg v_1\big)$$

$$(Falso \land v_1) \lor (p_1 \land Falso)$$

$$Falso \lor Falso \equiv \text{FALSO}$$

O estado de risco $S_{risco,1}$ é, portanto, uma **contradição** sob a regra de intertravamento vigente — o controlador nunca permitirá que esse estado seja alcançado.

## Prova 2 — Segurança do Dispensador

Analogamente, demonstra-se que a planta nunca abastecerá um veículo na presença de vazamento de H₂ detectado na área do dispensador.

* **Afirmação de Segurança:** "Não é possível ter vazamento de H₂ no dispensador ($g_2$) E manter a válvula de dispensação $v_2$ aberta."
* **Proposição do Estado de Risco ($S_{risco,2}$):**

$$S_{risco,2} \equiv g_2 \land v_2$$

Da regra de intertravamento E, sabe-se que $F_3 \rightarrow \neg v_2$, e que $g_2 \rightarrow F_3$ (pois $g_2$ é um dos disjuntos de $F_3$). Por silogismo hipotético:

$$g_2 \rightarrow \neg v_2 \equiv \neg g_2 \lor \neg v_2$$

Substituindo o estado de risco:

$$S_{risco,2} \land (\neg g_2 \lor \neg v_2)$$

$$(g_2 \land v_2) \land (\neg g_2 \lor \neg v_2)$$

Distribuindo $(g_2 \land v_2)$:

$$\big((g_2 \land v_2) \land \neg g_2\big) \lor \big((g_2 \land v_2) \land \neg v_2\big)$$

$$(Falso \land v_2) \lor (g_2 \land Falso)$$

$$Falso \lor Falso \equiv \text{FALSO}$$

O estado de risco $S_{risco,2}$ é igualmente uma **contradição** lógica: o SCADA-Core nunca permitirá abastecimento com vazamento de H₂ ativo na área do dispensador.
