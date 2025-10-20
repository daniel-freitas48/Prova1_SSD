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
