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

## 🎬 Vídeo Promocional / Pitch do Modelo Final

[![Assista ao vídeo no YouTube](https://img.youtube.com/vi/nC_IH6RFLqs/0.jpg)](https://youtu.be/nC_IH6RFLqs)


## Instruções de utilização

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

O modelo foi construído sobre a base `[base_processada_enriquecida.csv…]`

# Selecionamos apenas as colunas de interesse para criar nosso DataFrame de trabalho

```python
colunas_interesse = [
    "Idade", "Genero", "Cor/raca/etnia", "PCD", "Região onde mora", "Área de formação em tecnologia", "Situação de trabalho" , "Nível de Ensino"
```
## 4. Execução do Modelo


 Para executar a análise e treinar o modelo de árvore de decisão, rode o script principal a partir da pasta raiz do projeto
 Após a execução, os resultados, como a acurácia do modelo e a matriz de confusão, serão exibidos no terminal. Gráficos gerados serão salvos na pasta /resultados.


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

## 5. Resultados Esperados

O pipeline completo fornece:

* Métricas: Acurácia, Precisão, Recall, F1-Score
* Curva ROC e AUC
* Matriz de Confusão visual
* Melhor estratégia de SMOTE testada
* Melhor limiar para maximização do F1-score

## 6. Possíveis Problemas e Soluções

| Problema                                      | Causa Comum                                   | Solução                                                   |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------------------- |
| ValueError: could not convert string to float | Variável categórica não convertida            | Utilize `OneHotEncoder` no `ColumnTransformer`            |
| ValueError: y contains NaN                    | Variável alvo com valores ausentes            | Aplique `dropna()` antes de treinar                       |
| Baixa performance no teste                    | Variável alvo desbalanceada ou dados ruidosos | Ajuste `sampling_strategy` no SMOTE e revise os atributos |

## 7. Salvamento do Modelo Treinado (Opcional)

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
