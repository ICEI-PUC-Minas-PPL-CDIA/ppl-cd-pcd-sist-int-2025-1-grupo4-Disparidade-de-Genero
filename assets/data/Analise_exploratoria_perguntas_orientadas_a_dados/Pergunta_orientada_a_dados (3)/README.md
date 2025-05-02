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

