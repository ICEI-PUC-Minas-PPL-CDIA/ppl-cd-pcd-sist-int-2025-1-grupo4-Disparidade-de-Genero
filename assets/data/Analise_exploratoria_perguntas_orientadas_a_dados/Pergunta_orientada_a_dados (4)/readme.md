# 📊 Análise Exploratória - Disparidade de Gênero no Setor de Dados

**Hipótese:** Investigar como a disparidade de gênero interfere na situação atual de trabalho conforme a região onde a pessoa mora.

---

## 📦 Instalação de Pacotes

```python
!pip install pandas
Instala o pacote pandas para manipulação de dados tabulares.

📚 Importação de Bibliotecas
python
Copiar
Editar
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.tree import DecisionTreeClassifier, plot_tree
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import LabelEncoder
from sklearn.metrics import classification_report, accuracy_score
Importa bibliotecas utilizadas para análise de dados, visualização e machine learning.

📥 Leitura da Base de Dados
python
Copiar
Editar
base_princ = pd.read_csv('state_of_data_2023.csv')
Lê o arquivo CSV com os dados do projeto e armazena no DataFrame base_princ.

📝 Renomeando Colunas
python
Copiar
Editar
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
print(base_princ.columns)
Renomeia colunas da base para facilitar a leitura e análise dos dados.

🔎 Seleção de Colunas Relevantes
python
Copiar
Editar
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
base_princ.columns.tolist()
Seleciona apenas as colunas relevantes para a análise da hipótese proposta.

## 👀 Visualização Inicial da Base

```python
base_princ.head()
Exibe as primeiras linhas do DataFrame para verificar a estrutura dos dados.

python
Copiar
Editar
base_princ
Exibe todo o DataFrame (cuidado com uso em bases grandes).

python
Copiar
Editar
base_princ.info()
Mostra informações como número de entradas, colunas, tipos de dados e valores não nulos.

🧼 Tratamento de Valores Nulos
python
Copiar
Editar
for col in base_princ.columns:
    nulos = base_princ[col].isnull().sum()
    print(f'numero de valores nulos na coluna {col} é: {nulos}')
Conta e imprime a quantidade de valores nulos em cada coluna.

python
Copiar
Editar
# Remover valores nulos da coluna UF
base_princ = base_princ.dropna(subset=['UF'])

for col in base_princ.columns:
    nulos = base_princ[col].isnull().sum()
    print(f'numero de valores nulos na coluna {col} é: {nulos}')
Remove registros com valores ausentes na coluna UF.

📊 Cálculo da Moda
python
Copiar
Editar
# Calcular e imprimir a moda de cada coluna
for col in base_princ.columns:
    mode_value = base_princ[col].mode()
    print(f'A moda da coluna {col} é: {mode_value.iloc[0]}')
Calcula a moda (valor mais frequente) de cada coluna para avaliar possíveis preenchimentos.

✏️ Preenchimento de Dados Faltantes
python
Copiar
Editar
base_princ.fillna(value='Computação / Engenharia de Software / Sistemas de Informação/ TI', inplace=True)

for col in base_princ.columns:
    nulos = base_princ[col].isnull().sum()
    print(f'numero de valores nulos na coluna {col} é: {nulos}')
Preenche os valores nulos com a área de formação mais comum e confirma se ainda restam ausências.

🚫 Exclusão de Casos Ambíguos
python
Copiar
Editar
# Cortei o "Outro", por não identificar se era Homem ou Mulher
index_to_drop = base_princ[base_princ['Genero'] == 'Outro'].index
Filtra e identifica os registros onde o gênero é "Outro", para possível exclusão por não se enquadrar na análise binária.

🔢 Transformação de Variáveis Categóricas
python
Copiar
Editar
base_princ.loc[base_princ['Genero'] == 'Masculino', 'Genero'] = 0
base_princ.loc[base_princ['Genero'] == 'Feminino', 'Genero'] = 1
# Obtém os índices das linhas onde o gênero é "Outro"
index_to_drop = base_princ[base_princ['Genero'] == 'Outro'].index
Converte os valores da coluna Genero para formato binário (0 para masculino, 1 para feminino).

## Pré-processamento e transformação de colunas

### `base_princ = base_princ.drop(index_to_drop)`
Remove as linhas do DataFrame que foram marcadas anteriormente como indesejadas, por conterem valores como "Prefiro não informar" em colunas críticas.

### `base_princ['Cor/raca/etnia'] = LabelEncoder().fit_transform(base_princ['Cor/raca/etnia'])`
Aplica transformação numérica à coluna de raça/cor usando `LabelEncoder`, convertendo categorias textuais em valores numéricos.

### Substituição e exclusão de valores na coluna `PCD`
```python
base_princ.loc[base_princ['PCD'] == 'Sim', 'PCD'] = 1
base_princ.loc[base_princ['PCD'] == 'Não', 'PCD'] = 0
index_to_drop = base_princ[base_princ['PCD'] == 'Prefiro não informar'].index
base_princ = base_princ.drop(index_to_drop)
Converte respostas de "PCD" para valores binários (1 ou 0) e remove linhas com "Prefiro não informar".

Codificação de regiões
python
Copiar
Editar
base_princ.loc[base_princ['Regiao onde mora'] == 'Norte', 'Regiao onde mora'] = 0
...
base_princ.loc[base_princ['Regiao onde mora'] == 'Sul', 'Regiao onde mora'] = 4
Codifica a coluna Região onde mora em valores numéricos de 0 a 4, correspondendo a cada macrorregião do Brasil.

Codificação de estados (UF)
python
Copiar
Editar
base_princ.loc[base_princ['UF'] == 'AC', 'UF'] = 0
...
base_princ.loc[base_princ['UF'] == 'TO', 'UF'] = 26
Substitui siglas de estados por valores numéricos de 0 a 26.

Codificação do Nível de Ensino
python
Copiar
Editar
base_princ.loc[base_princ['Nível de Ensino'] == 'Não tenho graduação formal', 'Nível de Ensino'] = 0
...
base_princ.loc[base_princ['Nível de Ensino'] == 'Doutorado ou Phd', 'Nível de Ensino'] = 5
Converte os diferentes níveis de escolaridade em números de 0 a 5, facilitando análises e modelagem.

Atribuição da moda para valores faltantes
python
Copiar
Editar
mode_value = base_princ['Nível de Ensino'].mode()
base_princ.loc[base_princ['Nível de Ensino'] == 'Prefiro não informar', 'Nível de Ensino'] = 3
Substitui "Prefiro não informar" pela moda da coluna, assumida como "Pós-graduação".

Codificação da Área de formação
python
Copiar
Editar
base_princ.loc[base_princ['Área de formação'] == 'Computação / Engenharia de Software ...', 'Área de formação'] = 0
...
base_princ.loc[base_princ['Área de formação'] == 'Ciências Sociais', 'Área de formação'] = 8
Agrupa e codifica as áreas de formação por categorias numéricas.

Verificação do DataFrame
python
Copiar
Editar
base_princ.info()
Exibe um resumo das colunas, tipos de dados e contagem de valores não nulos.

Agrupamento da coluna Situação de trabalho
python
Copiar
Editar
base_princ.loc[base_princ['Situação de trabalho'] == 'Empregado (CLT)', 'Situação de trabalho'] = 'Empregado(a)'
...
base_princ.loc[base_princ['Situação de trabalho'] == 'Prefiro não informar', 'Situação de trabalho'] = 'Desempregado(a)'
Agrupa respostas da situação de trabalho em duas categorias: Empregado(a) e Desempregado(a).

Verificação de valores nulos na coluna
python
Copiar
Editar
null_counts = base_princ['Situação de trabalho'].isnull().sum()
print(f"Number of null values in 'Situação de trabalho': {null_counts}")
Verifica se há valores nulos na coluna Situação de trabalho.

## Conversão da coluna `Situação de trabalho` para variável binária

```python
base_princ.loc[base_princ['Situação de trabalho'] == 'Empregado(a)', 'Situação de trabalho'] = 1
base_princ.loc[base_princ['Situação de trabalho'] == 'Desempregado(a)', 'Situação de trabalho'] = 0
Transforma a variável Situação de trabalho em binária para fins de análise e modelagem preditiva: 1 representa empregado(a) e 0 representa desempregado(a).

Normalização dos dados
python
Copiar
Editar
scaler = StandardScaler()
base_princ.iloc[:, :] = scaler.fit_transform(base_princ.iloc[:, :])
Aplica StandardScaler para padronizar todas as colunas do DataFrame. A média passa a ser 0 e o desvio padrão 1, facilitando a performance de algoritmos de machine learning.

Separação das variáveis preditoras e alvo
python
Copiar
Editar
X = base_princ.drop('Situação de trabalho', axis=1)
y = base_princ['Situação de trabalho']
Separa os dados em duas partes:

X: todas as colunas preditoras

y: a variável alvo (situação de trabalho)

Divisão dos dados em treino e teste
python
Copiar
Editar
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, stratify=y, random_state=42)
Divide os dados em 70% para treino e 30% para teste, mantendo a proporção das classes com stratify=y.

Treinamento do modelo: Árvore de Decisão
python
Copiar
Editar
arvore = DecisionTreeClassifier(criterion='entropy', max_depth=3, random_state=42)
arvore.fit(X_train, y_train)
Cria e treina um modelo de árvore de decisão usando entropia como critério de divisão. A profundidade máxima é limitada a 3 para evitar overfitting.

Avaliação da acurácia do modelo
python
Copiar
Editar
acuracia = accuracy_score(y_test, arvore.predict(X_test))
print(f"Acurácia: {acuracia}")
Calcula e exibe a acurácia do modelo com base nos dados de teste.

Visualização da Árvore de Decisão
python
Copiar
Editar
plt.figure(figsize=(20,10))
plot_tree(arvore, filled=True, feature_names=X.columns, class_names=['Desempregado(a)', 'Empregado(a)'])
plt.show()
Gera uma visualização gráfica da árvore de decisão treinada, exibindo como as decisões foram tomadas com base nas variáveis preditoras.

Extração da importância das variáveis
python
Copiar
Editar
importances = pd.Series(arvore.feature_importances_, index=X.columns)
importances = importances[importances > 0]
importances = importances.sort_values(ascending=True)

plt.figure(figsize=(10, 6))
importances.plot(kind='barh')
plt.title('Importância das Variáveis')
plt.xlabel('Importância')
plt.ylabel('Variáveis')
plt.tight_layout()
plt.show()

