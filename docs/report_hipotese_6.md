# Disparidade de Gênero na Progressão de Carreira

Sendo feita por Vitor Martins

# Como o gênero afeta na progressão de carreira no setor de dados

## Sumário
Análise dos dados;
Relatórios dos algoritmos;
Motivos do uso de cada técnica;
Apresentação e análise dos resultados alcançados.

## Dicionário de dados


| Atributo                                   | Tipo do Dado | Escala         | Descrição                                                                        | Código                                                                               |
|--------------------------------------------|--------------|----------------|----------------------------------------------------------------------------------|------------------------------------------------------------------------------------------ |
| `Idade`                                    | Quantitativo | Nominal        | Idade do participante.                                                           |
| `Gênero`                                   | Qualitativo  | Nominal        | Gênero do participante.                                                          | Masculino = 0; <br> Feminino = 1                                                                |
| `Cor/raca/etnia`                           | Qualitativo  | Nominal        | Cor/raca/etnia do participante.                                                  | Amarela = 2; <br> Preta = 1 Branca = 0 Prefiro não informar = 5 Parda = 3 Outra = 5 Indígena = 4|
| `PCD`                                      | Qualitativo  | Nominal        | Se o particpante é PCD ou não.                                                   | Não = 0 Sim = 1                                                                           |
| `Oportunidades de progressão de carreira`  | Qualitativo  | Nominal        | Se o participante possui as oportunidades de progressão de carreira prejudicadas.| 0 = Prejudicado por outro motivo; <br> 1= Prejudicado na progressão de carreira
| `uf onde mora`                             | Qualitativo  | Nominal        | UF/Estado onde a pessoa mora no momento da pesquisa.                             |'AC'= 0;<br>  'AL' = 1;<br> 'AP' = 2;<br> 'AM' = 3;<br> 'BA' = 4;<br> 'CE' = 5;<br> 'DF' = 6;<br> 'ES' = 7;<br> 'GO' = 8;<br> 'MA' = 9;<br> 'MT' = 10;<br> 'MS' = 11;<br> 'MG' = 12;<br> 'PA' = 13;<br> 'PB' = 14;<br> 'PR' = 15;<br> 'PE' = 16;<br> 'PI' = 17;<br> 'RJ' = 18;<br> 'RN' = 19;<br> 'RS' = 20;<br> 'RO' = 21;<br> 'RR' = 22;<br> 'SC' = 23;<br> 'SP' = 24;<br> 'SE' = 25;<br> 'TO' = 26|
| `Regiao onde mora`                         | Qualitativo  | Nominal        | Região onde a pessoa mora no momento da pesquisa.                                |'Norte' = 0;<br> Nordeste = 1;<br> Sudeste = 2;<br> Sul = 3;<br> Centro-oeste = 4
| `Nivel de Ensino`                          | Qualitativo  | Ordinal        | Qual o nivel de ensino máximo que o partipante alcançou.                         |'Não tenho graduação formal' = 0;<br> 'Estudante de Graduação' = 1;<br> 'Graduação/Bacharelado' = 2;<br> 'Pós-graduação' = 3;<br> 'Mestrado' = 4;<br> 'Doutorado ou Phd' = 5;<br> 'Prefiro não informar' = 6<br>
| `Area de Formação`                         | Qualitativo  | Nominal        | Em qual área do conhecimento o participante é formado ou está se formando.       |'Computação / Engenharia de Software / Sistemas de Informação/ TI' = 0;<br> 'Economia/ Administração / Contabilidade / Finanças/ Negócios' = 1;<br> 'Estatística/ Matemática / Matemática Computacional/ Ciências Atuariais' = 2;<br> 'Outra opção' = 3;<br> 'Marketing / Publicidade / Comunicação / Jornalismo' = 4;<br> 'Ciências Biológicas/ Farmácia/ Medicina/ Área da Saúde' = 5;<br> 'Ciências Sociais' = 6;<br> 'Outras Engenharias' = 7;<br> 'Química / Física' = 8
| `Qual sua situação atual de trabalho?`     | Qualitativo  | Nominal        | Qual a situação de trabalho do participante.                                     |'Empregado (CLT)' = 0;<br> 'Empreendedor ou Empregado (CNPJ)' = 1;<br> 'Estagiário' = 2;<br> 'Freelancer' = 3;<br> 'Vivo no Brasil e trabalho remoto para empresa de fora do Brasil' = 4;<br> 'Vivo fora do Brasil e trabalho para empresa de fora do Brasil' = 5;<br> 'Servidor Público' = 6;<br> 'Prefiro não informar' = 7
| `Setor`                                    | Qualitativo  | Nominal        | Em qual setor o participante trabalha.                                           |'Administração', 'Setor'] = 0 <br>; 'Saúde', 'Setor'] = 1<br>; 'Educação', 'Setor'] = 2<br>; 'Tecnologia/Fábrica de Software' = 3<br>; 'Setor Alimentício'= 4<br>; 'Varejo' = 5<br>; 'Marketing' = 6<br>; 'Indústria' = 7<br>; 'Internet/Ecommerce' = 8<br>; 'Seguros ou Previdência' = 9<br>; 'Área de Consultoria' = 10<br>; 'Área da Saúde' = 11<br>; 'Entretenimento ou Esportes' = 12<br>; 'Setor de Energia' = 13<br>; 'Outra Opção' 14<br>; 'Setor Imobiliário/ Construção Civil'= 15<br>; 'Telecomunicação' = 16<br>; 'Setor Farmaceutico' = 17<br>; "Filantropia/ONG's" = 18<br>; 'Setor Automotivo' = 19<br>; 'Finanças ou Bancos' = 19<br>; 'Setor Público' = 19<br>; 'Agronegócios' = 19<br>
| `Cargo`                                    | Qualitativo  | Nominal        | Qual cargo o participante ocupa no trabalho.                                     |'Analista de Dados/Data Analyst' = 0;<br> 'Analista de BI/BI Analyst' = 1;<br> 'DBA/Administrador de Banco de Dados' = 2;<br> 'Engenheiro de Machine Learning/ML Engineer/AI Engineer' = 3;<br> 'Analista de Negócios/Business Analyst' = 4;<br> 'Desenvolvedor/ Engenheiro de Software/ Analista de Sistemas' = 5;<br> 'Engenheiro de Dados/Arquiteto de Dados/Data Engineer/Data Architect' = 6;<br> 'Analytics Engineer = 7;<br> 'Estatístico' = 8;<br> 'Economista' = 9;<br> 'Cientista de Dados/Data Scientist' = 10;<br> 'Analista de Suporte/Analista Técnico' = 11;<br> 'Outras Engenharias (não inclui dev)' = 12;<br> 'Analista de Inteligência de Mercado/Market Intelligence' = 13;<br> 'Data Product Manager/ Product Manager (PM/APM/DPM/GPM/PO)' = 14;<br> 'Professor/Pesquisador' = 15;<br> 'Outra Opção' = 16
| `Nivel`                                    | Qualitativo  | Nominal        | Qual o nivel de experiência do participante                                      |'Júnior', 'Nivel'] = 0;<br> 'Pleno' = 1;<br> 'Sênior' = 2
| `Forma de trabalho?`                       | Qualitativo  | Nominal        | Qual a forma de trabalho do particpante.                                         |'Modelo híbrido flexível (o funcionário tem liberdade para escolher quando estar no escritório presencialmente)' = 0;<br> 'Modelo 100% presencial' = 1;<br> 'Modelo 100% remoto' = 2;<br> 'Modelo híbrido com dias fixos de trabalho presencial' = 2
| `Atuacao`                                  | Qualitativo  | Nominal        | Com que serviços o participante atua.                                            |'Ciência de Dados' = 0;<br> 'Análise de Dados' = 1;<br> 'Engenharia de Dados' = 2;<br> 'Outra atuação' = 3


## 2 Análise Exploratória



## 3 Limpeza e Tratamento de Dados

Foram removidas todas as linhas que possuiam algum valor nulo nos campos selecionados acima exceto o atributo "Area de Formação"

No atributo `Area de Formação` foi colocado a moda nos valores nulos
O nome da coluna `Oportunidade de Progressão de Carreira` foi modificado para `progressao_prejudicada`
Foi modificada a ordem das colunas, colocando `progressao_prejudicada` em ultimo para facilitar a separação do atributo alvo do resto das colunas
E tipo de todas as colunas foi modificado de float para int



## 4 Modelagem

### Modelo 1
#### Árvore de Decisão

### Modelo 2
#### Random Forest 
Para o modelo 2 eu fiz os seguintes prompts no ChatGPT:
``"Olá, quero fazer um modelo com algoritmo para Machine Learning buscando classificar o que leva uma pessoa a ter a Progressão de Carreira prejudicada, quais algoritmos você me recomenda? Me explique detalhadamente cada um"``

Onde ele me restornou diversos tipos de algoritmos, e dentre esses o algoritmo RandomForest foi o que mais me chamou a atenção

``Faça um script Jupyter Notebook com a aplicação completa do algoritmo de Random Forest para a base State of Data Brazil 2023``

Onde ele me retornou o codigo em arquivo .ipynb para execução da indução do modelo

Relatório de Classificação <br>
![image](https://github.com/user-attachments/assets/1331531b-d61f-472d-9e0f-c49948d5796f)



Esse foi o resultado da matriz de confusão <br>
![image](https://github.com/user-attachments/assets/bc969730-2516-405c-a16c-2b689de0630e)
