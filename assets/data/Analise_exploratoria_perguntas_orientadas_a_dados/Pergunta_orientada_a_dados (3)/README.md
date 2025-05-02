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
  |Desenvolvedor/ Engenheiro de Software/ Analista de Sistemas	Desenvolvimento|
  |Data Product Manager/ Product Manager (PM/APM/DPM/GPM/PO)	Produto|
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

  
  #### 3.3.4. Preenchimento de valores ausentes de forma proporcional ou por estatística do grupo
  * Você deve ter percebido que os códigos citados acima apresentam algo a mais que só transformar dados qualitativos em quantitativos ou outras funções como a de agrupamento.
  Foram implementados nos códigos a tarefa de preencherem os dados faltantes proporcionalmente à frequência com que os dados reais aparecem.
  * Vamos analisar coluna por coluna:
  
  #### 3.3.5. Criação de uma nova feature: `Estou no trabalho ideal para mim?`

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
