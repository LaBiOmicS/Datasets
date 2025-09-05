# FISHMORPH Dataset – Traços Morfológicos de Peixes de Água Doce

O **FISHMORPH Dataset** reúne informações morfológicas padronizadas de peixes de água doce, com o objetivo de oferecer uma base consistente para análises de classificação e aprendizado de máquina. Este dataset foi construído a partir do banco **FISHMORPH Database**, passando por etapas de curadoria, pré-processamento, imputação de dados ausentes e formatação para uso direto em algoritmos de aprendizado supervisionado.

## Estrutura do Dataset

O dataset está dividido em duas versões, de acordo com a variável resposta (label) utilizada:

- **FISHMORPH_Order.csv** – classificação no nível taxonômico de **ordem**.
- **FISHMORPH_Family.csv** – classificação no nível taxonômico de **família**.

### Variáveis

As variáveis independentes correspondem a medidas morfológicas padronizadas:

- **MBl** – Comprimento da mandíbula  
- **BEl** – Comprimento do olho  
- **VEp** – Posição da abertura da nadadeira ventral  
- **REs** – Comprimento do espinho da nadadeira dorsal  
- **OGp** – Posição da abertura branquial  
- **RMl** – Comprimento da nadadeira peitoral  
- **BLs** – Forma do corpo (razão comprimento/largura)  
- **PFv** – Posição da nadadeira peitoral  
- **PFs** – Forma da nadadeira peitoral  
- **CPt** – Tipo de pedúnculo caudal  

Variável dependente (label):  
- **Order** (em `FISHMORPH_Order.csv`)  
- **Family** (em `FISHMORPH_Family.csv`)

## Pré-processamento

- **Remoção de colunas irrelevantes** (e.g., imagens/ilustrações).  
- **Tratamento de dados ausentes** com **KNN-Imputer (k=5)**.  
- **Normalização** aplicada nos pipelines de classificação para modelos sensíveis à escala.  
- **Filtragem de classes raras**: apenas classes com pelo menos 5 amostras foram mantidas (`MIN_SUPPORT=5`).  

## Uso

O dataset foi projetado para experimentos de classificação utilizando algoritmos de aprendizado supervisionado, incluindo:

- **Support Vector Machines (SVM)** – kernel linear e RBF  
- **Random Forests**  
- **Decision Trees e derivados (HistGradientBoosting)**  
- **k-Nearest Neighbors (kNN)**  
- **Regressão Logística**  

Os arquivos estão no formato `.csv`, prontos para carregamento em Python (pandas) ou R.

### Exemplo em Python

```python
import pandas as pd

# Carregar a versão com classificação por ordem
df_order = pd.read_csv("FISHMORPH_Order.csv")

# Carregar a versão com classificação por família
df_family = pd.read_csv("FISHMORPH_Family.csv")

print(df_order.head())

