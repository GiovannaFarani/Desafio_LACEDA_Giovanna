# 📊 Desafio LACEDA - Record Linkage (CNEFE)

Este repositório contém a solução para o desafio técnico de cruzamento de dados (Record Linkage). O objetivo do projeto é cruzar uma base local de endereços com a base massiva do CNEFE (Cadastro Nacional de Endereços para Fins Estatísticos) do IBGE, a fim de identificar o Setor Censitário (`COD_SETOR`) de cada endereço.

##⚙️ Metodologia e Pipeline de Dados

Para lidar com o grande volume de dados do CNEFE sem estourar a memória RAM de ambientes como o Google Colab ou computadores pessoais, a solução adota uma abordagem híbrida de funil:

1. **Extração e PySpark:** O Spark é utilizado para ler a base gigante. Filtraei apenas as colunas vitais (`COD_MUNICIPIO`, `NOM_SEGLOGR`, `COD_SETOR`) e isolei os dados referentes apenas aos municípios presentes na base menor.
2. **Conversão e Limpeza (Pandas):** Com a base reduzida, converti a base tratada para Pandas. Apliquei a limpeza de texto (conversão para maiúsculas, remoção de espaços em branco e eliminação de pontuações via RegEx).
3. **Blocagem:** O algoritmo de busca itera sobre a base menor e cria sub-tabelas filtrando os primeiros 6 dígitos do código do município, garantindo que o algoritmo só compare ruas da mesma cidade.
4. **Fuzzy Matching:** Utilização da Distância de Levenshtein para calcular a similaridade entre os nomes das ruas. Se o socore for igual ou superior a 85, o endereço é considerado correspondente e o `COD_SETOR` é extraído.

## 📂 Estrutura do Repositório

- `src/` ou `/` : Contém o notebook principal (`desafio_Giovanna.ipynb`).
- `dados/` : Pasta destinada a armazenar as bases de dados. (A base menor já está incluída. A base gigante do CNEFE deve ser inserida aqui).
- `README.md` : Documentação do projeto.

## 🚀 Como executar este projeto

Como a base oficial do CNEFE possui milhões de linhas e ultrapassa o limite de tamanho do GitHub, ela foi adicionada ao `.gitignore` e **não** está presente neste repositório. Para reproduzir o código perfeitamente, siga os passos abaixo:

1. Faça o clone deste repositório:
   ```bash
   git clone [https://github.com/GiovannaFarani/Desafio_LACEDA_Giovanna.git](https://github.com/GiovannaFarani/Desafio_LACEDA_Giovanna.git)
2. Crie uma pasta chamada dados na raiz do projeto (caso ela não exista).

3. As bases já estão carregadas automaticamente, a maior pelo drive e a menor pelo Github.
4. Apenas é necessário roda o notebook.
