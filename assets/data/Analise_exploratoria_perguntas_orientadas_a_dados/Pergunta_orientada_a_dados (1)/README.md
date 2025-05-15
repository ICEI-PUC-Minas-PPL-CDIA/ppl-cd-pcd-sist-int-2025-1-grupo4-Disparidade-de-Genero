# Introduçao Matriz de Confusao e Arvore de Decisao 

## 📌 Célula 1 — Instalar bibliotecas (apenas se necessário)

```python
# Execute esta célula apenas se estiver rodando pela primeira vez no Colab ou não tiver as bibliotecas instaladas
!pip install pandas scikit-learn matplotlib
```

##📌 Célula 2 — Importar bibliotecas

```python
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import LabelEncoder
from sklearn.tree import DecisionTreeClassifier, plot_tree
from sklearn.metrics import confusion_matrix, ConfusionMatrixDisplay
```

##📌 Célula 3 — Carregar os dados

```python
# Suba o arquivo 'dados_limpos.csv' na lateral esquerda do Colab ou no mesmo diretório do Jupyter
df = pd.read_csv("dados_limpos.csv", sep=";", encoding="ISO-8859-1")

# Visualizar as 5 primeiras linhas
df.head()
```

##📌 Célula 4 — Criar variável-alvo binária

```python
# Definir níveis que representam conclusão do ensino superior
ensino_superior = ["Graduação", "Pós-graduação", "Mestrado", "Doutorado"]

# Criar nova coluna binária: "Sim" se concluiu ensino superior, caso contrário "Não"
df["Conclusão_Sup"] = df["Nível de Ensino"].apply(lambda x: "Sim" if x in ensino_superior else "Não")

# Verificar distribuição
df["Conclusão_Sup"].value_counts()
```

## 📌 Célula 5 — Selecionar atributos e codificar

```python
# Selecionar os atributos relevantes
features = ["Gênero", "Área de Formação", "Região onde mora"]
X = df[features]
y = df["Conclusão_Sup"]

# Codificar variáveis categóricas
X_encoded = X.apply(LabelEncoder().fit_transform)

# Dividir em treino e teste
X_train, X_test, y_train, y_test = train_test_split(X_encoded, y, test_size=0.3, random_state=42)
```

##📌 Célula 6 — Treinar árvore de decisão

```python
# Criar e treinar o modelo de árvore de decisão
clf = DecisionTreeClassifier(max_depth=4, random_state=42)
clf.fit(X_train, y_train)
```

##📌 Célula 7 — Visualizar a árvore de decisão

```python
plt.figure(figsize=(16, 8))
plot_tree(clf, feature_names=features, class_names=clf.classes_, filled=True)
plt.title("Árvore de Decisão - Conclusão do Ensino Superior")
plt.show()
```

##📌 Célula 8 — Gerar e visualizar matriz de confusão

```python
# Fazer previsões
y_pred = clf.predict(X_test)

# Criar matriz de confusão
cm = confusion_matrix(y_test, y_pred, labels=["Sim", "Não"])
disp = ConfusionMatrixDisplay(confusion_matrix=cm, display_labels=["Sim", "Não"])

# Mostrar gráfico da matriz
disp.plot(cmap="Blues")
plt.title("Matriz de Confusão - Previsão de Conclusão do Ensino Superior")
plt.show()
y_pred = clf.predict(X_test)
cm = confusion_matrix(y_test, y_pred, labels=["Sim", "Não"])
disp = ConfusionMatrixDisplay(confusion_matrix=cm, display_labels=["Sim", "Não"])
disp.plot(cmap="Blues")
plt.title("Matriz de Confusão - Previsão de Conclusão do Ensino Superior")
plt.show()
```

# Arvore de Decisao 
![image](https://github.com/user-attachments/assets/19c75f01-349a-4061-88a3-9420b3edbff3)

# Matriz de Confusao 
![image](https://github.com/user-attachments/assets/9b95439c-c270-4740-b247-881be7b571a0)


