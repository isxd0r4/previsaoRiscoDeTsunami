# Previsão de Risco de Tsunami a partir de dados de terremotos
Este repositório contém um projeto de aprendizado de máquina focado em prever a ocorrência de tsunamis com base em dados de atividades sísmicas globais. O código realiza a extração dos dados, enálise exploratória, pré-processamento e o treinamento de três diferentes modelos de classificação, otimizando seus hiperparâmetros.

## Objetivo do projeto
O objetivo principal é classificar se um terremoto resultará em um tsunami (variável alvo: `tsunami`).
Para otimização dos modelos, a métrica prioritária foi o Recall. EM cenários de desastres naturais, minizar os falsos negativos (prever que não haverá tsunami quando, na verdade, haverá) é crítico para a segurança pública e emissão de alertas.

## Tecnologias e bibliotecas utilizadas
* **Ambiente**: Google Colab
* **Linguagem**: Python
* **Manipulação e análise de dados**: pandas, matplotlib
* **Aprendizado de máquina**: scikit-learn (Random Forest, Logistic Regression, Linear SVM)

## Metodologia
O pipeline do projeto está dividido nas seguintes etapas:
1. **Coleta de dados**: Download automático via curl do *Global Earthquake & Tsunami Risk Assessment Dataset* diretamente do Kaggle.
2. **Análise exploratória (EDA)**: Visualização da distribuição das variáveis através de histogramas.
3. **Pré-processamento**:
   * Remoção de colunas irrelevantes (`Year`, `Month`)
   * Divisão dos dados em treino (70%) e teste (30%) com `stratify` para manter a proporção da variável alvo
   * Padronização das váriaveis utilizando `StandardScaler` dentro de um `Pipeline`
4. **Treinamento e otimização**: Utilização do `GridSearchCV` para testar diferentes combinações de hiperparâmetros (Grid Search) com validação cruzada (CV = 5) nos modelos
5. **Avaliação**: Teste final dos melhores estimadores de cada modelo utilizando o `classification_report` para visualização Precissão, Recall e F1-Score

## Como executar no Google Colab
Este código foi desenvolvido especificamente para ser executado de forma sequencial no Google Colaboratory. Siga os passos abaixo:

### Passo 01: Importar o notebook
1. Acesse o [Google Colab](https://colab.research.google.com/)
2. Vá em **File** (Arquivo) > **Upload notebook** (Fazer upload de notebook)
3. Selecione o arquivo `.ipynb` deste repositório que você baixou para a sua máquina

### Passo 02: Executar o código
O notebook está estruturado para rodar direto sem configurações adicionais. Você não precisa baixar os dados manualmente, o próprio código faz isso (a primeira célula faz o download usando o comando !curl diretamente da API pública do Kaggle).
1. No menu superior, clique em **Runtime** (Ambiente de execução) > **Run all** (Executar tudo)
2. Alternativa: Execute célula por célula clicando no botão de *play* ao lado de cada bloco de código.

## Resultados esperados
Ao final da execução, o console do Colab exibirá:
* Informações gerais e histogramas do dataset
* A médica de Recall obtida na validação cruzada (treino) para os três modelos
* O relatório completo de classificação (`classification_report`) detalhando o desempenho do Random Forest, Regressão Logística e SVM nos dados de teste, permitindo a comparação de qual modelo generalizou melhor para prever o risco de tsunamis.
