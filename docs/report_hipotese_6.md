# Disparidade de Gênero na Progressão de Carreira

Sendo feita por Vitor Martins

Como o gênero, juntamente com o setor, situação atual de trabalho, cargo atual, forma de trabalho atual e região onde mora afetam a velocidade/oportunidade de  progressão de carreira

Atributos selecionados:


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
| `Setor`                                    | Qualitativo  | Nominal        | Em qual setor o participante trabalha.                                           |'Administração', 'Setor'] = 0
; == 'Saúde', 'Setor'] = 1
; == 'Educação', 'Setor'] = 2
base.loc[base['Setor'] == 'Tecnologia/Fábrica de Software', 'Setor'] = 3
base.loc[base['Setor'] == 'Setor Alimentício', 'Setor'] = 4
base.loc[base['Setor'] == 'Varejo', 'Setor'] = 5
base.loc[base['Setor'] == 'Marketing', 'Setor'] = 6
base.loc[base['Setor'] == 'Indústria', 'Setor'] = 7
base.loc[base['Setor'] == 'Internet/Ecommerce', 'Setor'] = 8
base.loc[base['Setor'] == 'Seguros ou Previdência', 'Setor'] = 9
base.loc[base['Setor'] == 'Área de Consultoria', 'Setor'] = 10
base.loc[base['Setor'] == 'Área da Saúde', 'Setor'] = 11
base.loc[base['Setor'] == 'Entretenimento ou Esportes', 'Setor'] = 12
base.loc[base['Setor'] == 'Setor de Energia', 'Setor'] = 13
base.loc[base['Setor'] == 'Outra Opção', 'Setor'] = 14
base.loc[base['Setor'] == 'Setor Imobiliário/ Construção Civil', 'Setor'] = 15
base.loc[base['Setor'] == 'Telecomunicação', 'Setor'] = 16
base.loc[base['Setor'] == 'Setor Farmaceutico', 'Setor'] = 17
base.loc[base['Setor'] == "Filantropia/ONG's", 'Setor'] = 18
base.loc[base['Setor'] == 'Setor Automotivo', 'Setor'] = 19
base.loc[base['Setor'] == 'Finanças ou Bancos', 'Setor'] = 19
base.loc[base['Setor'] == 'Setor Público', 'Setor'] = 19
base.loc[base['Setor'] == 'Agronegócios', 'Setor'] = 19
| `Cargo`                                    | Qualitativo  | Nominal        | Qual cargo o participante ocupa no trabalho.                                     |
| `Nivel`                                    | Qualitativo  | Nominal        | Qual o nivel de experiência do participante                                      |
| `Forma de trabalho?`                       | Qualitativo  | Nominal        | Qual a forma de trabalho do particpante.                                         |
| `Atuacao`                                  | Qualitativo  | Nominal        | Com que serviços o participante atua.                                            |
