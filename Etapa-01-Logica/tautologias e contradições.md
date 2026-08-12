# Tautologias e Contradições no Sistema SCADA

No contexto do controle lógico de processos da Estação de Reabastecimento de Hidrogênio, a análise de tautologias e contradições garante que as equações booleanas dos intertravamentos (SIS) sejam consistentes e seguras.

## Tautologias
Uma tautologia é uma proposição que é **sempre verdadeira**, independentemente do valor lógico de suas variáveis. Em sistemas SCADA, representam fatos absolutos da planta ou lógicas de falha-segura intrínsecas.

**Exemplo 1: Estado binário de um equipamento**
A válvula de saída do banco de armazenamento (XV-101) está aberta ou não está aberta. Não existe um terceiro estado na lógica discreta.
* **Expressão:** $v_1 \lor \neg v_1$
* **Interpretação:** É uma verdade absoluta que a válvula se encontra em um destes dois estados para o controlador lógico.

**Exemplo 2: Princípio de Identidade em Alarmes**
Se a parada de emergência foi acionada, então a parada de emergência foi acionada.
* **Expressão:** $e_1 \rightarrow e_1$
* **Interpretação:** O acionamento do botão físico ESD-100 reflete inequivocamente na variável de emergência lógica do sistema.

## Contradições
Uma contradição é uma proposição que é **sempre falsa**. Em automação, contradições muitas vezes indicam falha de sensoriamento, erros de lógica de programação ou estados fisicamente impossíveis.

**Exemplo 1: Estados mutuamente exclusivos simultâneos**
O alarme geral (ALM-101) estar ativado e desativado ao mesmo tempo no mesmo ciclo de scan do CLP.
* **Expressão:** $a_1 \land \neg a_1$
* **Interpretação:** É impossível que a lógica determine que a sirene deve tocar e não tocar no mesmo instante. Se isso ocorrer em um código, há um erro de concorrência ou dupla escrita na bobina.

**Exemplo 2: Falha de sensor/Física impossível**
O sistema acusa que a pressão excede o limite máximo ($p_1$: $P > 900$ bar) e, ao mesmo tempo, não excede o limite máximo ($\neg p_1$: $P \leq 900$ bar).
* **Expressão:** $p_1 \land \neg p_1$
* **Interpretação:** Matematicamente falso. Na prática, se dois sensores redundantes na mesma tubulação indicarem $p_1$ e $\neg p_1$, o SCADA deve identificar uma falha de instrumentação, pois trata-se de uma contradição lógica.
