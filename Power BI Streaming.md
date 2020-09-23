### __Streaming in Power Bi__
3 types of real-time datasets:
#### __Push__: the data is pushed into power bi service. PBI automatically creates a new database in the service to store the data.
  - Todos os visuais, alertas e etc funcionam nessa opção;
  - Os reports podem ser fixados como dashboards e os dados são atualizados real-time;
  - Dentro do serviço, o dashboard dispara uma __atualização de bloco__ sempre que novos dados são recebidos.
  - __Considerações__: Se uma página foi fixada inteira como Dashboard, os dados __não serão atualizados automaticamente__;
  - Você pode utilizar Q&A para perguntar sobre o conjunto de dados. O visual resultando pode ser fixado e também __Será atualizado automaticamente__
 - __Taxa de Ingestão__: 1 solicitação/s 16 MB/solicitação
 - __Limite Taxa de transferência__: 1 milhão de linhas/hora
 
 - __Como Enviar os Dados__
  - __API REST do PBI__ 
    -if _defaultmode_ is set to _pushStreaming_, the dataset is both, a __push__ and __streaming__ dataset, providing the benefits of both types;
    - Se o tamanho do conjunto passar de 15 MB mas não exceder 16 MB, a atualização ocorre. Caso contrário, falhará.
    - os Requests respeitam os protocolos de segurança do Azure AD OAuth;
  - __Streaming Dataset UI__
    - Power Bi Service > API
      - Se o histórico estiver desabilitado, você utilizará o tipo __streaming dataset__. Senão, será a combinado com __push dataset__
    - Autenticação não é requerida. URL com rowkey autoriza o requerente a carregar os dados sem usar o AAD;
  - __Azure Stream Analytics__
    - Usa a API REST do pbi;
    - With _defaultMode_ set to _pushStreaming_, resulta em um dataset que tem as vantagens do streaming e do push.
    - Quando o conjunto de dados é criado, o Azure Stream Analytics seta a  _retentionPolicy_ flag to _basicFIFO_. O que dá suporte para que o dataset __push__ armazene 200 mil linhas, e é determinado quais linhas são removidas emm um modo __FIFO__ (First in First out)
    - Se as saídas forem rápidas demais para serem ingeridas pelo PBI, o Azure Stream Analytics fará o envio em lotes dessas saídas em uma única solicitação. Podendo causar falha devido ao tamanho do lote. Desta forma, é recomendado diminuir a taca de saída de dados para o PBI. Exemplo: ao invés de um valor máximo a cada segundo, defina a taxa de saída como um valor máximo durante 10 segundos.
  
 #### Streaming DataSets
- Os dados são armazenados em um cache temporário, (por 1h) que expira rapidamente.
- __Não há banco de dados subjacente__, portanto você não pode criar visuais de relatório usando os dados que fluem do fluxo;
- Não é possível utilizar funcionalidades de relatório, como filtragem, visuais do pbi e etc. 
- A única maneira de visualizar os dados é utilizando um __custom streaming data source__
  - Otimizado para exibir os dados rapidamente;
  - A latência é menor pois não é necessário salvar o dado ou lê-lo de um banco;
  - Indicado para situações onde o tempo para visualizar os dados é critico;
- __Boa Prática:__ carregar o dado no formato que ele será visualizado, sem agregações adicionais;
 - __Taxa de Ingestão__: 5 solicitação/s 15 MB/solicitação
 - __Limite Taxa de transferência__: Nenhum

#### PubNub Streaming Dataset
- PBI web client uses the PubNub SDK to read an existing PubNub data stream;
- No data is stored by the Power Bi service (ou seja, não são enviados para o Power Bi. Diferente do Streaming Datasets)
- Call is made from the web client directly
- List traffic to PubNub as allowed from your network;
- There's no underlying database (as streaming datasets)
- Os dados só podem ser visualizados através de blocos(tiles) em dashboards;
- Tem as mesmas limitações do Streaming Datasets e também é indicado quando é necessário baixa latência na visualização dos dados;
 - __Taxa de Ingestão__: N/A - os dados não são enviados por push para o pbi
 - __Limite Taxa de transferência__: N/A

__Push__: Permite criar relatórios e os dados são armazenados para análises históricas. __Streaming e PubNub__ apenas "tiles" de streaming personalizados e adicionados diretamente ao dashboard. Não armazenam histórico.
