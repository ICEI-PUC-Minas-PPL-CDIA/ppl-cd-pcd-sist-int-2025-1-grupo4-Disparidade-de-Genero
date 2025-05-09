# ✍ Disparidade de Gênero na Contratação 
## ❓ Perguntas orientadas a dados
- Mulheres e homens têm taxas de contratação iguais no setor de tecnologia, considerando as mesmas qualificações, área de formação e nível de experiência?
-  A quantidade de vagas recebidas por mulheres na área de dados é inferior à quantidade recebida por homens, especialmente em empresas localizadas em regiões com alta demanda tecnológica?

## 💭 Seleção de atributos que respondem às perguntas orientadas a dados
Consultando o dicionário de dados da base do State of Data, foi possível selecionar os atributos que melhor respondem às perguntas. São eles:
### Pergunta 1:
- 'P1_b ', 'Genero'
- 'P2_f ', 'Cargo Atual'
- 'P2_i ', 'Quanto tempo de experiência na área de dados você tem?'
- 'P1_l ', 'Nivel de Ensino'
- 'P1_m ', 'Área de Formação'
### Pergunta 2:
- 'P1_b ', 'Genero'
- 'P1_f_1', 'Quantidade de oportunidades de emprego/vagas recebidas'
- 'P1_i ', 'Estado onde mora'
- 'P2_f ', 'Cargo Atual'


## 📊 Script para Criação de Bases de Dados 

Este script realiza a manipulação de dados de um arquivo CSV, criando duas bases de dados distintas a partir do DataFrame original. As bases de dados resultantes são salvas como arquivos CSV separados.

### 🧩 Passos para Execução

#### 🔹 Passo 1: Importar a biblioteca pandas

```python
import pandas as pd
```

A biblioteca pandas é essencial para a manipulação de dados, leitura de arquivos CSV, criação de DataFrames e realização de operações com os dados.

#### 🔹 Passo 2: Carregar o DataFrame Original

```python
df_survey = pd.read_csv('State_of_data_BR_2023_Kaggle - df_survey_2023.csv')
```

Usamos a função `pd.read_csv()` para ler o arquivo CSV original e criar um DataFrame chamado `df_survey`. Substitua `'State_of_data_BR_2023_Kaggle - df_survey_2023.csv'` pelo nome do seu arquivo CSV, se necessário.

#### 🔹 Passo 3: Definir as Colunas para Cada Base

```python
colunas_base1 = [
    "('P0', 'id')",
    "('P1_b ', 'Genero')",
    "('P2_f ', 'Cargo Atual')",
    "('P2_i ', 'Quanto tempo de experiência na área de dados você tem?')",
    "('P1_l ', 'Nivel de Ensino')",
    "('P1_m ', 'Área de Formação')"
]

colunas_base2 = [
    "('P0', 'id')",
    "('P1_b ', 'Genero')",
    "('P1_f_1', 'Quantidade de oportunidades de emprego/vagas recebidas')",
    "('P1_i ', 'Estado onde mora')",
    "('P2_f ', 'Cargo Atual')"
]
```

Aqui, definimos as listas `colunas_base1` e `colunas_base2`, que contêm os nomes das colunas desejadas para cada base de dados. Incluímos o ID do respondente (`"('P0', 'id')"`), que será utilizado em ambas as bases.

#### 🔹 Passo 4: Criar e Salvar as Bases de Dados

```python
df_base1 = df_survey[colunas_base1]
df_base1.to_csv('base1.csv', index=False)

df_base2 = df_survey[colunas_base2]
df_base2.to_csv('base2.csv', index=False)

print("Bases de dados criadas com sucesso!")
```

Neste passo, criamos os DataFrames `df_base1` e `df_base2` a partir das colunas definidas nas listas acima. Em seguida, salvamos cada DataFrame como um arquivo CSV (`base1.csv` e `base2.csv`), utilizando o método `to_csv()`. O argumento `index=False` garante que o índice do DataFrame não seja incluído nos arquivos CSV.

#### ✅ Resultado

Ao final da execução do script, as bases de dados serão salvas com sucesso e uma mensagem será exibida:

```
Bases de dados criadas com sucesso!
```

## 📘 Geração de Dicionário de Dados em Markdown com Python

Este repositório contém um script em Python que gera automaticamente tabelas em formato Markdown com dicionários de dados, a partir de um conjunto de atributos referentes a perguntas de um questionário.

---

### 📂 Estrutura do Script

#### 1. Importar a biblioteca `pandas`

```python
import pandas as pd
```

📌 Importa a biblioteca `pandas`, que é essencial para trabalhar com DataFrames e manipulação de dados tabulares em Python.

---

#### 2. Inicializar dicionários de dados

```python
dicionario_dados_q1 = []
dicionario_dados_q2 = []
```

📌 Cria duas listas vazias para armazenar os atributos das perguntas 1 e 2.

---

#### 3. Definir atributos para a pergunta 1

```python
atributos_q1 = {
    "('P1_b ', 'Genero')": {
        'Tipo do Dado': 'Qualitativo',
        'Escala': 'Nominal',
        'Descrição': 'Identidade de gênero do participante.'
    },
    # ... outros atributos ...
}
```

📌 Define os atributos da pergunta 1, especificando tipo de dado, escala e descrição.

---

#### 4. Criar dicionário de dados para a pergunta 1

```python
for atributo, info in atributos_q1.items():
    dicionario_dados_q1.append({
        'Atributo': atributo,
        'Tipo do Dado': info['Tipo do Dado'],
        'Escala': info['Escala'],
        'Descrição': info['Descrição']
    })
```

📌 Transforma os dados de `atributos_q1` em uma lista de dicionários.

---

#### 5. Definir atributos para a pergunta 2

```python
atributos_q2 = {
    "('P1_b ', 'Genero')": {
        'Tipo do Dado': 'Qualitativo',
        'Escala': 'Nominal',
        'Descrição': 'Identidade de gênero do participante.'
    },
    # ... outros atributos ...
}
```

📌 Define os atributos da pergunta 2 com suas informações.

---

#### 6. Criar dicionário de dados para a pergunta 2

```python
for atributo, info in atributos_q2.items():
    dicionario_dados_q2.append({
        'Atributo': atributo,
        'Tipo do Dado': info['Tipo do Dado'],
        'Escala': info['Escala'],
        'Descrição': info['Descrição']
    })
```

📌 Organiza as informações dos atributos da pergunta 2 na forma de lista de dicionários.

---

#### 7. Gerar tabelas em Markdown

```python
tabela_markdown_q1 = pd.DataFrame(dicionario_dados_q1).to_markdown(index=False)
tabela_markdown_q2 = pd.DataFrame(dicionario_dados_q2).to_markdown(index=False)
```

📌 Converte as listas em `DataFrame` e utiliza `.to_markdown()` para gerar as tabelas em Markdown.

---

#### 8. Imprimir as tabelas

```python
print("## Pergunta 1\n")
print(tabela_markdown_q1)
print("\n## Pergunta 2\n")
print(tabela_markdown_q2)
```

📌 Exibe no terminal as tabelas geradas para cada pergunta.

---

### ✅ Resultado Esperado

#### Pergunta 1

| Atributo                                                 | Tipo do Dado | Escala  | Descrição                                     |
|----------------------------------------------------------|--------------|---------|------------------------------------------------|
| ('P1_b ', 'Genero')                                      | Qualitativo  | Nominal | Identidade de gênero do participante.          |
| ('P2_f ', 'Cargo Atual')                                 | Qualitativo  | Nominal | Cargo atual do participante.                   |
| ('P2_i ', 'Quanto tempo de experiência na área de dados você tem?') | Quantitativo | Discreta | Tempo de experiência na área de dados em anos. |
| ('P1_l ', 'Nivel de Ensino')                             | Qualitativo  | Ordinal | Nível de ensino do participante.               |
| ('P1_m ', 'Área de Formação')                            | Qualitativo  | Nominal | Área de formação do participante.              |

#### Pergunta 2

| Atributo                                                                | Tipo do Dado | Escala  | Descrição                                                  |
|-------------------------------------------------------------------------|--------------|---------|-------------------------------------------------------------|
| ('P1_b ', 'Genero')                                                     | Qualitativo  | Nominal | Identidade de gênero do participante.                       |
| ('P1_f_1', 'Quantidade de oportunidades de emprego/vagas recebidas')    | Qualitativo  | Ordinal | Quantidade de oportunidades de emprego/vagas recebidas.     |
| ('P1_i ', 'Estado onde mora')                                           | Qualitativo  | Nominal | Estado onde o participante reside.                          |
| ('P2_f ', 'Cargo Atual')                                                | Qualitativo  | Nominal | Cargo atual do participante.                                |

---
# Árvore de decisão e Matriz de Confusão

![image](https://github.com/user-attachments/assets/2cd906e0-e074-4bb1-b25f-a93b005fe3a8)

![image](https://github.com/user-attachments/assets/d46c268e-5aed-47c9-abf4-62829f827344)

