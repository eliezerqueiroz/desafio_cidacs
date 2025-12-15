# Avaliação de Habilidades Técnicas - Análise de Dados do SINASC

Este repositório contém a solução para o desafio técnico do **Núcleo de Produção de Dados (NPD)**. O projeto consiste em um pipeline de Engenharia e Análise de Dados completo, utilizando Python e Pandas para processar, limpar e analisar uma base de dados de Nascidos Vivos (SINASC) entre 2020 e 2022.

## 📋 Sobre o Projeto

O objetivo foi transformar dados brutos (arquivos Parquet fragmentados e dados do IBGE) em informações estruturadas para responder a 17 questões de negócio, focando em:
*   **Performance:** Otimização de uso de memória e tempo de execução.
*   **Qualidade de Dados:** Tratamento robusto de inconsistências, outliers e erros de formatação.
*   **Reprodutibilidade:** Código estruturado para ser executado de ponta a ponta.

---

## 🛠️ Tecnologias Utilizadas

*   **Linguagem:** Python 3.11+
*   **Bibliotecas Principais:**
    *   `pandas`: Manipulação e análise de dados.
    *   `numpy`: Computação numérica.
    *   `matplotlib` & `seaborn`: Visualização de dados.
    *   `pyarrow` & `fastparquet`: Leitura eficiente de arquivos Parquet.
*   **Ambiente:** Jupyter Notebook (VS Code).

---

## 🚀 Destaques da Solução

Durante o desenvolvimento, foram aplicadas estratégias avançadas para lidar com o volume de dados (~4 milhões de registros) e a qualidade das informações:

1.  **Otimização de Memória:** Implementação de uma função de *downcasting* automático de tipos numéricos e conversão de strings para categorias, reduzindo o consumo de memória do DataFrame em **~95%** (de ~4GB para ~200MB).
2.  **Enriquecimento Eficiente:** Substituição da operação padrão de `merge` (que se mostrou lenta e custosa) por uma estratégia de **mapeamento via dicionários (`.map()`)**, acelerando drasticamente o cruzamento com os dados do IBGE.
3.  **Pipeline de Limpeza Robusto:**
    *   Uso de **Expressões Regulares (RegEx)** para extrair dados numéricos de colunas sujas (ex: códigos de município com caracteres especiais).
    *   **Filtros de Sanidade:** Identificação e tratamento de datas implausíveis (ex: nascimentos em 1888) e inconsistências lógicas entre a idade da mãe informada e a calculada.
    *   **Tratamento de Nulos:** Conversão segura para tipos `Int64` do Pandas, preservando a integridade dos dados ausentes.

---

## 📂 Estrutura do Repositório

```text
.
├── analise_sinasc.ipynb   # Notebook principal com todo o código e análises
├── requirements.txt       # Lista de dependências do projeto
├── .gitignore             # Arquivos ignorados (dados brutos, venv, etc.)
└── README.md              # Documentação do projeto
```

> **Nota:** A pasta `sinasc_2020_2022` contendo os dados brutos não está incluída no repositório devido ao tamanho, conforme boas práticas de versionamento.

---

## ▶️ Como Executar o Projeto

Siga os passos abaixo para reproduzir a análise em seu ambiente local:

### 1. Pré-requisitos
Certifique-se de ter o Python 3 instalado.

### 2. Configuração
Clone o repositório e entre na pasta:
```bash
git clone <URL_DO_SEU_REPOSITORIO>
cd desafio_cidacs
```

Crie e ative um ambiente virtual (recomendado):
```bash
# Criar
python3 -m venv venv

# Ativar (macOS/Linux)
source venv/bin/activate

# Ativar (Windows)
venv\Scripts\activate
```

Instale as dependências:
```bash
pip install -r requirements.txt
```

### 3. Dados
Os dados brutos não estão incluídos no repositório devido ao tamanho. Para executar o projeto:

1.  **Baixe a base de dados:** [Acesse aqui (Google Drive)](https://drive.google.com/file/d/1m3zqtP6FdL7Vj4ip1GzI053F97edCv-l/view)
2.  **Descompacte o arquivo zip.**
3.  Certifique-se de que a pasta extraída (chamada `sinasc_2020_2022`) esteja localizada na **raiz** do projeto, exatamente no mesmo nível do notebook `analise_sinasc.ipynb`.


### 4. Execução
Abra o Jupyter Notebook:
1.  Inicie o VS Code ou Jupyter Lab.
2.  Abra o arquivo `analise_sinasc.ipynb`.
3.  Execute as células sequencialmente (Run All).

---

## 📊 Estrutura da Análise

O notebook está dividido em partes lógicas para facilitar a leitura:
*   **Parte 0:** Configuração do ambiente e bibliotecas.
*   **Parte 1:** ETL (Carga dos Parquets, Carga do IBGE via URL, Enriquecimento).
*   **Parte 2:** Pipeline de Limpeza e Engenharia de Features (`IDADE_MAE_CRIADA`, `PESO_LEN`).
*   **Parte 3:** Análise de Qualidade de Dados (QA) e tratamento final de inconsistências.
*   **Parte 4:** Respostas detalhadas para as 17 questões do desafio, incluindo visualizações gráficas onde pertinente.

---

## 👨‍💻 Autor

Projeto desenvolvido como parte do processo seletivo para Engenheiro de Dados.

*   Eliezer Queiroz - [Meu LinkedIn](https://www.linkedin.com/in/eliezer-queiroz/)