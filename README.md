# Análise de Vendas de Veículos: Do Raw Data ao Dashboard Interativo

## Visão Geral do Projeto

Este projeto demonstra um pipeline completo de Análise de Dados, desde a ingestão e transformação de dados brutos até a criação de um dashboard interativo no Power BI. O objetivo principal é extrair insights valiosos sobre o mercado de vendas de veículos, identificando tendências de preços, modelos populares, desempenho de vendedores e padrões sazonais.

## Problema de Negócio

O mercado de veículos possui uma dinâmica complexa, com preços variando de acordo com o modelo, ano, condições e localização, além de apresentar sazonalidade nas vendas. A falta de uma visão clara e consolidada desses fatores dificulta a tomada de decisões estratégicas para fabricantes, vendedores e consumidores. Este projeto busca preencher essa lacuna, oferecendo ferramentas analíticas para entender e otimizar as operações de venda.

## Conjunto de Dados

O projeto utiliza um conjunto de dados contendo informações detalhadas sobre vendas de veículos, incluindo:
* `ano`: Ano de fabricação do veículo.
* `fabricante`: Marca do veículo.
* `modelo`: Modelo específico do veículo.
* `cambio`: Tipo de transmissão (automática, manual).
* `estado`: Estado onde a venda ocorreu.
* `vendedor`: Nome da concessionária.
* `preco_venda`: Preço final de venda do veículo.
* `data_venda`: Data em que a venda foi realizada.

## Ferramentas e Tecnologias

* **ETL (Extract, Transform, Load):**
    * **PySpark:** Utilizado para manipulação e transformação de grandes volumes de dados (Python Notebook).
    * **Power Query (M Language):** Implementado no Power BI para transformações adicionais e preparação final dos dados.
* **Análise e Visualização de Dados:**
    * **Power BI:** Para modelagem de dados, criação de medidas DAX e desenvolvimento do dashboard interativo.
* **Controle de Versão:**
    * **Git/GitHub:** Para gerenciamento do código-fonte e colaboração.

## Estrutura do Projeto

* `notebooks/`: Contém o notebook Colab (`Case_carros.ipynb`) com o código PySpark para o processo de ETL.
* `data/`: Pasta para os dados de entrada (`car_prices.csv`) e saída (`Carros.csv`).
* `powerbi/`: Contém o arquivo `.pbix` do dashboard Power BI.
* `README.md`: Este arquivo, detalhando o projeto.

## Detalhes do Pipeline de ETL

O processo de ETL foi implementado em duas etapas principais:

### 1. ETL com PySpark (`Case_carros.ipynb`)

Este notebook PySpark realiza a primeira fase robusta de transformação dos dados:
* **Configuração do Ambiente:** Inicialização da sessão Spark e importação das bibliotecas necessárias.
* **Extração:** Carregamento do dataset `car_prices.csv`.
* **Limpeza de Dados:**
    * Verificação e tratamento de valores nulos em colunas críticas (`model`, `sellingprice`, `transmission`).
* **Transformação de Dados:**
    * **Seleção de Colunas:** Focando nas colunas mais relevantes para a análise.
    * **Engenharia de Features - `data_venda`:** A coluna `saledate` original (string com formato complexo como "Tue Dec 16 2014 1...") foi transformada em um formato de data padronizado (`yyyy-MM-dd`) e convertida para o tipo `DateType()` para facilitar análises temporais.
    * **Renomeação de Colunas:** Nomes de colunas foram padronizados para português para melhor legibilidade e consistência com o Power BI (e.g., `year` para `ano`, `sellingprice` para `preco_venda`).
* **Carregamento:** O DataFrame final processado é salvo como um arquivo CSV (`/content/Carros.csv`).

### 2. Preparação de Dados com Power Query (M Language)

Dentro do Power BI, o Power Query foi utilizado para transformações adicionais e garantia da qualidade dos dados:
* **Ingestão:** Os dados são carregados de uma pasta local, utilizando o conector de pasta do Power BI.
* **Tratamento de Tipos:** Garantia de que os tipos de dados estejam corretos (ex: `preco_venda` como `Currency.Type`).
* **Padronização de Texto:** Conversão de texto para maiúsculas em colunas como `cambio`, `estado` e `vendedor` para consistência.
* **Filtragem de Anomalias:** Remoção de valores alfanuméricos incorretos da coluna `estado` que não representavam estados válidos.

## Medidas DAX e Análises

No Power BI, foram criadas medidas DAX para habilitar análises profundas e dinâmicas:
* **`Total Vendas`**: Soma total do `preco_venda`.
* **`Media Vendas`**: Média do `preco_venda`.
* **Variação Percentual (Exemplo):** Embora não implementada no dashboard atual, a estrutura de dados suporta facilmente a criação de medidas avançadas como `Variação Percentual Preco Medio` (do ano anterior para o atual), demonstrando capacidade em cálculos de inteligência de tempo.
* **Formatação:** Todas as medidas financeiras foram formatadas para **Real (R$)** para uma apresentação clara e profissional.

## Dashboard Interativo no Power BI

O dashboard foi projetado para ser intuitivo e fornecer insights rápidos sobre o mercado de vendas de veículos. Ele inclui:
* **Filtros Dinâmicos:** Por `Data`, `Montadora` (Fabricante) e `Vendedor`.
* **Preço Médio por Estado:** Visualização tabular do preço médio de venda de veículos em diferentes estados.
* **Top 10 Modelos Mais Vendidos:** Gráfico de barras mostrando os modelos com maior volume de vendas.
* **Top 5 Maiores Vendedores:** Lista dos vendedores que geraram o maior volume de vendas.
* **Períodos com Maior Número de Vendas:** Gráfico de área destacando a sazonalidade nas vendas ao longo dos meses do ano.

## Como Visualizar e Interagir

1.  **Clone o Repositório:** `git clone https://github.com/vancarlosreis/case_carros`
2.  **Dados:** Certifique-se de ter o arquivo `car_prices.csv` na estrutura de pastas esperada pelo notebook PySpark.
3.  **Executar ETL (PySpark):** Abra `notebooks/Case_carros.ipynb` em um ambiente como Google Colab ou Jupyter e execute todas as células para gerar o arquivo `Carros.csv` processado.
4.  **Abrir Dashboard (Power BI):** Baixe e abra o arquivo `.pbix` localizado em `powerbi/` utilizando o Power BI Desktop.
5.  **Interaja:** Explore os filtros e os visuais para obter diferentes perspectivas sobre os dados.

## Contribuições

Sinta-se à vontade para explorar, sugerir melhorias ou reportar problemas. Contribuições são sempre bem-vindas!

## Contato

Van Carlos Reis
https://www.linkedin.com/in/vancarlosreis/
