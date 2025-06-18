# 🧹 Limpeza de Dados - Taxas de Conclusão do Ensino Superior por Gênero, Área e Região  
[📄 Código da limpeza](src/code_data_cleanest/base_auxiliares/limpezadedados_2perguntaorientadadados_baux.ipynb)

---

## 📄 Objetivo

Preparar os dados brutos da base **dados_brutos.csv** para responder a uma **pergunta orientada a dados**, analisando **como as taxas de conclusão do ensino superior variam entre homens e mulheres**, considerando a **área de formação** e a **região geográfica** do participante.

---

## 🔍 Etapas da Limpeza de Dados

### 1. **Importação e Leitura do Arquivo**
- O arquivo foi lido usando `pandas.read_csv()` com os parâmetros adequados:
  - `sep=';'` para reconhecer o delimitador correto.
  - `encoding='latin-1'` para interpretar corretamente os caracteres especiais.
  - `low_memory=False` para evitar avisos durante a leitura de grandes volumes de dados.

```python
import pandas as pd

df = pd.read_csv('dados_brutos.csv', sep=';', encoding='latin-1', low_memory=False)
```

---

### 2. **Seleção de Colunas Relevantes**
Foram selecionadas apenas as colunas necessárias para a análise:

| Coluna Original       | Descrição                                        |  
|-----------------------|--------------------------------------------------| 
| ID	                  | Identificador único do participante              |   
| Idade	                | Idade do participante em anos completos          | 
| Gênero	              | Identidade de gênero do participante             | 
| Nível de Ensin o      | Nível mais alto de escolaridade concluído        | 
| Área de Formação      | Área do conhecimento da formação principal       | 
| Região onde mora	    | Região geográfica do Brasil onde reside          | 
| Código da Região	    | Código categórico associado à região geográfica  | 
| Estado onde mora      | Unidade Federativa (UF) de residência atual      |

---

### 3. **Filtragem e Remoção de Ruído**
```python
df_limpo = df_filtrado.dropna().drop_duplicates()
```

---

### 4. **Criação da Variável de Conclusão do Ensino Superior**
```python
df_limpo['Conclusao_Superior'] = df_limpo['Nível de Ensino'].apply(
    lambda x: x.lower() in ['graduação', 'pós-graduação', 'mestrado', 'doutorado']
)
```
---

### 5. **Agrupamento por Gênero, Área e Região**
```python
df_agrupado = df_limpo.groupby(['Gênero', 'Área de Formação', 'Região onde mora']).agg(
    Total_Pessoas=('ID', 'count'),
    Total_Concluintes=('Conclusao_Superior', 'sum')
).reset_index()

df_agrupado['Taxa_Conclusao'] = (
    df_agrupado['Total_Concluintes'] / df_agrupado['Total_Pessoas']
) * 100
```

---
### 6. **Exportação dos Dados Limpos**
```python
df_agrupado.to_csv('taxas_conclusao_superior_genero_area_regiao.csv', index=False)
```

---

## ✅ Resultado Final

Um arquivo .csv contendo as taxas de conclusão por gênero, área e região, permitindo análises como:

🎓 "Mulheres concluem mais o ensino superior em humanas ou exatas?"<br>
🌍 "Qual região tem maior desigualdade de gênero na educação superior?"<br>
📊 "Há equilíbrio entre homens e mulheres nas diferentes áreas?"<br>

---
