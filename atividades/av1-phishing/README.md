# AV1 — Experimentos com detecção de phishing

**Integrantes:** Paulo Eduardo e André Coelho  
**Disciplina:** IA para Cibersegurança

Esta atividade parte do notebook de classificação de phishing da aula. O objetivo foi fazer **duas alterações independentes**, comparar cada uma com o modelo original e discutir o efeito sobre a detecção de golpes e os alarmes falsos.

## Dados e avaliação

Foi utilizada a base [Phishing Websites, da UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/327/phishing), com **11.055 sites** e **30 features codificadas**. O notebook converte o rótulo original em `is_phishing`: `1` indica phishing e `0` indica site legítimo.

Os dados foram divididos uma única vez, de forma estratificada, em **7.738 sites para treino (70%)** e **3.317 para teste (30%)**, com `random_state=33`. Todas as comparações usam o mesmo conjunto de teste. A validação cruzada de cinco divisões calcula o F1 apenas sobre os dados de treino.

## Modelo de referência

O ponto de partida é um `RandomForestClassifier` com **150 árvores**, `class_weight='balanced'`, todas as 30 features e decisão padrão em torno de **0,50**. A comparação entre os três modelos usa esse mesmo ponto de decisão. A demonstração de limiar **0,50 × 0,20** já fazia parte do notebook da aula e não é uma das alterações da AV1.

## Alterações realizadas

### 1. Remoção de duas features

Foi treinado novamente o **mesmo Random Forest**, removendo `sslfinal_state` e `url_of_anchor` tanto do treino quanto do teste. Essas features apareciam no topo da importância calculada pelo modelo de referência: **0,300** e **0,246**, respectivamente.

O objetivo foi medir quanto o detector depende desses sinais quando eles deixam de estar disponíveis. Remover as colunas **não simula, por si só, um atacante alterando os valores de um site**.

### 2. Troca de algoritmo

Com **todas as 30 features**, foi treinada uma única `DecisionTreeClassifier(max_depth=5, class_weight='balanced', random_state=33)`. A profundidade máxima de 5 foi definida para manter a árvore compreensível e limitar seu crescimento. A comparação avalia essa configuração específica de árvore única frente ao Random Forest de 150 árvores.

## Resultados no conjunto de teste

| Modelo | TP: golpes detectados | FN: golpes perdidos | FP: alarmes falsos | F1 no teste | F1 na validação cruzada |
| --- | ---: | ---: | ---: | ---: | ---: |
| Referência: Random Forest, 30 features | 1.414 | 56 | 48 | 0,965 | 0,963 ± 0,004 |
| Alteração 1: Random Forest, 28 features | 1.365 | 105 | 163 | 0,911 | 0,903 ± 0,004 |
| Alteração 2: árvore única, profundidade 5 | 1.295 | 175 | 75 | 0,912 | 0,911 ± 0,007 |

**TP** significa phishing corretamente detectado; **FN**, phishing classificado como legítimo; **FP**, site legítimo marcado como phishing. Os valores são de avaliações separadas dos **mesmos 3.317 sites de teste**, e não devem ser somados entre as linhas.

A remoção das features aumentou principalmente os alarmes falsos (**48 → 163**) e também os golpes perdidos (**56 → 105**). A árvore única obteve F1 próximo ao da primeira alteração, mas com uma distribuição diferente de erros: **175 golpes perdidos** e **75 alarmes falsos**. Por isso, além do F1, é necessário observar o tipo de erro relevante para a segurança.

## Limites da interpretação

Os números vêm de uma única separação treino/teste e de uma base histórica. A validação cruzada foi feita no conjunto de treino, mas não substitui uma avaliação com dados mais recentes. A segunda alteração compara, ao mesmo tempo, um algoritmo de árvore única com capacidade limitada por `max_depth=5`; o experimento não isola o efeito de cada uma dessas escolhas.

## Execução

Abra o notebook desta pasta no **Google Colab** e execute as células em ordem. Ele instala `ucimlrepo`, baixa a base UCI durante a execução, reproduz as etapas da aula e apresenta, ao final, as duas alterações da AV1 e sua comparação.
