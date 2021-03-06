# Google-Trends
Este repositório é um trabalho desenvolvido pelo Grupo A do projeto Covid Data Analytics (veja mais em covid.dcc.ufmg.br). Aqui é desenvolvida a coleta de dados relativos ao Google Trends e o calculo de suas correlações com os indicadores oficiais de Minas Gerais e do Brasil disponíveis na pasta de indicadores epidemiológicos do seguinte repositório do projeto:https://github.com/CDA-EPCWeb/Tratamento-de-dados/tree/master/Indicadores%20Epidemiol%C3%B3gicos/resultados, na forma do arquivo indicadores.db. Além disso, são geradas diferentes visualizações para os dados obtidos.

# Objetivos
O objetivo principal desse repositório é explorar a possibilidade de se prever a progressão dos indicadores oficiais new week cases(novos casos na semana) e new week deaths(novas mortes na semana) a partir do aumento ou a redução das buscas por certos termos no Google, usando, para isso, a correlação de Spearman ou Pearson entre esses dados.

# Pré-requisitos: jupyter
Para conseguir executar os notebooks(arquivos .ipynb) é necessário, primeiramente, fazer o download de Python(disponível em:https://www.python.org/) ou da interface de Python anaconda (disponível em:https://anaconda.org/anaconda/python). Após isso, deve-se instalar a extensão jupyter notebooks, o que pode ser feito das seguintes maneiras:

1-Abra o python powershell ou o anaconda prompt. Digite: pip install jupyterlab

2-Alternativamente, caso tenha escolhido instalar anaconda, pode-se digitar conda install -c conda-forge jupyterlab.

# Pré-requisitos: bibliotecas
Para a execução dos notebooks desse repositório, são necessárias algumas bibliotecas além das padrões de python. Essas são: Pandas, Matplotlib, Sqlite3, numpy, pytrends, wordcloud, scikit-learn, statsmodels e pmdarima. Elas podem ser instaladas digitando os seguintes comandos em python powershell ou anaconda prompt:

pip install pandas

pip install matplotlib

pip install numpy

pip install pysqlite3

pip install pytrends

pip install wordcloud

pip install -U scikit-learn

pip install statsmodels

pip install pmdarima

# Bases de dados
A base de dados utilizada para os indicadores oficiais é gerada por outro repositório do projeto CDA e está disponíel em: https://github.com/CDA-EPCWeb/Tratamento-de-dados/tree/master/Indicadores%20Epidemiol%C3%B3gicos/resultados. Ela possui 9 indicadores: (novos casos, casos acumulados, novos óbitos, óbitos acumulados, incidencia, letalidade, mortalidade, fator de crescimento e prevalência) para cada, macrorregião, estado, município e para o país como um todo. Porém, para os fins da análise desse repositório só serão usados os novos casos e novos óbitos do Brasil e de Minas Gerais.

Outra base de dados utilizada é a base de dados queries categorizadas, que contém 124 termos relevantes, que foram frequentemente pesquisados, divididos em categorias mais gerais e subcategorias. Essas keywords são aquelas que serão utilizadas para as consultas no Google Trends.

# GtrendsQuery.ipynb
Esse notebook é o responsável pela consulta do Google Trends gerada. Para sua execução é necessária a instalação das bibliotecas pandas, sqlite3, pytrends e numpy, além dos bancos de dados indicadores.db e Queries categorizadas.csv. A partir disso, o script realizará as consultas relativas às semanas epidemiológicas 9 a 52 e salvará as series temporais resultantes no arquivo SeriesKeywords.csv e SeriesKeywordsMG.csv, que possuem, respectivamente, os dados quanto ao Brasil e Minas Gerais.

# correlacaoAnalise.ipynb
Esse notebook é o responsável por realizar o calculo de correlação e a partir dele gerar diferentes visualizações para os dados, notávelmente, gráficos de linha, scatter plots e wordclouds. Para sua execução são necessárias as bibliotecas pandas, sqlite3, numpy, matplotlib e wordcloud, além dos arquivos gerados por GtrendsQuery.ipynb, indicadores.db e Queries categorizadas.csv. O algoritmo utilizado para os bubblegraphs foi baseado em https://matplotlib.org/devdocs/gallery/misc/packed_bubbles.html

O output do código são os arquivos que podem ser vistos nas diversas pastas desse repositório: as spreadsheets da pasta Correlations, os gráficos da pasta Sintomas, os gráficos da pasta Top10, as wordclouds da pasta Wordclouds e os bubble graphs da pasta Bubbles.

# lagCorrelations.ipynb
Esse notebook é o responsável por realizar o calculo das correlações com lag, encontrando o intervalo de tempo que gera a melhor correlação (e consequentemente a melhor previsão dos indicadores a partir dos dados Google Trends). Para sua execução são necessárias as bibliotecas pandas e sqlite3, além dos arquivos gerados por GtrendsQuery.ipynb e indicadores.db.

O output do código são as maiores lag correlations encontradas. Além disso, o código permite encontrar todas correlações para um lag específico.

# Regressao.ipynb
Esse notebook realiza o calculo da regressão entre as keywords do Google trends e os indicadores, de diferentes formas, buscando fazer um forecast dos dados de interesse. Para sua execução são necessárias as bibliotecas matplotlib, numpy, pandas, sqlite3, scikit learn, statsmodels e pmdarima.

O output do código são diferentes regressões em relação aos dados.

# Metodologia de tratamento
Para a seleção dos termos de busca, inicialmente foi conduzido um levantamento piloto de dezenas de palavras que potencialmente poderiam relacionar-se às variações dos números de casos reais na série temporal. Para isso, foram considerados termos relacionados a sintomas da síndrome gripal, bem como alguns mais específicos do adoecimento por infecção pelo novo coronavírus. A experiência de isolamento social, as mudanças de hábitos impostas pela pandemia, as medidas de prevenção, os insumos hospitalares em popularidade midiática ascendente e os nomes de medicamentos em estudo também foram considerados para esta primeira seleção. Na sequência, um relatório com dados de busca de tais termos nos últimos doze meses e nos últimos cinco anos foi elaborado, contendo os gráficos gerados a partir dos dados obtidos no Google Trends e a justificativa para o interesse em se considerar cada termo. Por fim, por consenso dos pesquisadores das áreas da saúde e da ciência da computação envolvidos no projeto, foram definidos 124 termos-chave. Foram critérios de inclusão definitiva a associação na mídia e no ambiente clínico com a experiência de contato pessoal, direto ou indireto, com a COVID-19, bem como o padrão de variação previamente verificado como interessante para posteriores cálculos de correlação com dados epidemiológicos

# Resultados
Esse repositório ao fim da execução desses vários notebooks gera não somente as correlações entre os indicadores e as keywords utilizadas, como também diversas visualizações, o que permite uma mais fácil observação de relações entre esses dois dados, que podem ser vistas, por exemplo, por meio de gráficos como os abaixo:

![image](https://user-images.githubusercontent.com/57831311/115241132-dd4ad500-a0f6-11eb-882c-2a676fa3b1b9.png) ![image](https://user-images.githubusercontent.com/57831311/115241163-e340b600-a0f6-11eb-8ce8-e00d2a5f4e58.png)
![image](https://user-images.githubusercontent.com/57831311/111805981-464cec00-88b0-11eb-8991-759401a4d791.png)

Outro resultado são imagens de facil interpretação no geral, como os bubble graphs e wordclouds, nos quais o tamanho da bolha e palavra, respectivamente, indica quão alta é a correlação. Exemplos da aplicação desses métodos na pesquisa incluem:
Bubble graph das correlações em relação aos novos casos em MG(azul=positivo, vermelho=negativo):
![image](https://user-images.githubusercontent.com/57831311/111805902-37663980-88b0-11eb-8f37-cf71afa45f44.png)
Wordcloud das correlações em relação aos novos casos em MG a partir de seu valor absoluto:
![image](https://user-images.githubusercontent.com/57831311/111806063-5bc21600-88b0-11eb-822f-89044d881205.png)

Por fim, um resultado importante dos arquivos desse repositório foi a produção de diversas previsões, buscando encontrar aquela mais adequada para a pandemia.
Algumas dessas previsões podem ser vistas no gráfico abaixo:
![image](https://user-images.githubusercontent.com/57831311/120321873-2f684400-c2ba-11eb-9226-f25bdb7ea696.png)


