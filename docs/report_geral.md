# Disparidade de Gênero no Setor da Tecnologia


**Pedro Lansdowne Oliveira, pedro.lansdowne@sga.pucminas.br**

**Leonardo Andrade Caetano Dornelas, lacdornelas@sga.pucminas.br**

**Augusto Henrique Gonçalves Valbonetti, ahgvalbonetti@sga.pucminas.br**

**Eduardo Fraga Fonseca Gomes, eduardo.fonseca@sga.pucminas.br**

**Vitor Martins Gonçalves, vitor.goncalves@sga.pucminas.br**

**Gustavo Bacellar Nunes Soares, gbnsoares@sga.pucminas.br**


---

Professores:

**Hugo Bastos de Paula**

**Hayala Nepomuceno Curto**

---

_Curso de Ciência de Dados, Unidade Praça da Liberdade_

_Instituto de Informática e Ciências Exatas – Pontifícia Universidade de Minas Gerais (PUC MINAS), Belo Horizonte – MG – Brasil_

---
### Índice do Trabalho

1.  [**Introdução**](#introdução)
    * [1.1. Contextualização](#contextualização)
    * [1.2. Problema](#problema)
    * [1.3. Objetivo Geral](#objetivo-geral)
        * [1.3.1. Objetivos Específicos](#objetivos-específicos)
    * [1.4. Justificativas](#justificativas)

2.  [**Público-Alvo**](#público-alvo)
    * [2.1. Personas](#personas)

3.  [**Análise Exploratória e Preparação dos Dados**](#análise-exploratória---disparidade-de-gênero-no-mercado-de-trabalho)
    * [3.1. Dicionário de Dados (Base Principal e Auxiliar)](#dicionário-de-dados)
    * [3.2. Preparação dos Dados](#preparação-dos-dados)
        * [3.2.1. Seleção dos Atributos](#seleção-dos-atributos)
        * [3.2.2. Tratamento dos Valores Faltantes ou Omissos](#tratamento-dos-valores-faltantes-ou-omissos)
        * [3.2.3. Tratamento dos Valores Inconsistentes](#tratamento-dos-valores-inconsistentes)
    * [3.3. Conversão de Dados](#conversão-de-dados-em-base_princ)
        * [3.3.1. Discretização (Binning)](#1-discretização-binning)
        * [3.3.2. Codificação por Rótulo (Label Encoding)](#2-codificação-por-rótulo-label-encoding)
        * [3.3.3. Codificação Fictícia (One-Hot Encoding)](#3-codificação-fictícia-one-hot-encoding)
    * [3.4. Dicionário de Dados da Base Modificada](#22-dicionário-de-dados-da-base-modificadapré-processada)
    * [3.5. Análise Descritiva dos Dados](#3-análise-descritiva-dos-dados-utilizando-estatísticas-de-primeira-ordem)

4.  [**Desenvolvimento e Análise dos Modelos**](#indução-de-modelos)
    * [4.1. Indução do Modelo 1: Árvore de Decisão](#modelo-1-árvore-de-decisão)
        * [4.1.1. Justificativa da Escolha do Modelo](#justificativa-da-escolha-do-modelo)
        * [4.1.2. Processo de Amostragem de Dados](#processo-de-amostragem-de-dados)
        * [4.1.3. Descrição dos Parâmetros Utilizados](#descrição-dos-parâmetros-utilizados)
        * [4.1.4. Fluxo de Processamento e Visualizações](#fluxo-de-processamento-e-visualizações)
    * [4.2. Resultados do Modelo 1 (Árvore de Decisão)](#resultados-obtidos-com-o-modelo-1-árvore-de-decisão)
        * [4.2.1. Avaliação no Conjunto de Treino](#avaliação-do-modelo-final-no-conjunto-de-treino)
        * [4.2.2. Avaliação no Conjunto de Teste](#avaliação-do-modelo-final-no-conjunto-de-teste)
        * [4.2.3. Análise de Overfitting](#acurácia-nos-conjuntos-de-treino-e-teste)
        * [4.2.4. Importância das Features e Interpretação Geral](#importância-das-features-na-árvore-de-decisão)
    * [4.3. Resultados do Modelo 2 (Random Forest)](#resultados-obtidos-com-o-modelo-2-random-forest)
    * [4.4. Análise Comparativa dos Modelos](#análise-comparativa-dos-modelos)

5.  [**Conclusão**](#8-conclusão)
    * [5.1. Resumo do Trabalho Desenvolvido](#breve-resumo-do-que-foi-desenvolvido)
    * [5.2. Apresentação dos Resultados (Vantagens e Desvantagens)](#apresentação-geral-dos-resultados-vantagens-e-desvantagens)
    * [5.3. Limitações e Possibilidades de Melhoria](#limitações-e-possibilidades-de-melhoria)

6.  [**Referências**](#referências)

7.  [**Apêndices**](#apêndices)
---

**Resumo**. 

Este estudo investiga a disparidade de gênero no setor da tecnologia no Brasil, analisando os desafios enfrentados pelas mulheres. A pesquisa utiliza dados do State of Data Brazil 2023 para identificar diferenças na participação, salários e oportunidades de crescimento entre homens e mulheres no mercado de trabalho de dados. Um dos objetivos será  fornecer dados e insights que possam embasar políticas de inclusão, contribuindo para um mercado de trabalho mais diverso e inovador.

---


## Introdução

  É notório que o pensamento, tanto feminino quanto masculino, apresenta-se extremamente válido para o avanço tecnológico, inclusive no Setor da tecnologia no Brasil. Entretanto, tal realidade apresenta-se desvirtuada e validada por uma análise descritiva que pode ser realizada ao observar o banco de dados servindo como referência para esta pesquisa. Através de uma análise descritiva, esse estudo busca, primeiramente, validar tal infeliz realidade da disparidade (em todas as suas vertentes) de gênero no Setor da tecnologia no Brasil e então, propor alternativas válidas para a promoção da inclusão de gênero equalitária nesse nicho.  
  
  As causas que podem ser inferidas para esse desafio são várias e serão abordadas abaixo. Dentre elas, observa-se o imaginário social enraizado de que mulheres não são tão ábeis em tecnologia quanto os homens, além haver uma ausência de representatividade feminina nesse nicho, fora a dupla-jornada de trabalho que,normalmente, mulheres enfrentam, limitando ainda mais sua capacidade de cresimento, contribuição e evolução nesse ramo.  

  Essa pesquisa é importante uma vez que, com sua validação e correta execução, mais mulheres poderão ter lugar e espaço no Setor da tecnologia no Brasil. Com isso, além de fornecer mais rotatividade de empregos no mercado, mais vidas serão positivamente contribuídas pelo trabalho, com o incentivo, mesmo que sutil, a mais mulheres ingressando nesse ramo, sem haver disparidades, desigualdades ou destratamentos, haverão mais mentes pensantes dentro desse mercado, contribuindo para mais avanços científicos úteis para o mundo e o futuro, os quais podem estar sendo retardados pela presença de desvalorização da força feminina dentro desse mercado, tema pelo qual abordaremos com mais detalhes a seguir.

###    Contextualização

A área de ciência de dados cresce a passos largos, movimentando bilhões e influenciando decisões no mundo todo. Mas, quando olhamos para quem está por trás dessas análises e algoritmos, percebemos uma realidade preocupante: a disparidade de gênero ainda é grande. As mulheres continuam sub-representadas no setor, enfrentando barreiras que vão desde a entrada no mercado até a progressão na carreira.
Os números refletem essa realidade. Pesquisas mostram que a presença feminina na ciência de dados ainda é muito menor do que a masculina, e as chances de ocupar cargos de liderança são ainda mais reduzidas. Entender essa disparidade e buscar soluções para torná-la coisa do passado não é apenas uma questão de justiça – é também uma maneira de tornar o setor mais diverso, inovador e eficiente.

###    Problema

No Brasil, as mulheres que trabalham em setores da Tecnologia são prejudicadas por haver, intrinsicamente, uma disparidade de gênero em seu setor laboral. Tal problema ocorre por um viés social, por exemplo, por meio de esteriótipos sobre empregos ou, também, por um viés econômico, em que as mulheres perdem oportunidades de empregos ou de salários melhores para homens.
Dito isso, observa-se uma notória discrepância de gênero em um mercado de trabalho na área da computação.



###    Objetivo geral

 Desenvolver um sistema inteligente para classificar se a pessoa vai estar empregada ou desempregada conforme o gênero e a região onde ela mora.


####    Objetivos específicos

1- Analisar a distribuição de gênero entre os profissionais do setor de tecnologia

2-Comparar os salários médios entre homens e mulheres no setor de dados

3- Comparar as oportunidades de crescimento entre homens e mulheres no setor de dados

4- Identificar os principais desafios enfrentados por mulheres no setor de dados

5- Comparar a representatividade feminina em cargos de liderança no setor de dados

6- Examinar a relação entre nível de escolaridade e empregabilidade de mulheres no setor

7- Estudar a presença de viés de gênero nos processos seletivos do setor de tecnologia



###    Justificativas

A razão pela a escolha do tema Disparidade de gênero no setor de T.I vem da necessidade de apoiar a igualdade entre gêneros no mercado de dados, 
um lugar que ainda mostra diferenças grandes entre homens e mulheres. Ao olharmos para a diferença por gênero, 
tentamos achar as causas dessas desigualdades e dar números que podem ajudar políticas e ações de inclusão. 



##    Público alvo

O nosso público-alvo são gerentes de empresa que buscam uma menor disparidade de mulheres nos diversos setores da tecnologia, como gerentes de RH e chefes de setor de tecnologia.
Temos como público alvo diretores e coordenadores de instiruições de ensino da área, ja que podemos observar uma grande falta de mulheres nos cursos da área. Além de estudantes que buscam se graduar na área de tecnologia.

###  Personas

1️⃣ Persona: Desenvolvedora Plena em Tecnologia

- Nome: Carla Nunes

- Idade: 29 anos

- Objetivo: Entender se está sendo remunerada de forma justa em comparação aos colegas homens com funções similares.

- Desafios: Dificuldade em acessar dados transparentes e atualizados sobre salários com recorte de gênero.

2️⃣ Persona: Coordenadora de Diversidade e Inclusão

- Nome: Priscila Duarte

- Idade: 35 anos

- Objetivo: Desenvolver políticas internas que reduzam a desigualdade salarial de gênero.

- Desafios: Falta de indicadores específicos sobre mulheres em cargos técnicos e de liderança na empresa.

3️⃣ Persona: Engenheiro de Software Sênior

- Nome: Rafael Lima

- Idade: 41 anos

- Objetivo: Apoiar iniciativas de equidade de gênero no setor, incluindo revisão salarial.

- Desafios: Não tem acesso a comparativos salariais por gênero que possam embasar ações efetivas.

4️⃣ Persona: Consultora de Igualdade de Gênero em ONGs

- Nome: Sônia Ferreira

- Idade: 47 anos

- Objetivo: Promover ações públicas e privadas que eliminem a diferença salarial entre homens e mulheres na tecnologia.

- Desafios: Precisa de estudos aprofundados com dados desagregados por cargo, gênero, região e senioridade.


# Análise Exploratória - Disparidade de Gênero no Mercado de Trabalho

**Hipótese**: Investigar como a disparidade de gênero interfere na situação atual de trabalho conforme a região onde a pessoa mora.

---

###    Dicionário de dados

## Análise de Dados da Pesquisa State of Data BR 2023

## 1. Base de Dados Principal

* **Fonte:** Arquivo CSV 'State_of_data_BR_2023_Kaggle - df_survey_2023.csv' (processado no notebook).
* **Descrição:** Esta base de dados contém informações sobre profissionais e estudantes da área de dados no Brasil em 2023. Os dados foram processados para facilitar a análise, incluindo a seleção de colunas relevantes e a codificação de variáveis categóricas.

## 2. Dicionário de Dados da Base Principal

| Atributo | Descrição | Tipo |
|---|---|---|
| P1_a_Idade | Idade do respondente | Inteiro |
| P1_b_Genero | Gênero do respondente | Textual |
| P1_c_Cor_raca | Cor ou raça autodeclarada pelo respondente | Textual |
| P1_d_PCD | Indica se o respondente é uma pessoa com deficiência | Textual |
| P1_e_experiencia_profissional | Tempo de experiência profissional na área de dados | Textual |
| P1_f_estado_onde_nasceu | Estado de nascimento do respondente | Textual |
| P1_g_estado_onde_mora | Estado de residência atual do respondente | Textual |
| P1_h_possui_graduacao | Indica se o respondente possui diploma de graduação | Textual |
| P2_a_formacao_academica | Nível mais alto de formação acadêmica | Textual |
| P2_b_area_formacao | Área de formação principal do respondente | Textual |
| P2_c_foi_influenciado_a_entrar_na_area_de_dados | Nota de influência para entrar na área de dados | Inteiro |
| P2_e_se_considera_data_literate | Nota de autoavaliação de alfabetização em dados | Inteiro |
| P2_f_nivel_ingles | Nível de proficiência em inglês | Textual |
| P3_a_situacao_trabalho_atual | Situação de trabalho atual na área de dados | Textual |
| P4_a_cargo_atual | Cargo atual ou mais recente do respondente | Textual |
| P4_b_escolaridade_recomendada_para_cargo | Escolaridade recomendada para o cargo atual | Textual |
| P4_c_faixa_salarial | Faixa salarial mensal em Reais (R$) | Textual |
| P4_d_media_salario_area | Percepção do salário em relação à média da área | Inteiro |
| P4_e_pretensao_salarial_proximos_2_anos | Pretensão salarial para os próximos 2 anos | Textual |
| P4_f_setor_empresa | Setor de atuação da empresa | Textual |
| P4_g_tamanho_empresa | Porte da empresa onde trabalha | Textual |
| P4_h_regiao_empresa | Região da empresa | Textual |
| P4_i_modelo_trabalho | Modelo de trabalho (Presencial, Híbrido, Remoto) | Textual |
| P4_j_ambiente_trabalho_preferido | Preferência de ambiente de trabalho | Textual |
| P4_l_tipo_contrato_trabalho | Tipo de contrato de trabalho (CLT, PJ, etc.) | Textual |
| P4_m_nivel_satisfacao_trabalho | Nível de satisfação com o trabalho atual | Inteiro |
| P5_b_investe_em_educacao_continuada | Resposta sobre o investimento em educação continuada | Textual |
| P5_c_horas_estudo_semanais | Horas de estudo dedicadas à área de dados por semana | Inteiro |
| P6_a_preocupacao_ia_substituir_trabalho | Nível de preocupação sobre IA substituir seu trabalho | Inteiro |
| P6_b_entendimento_ia_generativa | Nível de entendimento sobre IA Generativa | Inteiro |
| P6_c_uso_ia_generativa_trabalho | Indica se utiliza IA Generativa no trabalho | Textual |
| P6_e_opiniao_regulamentacao_ia | Opinião sobre a regulamentação do uso de IA | Textual |
| P1_i_tipo_graduacao_Bacharelado | Resposta binária (0/1) para a opção 'Bacharelado' na pergunta 'Tipo de Graduação' | Inteiro |
| P1_i_tipo_graduacao_Licenciatura | Resposta binária (0/1) para a opção 'Licenciatura' na pergunta 'Tipo de Graduação' | Inteiro |
| P1_i_tipo_graduacao_Tecnólogo | Resposta binária (0/1) para a opção 'Tecnólogo' na pergunta 'Tipo de Graduação' | Inteiro |
| P1_i_tipo_graduacao_Pós-graduação | Resposta binária (0/1) para a opção 'Pós-graduação' na pergunta 'Tipo de Graduação' | Inteiro |
| P1_i_tipo_graduacao_Mestrado | Resposta binária (0/1) para a opção 'Mestrado' na pergunta 'Tipo de Graduação' | Inteiro |
| P1_i_tipo_graduacao_Doutorado | Resposta binária (0/1) para a opção 'Doutorado' na pergunta 'Tipo de Graduação' | Inteiro |
| P1_i_tipo_graduacao_Não conclui a graduação | Resposta binária (0/1) para a opção 'Não concluí a graduação' na pergunta 'Tipo de Graduação' | Inteiro |
| P1_i_tipo_graduacao_Outro | Resposta binária (0/1) para a opção 'Outro' na pergunta 'Tipo de Graduação' | Inteiro |
| P2_d_motivacao_area_dados_Gosto de programação | Resposta binária (0/1) para a opção 'Gosto de programação' na pergunta 'Motivação para entrar na área' | Inteiro |
| P2_d_motivacao_area_dados_Gosto de matemática e estatística | Resposta binária (0/1) para a opção 'Gosto de matemática e estatística' na pergunta 'Motivação para entrar na área' | Inteiro |
| P2_d_motivacao_area_dados_Estou fazendo uma transição de carreira | Resposta binária (0/1) para a opção 'Estou fazendo uma transição de carreira' na pergunta 'Motivação para entrar na área' | Inteiro |
| P2_d_motivacao_area_dados_Oportunidade de trabalhar remotamente | Resposta binária (0/1) para a opção 'Oportunidade de trabalhar remotamente' na pergunta 'Motivação para entrar na área' | Inteiro |
| P2_d_motivacao_area_dados_Área com boas oportunidades de crescimento | Resposta binária (0/1) para a opção 'Área com boas oportunidades de crescimento' na pergunta 'Motivação para entrar na área' | Inteiro |
| P2_d_motivacao_area_dados_Bons salários | Resposta binária (0/1) para a opção 'Bons salários' na pergunta 'Motivação para entrar na área' | Inteiro |
| P2_d_motivacao_area_dados_Sou novo no mercado de trabalho | Resposta binária (0/1) para a opção 'Sou novo no mercado de trabalho' na pergunta 'Motivação para entrar na área' | Inteiro |
| P2_d_motivacao_area_dados_Já trabalhava com dados | Resposta binária (0/1) para a opção 'Já trabalhava com dados' na pergunta 'Motivação para entrar na área' | Inteiro |
| P2_d_motivacao_area_dados_Outra motivação | Resposta binária (0/1) para a opção 'Outra motivação' na pergunta 'Motivação para entrar na área' | Inteiro |
| P3_b_principal_linguagem_programacao_Python | Resposta binária (0/1) para a opção 'Python' na pergunta 'Principal linguagem de programação' | Inteiro |
| P3_b_principal_linguagem_programacao_R | Resposta binária (0/1) para a opção 'R' na pergunta 'Principal linguagem de programação' | Inteiro |
| P3_b_principal_linguagem_programacao_SQL | Resposta binária (0/1) para a opção 'SQL' na pergunta 'Principal linguagem de programação' | Inteiro |
| P3_b_principal_linguagem_programacao_VBA | Resposta binária (0/1) para a opção 'VBA' na pergunta 'Principal linguagem de programação' | Inteiro |
| P3_b_principal_linguagem_programacao_SAS/Stata | Resposta binária (0/1) para a opção 'SAS/Stata' na pergunta 'Principal linguagem de programação' | Inteiro |
| P3_b_principal_linguagem_programacao_Java | Resposta binária (0/1) para a opção 'Java' na pergunta 'Principal linguagem de programação' | Inteiro |
| P3_b_principal_linguagem_programacao_C/C++/C# | Resposta binária (0/1) para a opção 'C/C++/C#' na pergunta 'Principal linguagem de programação' | Inteiro |
| P3_b_principal_linguagem_programacao_Javascript/Typescript | Resposta binária (0/1) para a opção 'Javascript/Typescript' na pergunta 'Principal linguagem de programação' | Inteiro |
| P3_b_principal_linguagem_programacao_PHP | Resposta binária (0/1) para a opção 'PHP' na pergunta 'Principal linguagem de programação' | Inteiro |
| P3_b_principal_linguagem_programacao_Não utilizo nenhuma linguagem | Resposta binária (0/1) para a opção 'Não utilizo nenhuma linguagem' na pergunta 'Principal linguagem de programação' | Inteiro |
| P3_b_principal_linguagem_programacao_Outra | Resposta binária (0/1) para a opção 'Outra' na pergunta 'Principal linguagem de programação' | Inteiro |
| P3_c_linguagens_de_programacao_mais_usadas_Python | Resposta binária (0/1) para a opção 'Python' na pergunta 'Linguagens mais usadas' | Inteiro |
| P3_c_linguagens_de_programacao_mais_usadas_R | Resposta binária (0/1) para a opção 'R' na pergunta 'Linguagens mais usadas' | Inteiro |
| P3_c_linguagens_de_programacao_mais_usadas_SQL | Resposta binária (0/1) para a opção 'SQL' na pergunta 'Linguagens mais usadas' | Inteiro |
| P3_c_linguagens_de_programacao_mais_usadas_VBA | Resposta binária (0/1) para a opção 'VBA' na pergunta 'Linguagens mais usadas' | Inteiro |
| P3_c_linguagens_de_programacao_mais_usadas_SAS/Stata | Resposta binária (0/1) para a opção 'SAS/Stata' na pergunta 'Linguagens mais usadas' | Inteiro |
| P3_c_linguagens_de_programacao_mais_usadas_Java | Resposta binária (0/1) para a opção 'Java' na pergunta 'Linguagens mais usadas' | Inteiro |
| P3_c_linguagens_de_programacao_mais_usadas_C/C++/C# | Resposta binária (0/1) para a opção 'C/C++/C#' na pergunta 'Linguagens mais usadas' | Inteiro |
| P3_c_linguagens_de_programacao_mais_usadas_Javascript/Typescript | Resposta binária (0/1) para a opção 'Javascript/Typescript' na pergunta 'Linguagens mais usadas' | Inteiro |
| P3_c_linguagens_de_programacao_mais_usadas_PHP | Resposta binária (0/1) para a opção 'PHP' na pergunta 'Linguagens mais usadas' | Inteiro |
| P3_c_linguagens_de_programacao_mais_usadas_Não utilizo nenhuma linguagem | Resposta binária (0/1) para a opção 'Não utilizo nenhuma linguagem' na pergunta 'Linguagens mais usadas' | Inteiro |
| P3_c_linguagens_de_programacao_mais_usadas_Outra | Resposta binária (0/1) para a opção 'Outra' na pergunta 'Linguagens mais usadas' | Inteiro |
| P3_d_ferramentas_bi_mais_usadas_Power BI | Resposta binária (0/1) para a opção 'Power BI' na pergunta 'Ferramentas de BI' | Inteiro |
| P3_d_ferramentas_bi_mais_usadas_Tableau | Resposta binária (0/1) para a opção 'Tableau' na pergunta 'Ferramentas de BI' | Inteiro |
| P3_d_ferramentas_bi_mais_usadas_Qlik Sense/Qlik View | Resposta binária (0/1) para a opção 'Qlik' na pergunta 'Ferramentas de BI' | Inteiro |
| P3_d_ferramentas_bi_mais_usadas_Looker | Resposta binária (0/1) para a opção 'Looker' na pergunta 'Ferramentas de BI' | Inteiro |
| P3_d_ferramentas_bi_mais_usadas_Microstrategy | Resposta binária (0/1) para a opção 'Microstrategy' na pergunta 'Ferramentas de BI' | Inteiro |
| P3_d_ferramentas_bi_mais_usadas_Metabase | Resposta binária (0/1) para a opção 'Metabase' na pergunta 'Ferramentas de BI' | Inteiro |
| P3_d_ferramentas_bi_mais_usadas_Superset | Resposta binária (0/1) para a opção 'Superset' na pergunta 'Ferramentas de BI' | Inteiro |
| P3_d_ferramentas_bi_mais_usadas_Redash | Resposta binária (0/1) para a opção 'Redash' na pergunta 'Ferramentas de BI' | Inteiro |
| P3_d_ferramentas_bi_mais_usadas_SAS Visual Analytics | Resposta binária (0/1) para a opção 'SAS VA' na pergunta 'Ferramentas de BI' | Inteiro |
| P3_d_ferramentas_bi_mais_usadas_Pentaho | Resposta binária (0/1) para a opção 'Pentaho' na pergunta 'Ferramentas de BI' | Inteiro |
| P3_d_ferramentas_bi_mais_usadas_Excel | Resposta binária (0/1) para a opção 'Excel' na pergunta 'Ferramentas de BI' | Inteiro |
| P3_d_ferramentas_bi_mais_usadas_Não utilizo ferramentas de BI | Resposta binária (0/1) para a opção 'Não utilizo' na pergunta 'Ferramentas de BI' | Inteiro |
| P3_d_ferramentas_bi_mais_usadas_Outra | Resposta binária (0/1) para a opção 'Outra' na pergunta 'Ferramentas de BI' | Inteiro |
| P3_e_plataformas_nuvem_mais_usadas_Amazon Web Services (AWS) | Resposta binária (0/1) para a opção 'AWS' na pergunta 'Plataformas de Nuvem' | Inteiro |
| P3_e_plataformas_nuvem_mais_usadas_Google Cloud (GCP) | Resposta binária (0/1) para a opção 'GCP' na pergunta 'Plataformas de Nuvem' | Inteiro |
| P3_e_plataformas_nuvem_mais_usadas_Microsoft Azure | Resposta binária (0/1) para a opção 'Azure' na pergunta 'Plataformas de Nuvem' | Inteiro |
| P3_e_plataformas_nuvem_mais_usadas_Oracle | Resposta binária (0/1) para a opção 'Oracle' na pergunta 'Plataformas de Nuvem' | Inteiro |
| P3_e_plataformas_nuvem_mais_usadas_IBM | Resposta binária (0/1) para a opção 'IBM' na pergunta 'Plataformas de Nuvem' | Inteiro |
| P3_e_plataformas_nuvem_mais_usadas_Hadoop | Resposta binária (0/1) para a opção 'Hadoop' na pergunta 'Plataformas de Nuvem' | Inteiro |
| P3_e_plataformas_nuvem_mais_usadas_Cloudera | Resposta binária (0/1) para a opção 'Cloudera' na pergunta 'Plataformas de Nuvem' | Inteiro |
| P3_e_plataformas_nuvem_mais_usadas_Databricks | Resposta binária (0/1) para a opção 'Databricks' na pergunta 'Plataformas de Nuvem' | Inteiro |
| P3_e_plataformas_nuvem_mais_usadas_Snowflake | Resposta binária (0/1) para a opção 'Snowflake' na pergunta 'Plataformas de Nuvem' | Inteiro |
| P3_e_plataformas_nuvem_mais_usadas_Não utilizo nenhuma | Resposta binária (0/1) para a opção 'Não utilizo' na pergunta 'Plataformas de Nuvem' | Inteiro |
| P3_e_plataformas_nuvem_mais_usadas_Outra | Resposta binária (0/1) para a opção 'Outra' na pergunta 'Plataformas de Nuvem' | Inteiro |
| P3_f_ferramentas_etl_mais_usadas_Apache Airflow | Resposta binária (0/1) para a opção 'Apache Airflow' na pergunta 'Ferramentas de ETL' | Inteiro |
| P3_f_ferramentas_etl_mais_usadas_AWS Glue | Resposta binária (0/1) para a opção 'AWS Glue' na pergunta 'Ferramentas de ETL' | Inteiro |
| P3_f_ferramentas_etl_mais_usadas_Google Dataflow | Resposta binária (0/1) para a opção 'Google Dataflow' na pergunta 'Ferramentas de ETL' | Inteiro |
| P3_f_ferramentas_etl_mais_usadas_Azure Data Factory | Resposta binária (0/1) para a opção 'Azure Data Factory' na pergunta 'Ferramentas de ETL' | Inteiro |
| P3_f_ferramentas_etl_mais_usadas_IBM DataStage | Resposta binária (0/1) para a opção 'IBM DataStage' na pergunta 'Ferramentas de ETL' | Inteiro |
| P3_f_ferramentas_etl_mais_usadas_Oracle Data Integrator | Resposta binária (0/1) para a opção 'Oracle Data Integrator' na pergunta 'Ferramentas de ETL' | Inteiro |
| P3_f_ferramentas_etl_mais_usadas_Talend | Resposta binária (0/1) para a opção 'Talend' na pergunta 'Ferramentas de ETL' | Inteiro |
| P3_f_ferramentas_etl_mais_usadas_SAP | Resposta binária (0/1) para a opção 'SAP' na pergunta 'Ferramentas de ETL' | Inteiro |
| P3_f_ferramentas_etl_mais_usadas_Pentaho | Resposta binária (0/1) para a opção 'Pentaho' na pergunta 'Ferramentas de ETL' | Inteiro |
| P3_f_ferramentas_etl_mais_usadas_Alteryx | Resposta binária (0/1) para a opção 'Alteryx' na pergunta 'Ferramentas de ETL' | Inteiro |
| P3_f_ferramentas_etl_mais_usadas_dbt | Resposta binária (0/1) para a opção 'dbt' na pergunta 'Ferramentas de ETL' | Inteiro |
| P3_f_ferramentas_etl_mais_usadas_Não utilizo nenhuma | Resposta binária (0/1) para a opção 'Não utilizo' na pergunta 'Ferramentas de ETL' | Inteiro |
| P3_f_ferramentas_etl_mais_usadas_Outra | Resposta binária (0/1) para a opção 'Outra' na pergunta 'Ferramentas de ETL' | Inteiro |
| P3_g_ferramentas_de_modelagem_de_dados_mais_usadas_SQL | Resposta binária (0/1) para a opção 'SQL' na pergunta 'Ferramentas de Modelagem' | Inteiro |
| P3_g_ferramentas_de_modelagem_de_dados_mais_usadas_Python | Resposta binária (0/1) para a opção 'Python' na pergunta 'Ferramentas de Modelagem' | Inteiro |
| P3_g_ferramentas_de_modelagem_de_dados_mais_usadas_R | Resposta binária (0/1) para a opção 'R' na pergunta 'Ferramentas de Modelagem' | Inteiro |
| P3_g_ferramentas_de_modelagem_de_dados_mais_usadas_SAS/Stata | Resposta binária (0/1) para a opção 'SAS/Stata' na pergunta 'Ferramentas de Modelagem' | Inteiro |
| P3_g_ferramentas_de_modelagem_de_dados_mais_usadas_Excel/Google Sheets | Resposta binária (0/1) para a opção 'Excel/Sheets' na pergunta 'Ferramentas de Modelagem' | Inteiro |
| P3_g_ferramentas_de_modelagem_de_dados_mais_usadas_MATLAB | Resposta binária (0/1) para a opção 'MATLAB' na pergunta 'Ferramentas de Modelagem' | Inteiro |
| P3_g_ferramentas_de_modelagem_de_dados_mais_usadas_SPSS | Resposta binária (0/1) para a opção 'SPSS' na pergunta 'Ferramentas de Modelagem' | Inteiro |
| P3_g_ferramentas_de_modelagem_de_dados_mais_usadas_Knime | Resposta binária (0/1) para a opção 'Knime' na pergunta 'Ferramentas de Modelagem' | Inteiro |
| P3_g_ferramentas_de_modelagem_de_dados_mais_usadas_Alteryx | Resposta binária (0/1) para a opção 'Alteryx' na pergunta 'Ferramentas de Modelagem' | Inteiro |
| P3_g_ferramentas_de_modelagem_de_dados_mais_usadas_Não utilizo nenhuma | Resposta binária (0/1) para a opção 'Não utilizo' na pergunta 'Ferramentas de Modelagem' | Inteiro |
| P3_g_ferramentas_de_modelagem_de_dados_mais_usadas_Outra | Resposta binária (0/1) para a opção 'Outra' na pergunta 'Ferramentas de Modelagem' | Inteiro |
| P3_h_banco_de_dados_mais_usados_MySQL | Resposta binária (0/1) para a opção 'MySQL' na pergunta 'Bancos de Dados' | Inteiro |
| P3_h_banco_de_dados_mais_usados_PostgreSQL | Resposta binária (0/1) para a opção 'PostgreSQL' na pergunta 'Bancos de Dados' | Inteiro |
| P3_h_banco_de_dados_mais_usados_Microsoft SQL Server | Resposta binária (0/1) para a opção 'SQL Server' na pergunta 'Bancos de Dados' | Inteiro |
| P3_h_banco_de_dados_mais_usados_Oracle Database | Resposta binária (0/1) para a opção 'Oracle' na pergunta 'Bancos de Dados' | Inteiro |
| P3_h_banco_de_dados_mais_usados_IBM DB2 | Resposta binária (0/1) para a opção 'DB2' na pergunta 'Bancos de Dados' | Inteiro |
| P3_h_banco_de_dados_mais_usados_SAP HANA | Resposta binária (0/1) para a opção 'SAP HANA' na pergunta 'Bancos de Dados' | Inteiro |
| P3_h_banco_de_dados_mais_usados_Amazon Redshift | Resposta binária (0/1) para a opção 'Redshift' na pergunta 'Bancos de Dados' | Inteiro |
| P3_h_banco_de_dados_mais_usados_Google BigQuery | Resposta binária (0/1) para a opção 'BigQuery' na pergunta 'Bancos de Dados' | Inteiro |
| P3_h_banco_de_dados_mais_usados_Apache Hive | Resposta binária (0/1) para a opção 'Hive' na pergunta 'Bancos de Dados' | Inteiro |
| P3_h_banco_de_dados_mais_usados_MongoDB | Resposta binária (0/1) para a opção 'MongoDB' na pergunta 'Bancos de Dados' | Inteiro |
| P3_h_banco_de_dados_mais_usados_Cassandra | Resposta binária (0/1) para a opção 'Cassandra' na pergunta 'Bancos de Dados' | Inteiro |
| P3_h_banco_de_dados_mais_usados_Elasticsearch | Resposta binária (0/1) para a opção 'Elasticsearch' na pergunta 'Bancos de Dados' | Inteiro |
| P3_h_banco_de_dados_mais_usados_Databricks/Delta Lake | Resposta binária (0/1) para a opção 'Databricks' na pergunta 'Bancos de Dados' | Inteiro |
| P3_h_banco_de_dados_mais_usados_Snowflake | Resposta binária (0/1) para a opção 'Snowflake' na pergunta 'Bancos de Dados' | Inteiro |
| P3_h_banco_de_dados_mais_usados_Não utilizo nenhum | Resposta binária (0/1) para a opção 'Não utilizo' na pergunta 'Bancos de Dados' | Inteiro |
| P3_h_banco_de_dados_mais_usados_Outro | Resposta binária (0/1) para a opção 'Outro' na pergunta 'Bancos de Dados' | Inteiro |
| P3_i_plataformas_de_big_data_mais_usadas_Hadoop | Resposta binária (0/1) para a opção 'Hadoop' na pergunta 'Plataformas de Big Data' | Inteiro |
| P3_i_plataformas_de_big_data_mais_usadas_Cloudera | Resposta binária (0/1) para a opção 'Cloudera' na pergunta 'Plataformas de Big Data' | Inteiro |
| P3_i_plataformas_de_big_data_mais_usadas_Databricks | Resposta binária (0/1) para a opção 'Databricks' na pergunta 'Plataformas de Big Data' | Inteiro |
| P3_i_plataformas_de_big_data_mais_usadas_Amazon EMR | Resposta binária (0/1) para a opção 'Amazon EMR' na pergunta 'Plataformas de Big Data' | Inteiro |
| P3_i_plataformas_de_big_data_mais_usadas_Google Dataproc | Resposta binária (0/1) para a opção 'Google Dataproc' na pergunta 'Plataformas de Big Data' | Inteiro |
| P3_i_plataformas_de_big_data_mais_usadas_Azure HDInsight | Resposta binária (0/1) para a opção 'Azure HDInsight' na pergunta 'Plataformas de Big Data' | Inteiro |
| P3_i_plataformas_de_big_data_mais_usadas_Apache Spark | Resposta binária (0/1) para a opção 'Apache Spark' na pergunta 'Plataformas de Big Data' | Inteiro |
| P3_i_plataformas_de_big_data_mais_usadas_Apache Flink | Resposta binária (0/1) para a opção 'Apache Flink' na pergunta 'Plataformas de Big Data' | Inteiro |
| P3_i_plataformas_de_big_data_mais_usadas_Apache Kafka | Resposta binária (0/1) para a opção 'Apache Kafka' na pergunta 'Plataformas de Big Data' | Inteiro |
| P3_i_plataformas_de_big_data_mais_usadas_MongoDB | Resposta binária (0/1) para a opção 'MongoDB' na pergunta 'Plataformas de Big Data' | Inteiro |
| P3_i_plataformas_de_big_data_mais_usadas_Cassandra | Resposta binária (0/1) para a opção 'Cassandra' na pergunta 'Plataformas de Big Data' | Inteiro |
| P3_i_plataformas_de_big_data_mais_usadas_Elasticsearch | Resposta binária (0/1) para a opção 'Elasticsearch' na pergunta 'Plataformas de Big Data' | Inteiro |
| P3_i_plataformas_de_big_data_mais_usadas_Não utilizo nenhuma | Resposta binária (0/1) para a opção 'Não utilizo' na pergunta 'Plataformas de Big Data' | Inteiro |
| P3_i_plataformas_de_big_data_mais_usadas_Outra | Resposta binária (0/1) para a opção 'Outra' na pergunta 'Plataformas de Big Data' | Inteiro |
| P3_j_bibliotecas_de_ia_mais_usadas_Scikit-learn | Resposta binária (0/1) para a opção 'Scikit-learn' na pergunta 'Bibliotecas de IA' | Inteiro |
| P3_j_bibliotecas_de_ia_mais_usadas_TensorFlow | Resposta binária (0/1) para a opção 'TensorFlow' na pergunta 'Bibliotecas de IA' | Inteiro |
| P3_j_bibliotecas_de_ia_mais_usadas_PyTorch | Resposta binária (0/1) para a opção 'PyTorch' na pergunta 'Bibliotecas de IA' | Inteiro |
| P3_j_bibliotecas_de_ia_mais_usadas_Keras | Resposta binária (0/1) para a opção 'Keras' na pergunta 'Bibliotecas de IA' | Inteiro |
| P3_j_bibliotecas_de_ia_mais_usadas_XGBoost | Resposta binária (0/1) para a opção 'XGBoost' na pergunta 'Bibliotecas de IA' | Inteiro |
| P3_j_bibliotecas_de_ia_mais_usadas_LightGBM | Resposta binária (0/1) para a opção 'LightGBM' na pergunta 'Bibliotecas de IA' | Inteiro |
| P3_j_bibliotecas_de_ia_mais_usadas_FastAI | Resposta binária (0/1) para a opção 'FastAI' na pergunta 'Bibliotecas de IA' | Inteiro |
| P3_j_bibliotecas_de_ia_mais_usadas_Spacy | Resposta binária (0/1) para a opção 'Spacy' na pergunta 'Bibliotecas de IA' | Inteiro |
| P3_j_bibliotecas_de_ia_mais_usadas_NLTK | Resposta binária (0/1) para a opção 'NLTK' na pergunta 'Bibliotecas de IA' | Inteiro |
| P3_j_bibliotecas_de_ia_mais_usadas_HuggingFace | Resposta binária (0/1) para a opção 'HuggingFace' na pergunta 'Bibliotecas de IA' | Inteiro |
| P3_j_bibliotecas_de_ia_mais_usadas_MLflow | Resposta binária (0/1) para a opção 'MLflow' na pergunta 'Bibliotecas de IA' | Inteiro |
| P3_j_bibliotecas_de_ia_mais_usadas_Não utilizo nenhuma | Resposta binária (0/1) para a opção 'Não utilizo' na pergunta 'Bibliotecas de IA' | Inteiro |
| P3_j_bibliotecas_de_ia_mais_usadas_Outra | Resposta binária (0/1) para a opção 'Outra' na pergunta 'Bibliotecas de IA' | Inteiro |
| P4_k_prioridade_proxima_oportunidade_Aprender novas ferramentas e tecnologias | Resposta binária (0/1) para a opção 'Aprender novas ferramentas' na pergunta 'Prioridade próxima oportunidade' | Inteiro |
| P4_k_prioridade_proxima_oportunidade_Mais desafios e responsabilidades | Resposta binária (0/1) para a opção 'Mais desafios' na pergunta 'Prioridade próxima oportunidade' | Inteiro |
| P4_k_prioridade_proxima_oportunidade_Melhor equilíbrio entre vida pessoal e profissional | Resposta binária (0/1) para a opção 'Melhor equilíbrio' na pergunta 'Prioridade próxima oportunidade' | Inteiro |
| P4_k_prioridade_proxima_oportunidade_Mudar de área de atuação | Resposta binária (0/1) para a opção 'Mudar de área' na pergunta 'Prioridade próxima oportunidade' | Inteiro |
| P4_k_prioridade_proxima_oportunidade_Oportunidade de liderar pessoas | Resposta binária (0/1) para a opção 'Oportunidade de liderar' na pergunta 'Prioridade próxima oportunidade' | Inteiro |
| P4_k_prioridade_proxima_oportunidade_Oportunidade de trabalhar em outra empresa | Resposta binária (0/1) para a opção 'Trabalhar em outra empresa' na pergunta 'Prioridade próxima oportunidade' | Inteiro |
| P4_k_prioridade_proxima_oportunidade_Salário mais alto | Resposta binária (0/1) para a opção 'Salário mais alto' na pergunta 'Prioridade próxima oportunidade' | Inteiro |
| P4_k_prioridade_proxima_oportunidade_Trabalhar remotamente | Resposta binária (0/1) para a opção 'Trabalhar remotamente' na pergunta 'Prioridade próxima oportunidade' | Inteiro |
| P4_k_prioridade_proxima_oportunidade_Outra | Resposta binária (0/1) para a opção 'Outra' na pergunta 'Prioridade próxima oportunidade' | Inteiro |
| P4_n_recebe_beneficios_Vale-alimentação | Resposta binária (0/1) para a opção 'Vale-alimentação' na pergunta 'Benefícios recebidos' | Inteiro |
| P4_n_recebe_beneficios_Vale-refeição | Resposta binária (0/1) para a opção 'Vale-refeição' na pergunta 'Benefícios recebidos' | Inteiro |
| P4_n_recebe_beneficios_Plano de saúde | Resposta binária (0/1) para a opção 'Plano de saúde' na pergunta 'Benefícios recebidos' | Inteiro |
| P4_n_recebe_beneficios_Plano odontológico | Resposta binária (0/1) para a opção 'Plano odontológico' na pergunta 'Benefícios recebidos' | Inteiro |
| P4_n_recebe_beneficios_Auxílio-creche | Resposta binária (0/1) para a opção 'Auxílio-creche' na pergunta 'Benefícios recebidos' | Inteiro |
| P4_n_recebe_beneficios_Seguro de vida | Resposta binária (0/1) para a opção 'Seguro de vida' na pergunta 'Benefícios recebidos' | Inteiro |
| P4_n_recebe_beneficios_Previdência privada | Resposta binária (0/1) para a opção 'Previdência privada' na pergunta 'Benefícios recebidos' | Inteiro |
| P4_n_recebe_beneficios_PLR | Resposta binária (0/1) para a opção 'PLR' na pergunta 'Benefícios recebidos' | Inteiro |
| P4_n_recebe_beneficios_Horário flexível | Resposta binária (0/1) para a opção 'Horário flexível' na pergunta 'Benefícios recebidos' | Inteiro |
| P4_n_recebe_beneficios_Auxílio home-office | Resposta binária (0/1) para a opção 'Auxílio home-office' na pergunta 'Benefícios recebidos' | Inteiro |
| P4_n_recebe_beneficios_Auxílio educação/estudo | Resposta binária (0/1) para a opção 'Auxílio educação/estudo' na pergunta 'Benefícios recebidos' | Inteiro |
| P4_n_recebe_beneficios_Ações da empresa (Stock Options) | Resposta binária (0/1) para a opção 'Ações da empresa' na pergunta 'Benefícios recebidos' | Inteiro |
| P4_n_recebe_beneficios_Não recebo nenhum benefício | Resposta binária (0/1) para a opção 'Não recebo nenhum' na pergunta 'Benefícios recebidos' | Inteiro |
| P4_n_recebe_beneficios_Outro | Resposta binária (0/1) para a opção 'Outro' na pergunta 'Benefícios recebidos' | Inteiro |
| P5_a_plataformas_conteudo_dados_Blogs/Artigos (Medium, Towards Data Science, etc) | Resposta binária (0/1) para a opção 'Blogs/Artigos' na pergunta 'Plataformas de conteúdo' | Inteiro |
| P5_a_plataformas_conteudo_dados_Cursos online (Udemy, Coursera, etc) | Resposta binária (0/1) para a opção 'Cursos online' na pergunta 'Plataformas de conteúdo' | Inteiro |
| P5_a_plataformas_conteudo_dados_Eventos/meetups/conferências | Resposta binária (0/1) para a opção 'Eventos/meetups' na pergunta 'Plataformas de conteúdo' | Inteiro |
| P5_a_plataformas_conteudo_dados_Fóruns (Stack Overflow, Reddit, etc) | Resposta binária (0/1) para a opção 'Fóruns' na pergunta 'Plataformas de conteúdo' | Inteiro |
| P5_a_plataformas_conteudo_dados_LinkedIn | Resposta binária (0/1) para a opção 'LinkedIn' na pergunta 'Plataformas de conteúdo' | Inteiro |
| P5_a_plataformas_conteudo_dados_Livros | Resposta binária (0/1) para a opção 'Livros' na pergunta 'Plataformas de conteúdo' | Inteiro |
| P5_a_plataformas_conteudo_dados_Newsletters | Resposta binária (0/1) para a opção 'Newsletters' na pergunta 'Plataformas de conteúdo' | Inteiro |
| P5_a_plataformas_conteudo_dados_Podcasts | Resposta binária (0/1) para a opção 'Podcasts' na pergunta 'Plataformas de conteúdo' | Inteiro |
| P5_a_plataformas_conteudo_dados_Twitter | Resposta binária (0/1) para a opção 'Twitter' na pergunta 'Plataformas de conteúdo' | Inteiro |
| P5_a_plataformas_conteudo_dados_Vídeos no YouTube | Resposta binária (0/1) para a opção 'Vídeos no YouTube' na pergunta 'Plataformas de conteúdo' | Inteiro |
| P5_a_plataformas_conteudo_dados_Comunidades do WhatsApp/Telegram/Discord | Resposta binária (0/1) para a opção 'Comunidades' na pergunta 'Plataformas de conteúdo' | Inteiro |
| P5_a_plataformas_conteudo_dados_Outro | Resposta binária (0/1) para a opção 'Outro' na pergunta 'Plataformas de conteúdo' | Inteiro |
| P5_d_plataformas_estudo_dados_Udemy | Resposta binária (0/1) para a opção 'Udemy' na pergunta 'Plataformas de estudo' | Inteiro |
| P5_d_plataformas_estudo_dados_Coursera | Resposta binária (0/1) para a opção 'Coursera' na pergunta 'Plataformas de estudo' | Inteiro |
| P5_d_plataformas_estudo_dados_edX | Resposta binária (0/1) para a opção 'edX' na pergunta 'Plataformas de estudo' | Inteiro |
| P5_d_plataformas_estudo_dados_DataCamp | Resposta binária (0/1) para a opção 'DataCamp' na pergunta 'Plataformas de estudo' | Inteiro |
| P5_d_plataformas_estudo_dados_Alura | Resposta binária (0/1) para a opção 'Alura' na pergunta 'Plataformas de estudo' | Inteiro |
| P5_d_plataformas_estudo_dados_Udacity | Resposta binária (0/1) para a opção 'Udacity' na pergunta 'Plataformas de estudo' | Inteiro |
| P5_d_plataformas_estudo_dados_LinkedIn Learning | Resposta binária (0/1) para a opção 'LinkedIn Learning' na pergunta 'Plataformas de estudo' | Inteiro |
| P5_d_plataformas_estudo_dados_YouTube | Resposta binária (0/1) para a opção 'YouTube' na pergunta 'Plataformas de estudo' | Inteiro |
| P5_d_plataformas_estudo_dados_Kaggle Learn | Resposta binária (0/1) para a opção 'Kaggle Learn' na pergunta 'Plataformas de estudo' | Inteiro |
| P5_d_plataformas_estudo_dados_Cursos de empresas de tecnologia (AWS, Google, Microsoft, etc) | Resposta binária (0/1) para a opção 'Cursos de empresas' na pergunta 'Plataformas de estudo' | Inteiro |
| P5_d_plataformas_estudo_dados_Cursos de escolas de dados (Data Science Academy, etc) | Resposta binária (0/1) para a opção 'Cursos de escolas de dados' na pergunta 'Plataformas de estudo' | Inteiro |
| P5_d_plataformas_estudo_dados_Não estudo por nenhuma plataforma | Resposta binária (0/1) para a opção 'Não estudo' na pergunta 'Plataformas de estudo' | Inteiro |
| P5_d_plataformas_estudo_dados_Outra | Resposta binária (0/1) para a opção 'Outra' na pergunta 'Plataformas de estudo' | Inteiro |
| P5_e_desafios_carreira_dados_Falta de oportunidades de crescimento na minha empresa | Resposta binária (0/1) para a opção 'Falta de oportunidades' na pergunta 'Desafios na carreira' | Inteiro |
| P5_e_desafios_carreira_dados_Falta de maturidade da empresa em relação à cultura de dados | Resposta binária (0/1) para a opção 'Falta de maturidade da empresa' na pergunta 'Desafios na carreira' | Inteiro |
| P5_e_desafios_carreira_dados_Infraestrutura de dados inadequada | Resposta binária (0/1) para a opção 'Infraestrutura inadequada' na pergunta 'Desafios na carreira' | Inteiro |
| P5_e_desafios_carreira_dados_Qualidade dos dados ruins | Resposta binária (0/1) para a opção 'Qualidade dos dados ruins' na pergunta 'Desafios na carreira' | Inteiro |
| P5_e_desafios_carreira_dados_Comunicação com outras áreas da empresa | Resposta binária (0/1) para a opção 'Comunicação com outras áreas' na pergunta 'Desafios na carreira' | Inteiro |
| P5_e_desafios_carreira_dados_Burocracia para colocar projetos em produção | Resposta binária (0/1) para a opção 'Burocracia' na pergunta 'Desafios na carreira' | Inteiro |
| P5_e_desafios_carreira_dados_Falta de clareza ou definição de um plano de carreira | Resposta binária (0/1) para a opção 'Falta de clareza no plano de carreira' na pergunta 'Desafios na carreira' | Inteiro |
| P5_e_desafios_carreira_dados_Dificuldade em me manter atualizado | Resposta binária (0/1) para a opção 'Dificuldade em me manter atualizado' na pergunta 'Desafios na carreira' | Inteiro |
| P5_e_desafios_carreira_dados_Síndrome do Impostor | Resposta binária (0/1) para a opção 'Síndrome do Impostor' na pergunta 'Desafios na carreira' | Inteiro |
| P5_e_desafios_carreira_dados_Excesso de reuniões | Resposta binária (0/1) para a opção 'Excesso de reuniões' na pergunta 'Desafios na carreira' | Inteiro |
| P5_e_desafios_carreira_dados_Salário abaixo da média do mercado | Resposta binária (0/1) para a opção 'Salário abaixo da média' na pergunta 'Desafios na carreira' | Inteiro |
| P5_e_desafios_carreira_dados_Nenhum desafio | Resposta binária (0/1) para a opção 'Nenhum desafio' na pergunta 'Desafios na carreira' | Inteiro |
| P5_e_desafios_carreira_dados_Outro | Resposta binária (0/1) para a opção 'Outro' na pergunta 'Desafios na carreira' | Inteiro |
| P6_d_ferramentas_ia_generativa_usadas_ChatGPT | Resposta binária (0/1) para a opção 'ChatGPT' na pergunta 'Ferramentas de IA Generativa' | Inteiro |
| P6_d_ferramentas_ia_generativa_usadas_Google Bard/Gemini | Resposta binária (0/1) para a opção 'Google Bard/Gemini' na pergunta 'Ferramentas de IA Generativa' | Inteiro |
| P6_d_ferramentas_ia_generativa_usadas_Microsoft Copilot | Resposta binária (0/1) para a opção 'Microsoft Copilot' na pergunta 'Ferramentas de IA Generativa' | Inteiro |
| P6_d_ferramentas_ia_generativa_usadas_Github Copilot | Resposta binária (0/1) para a opção 'Github Copilot' na pergunta 'Ferramentas de IA Generativa' | Inteiro |
| P6_d_ferramentas_ia_generativa_usadas_Claude | Resposta binária (0/1) para a opção 'Claude' na pergunta 'Ferramentas de IA Generativa' | Inteiro |
| P6_d_ferramentas_ia_generativa_usadas_Midjourney | Resposta binária (0/1) para a opção 'Midjourney' na pergunta 'Ferramentas de IA Generativa' | Inteiro |
| P6_d_ferramentas_ia_generativa_usadas_DALL-E | Resposta binária (0/1) para a opção 'DALL-E' na pergunta 'Ferramentas de IA Generativa' | Inteiro |
| P6_d_ferramentas_ia_generativa_usadas_Notion AI | Resposta binária (0/1) para a opção 'Notion AI' na pergunta 'Ferramentas de IA Generativa' | Inteiro |
| P6_d_ferramentas_ia_generativa_usadas_Nenhuma | Resposta binária (0/1) para a opção 'Nenhuma' na pergunta 'Ferramentas de IA Generativa' | Inteiro |
| P6_d_ferramentas_ia_generativa_usadas_Outra | Resposta binária (0/1) para a opção 'Outra' na pergunta 'Ferramentas de IA Generativa' | Inteiro |
| P1_i_tipo_graduacao_nan | Resposta binária (0/1) indicando ausência de resposta para 'Tipo de Graduação' | Inteiro |
| P2_d_motivacao_area_dados_nan | Resposta binária (0/1) indicando ausência de resposta para 'Motivação para entrar na área' | Inteiro |
| P3_b_principal_linguagem_programacao_nan | Resposta binária (0/1) indicando ausência de resposta para 'Principal linguagem de programação' | Inteiro |
| P3_c_linguagens_de_programacao_mais_usadas_nan | Resposta binária (0/1) indicando ausência de resposta para 'Linguagens mais usadas' | Inteiro |
| P3_d_ferramentas_bi_mais_usadas_nan | Resposta binária (0/1) indicando ausência de resposta para 'Ferramentas de BI' | Inteiro |
| P3_e_plataformas_nuvem_mais_usadas_nan | Resposta binária (0/1) indicando ausência de resposta para 'Plataformas de Nuvem' | Inteiro |
| P3_f_ferramentas_etl_mais_usadas_nan | Resposta binária (0/1) indicando ausência de resposta para 'Ferramentas de ETL' | Inteiro |
| P3_g_ferramentas_de_modelagem_de_dados_mais_usadas_nan | Resposta binária (0/1) indicando ausência de resposta para 'Ferramentas de Modelagem' | Inteiro |
| P3_h_banco_de_dados_mais_usados_nan | Resposta binária (0/1) indicando ausência de resposta para 'Bancos de Dados' | Inteiro |
| P3_i_plataformas_de_big_data_mais_usadas_nan | Resposta binária (0/1) indicando ausência de resposta para 'Plataformas de Big Data' | Inteiro |
| P3_j_bibliotecas_de_ia_mais_usadas_nan | Resposta binária (0/1) indicando ausência de resposta para 'Bibliotecas de IA' | Inteiro |
| P4_k_prioridade_proxima_oportunidade_nan | Resposta binária (0/1) indicando ausência de resposta para 'Prioridade próxima oportunidade' | Inteiro |
| P4_n_recebe_beneficios_nan | Resposta binária (0/1) indicando ausência de resposta para 'Benefícios recebidos' | Inteiro |
| P5_a_plataformas_conteudo_dados_nan | Resposta binária (0/1) indicando ausência de resposta para 'Plataformas de conteúdo' | Inteiro |
| P5_d_plataformas_estudo_dados_nan | Resposta binária (0/1) indicando ausência de resposta para 'Plataformas de estudo' | Inteiro |
| P5_e_desafios_carreira_dados_nan | Resposta binária (0/1) indicando ausência de resposta para 'Desafios na carreira' | Inteiro |
| P6_d_ferramentas_ia_generativa_usadas_nan | Resposta binária (0/1) indicando ausência de resposta para 'Ferramentas de IA Generativa' | Inteiro |
| cargo_atual_Analista de BI/BI Analyst | Resposta binária (0/1) para o cargo 'Analista de BI' | Inteiro |
| cargo_atual_Analista de Dados/Data Analyst | Resposta binária (0/1) para o cargo 'Analista de Dados' | Inteiro |
| cargo_atual_Cientista de Dados/Data Scientist | Resposta binária (0/1) para o cargo 'Cientista de Dados' | Inteiro |
| cargo_atual_Engenheiro de Dados/Data Engineer | Resposta binária (0/1) para o cargo 'Engenheiro de Dados' | Inteiro |
| cargo_atual_Engenheiro de Machine Learning/Machine Learning Engineer | Resposta binária (0/1) para o cargo 'Engenheiro de Machine Learning' | Inteiro |
| cargo_atual_Engenheiro de Analytics/Analytics Engineer | Resposta binária (0/1) para o cargo 'Engenheiro de Analytics' | Inteiro |
| cargo_atual_Especialista/Arquiteto(a) de Dados | Resposta binária (0/1) para o cargo 'Especialista/Arquiteto de Dados' | Inteiro |
| cargo_atual_Líder Técnico/Tech Lead | Resposta binária (0/1) para o cargo 'Líder Técnico' | Inteiro |
| cargo_atual_Coordenador/Manager | Resposta binária (0/1) para o cargo 'Coordenador/Manager' | Inteiro |
| cargo_atual_Outro | Resposta binária (0/1) para o cargo 'Outro' | Inteiro |
| cargo_atual_nan | Resposta binária (0/1) indicando ausência de resposta para 'Cargo Atual' | Inteiro |
| area_formacao_Ciências da Computação, Engenharia de Software, Sistemas de Informação, etc. | Resposta binária (0/1) para a área de formação 'Computação' | Inteiro |
| area_formacao_Engenharias (outras) | Resposta binária (0/1) para a área de formação 'Outras Engenharias' | Inteiro |
| area_formacao_Estatística | Resposta binária (0/1) para a área de formação 'Estatística' | Inteiro |
| area_formacao_Economia, Administração, Contabilidade, etc. | Resposta binária (0/1) para a área de formação 'Negócios' | Inteiro |
| area_formacao_Ciências Sociais, Marketing, etc. | Resposta binária (0/1) para a área de formação 'Ciências Sociais/Marketing' | Inteiro |
| area_formacao_Ciências Exatas (Matemática, Física, etc.) | Resposta binária (0/1) para a área de formação 'Ciências Exatas' | Inteiro |
| area_formacao_Outra | Resposta binária (0/1) para a área de formação 'Outra' | Inteiro |
| area_formacao_nan | Resposta binária (0/1) indicando ausência de resposta para 'Área de Formação' | Inteiro |
| situacao_trabalho_atual_Empregado (CLT) | Resposta binária (0/1) para a situação 'Empregado (CLT)' | Inteiro |
| situacao_trabalho_atual_Empregado (Servidor Público) | Resposta binária (0/1) para a situação 'Empregado (Servidor Público)' | Inteiro |
| situacao_trabalho_atual_Contrato (PJ) | Resposta binária (0/1) para a situação 'Contrato (PJ)' | Inteiro |
| situacao_trabalho_atual_Freelancer | Resposta binária (0/1) para a situação 'Freelancer' | Inteiro |
| situacao_trabalho_atual_Estagiário | Resposta binária (0/1) para a situação 'Estagiário' | Inteiro |
| situacao_trabalho_atual_Desempregado, buscando recolocação | Resposta binária (0/1) para a situação 'Desempregado' | Inteiro |
| situacao_trabalho_atual_Apenas estudando | Resposta binária (0/1) para a situação 'Apenas estudando' | Inteiro |
| situacao_trabalho_atual_Outra | Resposta binária (0/1) para a situação 'Outra' | Inteiro |
| situacao_trabalho_atual_nan | Resposta binária (0/1) indicando ausência de resposta para 'Situação de Trabalho' | Inteiro |
| faixa_salarial_Menos de R$ 1.000/mês | Resposta binária (0/1) para a faixa salarial 'Menos de R$ 1.000' | Inteiro |
| faixa_salarial_de R$ 1.001/mês a R$ 2.000/mês | Resposta binária (0/1) para a faixa salarial 'R$ 1.001 a R$ 2.000' | Inteiro |
| faixa_salarial_de R$ 2.001/mês a R$ 3.000/mês | Resposta binária (0/1) para a faixa salarial 'R$ 2.001 a R$ 3.000' | Inteiro |
| faixa_salarial_de R$ 3.001/mês a R$ 4.000/mês | Resposta binária (0/1) para a faixa salarial 'R$ 3.001 a R$ 4.000' | Inteiro |
| faixa_salarial_de R$ 4.001/mês a R$ 6.000/mês | Resposta binária (0/1) para a faixa salarial 'R$ 4.001 a R$ 6.000' | Inteiro |
| faixa_salarial_de R$ 6.001/mês a R$ 8.000/mês | Resposta binária (0/1) para a faixa salarial 'R$ 6.001 a R$ 8.000' | Inteiro |
| faixa_salarial_de R$ 8.001/mês a R$ 12.000/mês | Resposta binária (0/1) para a faixa salarial 'R$ 8.001 a R$ 12.000' | Inteiro |
| faixa_salarial_de R$ 12.001/mês a R$ 16.000/mês | Resposta binária (0/1) para a faixa salarial 'R$ 12.001 a R$ 16.000' | Inteiro |
| faixa_salarial_de R$ 16.001/mês a R$ 20.000/mês | Resposta binária (0/1) para a faixa salarial 'R$ 16.001 a R$ 20.000' | Inteiro |
| faixa_salarial_de R$ 20.001/mês a R$ 25.000/mês | Resposta binária (0/1) para a faixa salarial 'R$ 20.001 a R$ 25.000' | Inteiro |
| faixa_salarial_de R$ 25.001/mês a R$ 30.000/mês | Resposta binária (0/1) para a faixa salarial 'R$ 25.001 a R$ 30.000' | Inteiro |
| faixa_salarial_de R$ 30.001/mês a R$ 40.000/mês | Resposta binária (0/1) para a faixa salarial 'R$ 30.001 a R$ 40.000' | Inteiro |
| faixa_salarial_Mais de R$ 40.000/mês | Resposta binária (0/1) para a faixa salarial 'Mais de R$ 40.000' | Inteiro |
| faixa_salarial_nan | Resposta binária (0/1) indicando ausência de resposta para 'Faixa Salarial' | Inteiro |
| nivel_ingles_Nenhum | Resposta binária (0/1) para o nível de inglês 'Nenhum' | Inteiro |
| nivel_ingles_Básico | Resposta binária (0/1) para o nível de inglês 'Básico' | Inteiro |
| nivel_ingles_Intermediário | Resposta binária (0/1) para o nível de inglês 'Intermediário' | Inteiro |
| nivel_ingles_Avançado | Resposta binária (0/1) para o nível de inglês 'Avançado' | Inteiro |
| nivel_ingles_Fluente | Resposta binária (0/1) para o nível de inglês 'Fluente' | Inteiro |
| nivel_ingles_nan | Resposta binária (0/1) indicando ausência de resposta para 'Nível de Inglês' | Inteiro |
| experiencia_profissional_Sem experiência | Resposta binária (0/1) para a experiência 'Sem experiência' | Inteiro |
| experiencia_profissional_Menos de 1 ano | Resposta binária (0/1) para a experiência 'Menos de 1 ano' | Inteiro |
| experiencia_profissional_de 1 a 2 anos | Resposta binária (0/1) para a experiência 'de 1 a 2 anos' | Inteiro |
| experiencia_profissional_de 2 a 3 anos | Resposta binária (0/1) para a experiência 'de 2 a 3 anos' | Inteiro |
| experiencia_profissional_de 4 a 5 anos | Resposta binária (0/1) para a experiência 'de 4 a 5 anos' | Inteiro |
| experiencia_profissional_de 6 a 10 anos | Resposta binária (0/1) para a experiência 'de 6 a 10 anos' | Inteiro |
| experiencia_profissional_Mais de 10 anos | Resposta binária (0/1) para a experiência 'Mais de 10 anos' | Inteiro |
| experiencia_profissional_nan | Resposta binária (0/1) indicando ausência de resposta para 'Experiência Profissional' | Inteiro |



# Base auxiliar

## Dicionário de Dados - RELAÇÃO ANUAL DE INFORMAÇÕES SOCIAIS – RAIS

| Atributo | Descrição | Tipo |
| :--- | :--- | :--- |
| **Município** | Código do município (segundo o IBGE) onde o vínculo de trabalho está localizado. | Categórico |
| **CNAE 2.0 Classe** | Código da atividade econômica principal do estabelecimento, com base na Classificação Nacional de Atividades Econômicas (CNAE 2.0). | Categórico |
| **CBO Ocupação 2002** | Código da ocupação do trabalhador, com base na Classificação Brasileira de Ocupações (CBO), versão 2002. | Categórico |
| **Faixa Etária** | Intervalo de idade em que o trabalhador se encontra. | Categórico |
| **Escolaridade após 2005**| Nível de instrução formal do trabalhador. | Categórico |
| **Raça Cor** | Raça ou cor autodeclarada pelo trabalhador, seguindo as categorias do IBGE. | Categórico |
| **Sexo Trabalhador** | Sexo do trabalhador. | Categórico |
| **Vl Remun Média (SM)** | Valor da remuneração média mensal do trabalhador, expressa em quantidade de salários mínimos (SM). | Real |
| **Ind Trab Intermitente** | Indicador que aponta se o contrato de trabalho é do tipo intermitente (1 para Sim, 0 para Não). | Categórico |
| **Ind Trab Parcial** | Indicador que aponta se o contrato de trabalho é em regime de tempo parcial (1 para Sim, 0 para Não). | Categórico |
| **Tipo Vínculo** | Natureza do vínculo empregatício (ex: CLT, Estatutário). | Categórico |
| **Qtd Vínculos** | Número total de vínculos de trabalho existentes para o agrupamento de características da respectiva linha. | Inteiro |

### Observação: Agregamos à base principal usando o atributo Região onde mora, como atributo chave. 


## Preparação dos Dados

A fase de preparação dos dados é crucial para garantir a qualidade e adequação do dataset para a análise. Neste projeto, a preparação dos dados consistiu nos seguintes passos:

### Seleção dos Atributos

Com base no objetivo da análise e na hipótese a ser investigada, foi realizada a seleção manual dos atributos relevantes do dataset original. Os atributos selecionados para compor a base de dados principal foram:

* Idade
* Genero
* Cor/raca/etnia
* PCD (Pessoa com Deficiência)
* Regiao onde mora
* Nível de Ensino
* Área de formação em dados
* Situação de trabalho
* Estoque de Emprego Região (base auxiliar)

Estes atributos foram considerados essenciais para explorar as relações entre gênero, situação de trabalho e localização geográfica, além de fornecerem contexto demográfico e educacional dos respondentes.

### Tratamento dos Valores Faltantes ou Omissos

A presença de valores faltantes ou omissos nos dados pode impactar a análise. No processo de preparação, identificamos e tratamos esses valores:

* A categoria "Outras Engenharias" foi removida, pois não há dados nessa classe; 'nan' - nulos.
* "Outra opção" recebeu o mesmo valor que "Computação / Engenharia / Sistemas de Informação / TI" (0), pois a moda da àrea de fomação era a classe '0', então atribui 'Outra opção' a essa classe.
* Linhas com valores NaN nesta coluna foram removidas durante o processamento.
* *Linhas com valor “Prefiro não informar” em PCD foram removidas do DataFrame.*
* *Linhas com valor “Outro” em gênero foram removidas do DataFrame.*

### Tratamento dos Valores Inconsistentes

Valores inconsistentes podem distorcer os resultados da análise. Foram realizados tratamentos específicos para lidar com inconsistências identificadas:

* **Tratamento na Coluna 'Genero':** As categorias 'Outro' e 'Prefiro não informar' na coluna 'Genero' foram identificadas como inconsistentes para a análise de disparidade de gênero binária. Essas linhas foram removidas do dataset.
* **Tratamento na Coluna 'PCD':** Similarmente, as linhas onde a coluna 'PCD' apresentava o valor 'Prefiro não informar' foram removidas, pois não era possível inferir a informação de deficiência a partir desse valor.
* **Tratamento na Coluna 'Área de formação':** Foram identificados valores nulos (NaN) na coluna 'Área de formação' após o mapeamento, o que indicava a falta de informação para algumas entradas. As linhas com valores nulos nesta coluna também foram removidas.
* **Agrupamento na Coluna 'Situação de trabalho':** As diversas categorias de situação de trabalho foram agrupadas em duas categorias principais: 'Empregado(a)' e 'Desempregado(a)'. Este agrupamento simplifica a análise e foca na dicotomia emprego/desemprego. (É importante verificar e corrigir quaisquer erros de digitação durante este agrupamento).
* **Tratamento de Mapeamentos Duplicados/Inconsistentes:** Durante a codificação de variáveis categóricas, foi observado que a categoria 'Outras Engenharias' na coluna 'Área de formação' foi mapeada para dois valores diferentes (2 e 8), e 'Outra opção' foi mapeada para o mesmo valor que 'Computação / Engenharia...' (0). Embora o código original mostre esses mapeamentos, para uma análise precisa, estes devem ser revisados e corrigidos para garantir a unicidade dos códigos para cada categoria.


##  Conversão de Dados em `base_princ`

Esta seção detalha as transformações aplicadas às colunas da base de dados `base_princ` para converter todas as variáveis em categóricas
-

### **1. Discretização (*Binning*)**

Esta transformação foi aplicada para converter a variável numérica contínua `Idade` em uma variável categórica ordinal.

| Coluna Alvo | Transformação | Lógica | Novas Categorias (Rótulos) | Resultado |
| :--- | :--- | :--- | :--- | :--- |
| `Idade` | Agrupamento por Quartis (`pd.cut`) | A coluna foi dividida em 4 grupos de tamanho aproximadamente igual. | `Faixa_1_Idade`, `Faixa_2_Idade`, `Faixa_3_Idade`, `Faixa_4_Idade` | Criação da coluna `Faixa Etária` e remoção da coluna `Idade` original. |

---

### **2. Codificação por Rótulo (*Label Encoding*)**

Aplicada para converter variáveis categóricas binárias ou ordinais em valores numéricos.

| Coluna Alvo | Valor Original (Categoria) | Valor Novo (Numérico) |
| :--- | :--- | :--- |
| **Nível de Ensino** | `Não tenho graduação formal` | `0` |
| | `Estudante de Graduação` | `1` |
| | `Graduação/Bacharelado` | `2` |
| | `Pós-graduação` | `3` |
| | `Mestrado` | `4` |
| | `Doutorado ou Phd` | `5` |
| **Área de formação em tecnologia** | `Não` | `0` |
| | `Sim` | `1` |
| **Genero** | `Masculino` | `0` |
| | `Feminino` | `1` |
| **Situação de trabalho** | `Empregado(a)` | `0` |
| | `Desempregado(a)` | `1` |
| **PCD** | `Não` | `0` |
| | `Sim` | `1` |

**Observação:** Para as colunas `Genero`, `Situação de trabalho` e `PCD`, as linhas que não puderam ser mapeadas (por conterem valores nulos ou diferentes dos especificados) foram removidas da base (`dropna()`).

---

### **3. Codificação Fictícia (*One-Hot Encoding*)**

Aplicada a todas as variáveis categóricas nominais restantes para convertê-las em um formato numérico binário, utilizando `pd.get_dummies()`.

* **Função:** `pd.get_dummies(df, drop_first=False, dtype=int)`
* **Lógica:** Para cada categoria única em uma coluna, uma nova coluna binária (com valores `0` ou `1`) é criada.

| Colunas Afetadas (Exemplos) | Transformação | Exemplo de Novas Colunas Geradas |
| :--- | :--- | :--- |
| `Faixa Etária` | One-Hot Encoding | `Faixa Etária_Faixa_1_Idade`, `Faixa Etária_Faixa_2_Idade`, ... |
| `Cor/raca/etnia` | One-Hot Encoding | `Cor/raca/etnia_Amarela`, `Cor/raca/etnia_Branca`, `Cor/raca/etnia_Parda`, ... |
| `Região onde mora` | One-Hot Encoding | `Região onde mora_Centro-oeste`, `Região onde mora_Nordeste`, ... |



## 2.2. Dicionário de Dados da base modificada(pré-processada)

| Atributo | Qtde de Instâncias | Tipo do atributo |
|---|---|---|
| Genero | 5008 | Categórico |
| PCD | 5008 | Categórico |
| Área de formação em tecnologia | 5008 | Categórico |
| Situação de trabalho | 5008 | Categórico |
| Nível de Ensino | 5008 | Categórico |
| Cor/raca/etnia_Amarela | 5008 | Categórico |
| Cor/raca/etnia_Branca | 5008 | Categórico |
| Cor/raca/etnia_Indígena | 5008 | Categórico |
| Cor/raca/etnia_Outra | 5008 | Categórico |
| Cor/raca/etnia_Parda | 5008 | Categórico |
| Cor/raca/etnia_Prefiro não informar | 5008 | Categórico |
| Cor/raca/etnia_Preta | 5008 | Categórico |
| Região onde mora_Centro-oeste | 5008 | Categórico |
| Região onde mora_Nordeste | 5008 | Categórico |
| Região onde mora_Norte | 5008 | Categórico |
| Região onde mora_Sudeste | 5008 | Categórico |
| Região onde mora_Sul | 5008 | Categórico |
| Faixa Etária_Faixa_1_Idade | 5008 | Categórico |
| Faixa Etária_Faixa_2_Idade | 5008 | Categórico |
| Faixa Etária_Faixa_3_Idade | 5008 | Categórico |
| Faixa Etária_Faixa_4_Idade | 5008 | Categórico |


## 3. Análise Descritiva dos Dados utilizando Estatísticas de Primeira Ordem

* **Descrição:** Esta seção apresenta uma análise descritiva das colunas da base de dados processada (`base_princ`), utilizando estatísticas de primeira ordem para descrever a distribuição e as características dos dados.

## Descrição de Dados Numéricos

As colunas na base de dados processada foram convertidas para o tipo `int` após a codificação das variáveis categóricas. Embora representem categorias, sua análise estatística descritiva pode fornecer insights sobre a distribuição dos valores codificados. A coluna 'Idade' é a única numérica original antes do processamento extenso das demais colunas.

Para dados numéricos, as estatísticas de primeira ordem incluem:

* **Média:** Medida de tendência central.
* **Mediana:** Valor central dos dados ordenados.
* **Moda:** Valor mais frequente nos dados.
* **Desvio Padrão:** Medida de dispersão dos dados em torno da média.
* **Variância:** Quadrado do desvio padrão, outra medida de dispersão.
* **Mínimo e Máximo:** Limites inferior e superior dos dados.
* **Quartis:** Valores que dividem os dados em quatro partes iguais (25%, 50% - mediana, 75%).

Considerando a saída do seu código para a análise estatística, podemos descrever cada coluna:

### Análise da Coluna 'Idade'

* **Média:** 31.96 anos.
* **Mediana:** 30.00 anos.
* **Moda:** 27.00 anos (o valor mais frequente de idade).
* **Desvio Padrão:** 7.55 anos (indica a dispersão das idades em torno da média).
* **Mínimo:** 18.00 anos.
* **Máximo:** 73.00 anos.
* **Quartis:** 25% dos respondentes têm 27 anos ou menos, 50% têm 30 anos ou menos, e 75% têm 36 anos ou menos.

### Análise da Coluna 'Genero'

* **Média:** 0.25 (considerando a codificação, indica a proporção relativa entre os gêneros).
* **Mediana:** 0.00.
* **Moda:** 1.00 (o gênero com maior frequência na codificação).
* **Desvio Padrão:** 0.43.
* **Mínimo:** 0.00.
* **Máximo:** 1.00.
* **Quartis:** 75% dos valores codificados de gênero são 0.

### Análise da Coluna 'Cor/raca/etnia'

* **Média:** 0.91 (valor médio da codificação da cor/raça/etnia).
* **Mediana:** 0.00.
* **Moda:** 3.00 (a cor/raça/etnia com maior frequência na codificação).
* **Desvio Padrão:** 1.34.
* **Mínimo:** 0.00.
* **Máximo:** 6.00.
* **Quartis:** 75% dos valores codificados de cor/raça/etnia são 3 ou menos.

### Análise da Coluna 'PCD'

* **Média:** 0.02 (indica a proporção de respondentes que se identificam como PCD na codificação).
* **Mediana:** 0.00.
* **Moda:** 1.00 (a categoria de PCD com maior frequência na codificação).
* **Desvio Padrão:** 0.14.
* **Mínimo:** 0.00.
* **Máximo:** 1.00.
* **Quartis:** 75% dos valores codificados para PCD são 0.


### Análise da Coluna 'Regiao onde mora'

* **Média:** 2.17 (valor médio da codificação da região).
* **Mediana:** 2.00.
* **Moda:** 2.00 (a região com maior frequência na codificação).
* **Desvio Padrão:** 0.77.
* **Mínimo:** 0.00.
* **Máximo:** 4.00.
* **Quartis:** 75% dos respondentes moram em regiões codificadas como 3 ou menos.

### Análise da Coluna 'Nível de Ensino'

* **Média:** 2.59 (valor médio da codificação do nível de ensino).
* **Mediana:** 3.00.
* **Moda:** 3.00 (o nível de ensino com maior frequência na codificação).
* **Desvio Padrão:** 1.00.
* **Mínimo:** 1.00.
* **Máximo:** 5.00.
* **Quartis:** 75% dos respondentes têm nível de ensino codificado como 3 ou menos.

### Análise da Coluna 'Área de formação'

* **Média:** 1.32 (valor médio da codificação da área de formação).
* **Mediana:** 1.00.
* **Moda:** 2.00 (a área de formação com maior frequência na codificação).
* **Desvio Padrão:** 1.72.
* **Mínimo:** 0.00.
* **Máximo:** 7.00.
* **Quartis:** 75% dos respondentes têm área de formação codificada como 2 ou menos.

### Análise da Coluna 'Situação de trabalho'

* **Média:** 0.09 (indica a proporção de respondentes em uma das categorias de situação de trabalho na codificação).
* **Mediana:** 0.00.
* **Moda:** 1.00 (a situação de trabalho com maior frequência na codificação).
* **Desvio Padrão:** 0.28.
* **Mínimo:** 0.00.
* **Máximo:** 1.00.
* **Quartis:** 75% dos valores codificados para situação de trabalho são 0.

**Observação:** É crucial lembrar que a interpretação dessas estatísticas para as colunas codificadas deve ser feita com cautela, pois os números representam categorias e não possuem uma escala numérica inerente. A análise é mais útil para entender a distribuição dos códigos dentro de cada coluna. Para a coluna 'Idade', a interpretação é direta, pois se trata de uma variável numérica contínua.




## Indução de modelos

### Modelo 1: Árvore de Decisão

# Análise de Projeto de Classificação com Árvore de Decisão

Com base na análise do código Python fornecido, apresento uma descrição detalhada do projeto de classificação, abordando a escolha do modelo, o processo de amostragem, os parâmetros utilizados e os trechos de código mais relevantes.

## Justificativa da Escolha do Modelo

O modelo escolhido para este problema de classificação foi a **Árvore de Decisão (`DecisionTreeClassifier`)**. Essa escolha é justificada por várias razões:

* **Interpretabilidade**: As árvores de decisão são modelos de "caixa branca". Isso significa que a lógica por trás de suas previsões é fácil de entender e visualizar. Como o código demonstra ao final, é possível plotar a árvore inteira e seguir o caminho das decisões com base nas características (features) dos dados, tornando o resultado transparente.
* **Tratamento de Dados Não-Lineares**: O modelo pode capturar relações não-lineares complexas entre as features e o alvo, sem a necessidade de transformações complexas dos dados de entrada.
* **Requisitos Mínimos de Pré-processamento**: Árvores de decisão não exigem a normalização ou padronização dos dados numéricos, o que simplifica a fase de preparação.
* **Base para Modelos Mais Complexos**: A Árvore de Decisão é o bloco de construção fundamental para algoritmos mais robustos como `Random Forest` e `Gradient Boosting`, tornando-a um excelente ponto de partida para um projeto de classificação.

## Processo de Amostragem de Dados

O tratamento e a amostragem dos dados foram realizados de forma robusta para garantir que o modelo seja treinado e avaliado corretamente, evitando problemas comuns como superestimação de performance (*overfitting*) e vazamento de dados (*data leakage*).

### 1. Particionamento em Treino e Teste

Inicialmente, o conjunto de dados foi dividido em dois subconjuntos: um para treino (85%) e outro para teste (15%). Foi utilizada a função `train_test_split`.

* **Estratificação (`stratify=y`)**: A estratificação foi usada para garantir que a proporção das classes (ex: "Empregado" e "Desempregado") fosse a mesma tanto no conjunto de treino quanto no de teste. Isso é crucial em cenários com classes desbalanceadas, pois evita que um dos conjuntos tenha uma representação muito diferente do outro.
* **Reprodutibilidade (`random_state=42`)**: A definição de um `random_state` garante que a divisão dos dados seja sempre a mesma em todas as execuções do código, permitindo a reprodutibilidade dos resultados.
```python
# -*- coding: utf-8 -*-
# Separação da variável alvo (y) e das features (X)
y = df['Situação de trabalho']
X = df.drop('Situação de trabalho', axis=1)

# Divisão dos dados em treino e teste
# test_size=0.15 define que 15% dos dados serão para teste
# stratify=y garante a proporção das classes nos dois conjuntos
# random_state=42 garante a reprodutibilidade da divisão
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.15, stratify=y, random_state=42
)
```
### 2. Validação Cruzada (Cross-Validation)

Para o ajuste de hiperparâmetros e avaliação do modelo, foi utilizada a **Validação Cruzada com 5 folds (`cv=5`)**. Este método divide o conjunto de treinamento em 5 partes (folds). O modelo é treinado 5 vezes, usando 4 folds para treino e 1 para validação em cada iteração. A performance final é a média dos resultados das 5 iterações.

Isso proporciona uma estimativa mais estável e confiável da performance do modelo, reduzindo o risco de que o resultado seja apenas uma coincidência de uma única divisão de dados.

### 3. Balanceamento de Classes com SMOTE dentro de um Pipeline

O código identifica um potencial desbalanceamento de classes e utiliza a técnica **SMOTE (Synthetic Minority Over-sampling Technique)** para lidar com isso. O SMOTE cria novas amostras sintéticas da classe minoritária, balanceando o conjunto de dados de treinamento.

Para evitar o **vazamento de dados**, onde informações do conjunto de validação "vazam" para o treinamento, o SMOTE foi aplicado corretamente dentro de um **Pipeline**. O `Pipeline` garante que o SMOTE seja aplicado apenas nos dados de treinamento de cada fold da validação cruzada. O conjunto de validação (e o conjunto de teste final) permanece inalterado, simulando um ambiente real.

O código inclui uma ferramenta de verificação **(`DataChecker`)** para provar que o SMOTE está sendo aplicado corretamente dentro do fluxo.

```python
# -*- coding: utf-8 -*-
# Criação do Pipeline para o GridSearch
# O Pipeline encadeia os passos de pré-processamento e o modelo
pipeline_for_grid = Pipeline([
    # 1º Passo: Aplica o SMOTE para balancear as classes (apenas nos dados de treino de cada fold)
    ('smote', SMOTE(random_state=42)),
    # Passo de verificação para confirmar a aplicação do SMOTE
    ('data_checker', DataChecker()),
    # 2º Passo: Treina o modelo de Árvore de Decisão
    ('rf', DecisionTreeClassifier(random_state=42))
])

# Definição do GridSearchCV com o pipeline
# cv=5 indica a validação cruzada de 5 folds
grid_search = GridSearchCV(
    estimator=pipeline_for_grid,
    param_grid=param_grid,
    cv=5,
    scoring='precision',
    n_jobs=-1,
    verbose=2
)

# O grid_search.fit aplica o pipeline (com SMOTE) e a validação cruzada
grid_search.fit(X_train, y_train)
```

### Descrição dos Parâmetros Utilizados
A otimização do modelo foi realizada com GridSearchCV, que testa sistematicamente uma combinação de diferentes hiperparâmetros para encontrar a melhor configuração.

**Parâmetros da Árvore de Decisão (DecisionTreeClassifier)**

Os seguintes hiperparâmetros do modelo foram otimizados:

* **max_depth:** Controla a profundidade máxima da árvore. Os valores testados foram [None, 10, 20]. None permite que a árvore cresça até que todas as folhas sejam puras. Limitar a profundidade ajuda a prevenir o overfitting.
 
* **min_samples_split:** Define o número mínimo de amostras necessárias para dividir um nó interno. Os valores testados foram [2, 5]. Valores maiores podem prevenir a criação de divisões que se baseiam em poucas amostras, tornando o modelo mais geral.
  
* **min_samples_leaf:** Define o número mínimo de amostras que uma folha (um nó terminal) deve ter. Os valores testados foram [1, 2]. Assim como o min_samples_split, este parâmetro ajuda a suavizar o modelo e evitar o overfitting.


```python
# -*- coding: utf-8 -*-
# Definição da grade de parâmetros a ser testada
# A notação 'rf__<parametro>' informa ao GridSearchCV para aplicar
# o parâmetro ao passo nomeado 'rf' no pipeline.
param_grid = {
    'rf__max_depth': [None, 10, 20],
    'rf__min_samples_split': [2, 5],
    'rf__min_samples_leaf': [1, 2]
}

```

**Parâmetros do GridSearchCV**
* **estimator:** O objeto que será otimizado, que neste caso é o pipeline_for_grid.
* **param_grid:** O dicionário com os hiperparâmetros a serem testados.
* **cv:** O número de folds para a validação cruzada (definido como 5).
* **scoring:** A métrica usada para avaliar qual combinação de parâmetros é a melhor. Foi escolhida a precision (precisão). Isso sugere que o objetivo principal do modelo é minimizar os falsos positivos (ou seja, quando o modelo prevê "Desempregado(a)", ele deve estar muito certo disso).
* **n_jobs=-1:** Utiliza todos os processadores disponíveis para paralelizar a busca, acelerando o processo.
 
### Fluxo de Processamento e Visualizações
O código gera várias visualizações para diagnosticar, avaliar e interpretar o modelo.

**1. Curva de Aprendizagem:** Este gráfico (gerado no início) ajuda a diagnosticar se o modelo sofre de alto viés (underfitting) ou alta variância (overfitting). Ele plota a performance do modelo nos dados de treino e de validação cruzada à medida que o número de amostras de treinamento aumenta.


* **Resultado esperado:** Idealmente, as duas curvas (treino e validação) convergem para um score alto. Se a curva de validação permanece baixa enquanto a de treino é alta, há overfitting.
 
**2. Curva de Precisão-Recall vs. Limiar de Decisão:** Modelos de classificação retornam probabilidades. O limiar de decisão (padrão 0.5) converte essa probabilidade em uma classe (0 ou 1). Este gráfico permite escolher um limiar otimizado. No código, ele é gerado para ambas as classes, mostrando como a precisão e o recall de cada uma mudam conforme o limiar varia. Isso é fundamental para ajustar o comportamento do modelo às necessidades do negócio (por exemplo, aumentar o recall da classe "Desempregado" mesmo que a precisão diminua um pouco).


**3. Matrizes de Confusão:** Apresentam um resumo visual da performance do modelo. Elas mostram os verdadeiros positivos, verdadeiros negativos, falsos positivos e falsos negativos. O código gera matrizes para os conjuntos de treino e teste, permitindo comparar a performance e verificar se há overfitting.


```python
# -*- coding: utf-8 -*-
# Matriz de Confusão do Teste com o novo limiar
print("\nMatriz de Confusão Final:")
cm = confusion_matrix(y_test, y_pred_novo_limiar)
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues')
plt.xlabel("Previsto")
plt.ylabel("Real")
plt.title(f"Matriz de Confusão com Limiar = {novo_limiar}")
plt.show()
```


**Visualização da Árvore de Decisão:** Esta é a principal vantagem do modelo. O código plota a estrutura completa da árvore final, mostrando as regras de decisão em cada nó, o número de amostras e a distribuição das classes.


* **Como ler:** A partir do nó raiz (topo), cada nó faz uma pergunta sobre uma feature. Se a condição for verdadeira, segue-se para um lado; se for falsa, para o outro. O processo continua até chegar a uma folha, que determina a previsão da classe.
**Importância das Features:** Este gráfico de barras mostra quais características (features) foram mais importantes para o modelo tomar suas decisões. A importância é calculada com base em quanto cada feature contribui para reduzir a impureza nos nós da árvore. Isso ajuda a entender quais variáveis são mais preditivas para determinar a situação de trabalho de um indivíduo.
```python
# -*- coding: utf-8 -*-
# Acessar o passo do modelo de Árvore de Decisão DENTRO do pipeline
rf_step = final_model.named_steps['rf']
importances = rf_step.feature_importances_

# Criar um DataFrame para visualização
feature_importance_df = pd.DataFrame({'Feature': X.columns, 'Importance': importances})
top_20_features = feature_importance_df.sort_values(by='Importance', ascending=False).head(20)

# Gerar o gráfico de barras
plt.figure(figsize=(12, 10))
sns.barplot(x='Importance', y='Feature', data=top_20_features, palette='viridis')
plt.title('Top 20 Features Mais Importantes (Modelo Otimizado via Pipeline)', fontsize=18)
plt.xlabel('Importância', fontsize=14)
plt.ylabel('Feature', fontsize=14)
plt.tight_layout()
plt.show()
```




# Resultados obtidos com o modelo 1 (Árvore de decisão).
O modelo foi desenvolvido com o objetivo principal de identificar pessoas em situação de desemprego, priorizando a sensibilidade (recall) da classe Desempregado(a). Em cenários sociais e políticos, como o mapeamento da vulnerabilidade no mercado de trabalho, é mais crítico deixar de identificar alguém desempregado do que cometer um falso positivo. Por isso, o foco foi maximizar a capacidade do modelo de não deixar desempregados passarem despercebidos.

## Treino:

**Matriz de confusão Treino:**
![025a981b-f341-4fbb-85e0-efe417b982f1](https://github.com/user-attachments/assets/8631f073-9661-46fe-a96e-762400972d48)

**Legenda:** Linhas representam as classes reais, colunas as classes previstas. A diagonal principal mostra as classificações corretas; os demais valores indicam erros do modelo.

## Avaliação do Modelo Final no Conjunto de Treino

### [PROVA SMOTE]  
**Shape dos dados após SMOTE:** `(3756, 16)`

### Relatório de Classificação no Conjunto de Treino:

| Classe           | Precision | Recall | F1-Score | Support |
|------------------|-----------|--------|----------|---------|
| Empregado(a)     | 0.94      | 0.65   | 0.77     | 3430    |
| Desempregado(a)  | 0.14      | 0.59   | 0.22     | 326     |
|------------------|-----------|--------|----------|---------|
| Macro Avg        | 0.54      | 0.62   | 0.50     | 3756    |
| Weighted Avg     | 0.87      | 0.65   | 0.72     | 3756    |

**Accuracy:** `0.65` (base: 3756 amostras)




## Teste:
**Matriz de confusão Teste:**
![c6d84b5c-54f7-431b-9ffe-e717c29296ae](https://github.com/user-attachments/assets/d2df4018-e7b6-45ee-8ef6-80dee784565c)

**Legenda:** Linhas representam as classes reais, colunas as classes previstas. A diagonal principal mostra as classificações corretas; os demais valores indicam erros do modelo.

## Avaliação do Modelo Final no Conjunto de Teste

### [PROVA SMOTE]  
**Shape dos dados após SMOTE:** `(1252, 16)`

### Relatório de Classificação no Conjunto de Teste:

| Classe           | Precision | Recall | F1-Score | Support |
|------------------|-----------|--------|----------|---------|
| Empregado(a)     | 0.95      | 0.28   | 0.43     | 1144    |
| Desempregado(a)  | 0.10      | 0.85   | 0.18     | 108     |
|------------------|-----------|--------|----------|---------|
| Macro Avg        | 0.53      | 0.57   | 0.31     | 1252    |
| Weighted Avg     | 0.88      | 0.33   | 0.41     | 1252    |

**Accuracy:** `0.33` (base: 1252 amostras)


## Acurácia nos Conjuntos de Treino e Teste:

* **Acurácia de treino:** `0.65`
* **Acurácia de teste:** `0.33`

**Observações:** - _Análise de Overfitting_

Overfitting ocorre quando o modelo se ajusta excessivamente aos dados de treino, perdendo a capacidade de generalizar para novos dados. Um dos principais indícios de overfitting é a diferença significativa entre desempenho no treino e no teste — e isso aparece claramente aqui:

**Acurácia no treino: 0.65
Acurácia no teste: 0.33**

Essa queda expressiva de 32 pontos percentuais indica que o modelo pode estar aprendendo padrões específicos demais do conjunto de treino, e falhando ao aplicar esse conhecimento em dados novos.

 **Interpretação**
* Apesar do foco em maximizar o recall da classe Desempregado(a) (o que justifica quedas na acurácia geral), essa diferença entre treino e teste sugere sim presença de overfitting. O modelo está possivelmente:

* Aprendendo padrões superficiais ou específicos demais do conjunto sintético (após SMOTE);

* Compensando recall com excesso de falsos positivos, prejudicando a generalização;

* Tendo dificuldade para manter equilíbrio entre sensibilidade e robustez fora da amostra de treino.


### Interpretação do modelo 1


**Plotagem da árvore de decisão:**
![d174380a-3efb-4738-9704-dffa8e85ed1d](https://github.com/user-attachments/assets/5f792cd5-151c-4f5f-a978-1e531683a0eb)

 **Legenda da Árvore de Decisão:**
 
**feature_name ≤ valor:** Regra de decisão baseada em uma variável preditora.

**gini:** Índice de impureza Gini do nó (quanto menor, mais puro).

**samples:** Número de amostras que chegaram até o nó.

**value:** Distribuição das amostras por classe no nó.

**class:** Classe mais provável atribuída ao nó (previsão do modelo nesse ponto).

## Importância das Features na Árvore de Decisão

A análise da importância das variáveis no modelo final revela quais características mais influenciam a previsão da classe alvo (por exemplo, situação de emprego).

### Principais Conclusões:
**1. Nível de Ensino** é disparadamente a variável mais relevante, representando mais de 50% da importância total. Isso sugere que o grau de escolaridade tem forte relação com a probabilidade de estar empregado(a) ou desempregado(a).

**2. Área de Formação em Tecnologia** aparece como a segunda variável mais importante, indicando que a formação técnica ou tecnológica é um fator relevante na inserção profissional.

**3. Faixa Etária** (especialmente a Faixa 4, mais velha) também tem peso considerável, sugerindo que a idade influencia diretamente a situação de trabalho, possivelmente devido à experiência ou à dificuldade de reinserção.

**4. Região** de residência tem um papel significativo no modelo, especialmente as regiões Sul e Sudeste, o que pode refletir desigualdades regionais no acesso ao emprego.

**5. Gênero** tem alguma importância, embora menor, indicando uma possível diferença de oportunidades entre homens e mulheres, ainda que não seja um dos fatores mais decisivos.

**6. Cor/raça/etnia** teve baixa ou nenhuma relevância no modelo, com destaque para “Branca” e “Outra” com importância zero. Isso pode indicar que, no conjunto de dados analisado, essa variável não contribuiu para melhorar o desempenho do modelo — o que não significa ausência de desigualdade na realidade, mas sim limitação na sensibilidade do modelo ou na representatividade da base.

## **Interpretação Geral:**
**Prioridade:** Maximizar o recall da classe Desempregado(a), ou seja, identificar o maior número possível de pessoas realmente desempregadas, mesmo que isso custe mais falsos positivos (empregados classificados incorretamente como desempregados).

 ### Alto Recall (Teste): 
 O modelo cumpriu seu objetivo central, alcançando 0.85 de recall na classe Desempregado(a) no conjunto de teste. Isso indica que 85% das pessoas realmente desempregadas foram corretamente identificadas, o que é excelente sob o critério desejado.

 ### Baixa Precisão: 
 A precisão foi muito baixa (0.10), o que significa que o modelo também classificou incorretamente muitos empregados como desempregados. Em outras palavras, entre todos os que o modelo disse estarem desempregados, apenas 10% realmente estavam.

 ### Trade-off esperado: 
 Esse é um trade-off comum quando se prioriza recall, especialmente em situações com desequilíbrio de classes. Como a classe desempregado(a) é minoria, aumentar o recall normalmente leva à redução da precisão, o que o modelo de fato refletiu.

 ### Baixa acurácia geral (33% no teste): 
 Apesar do bom recall da classe minoritária, a acurácia global caiu. Isso é esperado, pois o modelo sacrificou o desempenho geral para favorecer uma classe específica.


# Resultados obtidos com o modelo 2 (Random Forest).


## Treino:

**Matriz de confusão Treino:**
![025a981b-f341-4fbb-85e0-efe417b982f1](https://github.com/user-attachments/assets/8631f073-9661-46fe-a96e-762400972d48)

**Legenda:** Linhas representam as classes reais, colunas as classes previstas. A diagonal principal mostra as classificações corretas; os demais valores indicam erros do modelo.

## Avaliação do Modelo Final no Conjunto de Treino

### [PROVA SMOTE]  
**Shape dos dados após SMOTE:** `(3756, 16)`

### Relatório de Classificação no Conjunto de Treino

|                    | precision | recall | f1-score | support |
| :----------------- | :-------: | :----: | :------: | :-----: |
| **Empregado(a)** |   0.96    |  0.80  |   0.87   |  3430   |
| **Desempregado(a)**|   0.23    |  0.63  |   0.34   |   326   |
|                    |           |        |          |         |
| **accuracy** |           |        |   0.78   |  3756   |
| **macro avg** |   0.59    |  0.72  |   0.61   |  3756   |
| **weighted avg** |   0.90    |  0.78  |   0.83   |  3756   |

**Accuracy:** `0.78` (base: 3756 amostras)




## Teste:
**Matriz de confusão Teste:**
![6d714672-d5fc-44e5-8463-952e328f7f38](https://github.com/user-attachments/assets/d3074933-1312-487a-994d-292693ce9dc0)

**Legenda:** Linhas representam as classes reais, colunas as classes previstas. A diagonal principal mostra as classificações corretas; os demais valores indicam erros do modelo.


## Avaliação do Modelo Final no Conjunto de Teste

### [PROVA SMOTE]  
**Shape dos dados após SMOTE:** `(1252, 16)`

### Relatório de Classificação no Conjunto de Teste:

| Classe           | Precision | Recall | F1-Score | Support |
|------------------|-----------|--------|----------|---------|
| Empregado(a)     | 0.95      | 0.49   | 0.64     | 1144    |
| Desempregado(a)  | 0.11      | 0.70   | 0.20     | 108     |
|------------------|-----------|--------|----------|---------|
| Macro Avg        | 0.53      | 0.59   | 0.42     | 1252    |
| Weighted Avg     | 0.87      | 0.50   | 0.60     | 1252    |

**Acurácia Total:** `0.50`


## Acurácia nos Conjuntos de Treino e Teste:

* **Acurácia de treino:** `0.78`
* **Acurácia de teste:** `0.50`

**Observações:** - _Análise de Overfitting_

Overfitting ocorre quando o modelo se ajusta excessivamente aos dados de treino, perdendo a capacidade de generalizar para novos dados. Um dos principais indícios de overfitting é a diferença significativa entre desempenho no treino e no teste — e isso aparece claramente aqui:

**Acurácia no treino: 0.78
Acurácia no teste: 0.50**

Essa queda expressiva de 28 pontos percentuais indica que o modelo pode estar aprendendo padrões específicos demais do conjunto de treino, e falhando ao aplicar esse conhecimento em dados novos.

 **Interpretação**
* Apesar do foco em maximizar o recall da classe Desempregado(a) (o que justifica quedas na acurácia geral), essa diferença entre treino e teste sugere sim presença de overfitting. O modelo está possivelmente:

* Aprendendo padrões superficiais ou específicos demais do conjunto sintético (após SMOTE);

* Compensando recall com excesso de falsos positivos, prejudicando a generalização;

* Tendo dificuldade para manter equilíbrio entre sensibilidade e robustez fora da amostra de treino.


## Importância das Features no Random Forest
![19b49541-3611-48a5-87be-84918d6712aa](https://github.com/user-attachments/assets/252ab476-0411-407f-a00c-57042b4e53fe)

 **Legenda – Importância das Features:**
 
_Importância das features representa o quanto cada variável contribuiu para a tomada de decisão da árvore._

* Ela é calculada com base na redução da impureza (ex: Gini ou Entropia) proporcionada por cada feature ao longo da árvore.

* Quanto maior o valor, mais relevante foi a feature para as decisões do modelo.

* Os valores são normalizados para somar 1 (ou 100% em porcentagem).

### Interpretação do modelo 2
O modelo é extremamente agressivo e sensível para encontrar a classe minoritária (Desempregado(a)).

**Ponto Forte Principal:** Alto Recall para "Desempregado(a)".
Interpretação: Se uma pessoa está realmente desempregada, existe uma alta probabilidade (70% no conjunto de teste) de que o seu modelo a identifique corretamente. Ele foi treinado para "não deixar ninguém para trás" dessa categoria.


**Falhas do modelo:**

Falha em Generalizar (Overfitting):

A falha mais grave. O modelo decorou os dados de treino, mas não aprendeu a lógica por trás deles. Por isso, seu desempenho despenca de 78% de acurácia no treino para 50% no teste. Ele não sabe aplicar o que "aprendeu" em dados novos.

**Precisão Inexistente :**

O modelo "vê" desempregados em todos os lugares. No conjunto de teste, sua precisão para a classe Desempregado(a) foi de apenas 0.11.
Interpretação Prática: A cada 100 pessoas que o seu modelo classifica como "Desempregado(a)", apenas 11 realmente estão. As outras 89 são Falsos Positivos — pessoas empregadas que foram classificadas incorretamente. Isso torna as previsões dessa classe completamente não confiáveis.

**Prejuízo à Classe Majoritária:**

Para ser tão sensível à classe Desempregado(a), o modelo sacrificou sua capacidade de identificar corretamente a classe Empregado(a). O recall para esta classe no teste foi de apenas 0.49.
Interpretação Prática: O modelo errou a classificação de metade das pessoas que estavam de fato empregadas no conjunto de teste.

# Análise comparativa dos modelos

## Análise Comparativa: Árvore de Decisão vs. Random Forest para Identificação de Desemprego

##  Objetivo Principal do Projeto

> O objetivo central é desenvolver um modelo de Machine Learning para identificar pessoas em situação de desemprego, priorizando a **sensibilidade (recall)**. Em um contexto de políticas sociais, é mais crítico deixar de identificar um desempregado (falso negativo) do que classificar erroneamente um empregado como desempregado (falso positivo).

---

##  Modelo 1: Árvore de Decisão

### Resultados no Conjunto de Teste

| Classe | Precision | Recall | F1-Score | Support |
| :--- | :---: | :---: | :---: | :---: |
| Empregado(a) | 0.95 | 0.28 | 0.43 | 1144 |
| **Desempregado(a)** | **0.10** | **0.85** | **0.18** | **108** |
| | | | | |
| **Weighted Avg** | 0.88 | 0.33 | 0.41 | 1252 |

- **Acurácia de Teste:** `0.33`

### Análise de Overfitting

- **Acurácia de Treino:** `0.65`
- **Acurácia de Teste:** `0.33`
- **Queda de Desempenho:** **-32 pontos percentuais**

A diferença expressiva entre as métricas de treino e teste indica um **forte overfitting**. O modelo decorou os padrões dos dados de treino e falhou em generalizar para dados novos.

### Interpretação do Modelo 1

- **Ponto Forte:** Cumpriu o objetivo principal com excelência, alcançando **85% de recall** para a classe `Desempregado(a)`.
- **Ponto Fraco:** A altíssima sensibilidade veio ao custo de uma precisão muito baixa (10%) e uma acurácia geral de apenas 33%. O modelo sacrifica completamente a performance na classe majoritária para focar na minoritária.

---


# Indução do modelo 02:

### Modelo 2: Random Forest

# Análise de Projeto de Classificação com Random Forest
Com base na análise do código Python fornecido, apresento uma descrição detalhada do projeto de classificação, abordando a escolha do segundo modelo, o processo de amostragem, os parâmetros utilizados e os trechos de código mais relevantes.

## Justificativa da Escolha do Modelo
O segundo modelo escolhido para este problema de classificação foi o Random Forest (RandomForestClassifier). Essa escolha é justificada por ser uma evolução direta da Árvore de Decisão, projetada para superar algumas de suas principais limitações. As razões são:

* **Redução de Overfitting e Maior Robustez:** Esta é a principal vantagem. O Random Forest é um modelo de ensemble que constrói múltiplas árvores de decisão durante o treinamento, cada uma em uma subamostra diferente dos dados e com um subconjunto aleatório de features. A decisão final é tomada por "votação" entre todas as árvores. Esse processo torna o modelo significativamente mais robusto e menos propenso a "decorar" os dados de treino, melhorando sua capacidade de generalização para dados novos.

* **Alto Desempenho Geral:** Random Forests são conhecidos por sua alta precisão e por serem modelos muito eficazes em uma vasta gama de problemas de classificação, muitas vezes com menos necessidade de ajuste fino de hiperparâmetros em comparação com outros algoritmos complexos.

* **Importância de Features Confiável:** Embora um Random Forest não seja diretamente visualizável como uma única árvore (é considerado um modelo de "caixa-preta"), ele oferece uma maneira robusta de medir a importância das features. A relevância de cada variável é calculada com base na média de sua contribuição para a redução de impureza em todas as árvores do conjunto, fornecendo uma estimativa mais estável e confiável do que a de uma única árvore.

* **Tratamento de Dados Não-Lineares:** Assim como as árvores de decisão individuais, o Random Forest é capaz de capturar relações complexas e não-lineares entre as variáveis, sem exigir transformações manuais dos dados.
  

### Resultados no Conjunto de Teste

| Classe | Precision | Recall | F1-Score | Support |
| :--- | :---: | :---: | :---: | :---: |
| Empregado(a) | 0.95 | 0.49 | 0.64 | 1144 |
| **Desempregado(a)** | **0.11** | **0.70** | **0.20** | **108** |
| | | | | |
| **Weighted Avg** | 0.87 | 0.50 | 0.60 | 1252 |

- **Acurácia de Teste:** `0.50`

### Análise de Overfitting

- **Acurácia de Treino:** `0.78`
- **Acurácia de Teste:** `0.50`
- **Queda de Desempenho:** **-28 pontos percentuais**

O overfitting também está presente de forma significativa, embora ligeiramente menor que na Árvore de Decisão.

### Interpretação do Modelo 2

- **Ponto Forte:** Apresenta uma acurácia geral superior (50%) e um desempenho mais equilibrado na classe `Empregado(a)` (recall de 49%).
- **Ponto Fraco:** O recall para a classe `Desempregado(a)` foi de **70%**, um valor bom, mas consideravelmente inferior ao da Árvore de Decisão, não atendendo ao objetivo principal com a mesma eficácia.

---

##  Análise Comparativa Direta

### Tabela de Comparação (Métricas de Teste)

| Métrica (Classe Desempregado(a)) | Modelo 1 (Árvore de Decisão) | Modelo 2 (Random Forest) | Vencedor (para o objetivo) |
| :--- | :---: | :---: | :---: |
| **Recall (Sensibilidade)** | **0.85** | 0.70 |  **Árvore de Decisão** |
| Precisão | 0.10 | 0.11 | Empate (ambos ruins) |
| F1-Score | 0.18 | 0.20 |  Random Forest |
| **Acurácia Geral** | 0.33 | 0.50 |  Random Forest |
| **Overfitting (Queda)** | -32 pts | -28 pts |  Random Forest |

###  Veredito: Qual modelo é melhor?

Considerando o objetivo principal de **maximizar a identificação de desempregados**, o **Modelo 1 (Árvore de Decisão) é superior**.

Ele foi o único que alcançou um nível de recall (85%) que garante que a grande maioria da classe-alvo seja encontrada, mesmo que isso tenha um custo alto em outras métricas. O Random Forest, apesar de ser um modelo mais robusto em geral, não cumpriu a tarefa prioritária com a mesma eficiência.

###  Pontos Críticos em Comum

Ambos os modelos sofrem de duas falhas graves que os tornam inadequados para uso em produção no estado atual:

1.  **Overfitting Severo:** A incapacidade de generalizar é o problema mais urgente. As previsões em dados novos não são confiáveis.
2.  **Precisão Muito Baixa:** Com precisão de ~10%, ambos os modelos geram 9 falsos positivos para cada acerto na classe `Desempregado(a)`. Isso pode levar a um grande desperdício de recursos se usado para guiar ações práticas.

##  Conclusão e Próximos Passos

Apesar de o Modelo 1 ser o vencedor conceitual, nenhum dos modelos está pronto. A estratégia recomendada é:

1.  **Combater o Overfitting (Prioridade #1):**
    - **Ação:** Realizar a "poda" (pruning) da Árvore de Decisão.
    - **Hiperparâmetros:** Focar em `max_depth` (profundidade máxima), `min_samples_leaf` (mínimo de amostras por folha) e `min_samples_split`. O objetivo é reduzir a diferença entre as métricas de treino e teste, mantendo o recall o mais alto possível.

2.  **Otimizar o Equilíbrio (Recall vs. Precisão):**
    - **Ação:** Após controlar o overfitting, ajustar os hiperparâmetros para encontrar um "ponto ideal". Um recall ligeiramente menor pode ser aceitável em troca de um aumento significativo na precisão. A métrica **F1-Score** é ideal para guiar essa otimização.

3.  **Refinar o Modelo Vencedor:**
    - **Ação:** Concentrar os esforços de otimização na **Árvore de Decisão**, pois ela demonstrou maior potencial para atingir o objetivo principal do projeto.

4.  **Explorar Outros Modelos (Opcional):**
    - **Ação:** Se a otimização não produzir um resultado satisfatório, considerar algoritmos como **Gradient Boosting (XGBoost, LightGBM)**, que são conhecidos por seu alto desempenho e podem oferecer um balanço superior entre recall e precisão.

### Distribuição do modelo (opcional)

Tende criar um pacote de distribuição para o modelo construído, para ser aplicado 
em um sistema inteligente.


## 8. Conclusão

O presente trabalho teve como objetivo o desenvolvimento de um sistema de inteligência artificial para identificar indivíduos em situação de desemprego, com um foco deliberado em maximizar a métrica de sensibilidade (recall) para a classe "Desempregado(a)". A conclusão abaixo sintetiza o processo completo, desde o tratamento inicial dos dados até a avaliação final dos modelos e as perspectivas futuras.

### **Breve Resumo do que Foi Desenvolvido**
O desenvolvimento do projeto iniciou-se com uma fase crucial de preparação dos dados. A partir de uma base bruta, foram selecionados atributos-chave e realizado um rigoroso tratamento de valores faltantes e inconsistentes. Decisões importantes foram tomadas, como a remoção de respostas ambíguas (ex: "Prefiro não informar") e o agrupamento da variável Situação de trabalho em uma classificação binária ("Empregado(a)" e "Desempregado(a)"), para focar a análise. Em seguida, o dataset foi transformado por meio de técnicas de discretização (binning para a idade), codificação por rótulo (Label Encoding) e codificação fictícia (One-Hot Encoding) para adequá-lo aos algoritmos de machine learning.

Sobre esta base processada, foram desenvolvidos e comparados dois modelos de classificação, uma Árvore de Decisão e um Random Forest. Para lidar com o desbalanceamento de classes, a técnica SMOTE foi utilizada no treinamento. A avaliação dos modelos foi centrada no objetivo de maximizar o recall, refletindo a importância social de identificar o maior número possível de desempregados.

### Apresentação Geral dos Resultados, Vantagens e Desvantagens
A análise comparativa revelou que o modelo de Árvore de Decisão se mostrou superior para o objetivo proposto.

**Vantagens:** A principal vantagem do sistema foi o cumprimento eficaz de sua missão principal: alcançar uma alta sensibilidade. O modelo atingiu um recall de 0.85 no conjunto de teste, identificando corretamente 85% dos indivíduos realmente desempregados. Além disso, a interpretabilidade da Árvore de Decisão validou a relevância dos atributos selecionados na fase de preparação, como "Nível de Ensino" e "Faixa Etária", que se destacaram como os mais importantes para a classificação.

**Desvantagens:** O foco agressivo no recall resultou em desvantagens significativas. O modelo apresentou uma precisão extremamente baixa (0.10), significando que 90% das suas previsões positivas eram incorretas (falsos positivos). Este desequilíbrio comprometeu a acurácia geral (33% no teste) e, em uma aplicação prática, poderia levar a uma alocação de recursos massivamente ineficiente. Ademais, em ambos os modelos possui overfitting, fazendo com que ele generalizasse mal novos dados.

### **Limitações e Possibilidades de Melhoria**
A análise crítica do processo e dos resultados revelou limitações importantes que abrem caminho para trabalhos futuros.

### **Limitações:**

**Overfitting Severo:** A principal limitação técnica foi o sobreajuste do modelo. A queda abrupta de desempenho entre treino e teste indica que o modelo "decorou" os dados em vez de aprender a generalizar, tornando-o pouco confiável para aplicação em dados inéditos.
Viés de Exclusão: As decisões tomadas no pré-processamento, como a remoção de linhas com respostas "Prefiro não informar" ou "Outro", embora necessárias para simplificar a análise, introduziram um potencial viés. O modelo resultante é especializado em um subconjunto da população que fornece respostas claras e completas, e sua validade para um público mais amplo é questionável.

### **Possibilidades de Melhoria:**

**Controle de Overfitting:** A aplicação de técnicas de poda (pruning) na Árvore de Decisão (ex: limitando max_depth e min_samples_leaf) é o próximo passo mais crítico para criar um modelo mais robusto e generalizável.
**Reavaliação do Tratamento de Dados:** Em vez de remover dados omissos, poderiam ser exploradas técnicas de imputação ou a criação de categorias específicas para "não informado", o que poderia gerar um modelo mais inclusivo e com melhor capacidade de lidar com a complexidade de dados reais.
**Otimização do Balanço de Métricas:** Ajustar os hiperparâmetros do modelo buscando um equilíbrio mais funcional entre recall e precisão, utilizando o F1-Score como métrica-guia para encontrar um ponto ótimo que minimize tanto os falsos negativos quanto os falsos positivos.
**Exploração de Outros Algoritmos:** Investigar o desempenho de modelos como Gradient Boosting (XGBoost, LightGBM), que podem oferecer uma solução mais balanceada e de maior performance para o problema.


# REFERÊNCIAS

Como um projeto de sistema inteligente não requer revisão bibliográfica, 
a inclusão das referências não é obrigatória. No entanto, caso você 
tenha utilizado referências na introdução ou deseje 
incluir referências relacionadas às tecnologias, padrões, ou metodologias 
que serão usadas no seu trabalho, relacione-as de acordo com a ABNT.

Verifique no link abaixo como devem ser as referências no padrão ABNT:

http://www.pucminas.br/imagedb/documento/DOC\_DSC\_NOME\_ARQUI20160217102425.pdf

Por exemplo:

**[1]** - _ELMASRI, Ramez; NAVATHE, Sham. **Sistemas de banco de dados**. 7. ed. São Paulo: Pearson, c2019. E-book. ISBN 9788543025001._

**[2]** - _COPPIN, Ben. **Inteligência artificial**. Rio de Janeiro, RJ: LTC, c2010. E-book. ISBN 978-85-216-2936-8._

**[3]** - _CORMEN, Thomas H. et al. **Algoritmos: teoria e prática**. Rio de Janeiro, RJ: Elsevier, Campus, c2012. xvi, 926 p. ISBN 9788535236996._

**[4]** - _SUTHERLAND, Jeffrey Victor. **Scrum: a arte de fazer o dobro do trabalho na metade do tempo**. 2. ed. rev. São Paulo, SP: Leya, 2016. 236, [4] p. ISBN 9788544104514._

**[5]** - _RUSSELL, Stuart J.; NORVIG, Peter. **Inteligência artificial**. Rio de Janeiro: Elsevier, c2013. xxi, 988 p. ISBN 9788535237016._



# APÊNDICES

**Colocar link:**

[Do código (armazenado no repositório)](https://github.com/ICEI-PUC-Minas-PPL-CDIA/ppl-cd-pcd-sist-int-2025-1-grupo4-Disparidade-de-Genero/tree/main/assets/models/hipoteses/hipotese_4);

[Dos artefatos (armazenado do repositório)](https://github.com/ICEI-PUC-Minas-PPL-CDIA/ppl-cd-pcd-sist-int-2025-1-grupo4-Disparidade-de-Genero/tree/main/assets);

[Da apresentação final (armazenado no repositório);](https://github.com/ICEI-PUC-Minas-PPL-CDIA/ppl-cd-pcd-sist-int-2025-1-grupo4-Disparidade-de-Genero/blob/main/Disparidade%20de%20G%C3%AAnero.pdf)

Do vídeo de apresentação (armazenado no repositório).
