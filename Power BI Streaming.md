### __Streaming in Power Bi__
3 types of real-time datasets:
#### __Push__: the data is pushed into power bi service. PBI automatically creates a new database in the service to store the data.
  - Todos os visuais, alertas e etc funcionam nessa opção;
  - Os reports podem ser fixados como dashboards e os dados são atualizados real-time;
  - Dentro do serviço, o dashboard dispara uma __atualização de bloco__ sempre que novos dados são recebidos.
  - __Considerações__: Se uma página foi fixada inteira como Dashboard, os dados __não serão atualizados automaticamente__;
  - Você pode utilizar Q&A para perguntar sobre o conjunto de dados. O visual resultando pode ser fixado e também __Será atualizado automaticamente__
 
 #### Streaming DataSets
- Os dados são armazenados em um cache temporário, que expira rapidamente.
- __Não há banco de dados subjacente__, portanto você não pode criar visuais de relatório usando os dados que fluem do fluxo
- Não é possível utilizar funcionalidades de relatório, como filtragem, visuais do pbi e etc. 
- A única maneira de visualizar os dados é utilizando um __custom streaming data source__
  - Otimizado para exibir os dados rapidamente;
  - A latência é menor pois não é necessário salvar o dado ou lê-lo de um banco;
  - Indicado para situações onde o tempo para visualizar os dados é critico;
- Boa Prática: carregar o dado no formato que ele será visualizado, sem agregações adicionais;
