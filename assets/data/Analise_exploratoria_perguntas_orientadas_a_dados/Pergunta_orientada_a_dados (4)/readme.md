 # Modelo explicativo da Análise Exploratória de Dados (EDA)
🎯 Objetivo
Investigar como a disparidade de gênero interfere na situação atual de trabalho conforme a região onde a pessoa mora 
a hipótese de que a disparidade de gênero na contratação e remuneração varia conforme a região onde a pessoa mora, com base na base state_of_data_2023.csv.

✅ Passo 1 – Configuração do ambiente no Google Colab
python
Copiar
Editar
from google.colab import files
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

uploaded = files.upload()
Explicação:
Importa bibliotecas essenciais para análise de dados (Pandas, Matplotlib e Seaborn) e permite carregar o arquivo CSV localmente no ambiente do Colab.

✅ Passo 2 – Carregar e inspecionar os dados
python
Copiar
Editar
df = pd.read_csv('state_of_data_2023.csv')
display(df.head())
print(df.info())
display(df.describe(include='all'))
Explicação:
Lê o dataset e exibe:

As primeiras linhas da base;

Informações sobre colunas e tipos de dados;

Estatísticas descritivas para entender distribuição, média, desvio padrão, valores nulos etc.

✅ Passo 3 – Limpeza e preparação dos dados
python
Copiar
Editar
print(df.isnull().sum())
df_clean = df[['gender', 'region', 'salary']].dropna()
df_clean['gender'] = df_clean['gender'].astype('category')
Explicação:

Verifica valores ausentes por coluna.

Seleciona apenas as colunas relevantes para a hipótese.

Remove linhas com dados ausentes.

Converte a coluna gender em variável categórica (mais eficiente para análise).

✅ Passo 4 – Análise de distribuição por gênero e região
python
Copiar
Editar
plt.figure(figsize=(12,6))
sns.countplot(data=df_clean, x='region', hue='gender', palette='coolwarm')
plt.title('Distribuição de Profissionais por Gênero e Região')
plt.xticks(rotation=45)
plt.show()
Explicação:
Gera um gráfico de contagem para visualizar a distribuição de homens e mulheres por região, evidenciando possíveis desigualdades quantitativas.

✅ Passo 5 – Análise salarial comparativa
python
Copiar
Editar
plt.figure(figsize=(14,7))
sns.boxplot(data=df_clean, x='region', y='salary', hue='gender', 
            palette='pastel', showfliers=False)
plt.title('Distribuição Salarial por Gênero e Região')
plt.ylabel('Salário (R$)')
plt.xticks(rotation=45)
plt.show()
Explicação:
Boxplot compara a distribuição de salários entre homens e mulheres em cada região, facilitando a visualização de medianas e dispersões salariais.

✅ Passo 6 – Estatísticas descritivas agrupadas
python
Copiar
Editar
salario_medio = df_clean.groupby(['region', 'gender'])['salary'].mean().unstack()
salario_medio['diferença'] = salario_medio['male'] - salario_medio['female']
display(salario_medio)
python
Copiar
Editar
plt.figure(figsize=(10,6))
salario_medio['diferença'].plot(kind='bar', color='darkred')
plt.title('Diferença Salarial Média entre Gêneros por Região')
plt.ylabel('Diferença Salarial (R$)')
plt.show()
Explicação:

Calcula a média salarial por gênero e região.

Cria uma nova coluna com a diferença média salarial entre homens e mulheres.

Exibe essas diferenças em gráfico de barras.

✅ Passo 7 – Análise estatística adicional (teste t de Student)
python
Copiar
Editar
from scipy import stats

regioes = df_clean['region'].unique()
resultados = []

for regiao in regioes:
    masc = df_clean[(df_clean['region'] == regiao) & (df_clean['gender'] == 'male')]['salary']
    fem = df_clean[(df_clean['region'] == regiao) & (df_clean['gender'] == 'female')]['salary']
    
    t_stat, p_val = stats.ttest_ind(masc, fem, equal_var=False)
    resultados.append({
        'Região': regiao,
        'T-Statistic': t_stat,
        'P-Value': p_val,
        'Significativo (p < 0.05)': p_val < 0.05
    })

resultados_df = pd.DataFrame(resultados)
display(resultados_df)
Explicação:

Realiza o teste estatístico t de Student para comparar salários entre homens e mulheres por região.

Verifica se a diferença observada é estatisticamente significativa (p < 0.05).

Gera uma tabela com estatísticas e interpretação dos resultados.
