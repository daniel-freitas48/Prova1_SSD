# Prova 1 - Sistemas de Suporte à Decisão
Desenvolvimento de MVP
Aluno: Daniel Cruz de Freitas

Matrícula: 180099515

Professor: André Serrano

# 1. Contexto (Baseado nas informações de DataSet do Kaggle)
Anti-phishing refere-se a esforços para bloquear ataques de phishing. Nesse tipo de cibercrime, atacantes se passam por entidades conhecidas ou confiáveis e contatam indivíduos (e-mail, SMS, telefone) solicitando informações sensíveis.

A base está disponível em: https://www.kaggle.com/datasets/shashwatwork/phishing-dataset-for-machine-learning/data

Objetivos
Desenvolver e comparar modelos clássicos de Machine Learning para classificar páginas como phishing ou legítimas, utilizando as 48 features disponibilizadas. Serão avaliados diferentes algoritmos e estratégias de pré-processamento, com divisão de treino/teste, validação cruzada e ajuste de hiperparâmetros, finalizando com comparação de métricas e análise crítica.

Quais restrições ou condições foram impostas para selecionar os dados?
As únicas restrições foram de que a base deveria se ruma base disponível em sites com datasets confiáveis e já validados, e que deveria ser utilizada a temática de CiberCrimes/CiberSegurança

# 2. Preparação dos Dados
O objetivo desta fase é preparar o conjunto de dados para o treinamento dos modelos. As etapas incluem:

* inspeção inicial e análise exploratória,
* tratamento de valores ausentes ou inconsistentes,
* normalização/padronização das variáveis,
* divisão entre conjuntos de treino e teste,
* verificação da proporcionalidade das classes (balanceamento).

Informações sobre os dados: O dataset contém 10 000 instâncias e 48 features numéricas já extraídas do conteúdo das páginas.

Cada linha representa um website (legítimo ou phishing), e a variável Result é a variável-alvo:

1 ➡ phishing ❌
-1 ➡ legítimo ✅

# 3. Modelagem e treinamento dos modelos
Após separar o conjunto de dados entre treino e teste, é possível fazer o treinamento de diferentes modelos clássicos de Machine Learning para comparar seus desempenhos no problema de classificação (phishing vs legítimo).

Foram utilizados os modelos:

* Regressão Logística: modelo linear que estima probabilidades e é eficiente em dados balanceados.
* Support Vector Machine (SVM): modelo que busca o hiperplano ótimo de separação entre classes, sensível à escala.
* Random Forest: conjunto de árvores de decisão que combina resultados de múltiplos classificadores, geralmente apresentando boa robustez e interpretabilidade.

Todos os modelos foram avaliados utilizando as mesmas métricas:

* Acurácia (Accuracy): proporção de previsões corretas.
* Matriz de confusão: visualiza erros e acertos entre as classes.
* Relatório de classificação (Precision, Recall, F1-Score): importante para medir desempenho equilibrado entre as classes.

Após o treino básico, o melhor modelo foi o Random Forest, que foi otimizado por meio de ajuste de hiperparâmetros, com validação cruzada.

<img width="584" height="436" alt="transferir" src="https://github.com/user-attachments/assets/e7daa2e1-8753-4bfc-883e-8bed10ab0071" />

