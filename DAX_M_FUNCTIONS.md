### DAX Functions
  - __CALCULATE__: apenas UM filtro é aceito como argumento;
  - __FORMAT__: FORMAT([Date], "MMMM DD, YYYY") >  December 01, 2014.

  - __RANK__: RANKX(ALL('Product'), [SalesAmount], DESC, Dense)
    - _Dense:_ Em caso de empate na posição do ranking, todos empatados serão considerados dentro de uma posição só;
    - _Skip:_ Em caso de empate, as posições ocupadas pelos registros empatados serão todas ocupadas;
  - __ALLSELECTED__: Remove filtros de contexto de colunas e linhas na consulta atual, mantendo todos os outros filtros de contexto ou filtros explícitos. 
 - __SAMEPERIODLASTYEAR()__:
 - __DATEADD()__:
 - __TOPN()__:
 - __REMOVEFILTERS()__:
 - __FILTER__:
 - __KEEPFILTER__
 - __DIVIDE()__
 - ISINSCOPE(): usada para testar se uma coluna é o nível em uma hierarquia de niveis
 #### Time Intelligence
   - __CALENDAR()__: você consegue setar a data de inicio e fim;
    - _MONTH, YEAR, STARTOFMONTH_
    - _EOMONTH_: End of month
  - __CALENDARAUTO()__: Identifica automaticamente o inicio e o fim do range de datas;
  - __TOTALYTD__:
  - __PREVIOUSMONTH__:
  - __PREVIOUSYEAR()__: 
  - __PARALLELPERIOD():__ Desloca mêses/anos/dias para trás de cada data no contexto do filtro

 
 ### M Language
  - Table.distinct:
  - Table.replace
  - Table.ReplaceMatchingRows
  - Table.RemoveMatchingRows
  - Table.RemoveColumns
  - Table.RenameColumns
