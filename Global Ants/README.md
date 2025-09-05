# GLAD Optimized Dataset for Machine Learning

## Descrição
Este repositório disponibiliza versões otimizadas do *Global Ants Database* (GLAD) estruturadas para aplicação em algoritmos de **aprendizado de máquina supervisionado**. O objetivo principal foi preparar dados ecológicos de formigas para classificação em três eixos: **Disturbance** (binário), **Habitat Type** (multiclasse) e **Continent** (multiclasse).  

A otimização envolveu pré-processamento, imputação de valores ausentes, padronização de variáveis e seleção de atributos, resultando em datasets compactos, consistentes e prontos para uso em modelos como **Support Vector Machines (SVM)**, **Random Forests** e **Decision Trees**.

---

## Estrutura dos Dados
- **Disturbance Optimized Dataset**: 4.389 linhas × 80 preditores + `target`
- **Habitat Type Optimized Dataset**: 4.422 linhas × 65 preditores + `target`
- **Continent Optimized Dataset**: 4.484 linhas × 74 preditores + `target`

Cada arquivo está em formato **CSV**, totalmente numérico e sem valores ausentes.

---

## Metodologia
O pipeline de preparação foi implementado em **Python 3.11**, utilizando as bibliotecas:
- **Pandas** e **NumPy** → manipulação e limpeza tabular  
- **Scikit-Learn** → imputação, transformação e seleção de variáveis  

### Etapas de pré-processamento
1. **Imputação de valores faltantes**:
   - Numéricos → `KNNImputer (k=5)`
   - Categóricos → `SimpleImputer (most_frequent)`
2. **Padronização** → `StandardScaler`
3. **Codificação de variáveis categóricas** → `OneHotEncoder (handle_unknown="ignore")`
4. **Redução dimensional** → `SelectKBest (chi²)`  
5. **Remoção de colunas não informativas**:
   - Constantes e quase-constantes (>99% iguais)  
   - Redundâncias conhecidas (ex.: `tot_ant_sp_rich` redundante em relação a `tot_nat_sp_rich` + `tot_non_nat_sp_rich`)

---

## Resultados
- Nenhum valor ausente remanescente.  
- Datasets reduzidos de milhares de colunas para **65–80 variáveis preditoras** relevantes.  
- Prontos para classificação multiclasse e binária.  

---

## Como usar
```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier

# Carregar dataset
df = pd.read_csv("disturbance_optimized.csv")
X = df.drop(columns=["target"])
y = df["target"]

# Divisão treino/teste
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, stratify=y)

# Modelo de exemplo
clf = RandomForestClassifier(n_estimators=100, random_state=42)
clf.fit(X_train, y_train)
print("Acurácia:", clf.score(X_test, y_test))
