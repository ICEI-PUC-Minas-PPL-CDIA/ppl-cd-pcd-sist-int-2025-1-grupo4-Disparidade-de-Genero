🧹 Limpeza de Dados - Pesquisa sobre Conclusão do Ensino Superior por Gênero, Área e Região
📄 Objetivo
Preparar os dados brutos da base de participantes para responder à pergunta:
“Como as taxas de conclusão do ensino superior variam entre homens e mulheres, considerando a área de estudo e a região geográfica?”

🔍 Etapas da Limpeza de Dados
1. Importação e Leitura do Arquivo
O arquivo foi lido usando pandas.read_csv() com os parâmetros apropriados:

df = pd.read_csv(input_file, sep=';', encoding='latin-1', low_memory=False)

2. Seleção de Colunas Relevantes
Apenas os campos diretamente relacionados à conclusão do ensino superior, gênero, área de formação e região foram mantidos:


Coluna Original	| Descrição
ID	            | Identificador único do participante
Idade           | Idade em anos
Gênero          | Gênero do participante
Nível de Ensino	| Nível mais alto de escolaridade concluído
Área de Formação| Área do conhecimento da formação principal
Região onde mora| Região geográfica (Norte, Sul, etc.)
Código da Região| Código identificador da região
Estado onde mora| Unidade Federativa de residência

colunas_relevantes = [
    'ID', 'Idade', 'Gênero', 'Nível de Ensino',
    'Área de Formação', 'Região onde mora',
    'Código da Região', 'Estado onde mora'
]
df_filtrado = df[colunas_relevantes].copy()

3. Filtragem e Remoção de Ruído
Remoção de registros incompletos e duplicados:

df_limpo = df_filtrado.dropna().drop_duplicates()

4. Criação de Variável de Conclusão do Ensino Superior
Criou-se uma variável booleana para indicar se o participante concluiu o ensino superior (ou acima):

df_limpo['Conclusao_Superior'] = df_limpo['Nível de Ensino'].apply(
    lambda x: x.lower() in ['graduação', 'pós-graduação', 'mestrado', 'doutorado']
)

5. Agrupamento por Gênero, Área de Formação e Região
Os dados foram agregados por gênero, área e região, e calculada a taxa de conclusão:

df_agrupado = df_limpo.groupby(['Gênero', 'Área de Formação', 'Região onde mora']).agg(
    Total_Pessoas=('ID', 'count'),
    Total_Concluintes=('Conclusao_Superior', 'sum')
).reset_index()

df_agrupado['Taxa_Conclusao'] = (df_agrupado['Total_Concluintes'] / df_agrupado['Total_Pessoas']) * 100

6. Exportação dos Dados Limpinhos

df_agrupado.to_csv('taxas_conclusao_superior_genero_area_regiao.csv', index=False)

✅ Resultado Final
Um arquivo .csv com a taxa de conclusão do ensino superior por gênero, área de formação e região, pronto para responder perguntas como:

Mulheres concluem mais cursos superiores em áreas exatas do que homens?

Existe desigualdade regional na conclusão do ensino superior entre os gêneros?

Quais regiões ou áreas apresentam maior equidade de gênero na formação superior?
