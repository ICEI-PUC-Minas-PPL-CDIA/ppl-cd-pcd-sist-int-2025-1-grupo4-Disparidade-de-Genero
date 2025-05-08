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

