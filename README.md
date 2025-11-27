# Algoritmo de Treinamento YOLOv8 para Detecção em Canteiros de Obras

Este repositório contém notebooks para treinar modelos YOLOv8 de detecção de objetos em canteiros de obras, utilizando diferentes estratégias de dataset e técnicas de data augmentation.

## Datasets utilizados

##### Imagens sintéticas
https://drive.google.com/drive/folders/1olY2FIPhVUBlvh5Rw_1fJ0fZsc9kvpnP?usp=sharing

##### Imagens reais
https://huggingface.co/datasets/LouisChen15/ConstructionSite

## Objetivo

Treinar modelos de detecção para identificar dois tipos de objetos em canteiros de obras:
- `machine`: Máquinas e equipamentos
- `worker`: Trabalhadores

## Estrutura do Projeto

```
training-algorithm/
├── notebooks/
│   ├── imgs_reais.ipynb
│   ├── imgs_reais_augmentation.ipynb
│   ├── imgs_sinteticas.ipynb
│   ├── imgs_sinteticas_augmentation.ipynb
│   ├── imgs_somadas.ipynb
│   └── imgs_somadas_aug.ipynb
└── README.md
```

## Descrição dos Notebooks

### 1. [imgs_reais.ipynb](notebooks/imgs_reais.ipynb)
**Dataset**: Imagens reais apenas
**Treinamento**: 304 imagens
**Validação**: 400 imagens
**Augmentation**: Não

### 2. [imgs_reais_augmentation.ipynb](notebooks/imgs_reais_augmentation.ipynb)
**Dataset**: Imagens reais com augmentation
**Treinamento**: 1.769 imagens
**Validação**: 400 imagens
**Augmentation**: Sim

### 3. [imgs_sinteticas.ipynb](notebooks/imgs_sinteticas.ipynb)
**Dataset**: Imagens sintéticas apenas
**Treinamento**: 304 imagens
**Validação**: 400 imagens
**Augmentation**: Não

### 4. [imgs_sinteticas_augmentation.ipynb](notebooks/imgs_sinteticas_augmentation.ipynb)
**Dataset**: Imagens sintéticas com augmentation
**Treinamento**: 1.773 imagens
**Validação**: 400 imagens
**Augmentation**: Sim (aplicado durante o treinamento)

### 5. [imgs_somadas.ipynb](notebooks/imgs_somadas.ipynb)
**Dataset**: Imagens reais + sintéticas (combinadas)
**Treinamento**: ~608 imagens
**Validação**: ~800 imagens
**Augmentation**: Não

### 6. [imgs_somadas_aug.ipynb](notebooks/imgs_somadas_aug.ipynb)
**Dataset**: Imagens reais + sintéticas com augmentation
**Treinamento**: 3.556 imagens
**Validação**: 800 imagens
**Augmentation**: Sim

## Configuração Padrão de Treinamento

Todos os notebooks utilizam a seguinte configuração padrão:

```python
EPOCHS = 200              # Número máximo de épocas
BATCH_SIZE = 16           # Tamanho do batch
IMAGE_SIZE = 1280         # Resolução da imagem
MODEL_SIZE = 'l'          # YOLOv8 Large
PATIENCE = 50             # Early stopping
DEVICE = 0                # GPU
OPTIMIZER = 'auto'        # Otimizador automático
SEED = 42                 # Seed para reprodutibilidade
```

## Integração com Roboflow

Todos os notebooks se conectam ao Roboflow para baixar os datasets:

```python
ROBOFLOW_API_KEY = "cN0yG1huh8mBnMJ4TUHv"
WORKSPACE_NAME = "tcc-hhkda"
PROJECT_NAME = "<nome-do-projeto>"
VERSION = <versão>
```

## Salvamento de Resultados

Os resultados são automaticamente salvos no Google Drive:

- Pasta completa de treinamento
- Melhor modelo (`best.pt`)
- Último modelo (`last.pt`)
- Métricas e gráficos de treinamento
- Parâmetros do treinamento (em alguns notebooks)

## Requisitos

- Python 3.8+
- Ultralytics YOLOv8
- Roboflow
- GPU para treinamento

## Modelo

Utiliza o **YOLOv8 Large** pré-treinado no COCO dataset, com fine-tuning para detecção em canteiros de obras.

## Classes Detectadas

- **machine** (ID: 0): Máquinas e equipamentos de construção
- **worker** (ID: 1): Trabalhadores no canteiro de obras
