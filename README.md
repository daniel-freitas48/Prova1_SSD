<div align="center">

# Prova 1 — Sistemas de Suporte à Decisão  
## Desenvolvimento de MVP: Detecção de Páginas *Phishing* com Machine Learning  

 **Aluno:** Daniel Cruz de Freitas  
**Matrícula:** 180099515  
**Professor:** André Serrano  

</div>

---

##  **1. Contexto**

 *Phishing* é uma forma de cibercrime em que atacantes se passam por entidades legítimas para induzir vítimas a fornecer informações sensíveis, como senhas ou dados bancários.  
 O projeto tem como foco o **desenvolvimento de modelos de Machine Learning** capazes de **detectar automaticamente páginas de phishing** com base em 48 variáveis técnicas extraídas das URLs e do conteúdo das páginas.

 **Fonte dos Dados:**  
[Phishing Dataset for Machine Learning – Kaggle](https://www.kaggle.com/datasets/shashwatwork/phishing-dataset-for-machine-learning/data)  
 *Tan, Choon Lin (2018), “Phishing Dataset for Machine Learning: Feature Evaluation”, Mendeley Data, V1.*

---

###  **Objetivo do Trabalho**

Desenvolver e comparar modelos clássicos de **classificação supervisionada** aplicados à detecção de *phishing*, passando por todas as etapas de um pipeline de Machine Learning:

-  Análise exploratória e verificação da integridade dos dados;  
-  Pré-processamento e normalização das variáveis;  
-  Treinamento e comparação de modelos clássicos (Logística, SVM, Random Forest);  
-  Otimização de hiperparâmetros via *GridSearchCV*;  
-  Avaliação de métricas e interpretação dos resultados.

 **Restrições na escolha dos dados:**
A base deveria ser **pública**, **validadamente reconhecida** e relacionada à **temática de Cibercrimes/Cibersegurança**.

---

##  **Formato do Dataset**

| Informação | Descrição |
|:--|:--|
| **Tamanho** | 10.000 amostras |
| **Variáveis preditoras** | 48 features numéricas |
| **Variável alvo** | `CLASS_LABEL` |
| **Classes** | 1 → *Phishing* ❌ / 0 → *Legítimo* ✅ |
| **Período de coleta** | 2015–2017 |
| **Ferramenta de extração** | Selenium WebDriver |

---

##  **Dicionário das Features — Phishing Dataset**

| **Feature** | **Descrição** |
|:--|:--|
| **NumDots** | Número de pontos (.) no URL. |
| **SubdomainLevel** | Quantidade de subdomínios antes do domínio principal. |
| **PathLevel** | Número de diretórios no caminho do URL. |
| **UrlLength** | Comprimento total do endereço. |
| **NumDash** | Quantidade de hifens (-) no URL. |
| **NumDashInHostname** | Hifens no nome do host. |
| **AtSymbol** | Presença do símbolo “@”. |
| **TildeSymbol** | Presença do símbolo “~” (usado em sites pessoais). |
| **NumUnderscore** | Número de sublinhados (_). |
| **NumPercent** | Número de caracteres de porcentagem (%). |
| **NumQueryComponents** | Quantidade de parâmetros de consulta (“?” no URL). |
| **NumAmpersand** | Número de símbolos “&”. |
| **NumHash** | Número de caracteres “#”. |
| **NumNumericChars** | Quantidade de dígitos numéricos. |
| **NoHttps** | Indica se o URL não usa HTTPS. |
| **RandomString** | Mede se o domínio é aleatório. |
| **IpAddress** | Indica se o domínio é um endereço IP. |
| **DomainInSubdomains** | Domínio aparece dentro de subdomínios. |
| **DomainInPaths** | Domínio repetido no caminho do URL. |
| **HttpsInHostname** | “https” aparece no nome do host. |
| **HostnameLength** | Comprimento do nome do host. |
| **PathLength** | Comprimento do caminho. |
| **QueryLength** | Comprimento da query. |
| **DoubleSlashInPath** | Presença de “//” no caminho. |
| **NumSensitiveWords** | Palavras sensíveis (secure, login...). |
| **EmbeddedBrandName** | Nome de marca no domínio. |
| **PctExtHyperlinks** | % de hyperlinks externos. |
| **PctExtResourceUrls** | % de recursos externos (imagens/scripts). |
| **ExtFavicon** | Favicon vindo de outro domínio. |
| **InsecureForms** | Formulários sem HTTPS. |
| **RelativeFormAction** | Formulário com ação relativa. |
| **ExtFormAction** | Formulário enviando para outro domínio. |
| **AbnormalFormAction** | Ação de formulário anormal. |
| **PctNullSelfRedirectHyperlinks** | % de hyperlinks sem redirecionamento próprio. |
| **FrequentDomainNameMismatch** | Domínio difere dos links internos. |
| **FakeLinkInStatusBar** | Link falso na barra de status. |
| **RightClickDisabled** | Clique direito desativado. |
| **PopUpWindow** | Página abre pop-ups automáticos. |
| **SubmitInfoToEmail** | Formulário envia dados por e-mail. |
| **IframeOrFrame** | Uso de iframes/frames. |
| **MissingTitle** | Página sem título. |
| **ImagesOnlyInForm** | Formulário contém apenas imagens. |
| **SubdomainLevelRT** | Nível de subdomínio (renderizado). |
| **PctExtNullSelfRedirectHyperlinksRT** | % de redirecionamentos externos (renderizados). |
| **ExtMetaScriptLinkRT** | % de meta/script/link externos. |
| **PctExtResourceUrlsRT** | % de recursos externos (renderizado). |
| **ExtFaviconRT** | Favicon externo (versão renderizada). |
| **CLASS_LABEL** | Variável alvo: 1 = phishing / 0 = legítimo. |

>  *Total de 48 variáveis preditoras + 1 variável alvo (CLASS_LABEL).*  
> Extraídas via **Selenium WebDriver**, balanceadas (5.000 phishing / 5.000 legítimas).

---

##  **2. Preparação dos Dados**

###  **Etapas Executadas**
- Verificação de nulos e duplicados (nenhum encontrado);  
- Normalização com `StandardScaler`;  
- Divisão treino/teste (70/30) com `stratify`;  
- Manutenção do balanceamento das classes;  
- Geração de amostras escalonadas (`X_train_scaled`, `X_test_scaled`).

 **Resultado:**
- Treino: 7.000 amostras  
- Teste: 3.000 amostras  
- Distribuição de classes: 50% / 50%

---

##  **3. Modelagem e Treinamento**

Três modelos clássicos foram testados:

| Modelo | Descrição | Observações |
|:--|:--|:--|
| **Regressão Logística** | Modelo linear, eficiente e interpretável. | Requer normalização. |
| **SVM (RBF)** | Busca o hiperplano ótimo de separação. | Alta acurácia, sensível à escala. |
| **Random Forest** | Conjunto de árvores de decisão independentes. | Mais robusto e estável. |

 **Métricas avaliadas:**  
- *Accuracy*  
- *Precision*  
- *Recall*  
- *F1-score*  
- Matriz de Confusão

 **Resultados iniciais:**

| Modelo | Acurácia |
|:--|:--:|
| Regressão Logística | 0.9517 |
| SVM | 0.9680 |
| Random Forest | **0.9857** ✅ |

<p align="center">
  <img width="600" src="https://github.com/user-attachments/assets/e7daa2e1-8753-4bfc-883e-8bed10ab0071" alt="Confusion Matrix">
</p>

> O Random Forest apresentou o melhor desempenho inicial, com F1 = 0.99 e 98,6% de acurácia — tornando-se o modelo selecionado para otimização.

---

##  **4. Análise dos Resultados**

- **Regressão Logística:** 83 falsos positivos e 62 falsos negativos.  
- **SVM:** redução equilibrada dos dois erros.  
- **Random Forest:** apenas 43 erros em 3.000 amostras (1,4%).

>  O modelo Random Forest demonstrou **excelente equilíbrio entre precisão e recall**, captando padrões robustos que distinguem páginas legítimas de phishing.

---

##  **5. Otimização de Hiperparâmetros (GridSearchCV)**

O *GridSearchCV (cv=5)* foi usado para refinar o Random Forest, testando diferentes combinações de parâmetros:

| Hiperparâmetro | Significado |
|:--|:--|
| `n_estimators` | Quantidade de árvores |
| `max_depth` | Profundidade máxima |
| `min_samples_split` | Amostras mínimas para divisão |
| `min_samples_leaf` | Amostras mínimas em cada folha |
| `max_features` | Quantidade de variáveis por divisão |

 **Melhor combinação encontrada:**

* max_depth = 20
* max_features = 'log2'
* min_samples_leaf = 1
* min_samples_split = 2
* n_estimators = 400

  
 **Desempenho final:**
- Acurácia (teste): **98,53%**
- *Precision*, *Recall*, *F1*: **0,99**
- Matriz de confusão equilibrada (FP = FN ≈ 22)

>  O desempenho otimizado manteve-se estável em relação ao modelo base, confirmando **robustez, ausência de overfitting e alta generalização.**

---

<div align="center">

 **Conclusão Final:**  
O projeto alcançou o objetivo proposto, apresentando um modelo de **alta acurácia e interpretabilidade**, aplicável em sistemas reais de detecção de *phishing*.  
O **Random Forest otimizado** demonstrou melhor custo-benefício entre desempenho, tempo de treino e explicabilidade.  

---

 Daniel Cruz de Freitas  
Engenharia de Produção — Universidade de Brasília (UnB)  
 *Sistemas de Suporte à Decisão — Prova 1*

</div>
