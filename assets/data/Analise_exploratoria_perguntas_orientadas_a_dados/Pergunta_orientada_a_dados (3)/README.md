# 🏁 Sprint 4 – Relatório Completo

## 1. Introdução

**Objetivo do projeto:**  
Prever a **intenção de saída** de colaboradores nos próximos 6 meses, auxiliando equipes de RH a identificar riscos de turnover.

**Utilidade do modelo:**  
- Antecipar demandas de retenção  
- Apoiar decisões de programas de engajamento  
- Reduzir custos de substituição e treinamento

---

## 2. Hipótese

> “A combinação de características demográficas, salariais e de satisfação no trabalho permite prever com boa acurácia quem pretende mudar de emprego.”

- **Variável-alvo (target):** `Pretenção de sair - TARGET` (binária: 1 = procura saída, 0 = não procura)
- **Features principais:** Idade média, Gênero, Nível, Cargo, Salário, Satisfação, Forma de trabalho, Trabalho ideal

---

## 3. Bases de Dados e Transformações
### 3.1. Base Original
A base original foi fornecida em formato .csv contendo 5294 linhas e 550 colunas. Ela reúne informações diversas sobre colaboradores, abrangendo dados demográficos, profissionais, salariais e de satisfação.

- [Base de Dados principal pura e crua (State_of_data_BR_2023_Kaggle - df_survey_2023.csv)]([https://github.com/seu_usuario/seu_repositorio/blob/main/dados.csv](https://github.com/ICEI-PUC-Minas-PPL-CDIA/ppl-cd-pcd-sist-int-2025-1-grupo4-Disparidade-de-Genero/blob/main/assets/data/Base_principal_State_of_data_2023/State_of_data_BR_2023_Kaggle%20-%20df_survey_2023.csv)

- Observação: A base contém muitas colunas irrelevantes ou redundantes para o objetivo da análise.

---

### 3.2. Seleção de Colunas Relevantes
* Para tornar a análise mais eficiente e alinhada à hipótese, filtrei apenas as colunas necessárias para a modelagem preditiva. O processo foi feito com base em critérios de relevância para o problema de previsão de saída de colaboradores.

  |     Código        |      Coluna             | Tipo de dado | Atributos correspondentes |
  | -----------|---------------------|----------------------------|------------------------|
   | 'P1_a_1'|       Faixa idade | Qualitativo intervalar |17-21 <br>22-24<br>25-29<br>30-34<br>35-39<br>40-44<br>45-49<br>50-54<br>55+ |
  |  'P1_b'  |       Gênero |  Qualitativo | Feminino<br>Masculino<br>Outro<br>Prefiro não informar |
  |  'P2_f'   |      Cargo Atual | Qualitativo | Analista de BI/BI Analyst<br>Analista de Dados/Data Analyst<br>Analista de Inteligência de Mercado/Market Intelligence<br>Analista de Negócios/Business Analyst<br>Analista de Suporte/Analista Técnico<br>Analytics Engineer<br>Cientista de Dados/Data Scientist<br>Data Product Manager/ Product Manager (PM/APM/DPM/GPM/PO)<br>DBA/Administrador de Banco de Dados<br>Desenvolvedor/ Engenheiro de Software/ Analista de Sistemas<br>Economista<br>Engenheiro de Dados/Arquiteto de Dados/Data Engineer/Data Architect<br>Engenheiro de Machine Learning/ML Engineer/AI Engineer<br>Estatístico<br>Outra Opção<br>Outras Engenharias (não inclui dev)<br>Professor/Pesquisador<br>(vazio) |
  |  'P2_g'   |     Nível | Qualitativo |Júnior<br>Pleno<br>Sênior<br>(vazio) |
  |  'P2_h'   |     Faixa salarial | Qualitativo intervalar | Acima de R$ 40.001/mês<br>de R$ 1.001/mês a R$ 2.000/mês<br>de R$ 1001/mês a R$ 2.000/mês<br>de R$ 12.001/mês a R$ 16.000/mês<br>de R$ 16.001/mês a R$ 20.000/mês<br>de R$ 2.001/mês a R$ 3.000/mês<br>de R$ 20.001/mês a R$ 25.000/mês<br>de R$ 25.001/mês a R$ 30.000/mês<br>de R$ 3.001/mês a R$ 4.000/mês<br>de R$ 30.001/mês a R$ 40.000/mês<br>de R$ 4.001/mês a R$ 6.000/mês<br>de R$ 6.001/mês a R$ 8.000/mês<br>de R$ 8.001/mês a R$ 12.000/mês<br>Menos de R$ 1.000/mês<br>(vazio) |
  |  'P2_k'   |     Satisfação empresa | Bool | 0<br>1<br>(vazio) |
  |  'P2_n'   |      Pretensão mudar emprego | Qualitativo | Estou em busca de oportunidades dentro ou fora do Brasil<br>Estou em busca de oportunidades, mas apenas fora do Brasil<br>Não estou buscando e não pretendo mudar de emprego nos próximos 6 meses<br>Não estou buscando, mas me considero aberto a outras oportunidades<br>(vazio) |
  |  'P2_r'    |     Forma de trabalho | Qualitativo |Modelo 100% presencial<br>Modelo 100% remoto<br>Modelo híbrido com dias fixos de trabalho presencial<br>Modelo híbrido flexível (o funcionário tem liberdade para escolher quando estar no escritório presencialmente)<br>(vazio) |
  |  'P2_s'     |     Forma de trabalho ideal | Qualitativo | Modelo 100% presencial<br>Modelo 100% remoto<br>Modelo híbrido com dias fixos de trabalho presencial<br>Modelo híbrido flexível (o funcionário tem liberdade para escolher quando estar no escritório presencialmente)<br>(vazio) |


### 3.3. Base Refinada e Transformações
Após a filtragem, realizei uma série de limpezas e transformações para preparar os dados para a modelagem. As principais etapas foram:

  #### 3.3.1. Conversão de faixas para valores médios (idade, salário)
  * 3.3.1.1 Média intervalos das faixas salariais:
  O programa precisava ler atributos float para ter uma noção boa do salário. A ideia foi tirar a média dos extremos dos intervalos.
  Código usado no excel:
  > =SE(ÉCÉL.VAZIA(H2);10000;
  SE(H2="Acima de R$ 40.001/mês";45000;
  SE(H2="de R$ 1.001/mês a R$ 2.000/mês";1500;
  SE(H2="de R$ 1001/mês a R$ 2.000/mês";1500;
  SE(H2="de R$ 12.001/mês a R$ 16.000/mês";14000;
  SE(H2="de R$ 16.001/mês a R$ 20.000/mês";18000;
  SE(H2="de R$ 2.001/mês a R$ 3.000/mês";2500;
  SE(H2="de R$ 20.001/mês a R$ 25.000/mês";22500;
  SE(H2="de R$ 25.001/mês a R$ 30.000/mês";27500;
  SE(H2="de R$ 3.001/mês a R$ 4.000/mês";3500;
  SE(H2="de R$ 30.001/mês a R$ 40.000/mês";35000;
  SE(H2="de R$ 4.001/mês a R$ 6.000/mês";5000;
  SE(H2="de R$ 6.001/mês a R$ 8.000/mês";7000;
  SE(H2="de R$ 8.001/mês a R$ 12.000/mês";10000;
  SE(H2="Menos de R$ 1.000/mês";500;"")))))))))))))))

  para a linha 2. Nas linhas subsequentes o código é o mesmo, só alterando a linha.
  * 3.3.1.2 Média intervalos das idades. O programa precisava ter um atributo int ou float. A ideia foi tirar a média dos extremos dos intervalos.
  Código usado no excel:
  > =SE(A2="17-21"; 19;
  SE(A2="22-24"; 23;
  SE(A2="25-29"; 27;
  SE(A2="30-34"; 32;
  SE(A2="35-39"; 37;
  SE(A2="40-44"; 42;
  SE(A2="45-49"; 47;
  SE(A2="50-54"; 52;
  SE(A2="55+"; 57,5)))))))))

  para a linha 2. Nas linhas subsequentes o código é o mesmo, só alterando a linha.
    
  #### 3.3.2. Agrupamento de cargos em categorias macro
  Havia muitos cargos, alguns "parecidos", podendo ser agrupados em macro-categorias. Alterações feitas:
  |Cargo Original|	Cargo Agrupado|
  |---------------|----------------|
  |Cientista de Dados/Data Scientist<br>Analista de Dados/Data Analyst<br>Analista de BI/BI Analyst<br>Analista de Inteligência de Mercado/Market Intelligence	|Análise de Dados|
  |Engenheiro de Dados/Arquiteto de Dados/Data Engineer/Data Architect<br>Analytics Engineer	|Engenharia de Dados|
  |Engenheiro de Machine Learning/ML Engineer/AI |Engineer	ML/IA|
  |Desenvolvedor/ Engenheiro de Software/ Analista de Sistemas	|Desenvolvimento|
  Data Product Manager/ Product Manager (PM/APM/DPM/GPM/PO)	|Produto|
  |Estatístico<br>Economista	|Científico/Quantitativo|
  |DBA/Administrador de Banco de Dados<br>Analista de Suporte/Analista Técnico|	Infraestrutura|
  |Outras Engenharias (não inclui dev)|	Outras Engenharias|
  |Professor/Pesquisador	|Acadêmico|
  |Analista de Negócios/Business Analyst|	Negócios|
  |Outra Opção	|Outro|
  |(vazio)	|Não informado|
  
  Código usado no excel:
  > =SE(ÉCÉL.VAZIA(D2);"Não informado";
  SE(OU(D2="Cientista de Dados/Data Scientist";D2="Analista de Dados/Data Analyst";D2="Analista de BI/BI Analyst";D2="Analista de Inteligência de Mercado/Market Intelligence");"Análise    de Dados";
  SE(OU(D2="Engenheiro de Dados/Arquiteto de Dados/Data Engineer/Data Architect";D2="Analytics Engineer");"Engenharia de Dados";
  SE(D2="Engenheiro de Machine Learning/ML Engineer/AI Engineer";"ML/IA";
  SE(D2="Desenvolvedor/ Engenheiro de Software/ Analista de Sistemas";"Desenvolvimento";
  SE(D2="Data Product Manager/ Product Manager (PM/APM/DPM/GPM/PO)";"Produto";
  SE(OU(D2="Estatístico";D2="Economista");"Científico/Quantitativo";
  SE(OU(D2="DBA/Administrador de Banco de Dados";D2="Analista de Suporte/Analista Técnico");"Infraestrutura";
  SE(D2="Outras Engenharias (não inclui dev)";"Outras Engenharias";
  SE(D2="Professor/Pesquisador";"Acadêmico";
  SE(D2="Analista de Negócios/Business Analyst";"Negócios";
  SE(D2="Outra Opção";"Outro";"Outro"))))))))))))

  para a linha 2. Nas linhas subsequentes o código é o mesmo, só alterando a linha.
  
  #### 3.3.3. Conversão de variáveis categóricas em numéricas (ordinal ou binária)
  * 3.3.3.1 Nível (júnior, pleno e sênior) são um atributo ordinal. Então decidi transformá-los em júnior=0, pleno=1 e sênior=2, porque sênior>pleno>júnior.
  Código usado:
  > =SE(F2="Júnior";0;
  SE(F2="Pleno";1;
  SE(F2="Sênior";2;
  SE(ÉCÉL.VAZIA(F2);ALEATÓRIOENTRE(0;2);""""))))

  para a linha 2. Nas linhas subsequentes o código é o mesmo, só alterando a linha.
  * 3.3.3.2 Pretensão de mudar de emprego está como atributo qualitativo. Para aquelas pessoas que apresentam qualquer vontade em sair de seu emprego, vou considerar que vão sair. 
  Inclusive, esse será o atributo-alvo. Segue abaixo o exemplo:

  |('P2_n ', 'Você pretende mudar de emprego nos próximos 6 meses?') | A pessoa vai sair da empresa?|
  |------------------------------------------------------------------|-------------------------------|
  |Estou em busca de oportunidades dentro ou fora do Brasil | Sim (1) |
  |Estou em busca de oportunidades, mas apenas fora do Brasil | Sim (1) |
  |Não estou buscando e não pretendo mudar de emprego nos próximos 6 meses | Não (0) |
  |Não estou buscando, mas me considero aberto a outras oportunidades | Sim (1) |
  |(vazio) | (vazio por enquanto) | 

  Código usado no excel: 
  > =SE(ÉCÉL.VAZIA(L2);
    SE(ALEATÓRIO()<=0,75;1;0);
    SE(OU(
        L2="Estou em busca de oportunidades dentro ou fora do Brasil";
        L2="Estou em busca de oportunidades, mas apenas fora do Brasil";
        L2="Não estou buscando, mas me considero aberto a outras oportunidades"
    );1;0))
  
  para a linha 2. Nas linhas subsequentes o código é o mesmo, só alterando a linha.

  
  #### 3.3.4. Preenchimento de valores ausentes de forma proporcional ou por estatística do grupo remoção de linhas. 
  * Você deve ter percebido que os códigos citados acima apresentam algo a mais que só transformar dados qualitativos em quantitativos ou outras funções como a de agrupamento.
  Foram implementados nos códigos a tarefa de preencherem os dados faltantes proporcionalmente à frequência com que os dados reais aparecem.
  * Vamos analisar coluna por coluna:
  * `('P1_a_1 ', 'Faixa idade')`:
    - não apresenta dados faltantes.
  * `('P1_b ', 'Genero')`:
    - Não apresenta dados faltantes. Entretanto, apresenta dados que podem não contribuir para a análise, como `Outro` e `Prefiro não informar`. Como esses dados são quase       insignificantes na base (veja a tabela abaixo), resolvi tirar.

  
  
   |('P1_b ', 'Genero')|	Porcentagem do total geral) |
   |-------------------|---------------------------------|
   |Feminino|	24,43%|
   |Masculino|	75,10%|
   |Outro	|0,17%|
   |Prefiro não informar|	0,30%|
  
  * `('P2_f ', 'Cargo Atual')`:
    - Nos dados faltantes, adicionei "Não foi informado"
  
  * `('P2_g ', 'Nivel')`
    - Haviam muitos dados faltantes. Para isso, distribuí proporcionalmente conforme eles aparecem realmente pelos dados faltantes, já que representam 27% de toda base e seria ruim removê-los. Na base, eles aparecem de forma equilibrada, confira:

  |Nível   |Quantidade|
  |--------|----------|
  |Júnior	| 1046|
  |Pleno	| 1392|
  |Sênior	| 1419|
  |(vazio) | 1437|	

  * `('P2_r ', 'Atualmente qual a sua forma de trabalho?')`
    - Haviam muitos dados faltantes. Para isso, distribuí proporcionalmente conforme eles aparecem realmente pelos dados faltantes, já que representam 10% de toda base e seria ruim removê-los. Na base, eles aparecem de forma que o Modelo 100% remoto se destaca. Confira:
   
  |('P2_r ', 'Atualmente qual a sua forma de trabalho?')|	Porcentaegm|
  |-----------------------------------------------------|--------------------------------|
  |Modelo 100% presencial	|14,93%|
  |Modelo 100% remoto	|41,58%|
  |Modelo híbrido com dias fixos de trabalho presencial|	14,93%|
  |Modelo híbrido flexível (o funcionário tem liberdade para escolher quando estar no escritório presencialmente)|	18,36%|
  |(vazio)	|10,20%|
   
  * `('P2_s ', 'Qual a forma de trabalho ideal para você?')`
    - Haviam muitos dados faltantes. Para isso, distribuí proporcionalmente conforme eles aparecem realmente pelos dados faltantes, já que representam 10% de toda base e seria ruim removê-los. Na base, eles aparecem de forma que o Modelo 100% remoto se destaca mais uma vez. Confira:
  
  |('P2_s ', 'Qual a forma de trabalho ideal para você?')|	Porcentagem|
  |------------------------------------------------------|--------------|
  |Modelo 100% presencial|	1,81%|
  |Modelo 100% remoto|	40,13%|
  |Modelo híbrido com dias fixos de trabalho presencial|	7,35%|
  |Modelo híbrido flexível (o funcionário tem liberdade para escolher quando estar no escritório presencialmente)|	40,51%|
  |(vazio)	|10,20%|
  
  #### 3.3.5. Criação de uma nova feature: `Estou no trabalho ideal para mim?`
  * Aqui a ideia foi pegar a coluna do trabalho que a pessoa está, juntamente com a coluna do trabalho que seria ideal para ela. Se a resposta for sim, eu criei uma nova coluna       simbolizando a satisfação pessoal da pessoa com seu trabalho. Se ela está no trabalho que é ideal para ela, as possibilidades de ela querer sair são reduzidas. Exemplo:

  |Forma de trabalho atual | Forma de trabalho ideal | Estou no trabalho ideal para mim? |
  |-------------------------------------------------------------------|---------------------------------------------|-----------|
  |Modelo híbrido flexível (o funcionário tem liberdade para escolher quando estar no escritório presencialmente)|Modelo 100% remoto| Não = 0|
  |Modelo 100% remoto |Modelo 100% remoto| Sim = 1|
  |Modelo 100% remoto|Modelo 100% remoto| Sim = 1|
  |Modelo 100% remoto|Modelo 100% remoto| Sim = 1|
  |Modelo híbrido com dias fixos de trabalho presencial|Modelo híbrido flexível (o funcionário tem liberdade para escolher quando estar no escritório presencialmente)| Não = 0|
  |Modelo 100% remoto|Modelo 100% remoto| Sim = 1|
  |Modelo híbrido com dias fixos de trabalho presencial|Modelo híbrido flexível (o funcionário tem liberdade para escolher quando estar no escritório presencialmente)| Não = 0|
  |Modelo híbrido flexível|Modelo híbrido flexível (o funcionário tem liberdade para escolher quando estar no escritório presencialmente)| Não = 0|
  |Modelo 100% presencial|Modelo híbrido flexível (o funcionário tem liberdade para escolher quando estar no escritório presencialmente)| Não = 0|

  Código para excel usado: 
  > =SE(O2=Q2;1;0)

  para a linha 2. Nas linhas subsequentes o código é o mesmo, só alterando a linha.

  
### 3.6. Base Refinada

* Após todas essas alterações, a base ficou assim: [base para modelo preditivo refinada.csv)]([https://github.com/seu_usuario/seu_repositorio/blob/main/dados.csv](https://github.com/ICEI-PUC-Minas-PPL-CDIA/ppl-cd-pcd-sist-int-2025-1-grupo4-Disparidade-de-Genero/blob/main/assets/data/Base_principal_State_of_data_2023/State_of_data_BR_2023_Kaggle%20-%20df_survey_2023.csv](https://github.com/ICEI-PUC-Minas-PPL-CDIA/ppl-cd-pcd-sist-int-2025-1-grupo4-Disparidade-de-Genero/blob/main/assets/data/Analise_exploratoria_perguntas_orientadas_a_dados/Pergunta_orientada_a_dados%20(3)/base%20para%20modelo%20preditivo%20refinada.csv))

  - Base original: 5294 linhas, 550 colunas
  - Base filtrada: 5294 linhas, 10 colunas
  - Base refinada: 5294 linhas, 18 colunas (após feature engineering)

* Observações:

  - Todas as etapas foram documentadas e os códigos utilizados estão nos blocos acima.
  - As transformações garantem que os dados estejam prontos para a modelagem preditiva.
  
---
## 4. Construção do 1º Modelo Induzido

Usei o Google Colab, programando em Python. Código usado:


> from google.colab import files
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier, plot_tree
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score
import matplotlib.pyplot as plt
import csv
uploaded = files.upload()
nome_arquivo = next(iter(uploaded))
data = pd.read_csv(
    nome_arquivo,
    sep=';',
    engine='python',
    encoding='latin1',
    quoting=csv.QUOTE_NONE
)
print("Dados carregados com sucesso!\n")
print(data.head())
print("\nColunas detectadas:")
print(data.columns.tolist())
target = 'Pretenção de sair - TARGET'
features = [
    'Média_Idades',
    "('P1_b ', 'Genero')",
    'Agrupamento_Cargo_Atual',
    'Nível_Ordinal',
    'MÉDIA_FAIXA_SALARIAL',
    'Satisfação na empresa dados preenchidos',
    'Forma de trabalho com dados faltantes preenchidos',
    'Estou no trabalho que quero?'
]
data = data.dropna(subset=[target])
X = data[features].copy()
y = data[target].copy()
X['Média_Idades'] = (
    X['Média_Idades']
      .astype(str)
      .str.replace(',', '.')
      .astype(float)
)
X['Nível_Ordinal'] = X['Nível_Ordinal'].astype(float)
X['Média_Idades'] = X['Média_Idades'].fillna(X['Média_Idades'].mean())
X['Nível_Ordinal'] = X['Nível_Ordinal'].fillna(X['Nível_Ordinal'].median())
X = pd.get_dummies(
    X,
    columns=[
        "('P1_b ', 'Genero')",
        'Agrupamento_Cargo_Atual',
        'Forma de trabalho com dados faltantes preenchidos'
    ],
    drop_first=True
    )
X_train, X_test, y_train, y_test = train_test_split(
    X, y,
    test_size=0.2,
    random_state=42
)
model = DecisionTreeClassifier(random_state=42)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
print(f'\nAcurácia:  {accuracy_score(y_test, y_pred):.2f}')
print(f'Precisão:  {precision_score(y_test, y_pred):.2f}')
print(f'Recall:    {recall_score(y_test, y_pred):.2f}')
print(f'F1-score:  {f1_score(y_test, y_pred):.2f}')
plt.figure(figsize=(20,10))
plot_tree(
    model,
    feature_names=X.columns,
    class_names=['Ficar','Sair'],
    filled=True,
    rounded=True,
    fontsize=10
)
plt.title("Árvore de Decisão – Intenção de Saída")
plt.show()

### Explicação do Código de Modelagem Preditiva

Este código implementa um fluxo completo de modelagem preditiva usando uma Árvore de Decisão para prever a intenção de saída de colaboradores. Veja o passo a passo:

* 1. Importação das Bibliotecas
`python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score`

  - `pandas`: manipulação e análise de dados.

  - `sklearn.model_selection.train_test_split`: separa os dados em conjuntos de treino e teste.

  - `sklearn.tree.DecisionTreeClassifier`: algoritmo de árvore de decisão para classificação.

  - `sklearn.metrics`: métricas para avaliação do modelo.

* 2. Carregamento da Base de Dados
`python
data = pd.read_csv('base para modelo preditivo refinada.csv')
print(data.head())`
  - Carrega o arquivo CSV com os dados já refinados e prontos para modelagem.

  - Exibe as primeiras linhas para conferência.

* 3. Definição das Variáveis
`target = 'Pretenção de sair - TARGET'
features = [
    'Média_Idades',
    'Genero',
    'Agrupamento_Cargo_Atual',
    'Nível de forma Ordinal',
    'MÉDIA_FAIXA_SALARIAL',
    'Satisfação na empresa dados preenchidos',
    'Forma de trabalho com dados faltantes preenchidos',
    'Estou no trabalho ideal para mim?'
]`

  - X = data[features]
  - y = data[target]
  - *target*: coluna que indica se o colaborador pretende sair (variável a ser prevista).

  - features: lista das colunas preditoras utilizadas pelo modelo.

  - X: DataFrame com as variáveis preditoras.

  - y: Série com a variável alvo.

* 4. Divisão dos Dados em Treinamento e Teste

`X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)`
  - Separa os dados em 80% para treino e 20% para teste, garantindo aleatoriedade reprodutível (random_state=42).

* 5. Treinamento do Modelo
`model = DecisionTreeClassifier(random_state=42)
model.fit(X_train, y_train)`
  - Inicializa o modelo de Árvore de Decisão.

  - Treina o modelo usando os dados de treino.

* 6. Realização de Previsões
`y_pred = model.predict(X_test)`
  - Utiliza o modelo treinado para prever a intenção de saída nos dados de teste.

* 7. Avaliação do Modelo
`accuracy = accuracy_score(y_test, y_pred)
print(f'Acurácia do modelo: {accuracy:.2f}')
precision = precision_score(y_test, y_pred)
print(f'Precisão do modelo: {precision:.2f}')
recall = recall_score(y_test, y_pred)
print(f'Recall do modelo: {recall:.2f}')
f1 = f1_score(y_test, y_pred)
print(f'F1-score do modelo: {f1:.2f}')`

  - *Acurácia*: proporção de previsões corretas.

  - *Precisão*: entre as previsões positivas, quantas estavam corretas.

  - *Recall*: entre os casos positivos reais, quantos foram identificados corretamente.

  - *F1-score*: média harmônica entre precisão e recall.

---

## 5. Resultados

### Avaliação do modelo:

  - Acurácia = 0.68
  - Precisão = 0.80
  - Recall = 0.78
  - F1-score = 0.79
  - cm = [[98,159],[178,619]]

### Árvore de decisão:

![arvore of the decisions](https://github.com/user-attachments/assets/5f882d5c-2e05-4c0d-9495-a391e5899638)


### Matriz de confusão:

![matriz confusao](https://github.com/user-attachments/assets/a0b3fdd8-f068-4555-9f72-40cff6184e96)




# 🏁 Sprint 4 ATUALIZADA – Relatório Completo

## 1. Introdução
**Objetivo do projeto:**
Antecipar a intenção de saída (turnover) de colaboradores no setor de tecnologia, fornecendo ao RH indicadores para programas de retenção.

**Por que este modelo?**

- Identificar riscos de desligamento antecipadamente
- Minimizar custos de substituição e treinamento
- Melhorar estratégias de engajamento e satisfação
- Em comparação com o a versão anterior, este modelo visa aumentar a acurácia, a precisão, o recall, o f1-score, AUROC, e aumentar os acertos da Matriz de Confusão, proporcionalmente ao conjunto analisado e testado.

## 2. Finalidade e explicações de o que foi feito
> “Quero otimizar o modelo preditivo anterior”

- **O que mudou em comparação à versão anterior do modelo?**
- Adicionei mais colunas: `('P1_a ', 'Idade')`(achei as idades numéricas sem estarem em faixas), `('P2_d ', 'Gestor?')`(vou remover todos os gestores porque o foco são os funcionários que pretendem sair), `('P0', 'id')`(para me ajudar nas análises no excel (vou remover posteriormente na hora do modelo)).
- Removi colunas: `('P1_a_1 ', 'Faixa idade')`(achei as idades numéricas sem estarem em faixas), `Média_Idades`(pelo mesmo motivo).
- Considerei remover todas as linhas as quais suas respectivas colunas continham algum atributo faltante ao invés de prever o dado vazio. (fiz isso na própria tabela do excel).
- Anteriormente, estive usando o Google Colab. Agora, adotei o Jupyter Notebook.
- Eu tinha separado 75% do modelo para aprendizado e 25% para teste. Mas agora separei 80% para aprendizado e 20% para teste.

- **O que foi mantido?**
- Optei por manter o algoritmo de árvore de decisão, uma vez que quero prever um conceito, mesmo que seja booleano (no caso, sair ou ficar, 1/0)
- O TARGET - `Pretenção de sair - TARGET`
- As outras colunas não citadas, como podemos ver na tabela abaixo: 


|      **Coluna**       | **Tipo de dado** | **Atributos correspondentes** | **Alteração** |
|-----------------------|------------------|-------------------------------|---------------|
|     `Faixa idade` | Qualitativo intervalar |17-21 <br>22-24<br>25-29<br>30-34<br>35-39<br>40-44<br>45-49<br>50-54<br>55+ | Removido |
|     `Gênero` |  Qualitativo | Feminino<br>Masculino<br>Outro<br>Prefiro não informar | Mantido |
|  `Cargo Atual` | Qualitativo | Analista de BI/BI Analyst<br>Analista de Dados/Data Analyst<br>Analista de Inteligência de Mercado/Market Intelligence<br>Analista de Negócios/Business Analyst<br>Analista de Suporte/Analista Técnico<br>Analytics Engineer<br>Cientista de Dados/Data Scientist<br>Data Product Manager/ Product Manager (PM/APM/DPM/GPM/PO)<br>DBA/Administrador de Banco de Dados<br>Desenvolvedor/ Engenheiro de Software/ Analista de Sistemas<br>Economista<br>Engenheiro de Dados/Arquiteto de Dados/Data Engineer/Data Architect<br>Engenheiro de Machine Learning/ML Engineer/AI Engineer<br>Estatístico<br>Outra Opção<br>Outras Engenharias (não inclui dev)<br>Professor/Pesquisador<br>(vazio) | Mantido |
|   `Nível` | Qualitativo |Júnior<br>Pleno<br>Sênior<br>(vazio) | Mantido |
|   `Faixa salarial` | Qualitativo intervalar | Acima de R$ 40.001/mês<br>de R$ 1.001/mês a R$ 2.000/mês<br>de R$ 1001/mês a R$ 2.000/mês<br>de R$ 12.001/mês a R$ 16.000/mês<br>de R$ 16.001/mês a R$ 20.000/mês<br>de R$ 2.001/mês a R$ 3.000/mês<br>de R$ 20.001/mês a R$ 25.000/mês<br>de R$ 25.001/mês a R$ 30.000/mês<br>de R$ 3.001/mês a R$ 4.000/mês<br>de R$ 30.001/mês a R$ 40.000/mês<br>de R$ 4.001/mês a R$ 6.000/mês<br>de R$ 6.001/mês a R$ 8.000/mês<br>de R$ 8.001/mês a R$ 12.000/mês<br>Menos de R$ 1.000/mês<br>(vazio) | Mantido |
|   `Satisfação empresa` | Bool | 0<br>1<br>(vazio) | Mantido |
|   `Pretensão mudar emprego` | Qualitativo | Estou em busca de oportunidades dentro ou fora do Brasil<br>Estou em busca de oportunidades, mas apenas fora do Brasil<br>Não estou buscando e não pretendo mudar de emprego nos próximos 6 meses<br>Não estou buscando, mas me considero aberto a outras oportunidades<br>(vazio) | Mantido |
|     `Forma de trabalho` | Qualitativo | Modelo 100% presencial<br>Modelo 100% remoto<br>Modelo híbrido com dias fixos de trabalho presencial<br>Modelo híbrido flexível (o funcionário tem liberdade para escolher quando estar no escritório presencialmente)<br>(vazio) | Mantido |
|     `Forma de trabalho ideal` | Qualitativo | Modelo 100% presencial<br>Modelo 100% remoto<br>Modelo híbrido com dias fixos de trabalho presencial<br>Modelo híbrido flexível (o funcionário tem liberdade para escolher quando estar no escritório presencialmente)<br>(vazio) | Mantido |
| `ID` | Qualitativo | códigos específicos como 001b2d1qtli8t9z7oqgdhj001b2d4i0g | Acrescido |
|`Gestor?` | Bool | 0 ou 1 | Acrescido |
|`Idade` | Quantitativo discreto | Números inteiros entre 18 e 73 incluindo os extremos | Acrescido |


---

- Como dessa vez eu vou manter as células vazias vazias para então removê-las, os códigos que adicionei às colunas mudaram: 

| **Qual coluna da base 2.0?** |**Nome da coluna na base 2.0** | **Código usado na filtragem dos dados** |
|------------------------------|-------------------------------|-----------------------------------------|
| A | `('P0', 'id')` | - |
| B | `('P1_a ', 'Idade')` | - |
| C | `('P1_b ', 'Genero')`| - |
| D | `('P1_e ', 'experiencia_profissional_prejudicada')` | - |
| E | `EXPERIÊNCIA PREJUDICADA SIM OU NAO` | =SE(ÉCÉL.VAZIA(D2);; SE(D2="Não acredito que minha experiência profissional seja afetada devido a esses fatores";0;1)) |
| F | `('P2_d ', 'Gestor?')` | - |
| G | `('P2_f ', 'Cargo Atual')` | - |
| H | `AGRUPAMENTO CARGOS` | =SE(ÉCÉL.VAZIA(G2);"Não informado"; SE(OU(G2="Cientista de Dados/Data Scientist";G2="Analista de Dados/Data Analyst";G2="Analista de BI/BI Analyst";G2="Analista de Inteligência de Mercado/Market Intelligence");"Análise de Dados"; SE(OU(G2="Engenheiro de Dados/Arquiteto de Dados/Data Engineer/Data Architect";G2="Analytics Engineer");"Engenharia de Dados"; SE(G2="Engenheiro de Machine Learning/ML Engineer/AI Engineer";"ML/IA"; SE(G2="Desenvolvedor/ Engenheiro de Software/ Analista de Sistemas";"Desenvolvimento"; SE(G2="Data Product Manager/ Product Manager (PM/APM/DPM/GPM/PO)";"Produto"; SE(OU(G2="Estatístico";G2="Economista");"Científico/Quantitativo"; SE(OU(G2="DBA/Administrador de Banco de Dados";G2="Analista de Suporte/Analista Técnico");"Infraestrutura"; SE(G2="Outras Engenharias (não inclui dev)";"Outras Engenharias"; SE(G2="Professor/Pesquisador";"Acadêmico"; SE(G2="Analista de Negócios/Business Analyst";"Negócios"; SE(G2="Outra Opção";"Outro";"Outro")))))))))))) |
| I | `('P2_h ', 'Faixa salarial')` | - |
| J | `MÉDIA FAIXA SALARIAL` | =SE(ÉCÉL.VAZIA(I2);; SE(I2="Acima de R$ 40.001/mês";45000; SE(I2="de R$ 1.001/mês a R$ 2.000/mês";1500; SE(I2="de R$ 1001/mês a R$ 2.000/mês";1500; SE(I2="de R$ 12.001/mês a R$ 16.000/mês";14000; SE(I2="de R$ 16.001/mês a R$ 20.000/mês";18000; SE(I2="de R$ 2.001/mês a R$ 3.000/mês";2500; SE(I2="de R$ 20.001/mês a R$ 25.000/mês";22500; SE(I2="de R$ 25.001/mês a R$ 30.000/mês";27500; SE(I2="de R$ 3.001/mês a R$ 4.000/mês";3500; SE(I2="de R$ 30.001/mês a R$ 40.000/mês";35000; SE(I2="de R$ 4.001/mês a R$ 6.000/mês";5000; SE(I2="de R$ 6.001/mês a R$ 8.000/mês";7000; SE(I2="de R$ 8.001/mês a R$ 12.000/mês";10000; SE(I2="Menos de R$ 1.000/mês";500;""))))))))))))))) |
| K | `('P2_g ', 'Nivel')` | - |
| L | `NÍVEL COM NÚMEROS ORDINAIS` | =SE(K2="Júnior";0; SE(K2="Pleno";1; SE(K2="Sênior";2; SE(ÉCÉL.VAZIA(K2);ALEATÓRIOENTRE(0;2);"""")))) |
| M | `('P2_k ', 'Você está satisfeito na sua empresa atual?')` | - |
| N | `('P2_n ', 'Você pretende mudar de emprego nos próximos 6 meses?')` | - |
| O | `PRETENDE SAIR SIM OU NAO - TARGET` | =SE(ÉCÉL.VAZIA(N2); SE(ALEATÓRIO()<=0,75;1;0); SE(OU(N2="Estou em busca de oportunidades dentro ou fora do Brasil"; N2="Estou em busca de oportunidades, mas apenas fora do Brasil"; N2="Não estou buscando, mas me considero aberto a outras oportunidades");1;0)) |
 | P | `('P2_r ', 'Atualmente qual a sua forma de trabalho?')` | - |
 | Q | `('P2_s ', 'Qual a forma de trabalho ideal para você?')` | - |
 | R | `ESTOU NO TRABALHO IDEAL?` | =SE(P2=Q2;1;0) |

Esta é a base refinada 2.0
---

- Para a base refinada 2.1, removi as colunas que não ajudariam na análise preditiva, removi todas as linhas com o atributo `1` correspondente à coluna `Gestor?`, depois removi a coluna `Gestor?` e removi todas as linhas com atributos faltantes, ficando assim:

Base 2.1: atributos: `('P1_a ', 'Idade')`, `('P1_b ', 'Genero')`, `EXPERIÊNCIA PREJUDICADA SIM OU NAO`, `AGRUPAMENTO CARGOS`, `MÉDIA FAIXA SALARIAL`, `NÍVEL COM NÚMEROS ORDINAIS`, `('P2_k ', 'Você está satisfeito na sua empresa atual?')`, `PRETENDE SAIR SIM OU NAO - TARGET`, `ESTOU NA FORMA DE TRABALHO IDEAL?`.

Esta é a base refinada 2.1
---

## 3. Acesso às bases de dados

**Base refinada 2.0**
- [BASE SPRINT 4 VERSAO 2.0.csv)]([https://github.com/seu_usuario/seu_repositorio/blob/main/dados.csv](https://github.com/ICEI-PUC-Minas-PPL-CDIA/ppl-cd-pcd-sist-int-2025-1-grupo4-Disparidade-de-Genero/commit/ed36a3a91a3095fc8c5fae1bcc7e1fb274cc9beb#diff-10b6f2cedd9707c28d337d832fd8dbc297debcce65626a4b2f86fd78f9b67988)

**Base refinada 2.1**
- [BASE SPRINT 4 VERSAO 2.1.csv)]([https://github.com/seu_usuario/seu_repositorio/blob/main/dados.csv](https://github.com/ICEI-PUC-Minas-PPL-CDIA/ppl-cd-pcd-sist-int-2025-1-grupo4-Disparidade-de-Genero/commit/c49d6555503f50f1eb98dc6c77e0e72bea512f7e)

| Base de dados | Número de linhas | Número de colunas |
|-----------------|------------------|-------------------|
| State of Data Brazil | 5294 | 399 |
| Refinada 1.0 | 5294 | 10 |
| Refinada 1.1 | 5294 | 18 |
| Refinada 2.0 | 5294 | 18 |
| Refinada 2.1 | 3857 | 9 |


---

## 4. Resultados

## 4.1. Modelo Anterior (árvore de decisão padrão)

- Accuracy: 0.68
- Precision: 0.80
- Recall: 0.78
- F1-score: 0.79

Matriz de Confusão:

| | Modelo disse que ficou | Modelo disse que saiu | 
|-|------------------------|-----------------------|
| Ficou | 98 | 159 |
| Saiu | 178 | 619 |

 
## 4.2. Modelo Atual (árvore otimizada via GridSearchCV)

- Melhores parâmetros:
> criterion='gini', max_depth=None, min_samples_leaf=1, class_weight=None

- Accuracy: 0.7552 (+11,7 pp)
- Precision: 0.7599 (–4,0 pp)
- Recall: 0.9880 (+20,8 pp)
- F1-score: 0.8591 (+6,9 pp)
- AUROC: 0.6878

Matriz de Confusão:

| | Modelo disse que ficou | Modelo disse que saiu | 
|-|------------------------|-----------------------|
| Ficou | 7 | 182 |
| Saiu | 7 | 576 |



### 4.2.1. Melhorias

- Recall saltou de 78 % para 98,8 %: o modelo quase não perde nenhum colaborador que vai sair.
- F1 subiu de 0,79 para 0,859: melhor equilíbrio geral.
- Accuracy cresceu de 0,68 para 0,755: bem acima do baseline de ~0,75.

### 4.2.2. Pioras
- Precision caiu de 0,80 para 0,76, aumentando falsos positivos (de 159 em 1024 (15%) para 182 em 772 (23%)).

- Justificativa: ao priorizar recall, o modelo ficou mais “conservador” em prever saída, aceitando mais alarmes falsos para não perder verdadeiros turnover — estratégia adequada quando perder um turnover real é mais custoso que lidar com intervenções desnecessárias.

---

## 5. Discussão e Conclusão
Trade-off recall × precision:
O novo modelo opta por maximizar recall, garantindo que quase ninguém que tenha intenção de sair seja ignorado.

### Impacto prático:

- Vantagem: RH consegue agir sobre praticamente 100 % dos potenciais turnover.
- Custo: maior número de falsos positivos (intervenções que não eram necessárias).

### Recomendação:
Este modelo é ideal quando o custo de perder um turnover (e permitir a saída sem reação) é maior que o custo de abordagens preventivas em falsos alarmes.

---

## 6. Reprodutibilidade
* Código em python 3 feito no jupyter notebook utilizado para o modelo 2.0 da SPRINT 4:


```
# 0. Instalação (executar apenas se necessário)
!pip install --upgrade pandas scikit-learn matplotlib

# 1. Importações
import os
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split, GridSearchCV
from sklearn.preprocessing import OneHotEncoder
from sklearn.compose import ColumnTransformer
from sklearn.dummy import DummyClassifier
from sklearn.tree import DecisionTreeClassifier, plot_tree
from sklearn import metrics

# 2. Carregar CSV (mesmo diretório do notebook)
filename = 'BASE SPRINT 4 VERSAO 2.1.csv'
df = pd.read_csv(filename, sep=';', encoding='latin1')

# 3. Renomear colunas para simplificar
df.rename(columns={
    "('P1_a ', 'Idade')": "Idade",
    "EXPERIÊNCIA PREJUDICADA SIM OU NAO": "ExperienciaPrejudicada",
    "AGRUPAMENTO CARGOS": "AgrupamentoCargos",
    "MÉDIA FAIXA SALARIAL": "MediaFaixaSalarial",
    "NÍVEL COM NÚMEROS ORDINAIS": "NivelOrdinal",
    "('P2_k ', 'Você está satisfeito na sua empresa atual?')": "Satisfeito",
    "PRETENDE SAIR SIM OU NAO - TARGET": "PretendeSair",
    "ESTOU NA FORMA DE TRABALHO IDEAL?": "TrabalhoIdeal"
}, inplace=True)

# 4. Definir features e target
feature_cols = [
    'Idade', 'ExperienciaPrejudicada', 'AgrupamentoCargos',
    'MediaFaixaSalarial', 'NivelOrdinal', 'Satisfeito', 'TrabalhoIdeal'
]
X = df[feature_cols]
y = df['PretendeSair']

# 5. Pré-processamento: One-Hot Encoding em AgrupamentoCargos
preproc = ColumnTransformer([
    ('onehot', OneHotEncoder(handle_unknown='ignore'), ['AgrupamentoCargos'])
], remainder='passthrough')
X_proc = preproc.fit_transform(X)

# 6. Dividir treino/teste 80% / 20% (estratificado)
X_train, X_test, y_train, y_test = train_test_split(
    X_proc, y, test_size=0.20, random_state=42, stratify=y
)

# 7. Baseline DummyClassifier
baseline = DummyClassifier(strategy='most_frequent', random_state=42)
baseline.fit(X_train, y_train)
y_base = baseline.predict(X_test)
print("=== Baseline Metrics ===")
print("Accuracy :", metrics.accuracy_score(y_test, y_base))
print("Precision:", metrics.precision_score(y_test, y_base, zero_division=0))
print("Recall   :", metrics.recall_score(y_test, y_base, zero_division=0))
print("F1 Score :", metrics.f1_score(y_test, y_base, zero_division=0))
print()

# 8. Hyperparameter Tuning com GridSearchCV
param_grid = {
    'criterion': ['gini', 'entropy'],
    'max_depth': [3, 5, 7, None],
    'min_samples_leaf': [1, 5, 10, 20],
    'class_weight': [None, 'balanced']
}
dt = DecisionTreeClassifier(random_state=42)
grid = GridSearchCV(dt, param_grid, cv=5, scoring='f1', n_jobs=-1)
grid.fit(X_train, y_train)

print("Melhores parâmetros:", grid.best_params_)
print("Melhor F1 em CV :", grid.best_score_, "\n")

# 9. Avaliar o melhor modelo no conjunto de teste
best_tree = grid.best_estimator_
y_pred = best_tree.predict(X_test)
y_proba = best_tree.predict_proba(X_test)[:, 1]

print("=== Test Metrics (Best Tree) ===")
print("Accuracy :", metrics.accuracy_score(y_test, y_pred))
print("Precision:", metrics.precision_score(y_test, y_pred, zero_division=0))
print("Recall   :", metrics.recall_score(y_test, y_pred, zero_division=0))
print("F1 Score :", metrics.f1_score(y_test, y_pred, zero_division=0))
print("AUROC    :", metrics.roc_auc_score(y_test, y_proba))
print()

# 10. Matriz de Confusão
cm = metrics.confusion_matrix(y_test, y_pred, labels=[0,1])
disp = metrics.ConfusionMatrixDisplay(cm, display_labels=['Fica (0)', 'Sai (1)'])
disp.plot(cmap=plt.cm.Blues)
plt.show()

# 11. Plot & exportar a árvore de decisão
plt.figure(figsize=(30,15), dpi=100)
plot_tree(
    best_tree,
    feature_names=preproc.get_feature_names_out(),
    class_names=['Fica','Sai'],
    filled=True, rounded=True, fontsize=12
)
plt.title("Árvore de Decisão Otimizada")
plt.savefig("decision_tree.png", dpi=300)
plt.show()

print("✅ Árvore exportada: decision_tree.png")

```
### Matriz de confusão:
![matriz de confusao 2](https://github.com/user-attachments/assets/2c3897dd-070b-4d92-90aa-d8bb22893583)

### Árvore de decisão: 
![arvore de decisao 2](https://github.com/user-attachments/assets/5ef9a7f3-7c81-4d12-ab86-ebc9ead490a5)


---

