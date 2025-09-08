# GLAD Optimized Dataset for Machine Learning


## Resumo

**Objetivo:** Desenvolver uma versão estruturada e otimizada do Global Ants Database (GLAD), adaptada para aplicação em algoritmos de aprendizado de máquina supervisionado, com foco na classificação de comunidades de formigas em relação a distúrbios ambientais, tipos de habitat e distribuição geográfica. O objetivo central foi transformar uma base ecológica global, originalmente heterogênea e de difícil aplicação direta em análises preditivas, em um recurso limpo, imputado e padronizado, capaz de suportar metodologias de classificação multiclasse e binária em ecologia quantitativa. **Métodos:** O estudo foi conduzido em 2025 em ambiente computacional de bioinformática. A amostra corresponde ao GLAD, contendo registros de abundância, riqueza de espécies, atributos ambientais e informações de habitat provenientes de milhares de localidades distribuídas em todos os continentes. O pré-processamento foi realizado em Python 3.11, empregando as bibliotecas Pandas e NumPy para manipulação tabular, e Scikit-Learn para imputação, padronização e seleção de atributos. Valores ausentes em variáveis numéricas foram tratados com KNNImputer (k=5), enquanto variáveis categóricas foram imputadas por moda. Em seguida, variáveis numéricas foram normalizadas com StandardScaler e categóricas codificadas com OneHotEncoder. Para reduzir redundâncias e ruídos, colunas constantes e quase-constantes foram eliminadas, e variáveis com sobreposição conceitual, como a soma da riqueza nativa e não nativa já representada pela riqueza total, foram removidas. Finalmente, aplicou-se SelectKBest (qui-quadrado) para selecionar as variáveis mais informativas em relação aos rótulos-alvo, resultando em versões otimizadas do dataset. **Resultados:** Foram produzidos três conjuntos finais: (i) Disturbance – classificação binária entre áreas perturbadas e não perturbadas; (ii) Habitat Type – classificação multiclasse de diferentes tipos de habitat; e (iii) Continent – classificação multiclasse de localidades por continente. O número de variáveis preditoras foi reduzido de mais de 1.800 colunas iniciais para entre 65 e 80 atributos informativos em cada dataset, mantendo aproximadamente 4.400 registros por conjunto. A imputação eliminou todos os valores ausentes, a padronização garantiu consistência entre escalas, e a seleção de atributos preservou a representatividade ecológica ao mesmo tempo em que reduziu drasticamente a dimensionalidade. Os datasets resultantes mostraram-se adequados para uso imediato em algoritmos de aprendizado supervisionado, como Support Vector Machines (SVM), Random Forests e Árvores de Decisão, além de possibilitar análises sobre a importância relativa de cada variável ecológica na classificação. **Conclusão:** O GLAD Optimized Dataset alcançou o objetivo de disponibilizar uma base ecológica global limpa, consistente e metodologicamente transparente, ampliando as possibilidades de integração entre ecologia de formigas e ciência de dados. Ao oferecer três versões otimizadas com diferentes variáveis-alvo, este recurso promove a aplicação de técnicas de aprendizado de máquina em ecologia funcional e biodiversidade, fortalecendo a capacidade de explorar padrões em larga escala, avaliar os efeitos de distúrbios ambientais e compreender a estrutura das comunidades de formigas em diferentes contextos ecológicos e geográficos.

**Palavras-chave:** formigas; biodiversidade; aprendizado de máquina; seleção de atributos; ecologia funcional

## Descrição Geral
O **GLAD Optimized Dataset** é uma versão estruturada e otimizada do *Global Ants Database* (GLAD), preparada para aplicação em algoritmos de **aprendizado de máquina supervisionado**. O dataset reúne informações morfológicas, ecológicas e ambientais relacionadas a comunidades de formigas em milhares de localidades ao redor do mundo.

Após pré-processamento (imputação de valores ausentes, padronização e codificação de variáveis categóricas), foram gerados três datasets otimizados, cada um com um **rótulo-alvo específico**:

- **Disturbance**: indica se a localidade apresenta **perturbação antrópica** ou está em condição **não perturbada** (classe binária).
- **Habitat Type**: descreve o **tipo de habitat predominante** em que a comunidade de formigas foi registrada (multiclasse).
- **Continent**: registra o **continente geográfico** da localidade de amostragem (multiclasse).

Todos os datasets estão em formato **CSV**, livres de valores ausentes e prontos para uso em modelos supervisionados.

---

## Estrutura dos Dados
- **Disturbance Optimized Dataset**: 4.389 registros × 80 preditores + `target`
- **Habitat Type Optimized Dataset**: 4.422 registros × 65 preditores + `target`
- **Continent Optimized Dataset**: 4.484 registros × 74 preditores + `target`

---

## Colunas (Features)
As variáveis preditoras foram reduzidas por meio de análise de importância e seleção univariada, resultando em **65 a 80 atributos informativos**. Elas podem ser agrupadas em:

1. **Variáveis geográficas**  
   - `lat`, `lon`, `elev`: latitude, longitude e elevação da localidade de coleta.

2. **Diversidade e abundância**  
   - `tot_ant_abund`: abundância total de formigas.  
   - `tot_nat_sp_rich`: riqueza de espécies nativas.  
   - `tot_non_nat_sp_rich`: riqueza de espécies não nativas.  

3. **Amostragem**  
   - `n_of_samp_ev`: número de eventos de amostragem.  
   - `tot_n_of_tran`: número de transectos.  
   - `len`, `wid`: dimensões da área de amostragem.  
   - `pitfall_n`, `winkler_n`, `berlese_n`: número de armadilhas utilizadas por método.  

4. **Características do habitat**  
   - Colunas codificadas (`hab_*`) indicando diferentes tipos de habitat (ex.: floresta, savana, manguezal).  

5. **Perturbação ambiental**  
   - Colunas derivadas (`disturb_type_*`) descrevendo categorias de distúrbio (ex.: agricultura, urbano, fogo).  

6. **Variáveis adicionais**  
   - Outras relacionadas à coleta ou ao ambiente, retidas pela seleção de atributos.

---

## Targets (Variáveis-Alvo)
- **`target` (Disturbance Dataset):**  
  - `disturbed` – áreas sob efeito de perturbação antrópica.  
  - `undisturbed` – áreas preservadas ou com mínima intervenção.  

- **`target` (Habitat Type Dataset):**  
  - Classes categóricas de habitat, como **forest**, **savanna**, **grassland**, **urban**, entre outras.  

- **`target` (Continent Dataset):**  
  - Categorias geográficas: **Africa**, **Asia**, **Europe**, **North America**, **South America**, **Oceania**.  

---

## Pré-processamento
- **Imputação de valores ausentes**:  
  - Numéricos → `KNNImputer (k=5)`  
  - Categóricos → `SimpleImputer (most_frequent)`  
- **Padronização** → `StandardScaler`  
- **Codificação categórica** → `OneHotEncoder`  
- **Seleção de atributos** → `SelectKBest (chi²)`  
- **Remoção de redundâncias**: exclusão de variáveis quase-constantes e redundantes, como `tot_ant_sp_rich`.

---

## Como usar
```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier

# Exemplo com o dataset de Disturbance
df = pd.read_csv("disturbance_optimized.csv")

X = df.drop(columns=["target"])
y = df["target"]

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, stratify=y, random_state=42
)

clf = RandomForestClassifier(n_estimators=100, random_state=42)
clf.fit(X_train, y_train)
print("Accuracy:", clf.score(X_test, y_test))
