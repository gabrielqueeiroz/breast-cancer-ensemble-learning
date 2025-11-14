# 🧬 Classificação de Subtipos de Câncer de Mama com Ensemble Learning
Este repositório contém o código-fonte e a metodologia do trabalho que propõe a utilização do Ensemble Learning para a classificação aprimorada de subtipos de câncer de mama, superando desafios comuns como dados transcriptômicos limitados e incompletos.

➡️**Artigo Completo (PDF):** [Acesse o Artigo Aceito no Congresso Pan-Amazônico de Oncologia](https://github.com/gabrielqueeiroz/breast-cancer-ensemble-learning/blob/main/gabriel-pan-amazonico1.pdf) <br>
➡️**Poster Apresentado:** [Visualize o Poster](https://github.com/gabrielqueeiroz/breast-cancer-ensemble-learning/blob/main/Poster-Pan-Amazonico-2.pdf)

## 💡 O problema: Limitação e Inconsistência nos Dados
A classificação molecular do câncer de mama é crucial para o tratamento eficaz. No entanto, os dados de expressão gênica utilizados apresentam barreiras significativas:
* **Dados Incompletos:** Os dados obtidos via microarrays podem conter valores perdidos ("omissos") devido a fatores técnicos, como poeira nas lâminas.
* **Dataset Limitado:** O conjunto de dados de 117 amostras (derivado do CPTAC e filtrado pelo PAM50) é considerado pequeno para técnicas avançadas.
* **Dificuldade de Distinção:** Classificadores individuais, como o Support Vector Classifier (SVC), apresentam considerável dificuldade em distinguir classes moleculares intimamente relacionadas, como Luminal A (LumA) e Luminal B (LumB).
  
## 🛠️ Nossa Solução:
Para mitigar o risco de sobreajuste (overfitting) e aumentar a capacidade de generalização em datasets pequenos , propusemos um modelo de Aprendizado em Comitê (Ensemble Learning) baseado em votação.

A solução utiliza o **VotingClassifier**, combinando as previsões de diferentes modelos para uma decisão final, sendo eles:
* Support Vector Classifier (SVC)
* Random Forest Classifier (RF)
* Gradient Boosting Classifier (GB)
* Logistic Regression (LR)

**Estratégia Otimizada:** Foi utilizada a modalidade Soft Voting, que calcula a média das probabilidades de previsão de cada modelo, permitindo que classificadores com maior confiança influenciem mais a decisão final.

## ✨ Contribuição Principal e Resultados
O modelo de ensemble superou significativamente o desempenho dos classificadores individuais, validando a hipótese de que a diversidade de modelos é crucial para otimizar a classificação em cenários desafiadores.

## Tabela 2 - Resultados da classificação com classificadores individuais e ensemble

| Métrica | Random Forest | Gradient Boosting | Logistic Regression | Support Vector Classification | Voting soft + GB | Voting soft | Voting hard + GB | Voting hard |
| :--- | :--- | :--- | :--- | :--- | :---: | :--- | :--- | :--- |
| Acurácia | 0.932 | 0.829 | 0.889 | 0.906 | **0.966** | 0.914 | 0.922 | 0.906 |
| Precisão | 0.873 | 0.778 | 0.890 | 0.917 | **0.957** | 0.900 | 0.880 | 0.896 |
| Recall | 0.917 | 0.791 | 0.913 | 0.891 | **0.976** | 0.910 | 0.949 | 0.901 |
| F1-Score | 0.885 | 0.760 | 0.875 | 0.891 | **0.960** | 0.894 | 0.897 | 0.885 |

*Obs: O melhor resultado foi obtido pelo Soft Voting com Gradient Boosting.*

A superioridade do Soft Voting demonstrou eficácia em:
* **Correção de Erros:** O comitê conseguiu acertar instâncias de fronteira que os modelos isolados classificaram erroneamente.
* **Resolução de Confusão:** O ensemble resolveu as dificuldades na classificação entre as classes Luminal A e Luminal B, generalizando de forma eficaz para todas as classes.
