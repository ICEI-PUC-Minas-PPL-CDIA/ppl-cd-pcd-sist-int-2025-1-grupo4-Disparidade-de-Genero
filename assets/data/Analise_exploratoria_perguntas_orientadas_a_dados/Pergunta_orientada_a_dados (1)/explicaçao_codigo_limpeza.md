📊 Análise de Taxas de Conclusão do Ensino Superior por Gênero, Área e Região
🎯 Objetivo
Preparar e limpar os dados para responder à pergunta orientada a dados:

Como as taxas de conclusão do ensino superior variam entre homens e mulheres, considerando a área de estudo e a região geográfica?

🧹 Etapas da Limpeza de Dados
1. 📥 Importação e Leitura do Arquivo
O arquivo foi lido utilizando pandas com os seguintes parâmetros:

python
Copiar
Editar
import pandas as pd

df = pd.read_csv('dados_brutos.csv', sep=';', encoding='latin-1', low_memory=False)
2. 📌 Seleção de Colunas Relevantes
Foram mantidas apenas as colunas necessárias para análise:


Coluna	Tipo	Escala	Descrição
ID	Qualitativo	Nominal	Identificador único do participante
Idade	Quantitativo	Discreta	Idade em anos completos
Gênero	Qualitativo	Nominal	Identidade de gênero
Nível de Ensino	Qualitativo	Ordinal	Nível mais alto de escolaridade concluído
Área de Formação	Qualitativo	Nominal	Área do conhecimento da formação principal
Região onde mora	Qualitativo	Nominal	Região do país de residência
Código da Região	Qualitativo	Nominal	Código da região geográfica
Estado onde mora	Qualitativo	Ordinal	Unidade Federativa de residência
python
Copiar
Editar
colunas_relevantes = [
    'ID', 'Idade', 'Gênero', 'Nível de Ensino',
    'Área de Formação', 'Região onde mora',
    'Código da Região', 'Estado onde mora'
]

df_filtrado = df[colunas_relevantes].copy()
3. 🧼 Remoção de Dados Faltantes e Duplicados
python
Copiar
Editar
df_limpo = df_filtrado.dropna().drop_duplicates()
4. 🎓 Criação da Variável “Conclusão do Ensino Superior”
Nova coluna booleana que identifica se o participante concluiu o ensino superior ou níveis acima:

python
Copiar
Editar
df_limpo['Conclusao_Superior'] = df_limpo['Nível de Ensino'].apply(
    lambda x: x.lower() in ['graduação', 'pós-graduação', 'mestrado', 'doutorado']
)
5. 📊 Agrupamento por Gênero, Área e Região
Calcula o total de pessoas, total de concluintes e taxa percentual por grupo:

python
Copiar
Editar
df_agrupado = df_limpo.groupby(['Gênero', 'Área de Formação', 'Região onde mora']).agg(
    Total_Pessoas=('ID', 'count'),
    Total_Concluintes=('Conclusao_Superior', 'sum')
).reset_index()

df_agrupado['Taxa_Conclusao'] = (
    df_agrupado['Total_Concluintes'] / df_agrupado['Total_Pessoas']
) * 100
6. 💾 Exportação dos Dados Finais
python
Copiar
Editar
df_agrupado.to_csv('taxas_conclusao_superior_genero_area_regiao.csv', index=False)
✅ Resultado Final
O arquivo taxas_conclusao_superior_genero_area_regiao.csv contém a taxa de conclusão do ensino superior segmentada por:

Gênero

Área de Formação

Região Geográfica

Exemplos de Análises Possíveis:
Quais áreas têm maior equilíbrio de gênero na conclusão do ensino superior?

As mulheres concluem mais o ensino superior em alguma região específica?

Em que regiões há maior disparidade nas taxas de conclusão entre homens e mulheres?
