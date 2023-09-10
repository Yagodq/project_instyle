
# Loja de Roupas InStyle - Classificador da Satisfação dos Clientes

A InStyle é uma das maiores lojas de roupas dos Estados Unidos que passa por problemas de experiência do cliente. O grande da empresa é manter a qualidade do produto e a taxa de satisfação do cliente em alta.

## 1. Problema de Negócio

O crescimento exponencial no número de vendas e clientes torna evidente problemas em diversas áreas como Produtos, Marketing e Desenvolvimento, os quais enfrentam problemas como determinar a necessidade dos clientes, determinar o cliente ideal e quedas do sistema por grande volume de acessos, respectivamente.

Nesse cenário, a medição da satisfação do cliente é extremamente importante para a empresa manter uma boa reputação perante o mercado, Como tarefa a equipe deve treinar um algoritmo de classificação dividindo os clientes em “Satisfeito” ou “Neutro/Insatisfeito”, prevendo quais clientes ficarão Insatisfeitos e portanto agindo rápido para entender o motivo da insatisfação e reverter o cenário do cliente.

A competição pode ser conferida pelo [Kaggle](https://www.kaggle.com/competitions/instyle-nps/leaderboard)

## 1.2 Premissas de Negócio assumidas

1. Este projeto foi desenvolvido para uma competição de dados, portanto, algumas etapas no desenvolvimento de um projeto são ignoradas pois o problema exige encontrar o modelo mais acertivo.
2. Os dados faltantes de atraso no tempo de entrega foram substituidos pelo tempo de atraso na saída da transportadora, pois foi considerado que são duas etapas com dependencia, levando a falta de dados de entrega pois o produto se encontra em processo e atraso na coleta pela transportadora .
3. A premissa anterior foi usada em preferencia a outras tecnicas como moda e média pois apresentou melhor desempenho para o resultado final do modelo.
4. Foram usadas todas as features para o treinamento do modelo, pois o modelo performou melhor neste cenário de competição, mas os gráficos de importância das features está presente no projeto.

## 2. Estratégia da Solução

A abordagem para resolver o desafio, seguindo a metodologia CRISP-DS , a qual se divide em 9 passos cíclicos para entrega de valor de forma rápida para a empresa, consiste em :

1. Problema de Negócio: Receber o problema de negócio das aréas solicitantes.

2. Entendimento de Negócio: Compreender a necessidade e dor dos setores envolvidos, validando protótipos de solução.

3. Coleta de Dados: Obter os dados necessários das tabelas do banco de dados da empresa.

4. Limpeza dos Dados: Remover sujeiras nos dados que possam afetar a performance do algoritmo de Machine Learning.

5. Exploração dos Dados: Analisar e entender as relações entre os dados, criando hipóteses acionáveis e novas features.

6. Análise Explorátoria dos Dados: Analisar e entender as relações entre os dados, criando hipóteses acionáveis e novas features.

7. Modelagem dos Dados: Preparar os dados para uso em algoritmos de Machine Learning, realizando transformações e encoding.

8. Aplicação de Algoritmos de Machine Learning: Selecionar e aplicar algoritmos nos dados preparados, comparando sua performance.

9. Avaliação de Performance: Verificar a performance do algoritmo selecionado em relação aos resultados atuais e traduzir para retorno financeiro.

10. Publicação da Solução: Publicar o algoritmo selecionado, tornando a solução disponível e utilizável.

### 2.1 Ferramentas Utilizadas

Foram utilizadas as seguintes ferramentas para criar a solução:

- Linguagem Python 3.9.17
- Jupyter Notebook para prototipação
- Git e Github para versionamento de código
- Manipulação e visualização de dados em linguagem Python
- Algoritmos de Classificação por meio das bibliotecas      [Scikit-Learn](https://scikit-learn.org/stable/), [Lightgbm](https://lightgbm.readthedocs.io/en/latest/pythonapi/lightgbm.LGBMClassifier.html) e [XGboost](https://xgboost.readthedocs.io/en/stable/index.html)
- Técnicas de Seleção de Features utilizando a biblioteca [Shap](https://shap.readthedocs.io/en/latest/)
- Otimização dos Hiperparâmetros pelo framework [Optuna](https://optuna.readthedocs.io/en/stable/)

### 2.2 Produto Final

O que será entregue efetivamente?

Uma tabela disponilizada por meio do Google Sheets, que contém os ID dos clientes classificados como 'Neutro/Insatisfeito' para os times de Marketing realizarem ações que possam reverter o cenário de insatisfação do cliente. 
## 3. Os 3 Principais Insights de Dados

Durante a Análise Exploratório dos dados foram levantadas hipóteses de negócio, as quais pode gerar novas informações ou contrapor crenças já estabelecidas, como resultado são gerados insights acionáveis ao time de negócio, podendo ser usados como direcionamento para tomada de decisão.

### *Hipótese 1 - Quem faz compras pessoais (uso próprio) fica mais satisfeito.*

**Falso:** Um dos possíveis motivos pode ser que esses clientes não usam de algumas features da loja, como o provador, lugar de espera, Wifi que podem estar impactando negativamente sua experiência. Nao podemos descartar a hipótese de que há um problema em relação à qualidade do produto.

### *Hipótese 2 - Clientes que dão notas 4 ou 5 em relação ao serviço da loja, ficam mais satisfeitos.*

**Falso :** Nota-se que mesmo com uma nota 4, ainda temos mais clientes insatisfeitos em maior número, fato que só muda na avaliação nota 5, onde temos um maior número de clientes satisfeitos. É preciso enfatizar a necessidade de oferecer um serviço excelente para otimizar a satisfação dos clientes, seja através de treinamentos, melhora na estrutura interna das lojas ou de outras informações obtidas com pesquisas.

### *Hipótese 3 - Quanto maior o tempo de entrega maior a insatisfação.*

**Verdadeiro:**  Quanto maior o atraso na entrega ( seja na operação ou na logística), maior a chance do cliente ficar insatisfeito. Isso ressalta na importância de se ter uma operação focada e entregando no prazo e serem áreas de destaque para receberem recursos.

#### *Cenários de possiveis ações:*


- Foco na compra online, menos custos relacionados à loja física e maior satisfação dos clientes.
    
- Otimização no sistema online para evitar sobrecargas e/ou possíveis ausências de dados.
    
- Avaliação das operações logísticas para entender os motivos de atrasos dentro e fora da operação.
## 4. Modelos de Machine Learning

No primeiro ciclo do projeto, foram testados quatro algoritmos  para escolher o melhor em termos de desempenho e custo de implementação.

Algoritmos selecionados:

- Lightgbm
- XGboost
- Random Forest
- Voting Classifier

### 4.1 Escolha do Modelo

O algoritmo Lightgbm foi escolhido pelos seguintes motivos:

1. O tempo de treinamento do Lightgbm é mais rápido em comparação com os demais modelos.
2. Foi o que melhor performou em relação aos demais, até mesmo em relação ao Voting que utiliza a técnica de ensemble.
3. Por ser o mais rápido em tempo de treinamento entre eles, o Lightgbm foi o modelo que sofreu melhores ajustes nos hiperparâmetros, motivo pelo qual o levou a ser mais o mais acertivo e escolhido para o desafio em questão.

### 4.2 Ajuste dos Hiperparâmetros 

Nesse problema em questão, o ajuste foi o fator principal para o desempenho do algoritmo e foi basntente explorado, segue como ilustração um gráfico de variação dos hiperparâmetros e como essa variação afetou o desempenho do modelo.



O gráfico auxilou na delimitação do range para encontrar mais facilmente os parametros ideais para atingir uma maior precisão.

### 4.3 Resultado do Modelo Treinado

O Algoritmo Lightgbm apresentou o melhor Precisão no treinamento do modelo, apresentando uma Precisão de 0.95127 nos dados de teste. 
Segue a Matriz de confusão obtida no treinamento do modelo, onde são demonstrado os acertos e erros do modelo em relação as duas classes da variável resposta.Vale notar que os quadrantes em azul são onde o modelo fez a previsão correta, e os demais onde ele errou.


## 5. Resultado de Negócio

Após  implementar o modelo de classificação de satisfação do cliente com Machine Learning, a satifação poderá sem melhor mensurada e resultara na criação de ações para reversão desse cenário.

Uma ação proposta é a reativação de clientes insatisfeitos por meio de ações com cupons de desconto pelo setor de Marketing. A escolha dos clientes alvo (Neutro/Insatisfeitos) de forma aleatória por parte do time de Marketingo pode gerar desperdício de recursos.

Foi constatado que por meio do uso do algoritmo de Classificação a precisão da campanha será 38,13% mais precisa que uma escolha de forma randômica, em uma cenário hipotético de receita de R$1.000.000 alocado, teriamos um econômia de R$381.300, valor o qual poderia ser realocado em outras áreas ou usado para potencializar o alcance da própria ação de marketing.
## 6. Conclusão

Como apresentado, o problema de negócio inicial foi resolvido com recursos para tomada de decisão das equipes e ganho de confiabilidade na identificação dos clientes Insatisfeitos.

## 7. Próximos passos

1. Colocar o modelo em produção para tornar o modelo utilizável e acessível a todos os setores interessados nas informações.
3. Criar um Dashboard gerencial por meio do framework Streamlit para disponibilizar uma análise mais detalhada das features e seu impacto na insatisfação dos clientes.

