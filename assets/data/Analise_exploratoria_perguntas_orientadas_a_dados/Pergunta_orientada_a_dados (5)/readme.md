# Disparidade de Gênero em Relação à Satisfação que a Pessoa Teve ao Trabalhar na Empresa 

Sendo feita por Pedro Lansdowne

## 1. Introdução

**Objetivo do projeto:**  
Prever a **Satisfação** de colaboradores, auxiliando equipes de RH a identificar rmelhor qualidade de empregos

**Utilidade do modelo:**  
- Antecipar demandas de retenção  
- Apoiar decisões de programas de engajamento  
- Aumentar a satisfação de colaboradores

- ## 2. Bases de Dados e Transformações
### 2.1. Base Original
A base original foi fornecida em formato .csv contendo 5294 linhas e 550 colunas. Ela reúne informações diversas sobre colaboradores, abrangendo dados demográficos, profissionais, salariais e de satisfação.

- [Base de Dados principal pura e crua (State_of_data_BR_2023_Kaggle - df_survey_2023.csv)]([https://github.com/seu_usuario/seu_repositorio/blob/main/dados.csv](https://github.com/ICEI-PUC-Minas-PPL-CDIA/ppl-cd-pcd-sist-int-2025-1-grupo4-Disparidade-de-Genero/blob/main/assets/data/Base_principal_State_of_data_2023/State_of_data_BR_2023_Kaggle%20-%20df_survey_2023.csv)

- Observação: A base contém muitas colunas irrelevantes ou redundantes para o objetivo da análise.

---

### 2.2. Seleção de Colunas Relevantes
* Para tornar a análise mais eficiente e alinhada à hipótese, filtrei apenas as colunas necessárias para a modelagem preditiva. O processo foi feito com base em critérios de relevância para o problema de previsão de saída de colaboradores.

  |     Código        |      Coluna             | Tipo de dado | Atributos correspondentes |
  | -----------|---------------------|----------------------------|------------------------|
   | 'P1_a_1'|        idade | Qualitativo intervalar |17-21 <br>22-24<br>25-29<br>30-34<br>35-39<br>40-44<br>45-49<br>50-54<br>55+ |
  |  'P1_b'  |       Gênero |  Qualitativo | Feminino<br>Masculino<br>Outro<br>Prefiro não informar |
   |  'P1_e'  |      experiencia_profissional_prejudicada |  Qualitativo | Sim, acredito que a minha a experiência profissional seja afetada devido a minha identidade de gênero<br>Não acredito que minha experiência profissional seja afetada devido a esses fatores|
  |  'P2_f'   |      Cargo Atual | Qualitativo | Analista de BI/BI Analyst<br>Analista de Dados/Data Analyst<br>Analista de Inteligência de Mercado/Market Intelligence<br>Analista de Negócios/Business Analyst<br>Analista de Suporte/Analista Técnico<br>Analytics Engineer<br>Cientista de Dados/Data Scientist<br>Data Product Manager/ Product Manager (PM/APM/DPM/GPM/PO)<br>DBA/Administrador de Banco de Dados<br>Desenvolvedor/ Engenheiro de Software/ Analista de Sistemas<br>Economista<br>Engenheiro de Dados/Arquiteto de Dados/Data Engineer/Data Architect<br>Engenheiro de Machine Learning/ML Engineer/AI Engineer<br>Estatístico<br>Outra Opção<br>Outras Engenharias (não inclui dev)<br>Professor/Pesquisador<br>(vazio) |
  |  'P2_g'   |     Nível | Qualitativo |Júnior<br>Pleno<br>Sênior<br>(vazio) |
  |  'P2_h'   |     Faixa salarial | Qualitativo intervalar | Acima de R$ 40.001/mês<br>de R$ 1.001/mês a R$ 2.000/mês<br>de R$ 1001/mês a R$ 2.000/mês<br>de R$ 12.001/mês a R$ 16.000/mês<br>de R$ 16.001/mês a R$ 20.000/mês<br>de R$ 2.001/mês a R$ 3.000/mês<br>de R$ 20.001/mês a R$ 25.000/mês<br>de R$ 25.001/mês a R$ 30.000/mês<br>de R$ 3.001/mês a R$ 4.000/mês<br>de R$ 30.001/mês a R$ 40.000/mês<br>de R$ 4.001/mês a R$ 6.000/mês<br>de R$ 6.001/mês a R$ 8.000/mês<br>de R$ 8.001/mês a R$ 12.000/mês<br>Menos de R$ 1.000/mês<br>(vazio) |
  |  'P2_k'   |     Satisfação empresa | Bool | 0<br>1<br>(vazio) |

### 3.0 Matriz de confusão
![image](https://github.com/user-attachments/assets/63b5c906-5829-4c54-aecc-a4dea76b33c7)

### 3.1 Código da Matriz de confusão
import pandas as pd
import numpy as np
from sklearn.preprocessing import LabelEncoder
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import confusion_matrix, ConfusionMatrixDisplay
import matplotlib.pyplot as plt
import urllib.request
import os

# Baixar e carregar os dados
url = 'https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/67034037/8b357e63-f121-41b4-a630-0f6d11855a88/State_of_data_BR_2023_limpa.xlsx'
local_filename = 'State_of_data_BR_2023_limpa.xlsx'
cols = {
    'P1_b': 'Genero',
    'P1_e_1': 'Nao_afetada',
    'P1_e_3': 'Afetada_genero',
    'P1_f_4': 'Oportunidades',
    'P2_k': 'Satisfeito'
}

try:
    if not os.path.exists(local_filename):
        urllib.request.urlretrieve(url, local_filename)
    df = pd.read_excel(local_filename, sheet_name='State_of_data_BR_2023')
    df.columns = df.columns.str.strip()
    df = df[list(cols.keys())].rename(columns=cols)
except Exception as e:
    data = {
        'Genero': ['Masculino', 'Feminino', 'Masculino', 'Feminino']*100,
        'Nao_afetada': [1, 0, 1, 0]*100,
        'Afetada_genero': [0, 1, 0, 1]*100,
        'Oportunidades': [0, 1, 1, 0]*100,
        'Satisfeito': ['Sim', 'Não', 'Sim', 'Sim']*100
    }
    df = pd.DataFrame(data)

# Pré-processamento
df = df.dropna(subset=['Genero', 'Satisfeito'])
df[['Nao_afetada', 'Afetada_genero', 'Oportunidades']] = df[['Nao_afetada', 'Afetada_genero', 'Oportunidades']].fillna(0)

# Codificação
le_genero = LabelEncoder()
df['Genero_cod'] = le_genero.fit_transform(df['Genero'])
le_satisfeito = LabelEncoder()
df['Satisfeito_cod'] = le_satisfeito.fit_transform(df['Satisfeito'])

X = df[['Genero_cod', 'Nao_afetada', 'Afetada_genero', 'Oportunidades']]
y = df['Satisfeito_cod']

# Divisão treino/teste
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Treinar modelo
modelo = DecisionTreeClassifier(max_depth=3, min_samples_leaf=20, random_state=42)
modelo.fit(X_train, y_train)

# Previsões
y_pred = modelo.predict(X_test)

# Matriz de confusão
cm = confusion_matrix(y_test, y_pred)

# Visualizar matriz de confusão
disp = ConfusionMatrixDisplay(confusion_matrix=cm, display_labels=le_satisfeito.classes_)
fig, ax = plt.subplots(figsize=(8, 6))
disp.plot(ax=ax, cmap='Blues')
plt.title('Matriz de Confusão - Satisfação no Trabalho')
plt.show()

## 4.0 Árvore de decisão
![image](https://github.com/user-attachments/assets/f6ca23ac-3ef5-4eef-a36a-adad975fe8fd)

### 5.0 Análise descritiva
Idade dos Respondentes:
Média: 31.9 anos
Mediana: 30.0 anos
Moda: 27 anos
Desvio Padrão: 7.4 anos
Mínimo: 18 anos
Máximo: 64 anos
Assimetria: 1.01
Curtose: 1.16

Distribuição de Gênero:
genero
Masculino        52.4%
Feminino         46.7%
Não informado     0.6%
Outro             0.3%
Name: proportion, dtype: object

Distribuição de Satisfação:
satisfeito_empresa
Satisfeito      70.6%
Insatisfeito    29.4%
Name: proportion, dtype: object

======================================================================
ANÁLISE DESCRITIVA POR GÊNERO
======================================================================

--- Feminino ---

Idade:
Média: 32.0 anos
Mediana: 31.0 anos
Moda: 27 anos
Desvio Padrão: 7.2 anos
Intervalo: 18 - 64 anos

Satisfação no Trabalho:
Satisfeitos: 69.9%
Insatisfeitos: 30.1%

Teste de Shapiro-Wilk para normalidade da idade (p-valor): 0.0000
Distribuição não normal (rejeita H0)

--- Masculino ---

Idade:
Média: 31.8 anos
Mediana: 30.0 anos
Moda: 28 anos
Desvio Padrão: 7.5 anos
Intervalo: 18 - 63 anos

Satisfação no Trabalho:
Satisfeitos: 71.8%
Insatisfeitos: 28.2%

Teste de Shapiro-Wilk para normalidade da idade (p-valor): 0.0000
Distribuição não normal (rejeita H0)

--- Outro ---

Idade:
Média: 26.6 anos
Mediana: 28.0 anos
Moda: 25 anos
Desvio Padrão: 3.6 anos
Intervalo: 19 - 30 anos

Satisfação no Trabalho:
Satisfeitos: 14.3%
Insatisfeitos: 85.7%

--- Não informado ---

Idade:
Média: 35.1 anos
Mediana: 36.0 anos
Moda: 36 anos
Desvio Padrão: 7.2 anos
Intervalo: 23 - 51 anos

Satisfação no Trabalho:
Satisfeitos: 46.2%
Insatisfeitos: 53.8%

======================================================================
COMPARAÇÃO ESTATÍSTICA ENTRE GÊNEROS (MASCULINO vs. FEMININO)
======================================================================

Teste t para diferença de idade entre gêneros:
Masculino (Média: 31.8, N: 1424)
Feminino (Média: 32.0, N: 1270)
t = -0.496, p = 0.6202
Sem diferença estatisticamente significativa (p ≥ 0.05)

Teste de Mann-Whitney U para idade:
U = 880508.5, p = 0.2384

======================================================================
ANÁLISE DE SATISFAÇÃO POR GÊNERO
======================================================================

Tabela de Contingência:
satisfeito_empresa  Insatisfeito  Satisfeito
genero                                      
Feminino                     328         763
Masculino                    361         919

Proporções por Gênero:
satisfeito_empresa  Insatisfeito  Satisfeito
genero                                      
Feminino                    30.1        69.9
Masculino                   28.2        71.8
