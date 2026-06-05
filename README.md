# Inspeção Visual Automática - Classificação de Defeitos em Grãos de Café

## Cenário
**Cenário B**: Inspeção de grãos de café em cooperativa. Classificação de 17 tipos de defeitos em grãos de café verde, seguindo critérios da Classificação Oficial Brasileira (COB).

## Dataset
- **Fonte**: Coffee Green Bean with 17 Defects (Kaggle)
- **Classes**: Broken, Cut, Dry Cherry, Fade, Floater, Full Black, Full Sour, Fungus Damage, Husk, Immature, Parchment, Partial Black, Partial Sour, Severe Insect Damage, Shell, Slight Insect Damage, Withered
- **Total**: ~979 imagens JPG

## Estrutura do Repositório

```
notebooks/
    01_segmentacao.ipynb       # Segmentação dos grãos (Otsu vs Adaptativo)
    02_features.ipynb          # Extração e análise de features
    03_classificacao.ipynb     # Classificação e avaliação
outputs/
    X.csv                      # Tabela de features (979 x 29)
    y.csv                      # Vetor de rótulos (979 x 1)
    tabela_metricas.csv        # Resultados comparativos dos modelos
    *.png                      # Figuras e gráficos (19 arquivos)
archive/                       # Dataset (17 pastas, uma por classe)
requirements.txt               # Dependências
README.md                      # Este arquivo
```

## Como executar

```bash
# 1. Instalar dependências
pip install -r requirements.txt

# 1.1 Se caso o primeiro pip install não funcionar, use esse:
python -m pip install -r requirements.txt

# 2. Executar os notebooks em ordem
jupyter notebook notebooks/01_segmentacao.ipynb
jupyter notebook notebooks/02_features.ipynb
jupyter notebook notebooks/03_classificacao.ipynb
```

## Pipeline

```
Imagem RGB → Pré-processamento (blur) → Segmentação (Otsu) → Extração de Features → Classificação → Avaliação
```

### Features extraídas (29 total):
- **Forma (6)**: area, perímetro, circularidade, solidez, extensão, excentricidade
- **Momentos de Hu (7)**: 7 momentos invariantes em escala logarítmica
- **Cor (12)**: média e desvio padrão de B, G, R, H, S, V
- **Textura (4)**: GLCM - contraste, homogeneidade, energia, correlação

### Classificadores (com GridSearchCV para ajuste de hiperparâmetros):
- SVM (RBF) - melhor modelo (F1 macro ≈ 0.65)
- Random Forest
- KNN

## Dependências
- Python 3.10+
- numpy, pandas, opencv-python, scikit-image, scikit-learn, matplotlib, seaborn

## Equipe
- João Antônio de Souza Vieira Sandes
- Gustavo Godoy

## Licença
Projeto acadêmico - Visão Computacional
