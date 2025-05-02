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
  |  'P2_n'   |      Pretensão mudar emprego | Qualitativo |
  |  'P2_r'    |     Forma de trabalho | Qualitativo |
  |  'P2_s'     |     Forma de trabalho ideal | Qualitativo |
]
df_filtrada = df_original[features + ['P0']]
print(df_filtrada.head())
print(df_filtrada.shape)  # (5294, 10)
Explicação dos campos selecionados:

P1_a_1: Faixa de idade do colaborador

P1_b: Gênero

P2_f: Cargo atual

P2_g: Nível profissional

P2_h: Faixa salarial

P2_k: Satisfação com a empresa

P2_n: Pretensão de mudar de emprego (target)

P2_r: Forma de trabalho atual

P2_s: Forma de trabalho ideal

P0: Identificador único

2.3. Base Refinada e Transformações
Após a filtragem, realizamos uma série de limpezas e transformações para preparar os dados para a modelagem. As principais etapas foram:

Conversão de faixas para valores médios (idade, salário)

Agrupamento de cargos em categorias macro

Conversão de variáveis categóricas em numéricas (ordinal, binária ou one-hot)

Preenchimento de valores ausentes de forma proporcional ou por estatística do grupo

Criação de novas features (ex: estou_no_trabalho_ideal)

Binarização do target

Exemplo de código para transformação:

text
# Idade média
df_filtrada['Média_Idades'] = df_filtrada['P1_a_1'].apply(lambda x: ... )

# Agrupamento de cargos
df_filtrada['Cargo_Categoria'] = df_filtrada['P2_f'].map({...})

# Nível ordinal
df_filtrada['Nível_Ordinal'] = df_filtrada['P2_g'].map({'Júnior': 0, 'Pleno': 1, 'Sênior': 2})

# Salário médio
df_filtrada['Média_Faixa_Salarial'] = df_filtrada['P2_h'].map({...})

# Satisfação binária
df_filtrada['Satisfação_empresa'] = df_filtrada['P2_k'].apply(lambda x: 1 if x == 'Satisfeito' else 0)

# Target binário
df_filtrada['vai_sair'] = df_filtrada['P2_n'].apply(lambda x: 1 if x == 'Sim, estou em busca' else 0)

# Forma de trabalho one-hot e preenchimento de nulos
df_filtrada['Forma_Trabalho'] = df_filtrada['P2_r'].fillna('Remoto')

# Nova coluna: Estou no trabalho ideal
df_filtrada['Estou_no_trabalho_ideal'] = (df_filtrada['P2_r'] == df_filtrada['P2_s'])
Visualização da base refinada:

text
print(df_filtrada.head())
print(df_filtrada.shape)  # (n_linhas, n_colunas_final)
Resumo das principais transformações:

Coluna original	Transformação aplicada	Nova coluna/resultante
P1_a_1	Faixa -> valor médio	Média_Idades
P1_b	Remoção de valores "Outro" e "Prefiro não informar"	P1_b
P2_f	Agrupamento em categorias macro	Cargo_Categoria
P2_g	Ordinal + preenchimento proporcional de nulos	Nível_Ordinal
P2_h	Faixa -> valor médio + preenchimento de nulos	Média_Faixa_Salarial
P2_k	Binarização + preenchimento de nulos	Satisfação_empresa
P2_n	Binarização (target)	vai_sair
P2_r	One-hot + preenchimento de nulos	Forma_Trabalho
P2_s	Comparação com P2_r para nova feature	Estou_no_trabalho_ideal
Resumo visual do processo:

Base original: 5294 linhas, 550 colunas

Base filtrada: 5294 linhas, 10 colunas

Base refinada: 5294 linhas, ~10-13 colunas (após feature engineering)

Observações:

Todas as etapas foram documentadas e os códigos utilizados estão nos blocos acima.

Prints dos DataFrames em cada etapa podem ser inseridos para facilitar a visualização.

As transformações garantem que os dados estejam prontos para a modelagem preditiva.
