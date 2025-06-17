

Classificação da Doença de Parkinson a partir de Características da Voz
Este repositório contém o código-fonte e os dados utilizados na pesquisa intitulada: "Uma Abordagem de Classificação para a Doença de Parkinson Baseado em Ensemble Stacking e Múltiplas Representações de Características Vocais".

O objetivo deste trabalho é avaliar uma abordagem de ensemble stacking para a classificação da Doença de Parkinson (DP), utilizando um conjunto abrangente de características extraídas de sinais de voz.

Dataset
O conjunto de dados utilizado é o "Parkinson's Disease Speech Feature Set", coletado e disponibilizado publicamente por Sakar et al. (2019).

Fonte: UCI Machine Learning Repository
Composição: O dataset contém 756 amostras de 252 indivíduos (188 com DP e 64 controles saudáveis). Para cada amostra, 754 características acústicas foram extraídas.
Metodologia Implementada
O script main_parkinson_analysis.py implementa o pipeline experimental completo descrito no artigo. As principais características da metodologia são:

Validação Cruzada Leave-One-Subject-Out (LOSO): Para garantir uma avaliação de desempenho robusta e clinicamente relevante, o modelo é validado utilizando o protocolo LOSO. A cada iteração, todos os registros de um único indivíduo são reservados para teste, enquanto o modelo é treinado com os dados de todos os outros indivíduos.

Arquitetura Ensemble Stacking: O modelo de classificação é um ensemble de dois níveis.

Nível 1 (Classificadores Base): Um comitê composto por três algoritmos (Random Forest, Support Vector Classifier e Regressão Logística) é treinado.
Nível 2 (Meta-Classificador): As previsões dos classificadores base são usadas como entrada para treinar um meta-classificador (Regressão Logística), que realiza a predição final.
Múltiplas Representações de Características: A eficácia do ensemble é avaliada em três pipelines paralelos para investigar o impacto da representação dos dados:

Sem Redução: Utilizando o conjunto completo de 754 características originais.
Autoencoder (AE): Utilizando uma representação de 64 dimensões aprendida por um Autoencoder.
Análise Discriminante Linear (LDA): Utilizando uma projeção supervisionada gerada pelo LDA com regularização por shrinkage.
#Requisitos
Para executar este código, as seguintes bibliotecas Python são necessárias:

pandas
numpy
scikit-learn
tensorflow
(O código foi projetado para o ambiente Google Colab, que já possui estas bibliotecas pré-instaladas.)
Como Executar (Ambiente Google Colab)
Faça o upload do código: Copie o conteúdo do script .py para uma nova célula em um notebook do Google Colab.
Posicione o Dataset: Certifique-se de que o arquivo pd_speech_features.csv esteja no seu Google Drive, no caminho especificado dentro do código (atualmente: /content/drive/MyDrive/pd_speech_features.csv). Ajuste o caminho no script se necessário.
Execute a Célula: Ao executar a célula, o Colab solicitará permissão para acessar seu Google Drive. Siga as instruções para autorizar.
Aguarde os Resultados: O script irá executar o pipeline completo de validação LOSO e, ao final, imprimirá os relatórios de desempenho (Acurácia, F1-Score, ROC AUC, Matriz de Confusão, etc.) para cada um dos três pipelines.

Nota sobre Reprodutibilidade
O código neste repositório representa a versão final e estável da metodologia apresentada no artigo.

O melhor resultado reportado no artigo (Acurácia de 85,05% com o pipeline de Autoencoder) foi obtido durante a fase de desenvolvimento experimental. Devido à natureza estocástica de alguns algoritmos de aprendizado de máquina (ex: inicialização de pesos no Autoencoder, divisões internas do RandomForest), os resultados obtidos ao executar este código podem apresentar pequenas variações.

No entanto, espera-se que os resultados gerados por este script sejam consistentes e muito próximos aos valores apresentados na tabela de resultados da versão final do código (acurácia na faixa de 84-85%).
