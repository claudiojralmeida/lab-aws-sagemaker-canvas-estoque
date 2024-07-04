# 📊 Previsão de Estoque Inteligente na AWS com [SageMaker Canvas](https://aws.amazon.com/pt/sagemaker/canvas/)

# Bootcamp da DIO em parceria com a Nexa - Machine Learning na AWS 

O projeto "Previsão de Estoque Inteligente na AWS com SageMaker Canvas" tem como objetivo criar previsões de estoque baseadas em Machine Learning (ML). Neste laboratório, foi utilizado o SageMaker Canvas, uma ferramenta no-code, para criar modelos precisos de Machine Learning através de uma interface sem código. Com o Amazon SageMaker Canvas, é possível facilmente criar, treinar, gerar previsões e implantar modelos de ML em um ambiente de produção, sem a necessidade de escrever nenhuma linha de código.

## 🎯 Neste repositório, compartilho o passo a passo da minha experiência com o projeto proposto no bootcamp. Ao longo da transcrição do laboratório, você encontrará insights sobre meu aprendizado com uma ferramenta em ML no-code, o Amazon SageMaker Canvas.


## 🚀 Passo a Passo

### 1. Seleção do Dataset

-   O dataset escolhido foi disponibilizado para o projeto na pasta 'datasets' deste repositório. Fiz o upload do dataset para o SageMaker Canvas para treinar e testar o modelo de Machine Learning.
-   O dataset para treinar o modelo de previsão de estoque é composto por:
    - 1000 observações (linhas);
    - 5 colunas: ID_PRODUTO, DATA_EVENTO, PRECO, FLAG_PROMOCAO e QUANTIDADE_ESTOQUE;
      - ID_PRODUTO: identificador único do tipo inteiro;
      - DATA_EVENTO: String com datas relacionadas ao produto variando entre o período de 2023-01-01 a 2023-12-31;
      - PRECO: Float com valores médios de 78.64, mínimo de 18.31 e máximo de 187.04;
      - FLAG_PROMOCAO: Inteiro, caracterizando uma variável categórica onde 1 indica que o produto está em promoção e 0 que não está em promoção;
      - QUANTIDADE_ESTOQUE: Inteiro, com valores variando de 1 a 100 e uma média de 55.73      

### 2. Construir/Treinar

-   Após importar o dataset selecionado para o SageMaker Canvas, analisei se foi carregado corretamente, verifiquei as linhas e colunas para assegurar que as informações estavam de acordo, com os tipos de dados corretos e sem valores faltantes. Em seguida, indiquei a coluna 'QUANTIDADE_ESTOQUE' como a variável alvo (target) para prever.
-   As demais configurações do modelo foram sugeridas automaticamente pelo SageMaker Canvas. Revisei as variáveis selecionadas da seguinte maneira: a coluna 'ID_PRODUTO' foi utilizada para identificar os preços dos produtos em estoque, e as variáveis independentes (features) incluíram 'PRECO', 'FLAG_PROMOCAO' e 'DATA_EVENTO' para treinar o modelo. O SageMaker Canvas selecionou a coluna 'DATA_EVENTO' como a que contém as datas e definiu o período de previsão entre 1 a 4 dias, com o padrão definido para 1 dia. O tipo do modelo também foi pré-definido pela ferramenta como um modelo de séries temporais.
-   O SageMaker Canvas fez sugestões sobre como tratar os dados. Para o dataset escolhido, a ferramenta sugeriu colocar valor ZERO para valores nulos em 'QUANTIDADE_ESTOQUE'. Embora outras sugestões de tratamento fossem oferecidas automaticamente, não houve necessidade de aplicá-las, pois os dados já estavam bem definidos.
-   Iniciei o treinamento do modelo com a opção de build rápida, que levou entre 15 a 20 minutos para completar. Esse tempo foi escolhido para não exceder o limite de computação gratuita da AWS para o SageMaker Canvas. A opção de standard build poderia ter sido utilizada para maior precisão no treinamento do modelo, embora levasse de 2 a 4 horas para completar.

### 3. Analisar

-   Após o treinamento, passei para a fase de analise.
-   Examinei as métricas de performance do modelo, como:
    -   Avg. wQL (Média da Perda Quantil Ponderada): Mede os erros nas previsões e deve ter valores próximos a zero para garantir melhores resultados;
    -   MAPE (Erro Percentual Médio Absoluto) e WAPE (Erro Percentual Absoluto Ponderado): Calculam a média da porcentagem de erro das previsões. O WAPE, além disso, leva em consideração a importância de cada item no estoque. Valores menores de WAPE são desejáveis;
    -   RMSE (Raiz do Erro Quadrático Médio): Mede a diferença média entre os valores previstos e os valores reais. Valores menores de RMSE são melhores;
    -   MASE (Erro Escalado Médio Absoluto): Compara o erro da previsão com um modelo simples. Um valor de MASE menor que 1 indica que o modelo está fazendo previsões mais precisas. 
-   Verifiquei as principais características que influenciram as previsões
-   Constatei que os preços têm pouco impacto no modelo e que as Flags de promoção praticamente não influenciam no estoque.

### 4. Prever

-   Na etapa de predição, gerei as previsões usando a opção 'single prediction', que apresenta todas as informações relevantes da previsão. Para analisar o padrão de vendas e estoque de um determinado produto, é necessário selecionar o identificador do produto que se deseja analisar.
-   Consegui visualizar um gráfico que mostra a demanda histórica do produto e os percentis (P10, P50 e P90). Os percentis representam diferentes cenários de previsão: P10 = previsões pessimistas, P50 = previsões normais e P90 = previsões otimistas.
-   Com isso, é possível entender a demanda de um produto em diferentes cenários, de acordo com os percentis apresentados (pessimista, normal e otimista). Dessa forma, pode-se tomar decisões com base nas interpretações dos valores e gráficos de cada produto, gerenciando o estoque de maneira inteligente.
-   Realizei a exportação dos dados gerados, contendo os percentis e a média de todos os produtos listados, para obter uma visão geral dos dados.

## 🚀 Melhorias e conclusão

Por conseguinte, se eu tiver a oportunidade de aprimorar o modelo treinado no SageMaker Canvas para previsão de estoque inteligente, pretendo incluir novos dados como conjunto de teste para realizar predições conforme o modelo desenvolvido. Isso permitirá avaliar como ele se comporta com os dados adicionados e garantir uma precisão ainda maior nas previsões.

Utilizar a ferramenta Amazon SageMaker Canvas foi fundamental para gerar insights valiosos a partir dos dados incorporados ao modelo de previsão, os quais podem ser facilmente aplicados no mundo real para apoiar decisões precisas. Aprendi de maneira intuitiva e eficiente a preparar, criar, treinar, gerar previsões e implantar modelos de ML, otimizando assim o gerenciamento e controle de estoque. Esse processo considera variáveis como promoções de produtos e renovação de estoque.

O SageMaker Canvas se destaca como uma excelente ferramenta para profissionais que buscam realizar análises de dados de forma ágil, especialmente pela abordagem no-code que oferece.
