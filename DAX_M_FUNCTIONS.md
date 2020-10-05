### DAX Functions
  - __CALCULATE__: apenas UM filtro é aceito como argumento;
  - __FORMAT__: FORMAT([Date], "MMMM DD, YYYY") >  December 01, 2014.
  - __RANK__: RANKX(ALL('Product'), [SalesAmount], DESC, Dense)
    - _Dense:_ Em caso de empate na posição do ranking, todos empatados serão considerados dentro de uma posição só;
    - _Skip:_ Em caso de empate, as posições ocupadas pelos registros empatados serão todas ocupadas;
  - __ALLSELECTED__: Remove filtros de contexto de colunas e linhas na consulta atual, mantendo todos os outros filtros de contexto ou filtros explícitos. 
  - __TOPN()__: TOPN(<10>, <table>, <FUNÇÃO USADA PARA ORDENAR OS VALORES>)
  - __REMOVEFILTERS()__: Remove filtros de tabela ou coluna
  - __FILTER__: FILTER(TABELA, expressão booleana)
  - __ALLCROSSFILTERED(<table>)__: remove todos os filtros da tabela
  - __KEEPFILTER__: Use KEEPFILTERS nas funções de contexto CALCULATE e CALCULATETABLE, para substituir o comportamento padrão dessas funções.
  - __DIVIDE()__:DIVIDE(numerator, denominator [,alternateresult])
  - __ISINSCOPE():__ usada para testar se uma coluna é o nível em uma hierarquia de niveis
  - __CONTAINS__(table, columnName, value[, columnName, value]…)
  - __COUNTAX__: O exemplo a seguir conta o número de linhas que não estão em branco na coluna Phone usando a tabela resultante da filtragem da tabela 
    ```
    Reseller em [Status] = Active- =COUNTAX(FILTER('Reseller',[Status]="Active"),[Phone])
    ```
  - __COUNTA__: A função COUNTA conta o número de células de uma coluna que não estão vazias COUNTA(COLUMN)
  - __COUNTX(table,expression):__ Conta o número de linhas que contêm um valor que não esteja em branco ou uma expressão que é avaliada como um valor que não esteja em branco, ao avaliar uma expressão em uma tabela. Não trabalha com expressões booleanas. 
  - __COUNTROWS(table):__ A função COUNTROWS conta o número de linhas na tabela especificada ou em uma tabela definida por uma expressão.
  - __UNICHAR(number)__:Retorna o caractere Unicode referenciado pelo valor numérico.   
  - __ROLLUP__: Modifica o comportamento da função SUMMARIZE adicionando linhas de valores acumulados ao resultado nas colunas definidas pelo parâmetro groupBy_columnName. Essa função pode ser usada apenas dentro de uma expressão SUMMARIZE.
  ```
  SUMMARIZE(<table>, <groupBy_columnName>[, <groupBy_columnName>]…[, ROLLUP(<groupBy_columnName>[,< groupBy_columnName>…])][, <name>, <expression>]…)
  ```
  
 #### Time Intelligence
  - __CALENDAR()__: você consegue setar a data de inicio e fim;
    - _MONTH, YEAR, STARTOFMONTH_
    - _EOMONTH_: End of month
  - __CALENDARAUTO()__: Identifica automaticamente o inicio e o fim do range de datas;
  - __TOTALYTD__: TOTALYTD(SUM(InternetSales_USD[SalesAmount_USD]),DateTime[DateKey])
  - __PREVIOUSMONTH__: Retorna uma tabela que contém uma coluna de todas as datas do mês anterior, com base na primeira data na coluna dates, no contexto atual.
  - __PREVIOUSYEAR()__: Retorna uma tabela que contém uma coluna de todas as datas do ano anterior, com base na primeira data na coluna dates, no contexto atual.
  - __PARALLELPERIOD():__ Desloca mêses/anos/dias para trás de cada data no contexto do filtro
  - __DATESYTD__: Retorna uma tabela que contém uma coluna das datas do ano até a data, no contexto atual.
  - __DATESQTD__: Retorna uma tabela que contém uma coluna das datas do trimestre até a data, no contexto atual.
  ```CALCULATE ( 
                  SUM ( Vendas[Total Venda] );
                    FILTER (
                        ALL ( CalendarioDAX[Date] );
                        CalendarioDAX[Date] <= MAX ( CalendarioDAX[Date] )
                            && YEAR ( CalendarioDAX[Date] ) = YEAR ( MAX ( CalendarioDAX[Date] ) )
                    )
                )
 ```
 - __SAMEPERIODLASTYEAR()__:mesmo periodo no ultimo ano.Parâmetro: DATA
 - __DATEADD()__: DATEADD(<dates>,<1, 2, 3>,<DIA, MES, ANO>)  
 ### M Language
  - __Table.distinct:__ remove as linhas duplicadas da tabelas. Um parâmetro opcional especifica quais colunas da tabela são testadas para duplicação. 
  ```
    Table.Distinct(table as table, optional equationCriteria as any) as table
  ```
  - __Table.replace:__
   ```
  Text.Replace(the quick brown fox jumps over the lazy dog, the, a)
   ```
  - __Table.ReplaceMatchingRows__ Substitui todas as linhas especificadas na table pelas linhas fornecidas. As linhas a serem substituídas e as substituições são especificadas em replacements, usando a formatação {old, new}. 
  ```
    Table.ReplaceMatchingRows(
    Table.FromRecords({
        [a = 1, b = 2],
        [a = 2, b = 3],
        [a = 3, b = 4],
        [a = 1, b = 2]
    }),
    {
        {[a = 1, b = 2], [a = -1, b = -2]},
        {[a = 2, b = 3], [a = -2, b = -3]}
    }
)
  ```
  - __Table.RenameColumns__: Executa os renomeações fornecidas para as colunas na tabela table. Uma operação de substituição renames consiste em uma lista de dois valores, o nome de coluna antigo e o novo, fornecidos em uma lista.
  - Replaced Errors = 
  ```Table.ReplaceErrorValues(#"Changed Type", {{"Customer Key", 0}}) in #"Replaced Errors"
  ```
  - __Table.TransformRows(Table, função de transformação)__ as list/record: cria uma tabela com base em table, utilizando a função de transformação
  - __Table.TransformColumnTypes__
  ```Table.TransformColumnTypes(
    Table.FromRecords({
        [a = 1, b = 2],
        [a = 3, b = 4]
    }),
    {"a", type text},
    "en-US"
)
 ```
 - __Table.FromRecords__ converte records (lista de registros), em uma tabela; 
