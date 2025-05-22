# Análise Exploratória - Disparidade de Gênero no Mercado de Trabalho

**Hipótese**: Classificar se a pessoa vai estar empregada ou desempregada conforme o gênero e a região onde ela mora.

Objetivo do seu modelo
Prever (classificar) a situação de trabalho com base em gênero e região — e com isso, entender como o gênero e a localização influenciam na desigualdade de emprego.
---

## 1. Importação de Bibliotecas

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.tree import DecisionTreeClassifier, plot_tree
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import LabelEncoder
from sklearn.metrics import classification_report, accuracy_score
```
Foram importadas bibliotecas para análise de dados (pandas, seaborn, matplotlib) e para machine learning (sklearn).

## 2. Leitura da Base de Dados
```python
base_princ = pd.read_csv('state_of_data_2023.csv')
```
Leitura da base de dados state_of_data_2023.csv.

## 3. Renomeação das Colunas
```python
novo_nome_colunas = {
    "('P1_a ', 'Idade')": 'Idade',
    "('P1_b ', 'Genero')": 'Genero',
    "('P1_c ', 'Cor/raca/etnia')": 'Cor/raca/etnia',
    "('P1_d ', 'PCD')": 'PCD',
    "('P1_i_1 ', 'uf onde mora')": 'UF',
    "('P1_i_2 ', 'Regiao onde mora')": 'Regiao onde mora',
    "('P1_l ', 'Nivel de Ensino')": 'Nível de Ensino',
    "('P1_m ', 'Área de Formação')": 'Área de formação',
    "('P2_a ', 'Qual sua situação atual de trabalho?')": 'Situação de trabalho'
}

base_princ.columns = [novo_nome_colunas.get(col, col) for col in base_princ.columns]
```
Mapeamento de nomes longos e complexos para nomes mais simples e intuitivos.

## 4. Seleção das Colunas Relevantes
```python
colunas = [
    "Idade",
    "Genero",
    "Cor/raca/etnia",
    "PCD",
    "UF",
    "Regiao onde mora",
    "Nível de Ensino",
    "Área de formação",
    "Situação de trabalho"
]
base_princ = base_princ[colunas]
```
Seleciona apenas as colunas relevantes para a hipótese.

## 5. Visualização Inicial
```python
base_princ.head()
```
Exibe as primeiras linhas da base para inspeção visual dos dados.

## 6. Verificação da Estrutura da Tabela
```python
base_princ.info()
```
Verifica o tipo de cada variável e a presença de valores nulos.

## 7. Verificação de valores nulos
```python
for col in base_princ.columns:
    nulos = base_princ[col].isnull().sum()
    print(f'numero de valores nulos na coluna {col} é: {nulos}')
```

## 8. Remoção de Valores Nulos em UF
```python
base_princ = base_princ.dropna(subset=['UF'])
```

## 9. Cálculo da Moda para Cada Coluna
```python
for col in base_princ.columns:
    mode_value = base_princ[col].mode()
    print(f'A moda da coluna {col} é: {mode_value.iloc[0]}')
```
Objetivo: Obter o valor mais frequente (moda) de cada coluna para entender padrões centrais em variáveis categóricas.

## 10. Preenchimento dos valores nulos
```python
base_princ.fillna(value='Computação / Engenharia de Software / Sistemas de Informação/ TI', inplace=True)
```
Objetivo: Preencher os valores nulos com a área de formação predominante, evitando perda de dados.

## 11. Remoção de Registros com Gênero "Outro"
```python
index_to_drop = base_princ[base_princ['Genero'] == 'Outro'].index
base_princ = base_princ.drop(index_to_drop)
```
Objetivo: Garantir a dicotomia homem/mulher, já que a categoria "Outro" não se enquadra no foco da análise de disparidade binária.

## 12. Análise Estrutual do DataFrame
```python
base_princ.info()
```
Objetivo: Verificar tipos de dados, valores não nulos e dimensões após as alterações iniciais.

## 13. Codificação de variáveis categóricas
```python
base_princ.loc[base_princ['Genero'] == 'Masculino', 'Genero'] = 0
base_princ.loc[base_princ['Genero'] == 'Feminino', 'Genero'] = 1
```
Objetivo: Transformar o gênero em valores numéricos para análise estatística.

```python
base_princ['Cor/raca/etnia'] = LabelEncoder().fit_transform(base_princ['Cor/raca/etnia'])
```
## 14. Padronização da coluna PCD
```python
base_princ.loc[base_princ['PCD'] == 'Sim', 'PCD'] = 1
base_princ.loc[base_princ['PCD'] == 'Não', 'PCD'] = 0
index_to_drop = base_princ[base_princ['PCD'] == 'Prefiro não informar'].index
base_princ = base_princ.drop(index_to_drop)
```
Objetivo: Binário para “Sim” e “Não”; removidos valores “Prefiro não informar”.

## 15. Codificação de Regiões e Estados
```python
base_princ['Regiao onde mora'] = base_princ['Regiao onde mora'].map({
    'Norte': 0, 'Nordeste': 1, 'Sudeste': 2, 'Sul': 3, 'Centro-Oeste': 4
})
```
Objetivo: Transformar regiões em dados numéricos ordenados .
```python
# Codificação manual dos estados brasileiros (UF)
base_princ['UF'] = base_princ['UF'].map({
    'AC': 0, 'AL': 1, 'AP': 2, 'AM': 3, 'BA': 4, 'CE': 5, 'DF': 6, 'ES': 7, 'GO': 8,
    'MA': 9, 'MT': 10, 'MS': 11, 'MG': 12, 'PA': 13, 'PB': 14, 'PR': 15, 'PE': 16,
    'PI': 17, 'RJ': 18, 'RN': 19, 'RS': 20, 'RO': 21, 'RR': 22, 'SC': 23, 'SP': 24,
    'SE': 25, 'TO': 26
})
```
Objetivo: Converter UF em valores numéricos únicos.

## 15. Nível de Ensino
```python
base_princ['Nível de Ensino'] = base_princ['Nível de Ensino'].map({
    'Não tenho graduação formal': 0,
    'Estudante de Graduação': 1,
    'Graduação/Bacharelado': 2,
    'Pós-graduação': 3,
    'Mestrado': 4,
    'Doutorado ou Phd': 5,
    'Prefiro não informar': 3
})
```
Objetivo: Codifcação e tratamento de dados faltantes com valores intermediário.

## 16. Área de formação
```python
base_princ['Área de formação'] = base_princ['Área de formação'].map({
    'Computação / Engenharia de Software / Sistemas de Informação/ TI': 0,
    'Economia/ Administração / Contabilidade / Finanças/ Negócios': 1,
    'Outras Engenharias': 6,
    'Química / Física': 3,
    'Estatística/ Matemática / Matemática Computacional/ Ciências Atuariais': 4,
    'Marketing / Publicidade / Comunicação / Jornalismo': 5,
    'Ciências Biológicas/ Farmácia/ Medicina/ Área da Saúde': 7,
    'Outra opção': 0,
    'Ciências Sociais': 8
})
```
Objetivo: Codificar áreas de formação com foco em facilitar segmentação posterior.

## 17. Situação de trabalho
```python
# Agrupando em 'Empregado(a)'
base_princ.loc[base_princ['Situação de trabalho'] == 'Empregado (CLT)', 'Situação de trabalho'] = 'Empregado(a)'
base_princ.loc[base_princ['Situação de trabalho'] == 'Empreendedor ou Empregado (CNPJ)', 'Situação de trabalho'] = 'Empregado(a)'
base_princ.loc[base_princ['Situação de trabalho'] == 'Estagiário', 'Situação de trabalho'] = 'Empregado(a)'
base_princ.loc[base_princ['Situação de trabalho'] == 'Trabalho na área Acadêmica/Pesquisador', 'Situação de trabalho'] = 'Empregado(a)'
base_princ.loc[base_princ['Situação de trabalho'] == 'Servidor Público', 'Situação de trabalho'] = 'Empregado(a)'
base_princ.loc[base_princ['Situação de trabalho'] == 'Vivo no Brasil e trabalho remoto para empresa de fora do Brasil', 'Situação de trabalho'] = 'Empregado(a)'
base_princ.loc[base_princ['Situação de trabalho'] == 'Vivo fora do Brasil e trabalho para empresa de fora do Brasil', 'Situação de trabalho'] = 'Empregado(a)'
base_princ.loc[base_princ['Situação de trabalho'] == 'Trabalho na área Acadêmica/Pesquisador', 'Situação de trabalho'] = 'Empregado(a)'
base_princ.loc[base_princ['Situação de trabalho'] == 'Freelancer', 'Situação de trabalho'] = 'Empregado(a)'

# Agrupando em 'Desempregado(a)'
base_princ.loc[base_princ['Situação de trabalho'] == 'Desempregado, buscando recolocação', 'Situação de trabalho'] = 'Desempregado(a)'
base_princ.loc[base_princ['Situação de trabalho'] == 'Desempregado e não estou buscando recolocação', 'Situação de trabalho'] = 'Desempregado(a)'
base_princ.loc[base_princ['Situação de trabalho'] == 'Somente Estudante (pós-graduação)', 'Situação de trabalho'] = 'Desempregado(a)'
base_princ.loc[base_princ['Situação de trabalho'] == 'Somente Estudante (graduação)', 'Situação de trabalho'] = 'Desempregado(a)'
base_princ.loc[base_princ['Situação de trabalho'] == 'Prefiro não informar', 'Situação de trabalho'] = 'Desempregado(a)'

# Verificando o resultado
print(base_princ['Situação de trabalho'].value_counts())

```
Objetivo: Reduzir a granularidade de situações de trabalho em duas categorias: Empregado(a) e Desempregado(a).

## 18. Verificação de Consistência
```python
base_princ['Situação de trabalho'].isnull().sum()
base_princ['Situação de trabalho'].unique()
base_princ.info()
```
Objetivo: Garantir que os dados estejam devidamente limpos e categorizados.

## 19. Análise Estatística das Variáveis
```python
# Statistical analysis
for col in base_princ.columns:
    print(f"\nAnalysis for {col}:")

    if pd.api.types.is_numeric_dtype(base_princ[col]):
        print(base_princ[col].describe())  # Descriptive stats for numerical
    else:
        print(base_princ[col].value_counts())  # Frequency counts for categorical
        print(f"Mode: {base_princ[col].mode()[0]}")  # Mode for categorical
```
Descrição:
Esta etapa realiza uma análise estatística básica para todas as colunas da base de dados base_princ.

Para colunas numéricas, são exibidas estatísticas descritivas como média, desvio padrão, valor mínimo, máximo e quartis.

Para colunas categóricas, são mostradas as frequências de cada categoria e a moda (valor mais comum).

Essa análise ajuda a entender melhor a distribuição e os valores predominantes em cada variável, servindo como base para decisões futuras de limpeza e transformação dos dados.

## 20. Exportação da Base de Dados Modificada
```python
base_princ.to_csv('base_princ_modificado.csv', index=False)
```
Descrição:
Após as análises e eventuais modificações realizadas na base base_princ, este comando exporta o DataFrame para um novo arquivo CSV chamado base_princ_modificado.csv.
O parâmetro index=False garante que o índice do DataFrame não seja salvo como uma coluna no arquivo final.

Essa etapa é importante para registrar as alterações feitas na base e possibilitar seu uso em futuras análises ou modelo

## 21. Download do arquivo modificado no google colab
```python
from google.colab import files
files.download('base_princ_modificado.csv')
```
Descrição:
Este comando permite o download do arquivo CSV modificado diretamente para o computador do usuário, quando o código está sendo executado no Google Colab.
A função files.download() baixa o arquivo 'base_princ_modificado.csv', que foi gerado na etapa anterior, tornando possível armazená-lo localmente para uso posterior ou compartilhamento.

# Primeiro modelo Induzido (Árvore de Decisão)
# Segundo modelo Induzido (K-Means)
