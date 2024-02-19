# Azure-MLAUTOMIZADO

## Configuração de Trabalho de ML Automatizado no Azure Machine Learning Studio
Este guia descreve como configurar um novo trabalho de Machine Learning automatizado no Azure Machine Learning Studio usando a interface de autorização.

### Configurações Básicas
* Nome do Trabalho: mslearn-bike-automl
* Novo Nome do Experimento: mslearn-bike-rental
* Descrição: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
* Marcadores: Nenhum

### Tipo de Tarefa e Dados
* Tipo de Tarefa: Regressão
* Selecionar Conjunto de Dados: Criar um novo conjunto de dados com as seguintes configurações:
* Tipo de Dados: Tabular
* Nome: Aluguel de Bicicletas
* Descrição: Dados históricos de aluguel de bicicletas
* Fonte de Dados: Dos arquivos da web
* URL da Web: https://aka.ms/bike-rentals
* Formato de Arquivo: Delimitado
* Delimitador: Vírgula
* Codificação: UTF-8
* Cabeçalhos de Coluna: Apenas o primeiro arquivo possui cabeçalhos

### Esquema:
* Incluir todas as colunas exceto Caminho
* Revise os tipos detectados automaticamente

### Configurações de Tarefa
* Tipo de Tarefa: Regressão
* Conjunto de Dados: Aluguel de Bicicletas
* Coluna de Destino: Aluguéis (inteiro)
* Configurações Adicionais:
    * Métrica Primária: Raiz do Erro Quadrático Médio Normalizado
    * Explique o Melhor Modelo: Não selecionado
    * Usar Todos os Modelos Suportados: Desmarcado
    * Modelos Permitidos: RandomForest e LightGBM

### Limites
* Máximo de Testes: 3
* Máximo de Testes Simultâneos: 3
* Máximo de Nós: 3
* Limite de Pontuação da Métrica: 0.85
* Tempo Limite: 15 minutos
* Tempo Limite de Iteração: 5 minutos
*  Habilitar Rescisão Antecipada: Selecionado

### Validação e Teste
* Tipo de Validação: Divisão de Validação de Trem
* Porcentagem de Dados de Validação: 10%
* Conjunto de Dados de Teste: Nenhum

### Cálculo
* Tipo de Computação: Sem Servidor
* Tipo de Máquina Virtual: CPU
* Camada de Máquina Virtual: Dedicada
* Tamanho da Máquina Virtual: Standard_DS3_V2
* Número de Instâncias: 1

Agora você pode usar este guia para configurar e executar o trabalho de treinamento automaticamente.

## Avalie o melhor modelo

1. Na guia Visão geral do trabalho automatizado de aprendizado de máquina, observe o melhor resumo do modelo.
2. Selecione o texto em Nome do algoritmo do melhor modelo para visualizar seus detalhes
3. Selecione a guia Métricas e selecione os gráficos residuais e predito_true se eles ainda não estiverem selecionados.

# Implantar e testar modelo

1.  Na guia Modelo do melhor modelo treinado pelo seu trabalho automatizado de machine learning, selecione Implantar e use a opção de serviço Web para implantar o modelo com as seguintes configurações:
  * Nome : prever-aluguéis
  * Descrição : Prever aluguel de bicicletas
  * Tipo de computação : Instância de Contêiner do Azure
  * Habilitar autenticação : selecionado
2. Aguarde o início da implantação – isso pode levar alguns segundos. O status de implantação do endpoint de previsão de aluguel será indicado na parte principal da página como Running .
3. Aguarde até que o status da implantação mude para Succeeded . Isso pode levar de 5 a 10 minutos.

## Testar o serviço implantado

1. No estúdio Azure Machine Learning, no menu esquerdo, selecione Endpoints e abra o ponto final em tempo real de previsão de alugueres .

2. Na página do endpoint em tempo real de previsão de aluguel, visualize a guia Teste .

3. No painel Dados de entrada para testar o endpoint , substitua o modelo JSON pelos seguintes dados de entrada:

## Codigo para teste
```
{
  "Inputs": {
    "data": [
      {
        "day": 5,
        "mnth": 2,
        "year": 2023,
        "season": 0,
        "holiday": 0,
        "weekday": 0,
        "workingday": 0,
        "weathersit": 0,
        "temp": 0.0,
        "atemp": 0.0,
        "hum": 0.0,
        "windspeed": 0.0
      }
    ]
  },
  "GlobalParameters": 0.0
}
```
