# IA para Cibersegurança

Repositório de estudos e atividades da disciplina **IA para Cibersegurança**. Os notebooks acompanham as aulas e exploram aplicações de aprendizado de máquina na análise de tráfego de rede, detecção de phishing e malware, além de identificação de anomalias de comportamento.

## Conteúdo

| Aula | Tema | Notebook |
| --- | --- | --- |
| 1 | Preparação do ambiente | [Aula 1](aulas/aula01-setup/) |
| 2 | Fundamentos de aprendizado de máquina com Teachable Machine | [Aula 2](aulas/aula02-fundamentos-ml/) |
| 3 | Detecção de intrusões e análise de features com CIC-IDS2017 | [Aula 3](aulas/aula03-cicids2017/) |
| 4 | Métricas, validação e classificação de phishing | [Aula 4](aulas/aula04-phishing/) |
| 5 | Modelagem de um detector de malware | [Aula 5](aulas/aula05-malware/) |
| 6 | Detecção de anomalias, UEBA e mineração de processos | [Aula 6](aulas/aula06-anomalias-ueba/) |

## Atividades

- [AV1 — Experimentos com detecção de phishing](atividades/av1-phishing/): comparação de um Random Forest de referência com duas alterações independentes — remoção de duas features e uso de uma árvore de decisão.

## Como executar

1. Abra o notebook desejado no Google Colab ou em um ambiente Jupyter com Python.
2. Execute as células na ordem em que aparecem.
3. Verifique as instruções do próprio notebook para instalar bibliotecas e obter os dados. Algumas aulas baixam bases públicas durante a execução; a Aula 6 também permite gerar os dados no próprio notebook.

Os notebooks de aula são materiais de estudo da disciplina. A atividade AV1 reúne as alterações e a análise realizadas por **Paulo Eduardo e André Coelho**. Para entender o experimento e seus resultados, consulte o [README da AV1](atividades/av1-phishing/README.md).
