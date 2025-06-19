## Disparidade de Gênero no Setor de Dados

O projeto tem como objetivo desenvolver um sistema inteligente para analisar a disparidade de gênero no setor da tecnologia. Utilizando técnicas de inteligência artificial e aprendizado de máquina, o sistema será projetado para coletar, processar e interpretar informações sobre a participação de diferentes gêneros na área, identificando padrões e possíveis desigualdades.


## Integrantes

* Augusto Henrique Gonçalves Valbonetti
* Eduardo Fraga Fonseca Gomes
* Gustavo Bacellar Nunes Soares
* Leonardo Andrade Caetano Dornelas
* Pedro Lansdowne Oliveira
* Vitor Martins Gonçalves

## Professores

* Hugo Bastos de Paula
* Hayala Nepomuceno Curto

## Instruções de utilização

Aqui está o README completo com **todos os tópicos**, bem estruturado e formatado em Markdown:

````markdown
# Instruções de Execução do Projeto

## 1. Requisitos do Sistema

Antes de iniciar, verifique os seguintes pré-requisitos:

- Python 3.9 ou superior instalado (ou uso do Google Colab)
- Acesso à internet para instalação de bibliotecas
- Permissão para upload de arquivos no ambiente escolhido

## 2. Instalação de Dependências

Caso esteja executando localmente (Jupyter Notebook):

```bash
pip install pandas numpy seaborn matplotlib scikit-learn imbalanced-learn
````

Se estiver no Google Colab, execute também:

```bash
!pip install -U imbalanced-learn
```

## 3. Upload da Base de Dados

O modelo foi construído sobre a base `base_final_combinada_kaggle_caged_corrigida_ok.csv`.

**Atenção:** É fundamental que a base siga este formato:

* Colunas `cor_raca` e `nivel_ensino` sem inconsistências (letras minúsculas, sem espaços extras)
* Coluna `vinculo_formal` com valores binários: `1` (formal) e `0` (não formal)
* Ausência de valores nulos (`NaN`)
* Nomes das colunas preservados conforme o código

## 4. Pré-processamento Obrigatório

Se estiver usando uma base nova, execute o seguinte:

```python
df['cor_raca'] = df['cor_raca'].astype(str).str.lower().str.strip()
df['nivel_ensino'] = df['nivel_ensino'].astype(str).str.lower().str.strip()
df = df.dropna()
df = df[df['vinculo_formal'].isin([0, 1])]
```

Esse tratamento garante que os dados estejam compatíveis com o pipeline do modelo.

## 5. Execução do Modelo

Siga a ordem dos blocos de código conforme estruturado no notebook/colab:

* Importação das bibliotecas
* Leitura da base
* Separação de variáveis `X` e `y`
* Pré-processamento com `ColumnTransformer`
* Split entre treino e teste (`train_test_split`)
* Balanceamento com `SMOTE`
* Treinamento com `SVM + GridSearchCV`
* Avaliação com ajuste de limiar (F1-score)
* Geração de matriz de confusão e curva ROC
* Validação cruzada estratificada (opcional)

## 6. Resultados Esperados

O pipeline completo fornece:

* Métricas: Acurácia, Precisão, Recall, F1-Score
* Curva ROC e AUC
* Matriz de Confusão visual
* Melhor estratégia de SMOTE testada
* Melhor limiar para maximização do F1-score

## 7. Possíveis Problemas e Soluções

| Problema                                      | Causa Comum                                   | Solução                                                   |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------------------- |
| ValueError: could not convert string to float | Variável categórica não convertida            | Utilize `OneHotEncoder` no `ColumnTransformer`            |
| ValueError: y contains NaN                    | Variável alvo com valores ausentes            | Aplique `dropna()` antes de treinar                       |
| Baixa performance no teste                    | Variável alvo desbalanceada ou dados ruidosos | Ajuste `sampling_strategy` no SMOTE e revise os atributos |

## 8. Salvamento do Modelo Treinado (Opcional)

Para reuso posterior do modelo já treinado:

```python
import joblib
joblib.dump(best_model, 'modelo_final_svm.pkl')
```

---


```


## Histórico de versões

- 0.1  
  - Definição dos integrantes.

- 0.2  
  - Definição do tema.

- 0.3  
  - 0.4.1  
    - Criação do resumo.  
  - 0.4.2  
    - Criação da introdução.  
  - 0.4.3  
    - Criação da contextualização.  
  - 0.4.4  
    - Criação da problematização.  
  - 0.4.5  
    - Criação dos objetivos.  
  - 0.4.6  
    - Criação das justificativas.  
  - 0.4.7  
    - Criação do público alvo.  
  - 0.4.8  
    - Criação do dicionário de dados.  
  - 0.4.9  
    - Criação da descrição de dados.

- 1.0  
  - Definição das perguntas orientadas a dados.

- 1.1  
  - Preparação de dados.

- 1.2  
  - Enriquecimento de dados.

- 2.0  
  - Criação do sumário das análises exploratórias.

- 2.1  
  - Desenvolvimento das análises exploratórias.

- 2.2  
  - Anexando resultados obtidos.  
  - 2.2.1  
    - Explicando resultados obtidos.

- 3.0  
  - A partir dos resultados obtidos, iniciamos o desenvolvimento do algoritmo de aprendizado de máquina, para previsão da disparidade de gênero em relação a região que a pessoa mora.

- 3.1
  - Realização de diversos testes de algoritmos e desenvolvimento de diversas versões.

- 4.0  
  - Implementação do algoritmo no Colab e no Kaggle Notebook.  
  - 4.1  
    - Manutenções e gerações de diversas versões do algoritmo.  
  - 4.2  
    - Obtenção dos resultados.

- 5.0  
  - Explicação dos resultados.  
  - 5.1  
    - Explicação dos códigos do trabalho.  
  - 5.2  
    - Interpretação dos modelos.  
  - 5.3  
    - Análise comparativa dos modelos.

- 6.0  
  - Preenchimento do Citation.CFF.
