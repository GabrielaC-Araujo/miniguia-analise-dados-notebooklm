# miniguia-analise-dados-notebooklm

Projeto prático da DIO explorando o NotebookLM para criar um guia de estudos em Análise de Dados.

---

## 1. Contexto e Objetivos

### Contexto

Com o mercado global inteiramente guiado por dados, a habilidade de extrair, limpar e transformar grandes volumes de informação é o pilar fundamental para qualquer análise preditiva ou tomada de decisão estratégica. A linguagem Python, liderado por bibliotecas como **Pandas** e **NumPy**, tornou-se padrão para essas tarefas devido à sua flexibilidade e eficiência.

### Objetivos de Estudo

O objetivo central deste caderno temático é servir como um hub de consulta rápida e consolidação de conhecimento sobre os processos de:

* **Carga de Dados:** Leitura eficiente de diferentes formatos de arquivos (CSV, Excel, JSON).
* **Limpeza de Dados:** Identificação e tratamento de valores ausentes (*missing data*), remoção de duplicatas e correção de tipos de dados.
* **Manipulação de Bases de Dados:** Filtragem, agrupamento (*groupby*), junções (*merges/joins*) e transformações estruturais de DataFrames.

---

## 2. Curadoria de Fontes

Para alimentar o NotebookLM e garantir respostas precisas e contextualizadas, foram selecionadas fontes abertas in formato de texto e referências de vídeo:

### Fontes de Texto e Documentação

1. **Introdução à Análise de Dados (Python e Pandas) - Kaggle**
   * *Link:* [Kaggle Notebook - Pandas](https://www.kaggle.com/code/joaoavf/introducao-a-analise-de-dados-python-e-pandas)
2. **Guia Prático de NumPy - Kaggle**
   * *Link:* [Kaggle Notebook - NumPy](https://www.kaggle.com/code/ayushsaklani/numpy)
3. **Introdução à Análise Exploratória de Dados com Python - ResearchGate**
   * *Link:* [Artigo ResearchGate](https://www.researchgate.net/profile/Gesiel-Lopes/publication/336778766_Introducao_a_Analise_Exploratoria_de_Dados_com_Python/links/5db225d2a6fdccc99d9426f2/Introducao-a-Analise-Exploratoria-de-Dados-com-Python.pdf)
4. **Livro: Python para Análise de Dados (Google Books - Ref 1)**
   * *Link:* [Google Books - Referência 1](https://books.google.com.br/books?hl=pt-BR&lr=&id=Oj5FDwAAQBAJ&oi=fnd&pg=PA4&dq=python+analise+de+dados&ots=ZYO4oMKz4y&sig=gr2OFhvKKu_p40g-bmZjUZEAooI&redir_esc=y#v=onepage&q&f=false)
5. **Livro: Python para Análise de Dados (Google Books - Ref 2)**
   * *Link:* [Google Books - Referência 2](https://books.google.com.br/books?hl=pt-BR&lr=&id=ILFwDwAAQBAJ&oi=fnd&pg=PA13&dq=python+analise+de+dados&ots=sQ5eTeigks&sig=YHfDqN8qUvIWAzNlxmrAsNt7vzI&redir_esc=y#v=onepage&q&f=false)

### Fontes de Vídeo

* Seleção de 11 vídeos especializados do YouTube cobrindo desde lógica de programação com Python até manipulação avançada de DataFrames.
  * https://www.youtube.com/watch?v=MKg2s34TEtI
  * https://www.youtube.com/watch?v=QgWoNFdYk04
  * https://www.youtube.com/watch?v=6dx3LYk_h8A
  * https://www.youtube.com/watch?v=1JpYOqvDJNU
  * https://www.youtube.com/watch?v=TMfMkgLkeBQ
  * https://www.youtube.com/watch?v=wnGsAOPKjLo
  * https://www.youtube.com/watch?v=sODNyvVW8wY
  * https://www.youtube.com/watch?v=LZDZ0AZmWHI
  * https://www.youtube.com/watch?v=xECXZ3tyONo
  * https://www.youtube.com/watch?v=LidaJMcVmu4
  * https://www.youtube.com/watch?v=zI5ducyfyNc

---

## 3. Engenharia de Prompts e "Cicatrizes" (Troubleshooting)

### Prompt de Teste Executado

* **Comando enviado:** *"Me explique como limpar dados usando o Pandas."*
* **Resposta obtida da IA:**

> "A limpeza de dados, muitas vezes chamada de etapa de "Transformação" no processo de ETL (Extract, Transform, Load), é uma das tarefas que mais consome tempo no dia a dia de um analista de dados. O Pandas oferece diversas ferramentas para identificar e corrigir inconsistências.
> Aqui estão os principais passos para limpar dados usando o Pandas, conforme as fontes:
> 
> **1. Tratamento de Valores Nulos (Vazios)**
> Os valores nulos aparecem no Pandas como NaN (Not a Number).
> * Identificação: Use `df.isnull().sum()` para contar quantos valores nulos existem em cada coluna. O comando `df.info()` também mostra o total de valores "non-null".
> * Remoção: O método `df.dropna()` exclui linhas que contenham pelo menos um valor vazio. É possível usar o parâmetro `subset=['coluna']` para remover apenas linhas onde colunas específicas estão vazias.
> * Preenchimento: Use `df.fillna(valor)` para substituir os vazios por um valor padrão (como "Online" ou "0") ou pela média da própria coluna.
> 
> **2. Remoção de Duplicatas**
> Dados repetidos podem distorcer as análises.
> * Use `df.drop_duplicates()` para remover linhas idênticas.
> * O parâmetro `subset=['coluna']` permite definir quais colunas considerar para identificar a duplicata (por exemplo, remover linhas com o mesmo ID de pedido).
> 
> **3. Correção de Tipos de Dados**
> Muitas vezes, números ou datas são importados incorretamente como texto (object).
> * Conversão Numérica: Use `df['coluna'].astype(float)` ou `int` para converter tipos.
> * Datas: Use `pd.to_datetime(df['coluna'], format='...')` para transformar textos em objetos de data reais, permitindo análises temporais.
> 
> **4. Padronização de Strings (Textos)**
> Textos com espaços extras ou capitalização diferente (ex: "RIO" e "rio") são tratados como valores distintos se não forem limpos.
> * Espaços: `df['coluna'].str.strip()` remove espaços em branco inúteis no início e no fim das frases.
> * Capitalização: Use `str.title()`, `str.upper()` ou `str.lower()` para garantir que todos os textos sigam o mesmo padrão de letras maiúsculas/minúsculas.
> * Substituição: `str.replace(',', '.')` é útil para corrigir separadores decimais ou remover caracteres especiais como parênteses de números.
> 
> **5. Ajuste de Colunas e Índices**
> * Renomear: Use `df.rename(columns={'nome_antigo': 'nome_novo'})` para tornar os nomes das colunas mais intuitivos.
> * Excluir colunas: Se uma coluna for inútil, use `df.drop(columns=['coluna'])`.
> * Resetar Índice: Após filtrar ou ordenar a base, os números das linhas podem ficar bagunçados. Use `df.reset_index(drop=True)` para reordenar os índices de 0 até o final.
> 
> Dica importante: Lembre-se que muitas dessas funções não alteram o DataFrame original automaticamente. Para salvar as alterações, você deve atribuir o resultado de volta à variável (ex: `df = df.dropna()`) ou usar o parâmetro `inplace=True` quando disponível"

### Análise Crítica e "Cicatriz" (Troubleshooting)

* **O que funcionou bem:** A IA estruturou muito bem a resposta, cobrindo os pilares fundamentais (Nulos, Duplicatas, Tipos, Strings e Índices). A inclusão do lembrete sobre o `inplace=True` ao final foi um excelente ponto de maturidade técnica que a IA extraiu dos textos.
* **A "Cicatriz" / Ponto de Melhoria:** Como o comando inicial foi muito aberto a resposta gerada foi de um panorama geral. Portanto, para extrair respostas mais profundas, é necessário restringir o escopo do prompt, instruindo a IA a focar em cenários práticos específicos.

---

## 4. Miniguia de Estudo (Entrega Final)

### Resumos Estruturados do Assunto

Este resumo estruturado aborda a análise de dados com Python, focando nas bibliotecas NumPy e Pandas, além de descrever o papel e o fluxo de trabalho do analista de dados.

#### 1. A Profissão de Analista de Dados
O analista de dados é o profissional responsável por coletar, organizar e analisar dados para extrair informações que auxiliem na tomada de decisões de negócio. Seu dia a dia é dinâmico e focado em resolver problemas específicos de áreas como marketing, finanças e logística.
* **Tipos de Análise:** A atuação pode ser dividida em análise descritiva (o que aconteceu), diagnóstica (por que aconteceu), preditiva (o que acontecerá) e prescritiva (o que deve ser feito).
* **Rotina e Desafios:** Grande parte do tempo é dedicada à limpeza e exploração de dados, tarefas muitas vezes "invisíveis", mas cruciais para garantir que as conclusões sejam baseadas em dados íntegros.

#### 2. NumPy: Computação Numérica Eficiente
O NumPy (Numerical Python) é a biblioteca base para computação científica e estatística em Python. Sua principal estrutura é o ndarray (array n-dimensional), que é significativamente mais rápido e eficiente em termos de memória do que as listas nativas do Python.
* **Vantagens:** Permite operações vetorizadas (aplicar cálculos em todo o conjunto de uma vez) sem a necessidade de loops explícitos (for), o que acelera o processamento de grandes volumes de dados.
* **Funcionalidades:** Inclui suporte para álgebra linear, geração de números aleatórios e funções matemáticas complexas.

#### 3. Pandas: A Ferramenta de Manipulação de Dados
O Pandas é considerado o "Excel do Python", sendo a biblioteca mais utilizada para manipulação e análise de dados estruturados. Ele facilita o processo de ETL (Extração, Transformação e Carga).
* **Estruturas Principais:** Trabalha com Series (unidimensionais, como colunas) e DataFrames (bidimensionais, como tabelas).
* **Importação:** Suporta diversos formatos, como CSV, Excel, SQL, JSON e HTML.
* **Inspeção Inicial:** Comandos como `head()`, `tail()`, `info()` e `describe()` permitem visualizar rapidamente a estrutura, tipos de dados e estatísticas básicas da base.

#### 4. Limpeza e Tratamento de Dados
Esta etapa visa corrigir inconsistências identificadas na inspeção.
* **Valores Nulos (NaN):** Podem ser removidos com `dropna()` ou preenchidos com `fillna()` (usando médias ou valores padrão).
* **Padronização de Strings:** Uso de métodos como `str.strip()` para remover espaços e `str.title()` ou `str.upper()` para uniformizar a capitalização.
* **Correção de Tipos e Duplicatas:** Conversão de textos para datas ou números com `astype()` e `pd.to_datetime()`, além da remoção de linhas repetidas com `drop_duplicates()`.

#### 5. Análise e Engenharia de Dados
Após a limpeza, o analista realiza transformações para extrair valor.
* **Criação de Colunas:** Novas variáveis podem ser geradas através de cálculos entre colunas existentes ou lógicas condicionais usando `np.where()`.
* **Agrupamentos:** O método `groupby()` é essencial para resumir dados por categorias (ex: faturamento médio por loja).
* **Junção de Bases:** O `merge()` combina tabelas diferentes através de chaves comuns (similar ao JOIN do SQL), enquanto o `concat()` empilha bases com a mesma estrutura.

#### 6. Visualização de Dados
A visualização transforma informações em conhecimento para os stakeholders. O Pandas possui integração com o Matplotlib para gráficos simples, mas bibliotecas como Seaborn e Plotly são recomendadas para visualizações mais sofisticadas, estéticas ou interativas. São utilizados gráficos de barras, linhas, histogramas, boxplots e gráficos de dispersão conforme a mensagem que se deseja passar.

### Prompts Reutilizáveis para Revisões Futuras

Abaixo estão os prompts validados que você pode copiar e colar no seu NotebookLM para revisar os conteúdos:

* **Prompt para Revisão de Carga/Performance:**
  > "Explique quais são as estratégias recomendadas nas fontes para otimizar a leitura de arquivos CSV de grande porte utilizando o Pandas."

* **Prompt para Simulação de Entrevistas Técnicas:**   
  > "Com base no material de Análise Exploratória, faça 3 perguntas difíceis sobre manipulação de dados (merge vs join, groupby complexo) para que eu possa testar meus conhecimentos. Aguarde eu responder uma por uma."
