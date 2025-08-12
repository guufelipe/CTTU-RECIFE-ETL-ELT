# Projeto de Integração de Dados com ETL e ELT

Este repositório contém o projeto de integração de dados da disciplina de Banco de Dados, realizado em colaboração com outros colegas. O objetivo principal foi consolidar três conjuntos de dados distintos sobre infrações de trânsito em uma única base de dados, utilizando as abordagens **ETL (Extract, Transform, Load)** e **ELT (Extract, Load, Transform)**.

O projeto foi desenvolvido para permitir análises aprofundadas e a geração de insights a partir de uma base de dados coesa e padronizada. O foco está nos registros de Infrações de Trânsito da cidade do Recife, nos anos de 2023, 2024 e 2025.

## Gerenciamento de Dados Grandes (Git LFS)

Este projeto utiliza arquivos de dados grandes que excedem o limite do GitHub. Para lidar com isso, estamos utilizando o **Git Large File Storage (Git LFS)**.

**É necessário ter o Git LFS instalado para conseguir trabalhar com os arquivos da base de dados deste repositório.**

### Como Configurar e Usar o Git LFS:

**Se você não tiver o Git LFS, baixe o instalador no site oficial:** [**https://git-lfs.com/**](https://git-lfs.com/)

1.  **Instale o Git LFS:**
    Verifique se o Git LFS está instalado executando `git lfs install` no seu terminal.
    ```bash
    git lfs install
    ```
2.  **Clone o repositório (se ainda não o fez):**
    ```bash
    git clone [insira aqui o link do seu repositório]
    ```
3.  **Entre no diretório do projeto:**
    ```bash
    cd [nome-do-seu-repositorio]
    ```
4.  **Baixe os arquivos grandes:**
    Após clonar ou puxar atualizações, os arquivos grandes podem aparecer como "ponteiros". Para baixar o conteúdo real dos dados, execute:
    ```bash
    git lfs pull
    ```
    Este comando garantirá que todos os arquivos de dados gerenciados pelo LFS estejam disponíveis em sua máquina.

---

## Estrutura do Repositório

A estrutura de pastas e arquivos está organizada da seguinte forma, de acordo com as etapas do projeto:

* `1-Datasets`: Contém os arquivos originais em formato CSV dos anos de 2023, 2024 e 2025.
* `2-ETL`: Contém o notebook e os scripts do pipeline de ETL, que realiza a transformação dos dados antes de carregá-los no banco de dados.
* `3-ELT`: Contém o notebook e os scripts do pipeline de ELT, que carrega os dados brutos no banco de dados para depois aplicar as transformações.
* `4-Documentos_Finais`: Pasta que armazena a documentação final do projeto, incluindo diagramas, relatórios e a apresentação.
* `README.md`: Este arquivo, que oferece uma visão geral do projeto e suas instruções.

## 1. Abordagem ETL (Extract, Transform, Load)

### Objetivo
Demonstrar um pipeline de ETL para processar dados de infrações de trânsito. Os dados são lidos de arquivos CSV, transformados no ambiente do notebook Python e, em seguida, carregados em um banco de dados PostgreSQL.

### Fluxo de Trabalho
Para executar o pipeline de ETL:
1.  Primeiro, execute o notebook `concat.ipynb` na pasta `1-Datasets` para concatenar os arquivos CSV dos anos 2023, 2024 e 2025 em uma única base.
2.  Em seguida, abra e execute as células do notebook `processos.ipynb` na pasta `2-ETL`. Este notebook realizará as transformações necessárias na base de dados concatenada.

### Transformações Realizadas
Antes de carregar os dados, as seguintes transformações foram aplicadas para garantir a uniformidade e a qualidade dos dados:
* **Padronização de Datas:** Uniformização do formato das colunas de data (`datainfracao` e `data_implementacao`) para o padrão `YYYY-MM-DD`.
* **Renomeação de Colunas:** As colunas foram renomeadas para nomes mais legíveis e padronizados, como de `'datainfracao'` para `'data_infracao'`.
* **Divisão de Colunas:** A coluna `'amparo_legal'` foi dividida nas colunas `'artigo'` e `'subdivisao_artigo'`.
* **Tratamento de Valores:** Foram tratados valores indesejados e nulos nas colunas de `artigo`, `subdivisao_artigo` e `agente_equipamento`, substituindo-os por "Não informado".
* **Padronização de Tipos de Dados:** Os tipos de dados das colunas foram ajustados para o formato correto.

## 2. Abordagem ELT (Extract, Load, Transform)

### Objetivo
Demonstrar um pipeline de ELT, onde os dados de infrações de trânsito são lidos de arquivos CSV, carregados brutos em um banco de dados PostgreSQL (via Supabase) e, só então, transformados diretamente no banco de dados.

### Fluxo de Trabalho
1.  **Extração (Extract):** O notebook lê os arquivos CSV dos anos de 2023, 2024 e 2025.
2.  **Carga (Load):** Os dados são carregados em sua forma bruta para uma tabela no banco de dados PostgreSQL, utilizando o `sqlalchemy` e as credenciais configuradas.
3.  **Transformação (Transform):** As transformações são aplicadas diretamente no banco de dados através de comandos SQL. Essas transformações incluem:
    * **Tratamento de Colunas de Data e Hora:** Conversão e renomeação das colunas de data (`datainfracao`, `dataimplantacao`) e hora (`horainfracao`).
    * **Renomeação de Colunas:** Ajustes nos nomes das colunas (`agenteequipamento`, `descricaoinfracao`, `localcometimento`) para maior clareza.
    * **Divisão da Coluna `amparolegal`:** Divisão da coluna em `artigo` e `subdivisao_artigo` para melhor granularidade.

## Como Executar os Notebooks

### Pré-requisitos
* **Bibliotecas Python:** Instale as bibliotecas necessárias executando o comando:
    ```
    pip install pandas sqlalchemy psycopg2-binary
    ```
* **Ambiente:** É necessário ter a extensão do Jupyter Notebook instalada no VS Code ou utilizar o Google Colab.
* **Banco de Dados:** Para os processos de carga e transformação, certifique-se de ter um banco de dados PostgreSQL disponível e as credenciais de acesso configuradas.

### Passos
1.  Certifique-se de que os arquivos CSV (`infracoes_2023.csv`, `infracoes_2024.csv`, `infracoes_2025.csv`) estejam presentes na pasta `1-Datasets`.
2.  Siga as instruções nas seções "Abordagem ETL" e "Abordagem ELT" para executar os notebooks correspondentes.

## Documentos Finais

Os resultados e as análises do projeto estão disponíveis na pasta `4-Documentos_Finais`, que inclui:
* Diagrama das colunas, representando as alterações feitas nos dados.
* Relatório completo do projeto.
* Apresentação em slides.

## Repositório Oficial e Colaboradores

Este projeto foi desenvolvido em equipe. Você pode encontrar o repositório original (utilizado durante a disciplina) e informações sobre os demais colaboradores no link abaixo.

* **Link do Repositório Oficial**: https://github.com/dudalbuquerque/ETL-ELT/blob/main/ELT/ELT.ipynb

---