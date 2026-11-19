# banknote-classification
Classificação de cédulas usando XGBoost e Amazon SageMaker

# Classificação de Cédulas com Aprendizado de Máquina

## Sobre o projeto

Projeto desenvolvido para criar uma esteira de aprendizado de máquina capaz de classificar cédulas como autênticas ou falsificadas, utilizando o algoritmo XGBoost no Amazon SageMaker.

## Base de dados

Foi utilizada a base **Banknote Authentication**, disponível no [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/267/banknote+authentication).

A base possui 1.372 registros e quatro características numéricas: `variance`, `skewness`, `curtosis` e `entropy`. A coluna `class` representa a classificação da cédula.

## Etapas do projeto

1. Carregamento da base de dados.
2. Análise exploratória e estatísticas descritivas.
3. Remoção de registros duplicados.
4. Divisão dos dados em treinamento (60%), validação (20%) e teste (20%).
5. Normalização da coluna `variance`.
6. Preparação dos arquivos CSV e armazenamento no Amazon S3.
7. Configuração e treinamento do modelo XGBoost no SageMaker.
8. Avaliação usando acurácia e matriz de confusão.
9. Previsão individual com o modelo implantado.

## Resultados

Após a remoção de 24 registros duplicados, a base ficou com 1.348 registros.

O modelo apresentou **98,52% de acurácia** no conjunto de teste, com 266 classificações corretas e 4 incorretas.

Também foi realizada uma previsão individual com um registro do conjunto de teste, e o modelo classificou a cédula corretamente.

## Tecnologias utilizadas

- Python
- Pandas e NumPy
- Scikit-learn
- Matplotlib
- XGBoost
- Amazon SageMaker
- Amazon S3
- Boto3
- Jupyter Notebook

## Como executar o projeto

**1. Preparar o ambiente**

Utilizar um ambiente Python com Jupyter Notebook e acesso à AWS, com permissões para usar o Amazon S3 e o Amazon SageMaker.

O projeto foi desenvolvido no laboratório AWS Academy, utilizando o kernel `conda_python3` e a biblioteca SageMaker SDK 2.189.0.

**2. Baixar o notebook**

Baixar o arquivo `banknote_classification.ipynb` deste repositório e abri-lo no JupyterLab.

**3. Instalar as bibliotecas**

Executar a célula de instalação no início do notebook:

```python
%pip install scikit-learn matplotlib "cloudpickle==2.2.1"
```

O ambiente também precisa ter `pandas`, `numpy`, `boto3` e `sagemaker` disponíveis. O projeto utilizou o contêiner XGBoost 1.7-1 do SageMaker.

**4. Configurar a AWS**

Na etapa 7 do notebook, alterar a variável `bucket` para o nome de um bucket S3 ao qual o ambiente tenha acesso.

Também é necessário ter uma função de execução (IAM role) com as permissões necessárias para treinamento e implantação no SageMaker.

**5. Executar as etapas**

Executar as células na ordem apresentada no notebook.

A base de dados é carregada diretamente do UCI Machine Learning Repository. Depois, os dados são preparados, divididos e enviados ao S3.

O treinamento é realizado no SageMaker, utilizando uma instância `ml.m5.large`.

**6. Avaliar o modelo**

Após o treinamento, o notebook implanta o modelo em um endpoint para realizar as previsões.

Os resultados são avaliados usando acurácia e matriz de confusão. Também é realizada uma previsão individual com um registro do conjunto de teste.

**7. Encerrar os recursos**

Ao finalizar as previsões, executar a etapa de salvamento do modelo e exclusão do endpoint.

## Arquivo do projeto

`banknote_classification.ipynb` — notebook com os códigos, as etapas da esteira e os resultados obtidos.
