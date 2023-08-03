<h1>SQL/SQLServer</h1>

<h2>DEFINIÇÕES</h2>

       Domain Controller - Servidor onde armazena todas as informações dos usuarios 
       Management Studio SSMS - Ferramenta client que conecta o servidor do SQÇ Server e permite a administração do DB
       Linked Server - possibilita a ligação entre dois servidores diferentes até mesmo remotos (baixa performace)
       Query - Solicitação de informações a um banco de dados (consulta)
       Procedures - São rotinas/processos que são definidos e podem ser chamados pelo seu nome
       Concatenar - Juntar dados (EX: nome + '(espaço)' + sobrenome) vai resultar em nome sobrenome
       Views - usado para reaproveitar SELECT facilitando uma proxima consulta, deixando as informações mais seguras e simples, disponibilizando somente o necessario para aquela informação 
       Procedures - São procedimentos armazenados, onde são passados procedimentos a serem realizados diretamente no SQL 
       Cast/Convert - função usada para converter valores de uma variavel
       Output - ao declarar uam variavel e usarmos essa função, após o termino dos codigos digitados será retornado o valor desta variavel
       @@ROWCOUNT - função que retorna a quantidade de linhas que foram afetadas após um SELECT
       TRY Catch - função usada para informar o usuario em caso de erro , a função irá no TRY e a msg de erro no catch caso o try nao seja exec
       Trigger - são gatilhos programaveis que podem ser acionandos quando ocorre alguma determinada situação
       Check - função usada para realizar checagem (Ex: operação Insert ou Delete, so aceitará essas opções escolhidas)
       Inserted - tabela temporaria propia do sql onde fica os dados que acabaram de ser inseridos (permitindo o uso do ROLLBACK)
       Deleted - tabela temporaria propia do sql onde fica os dados que acabaram de ser deletados  (permitindo o uso do ROLLBACK)
       Functions - Reutilizar por exemplo calculos que vamos usar muitas vezes, ou uma consulta, para isso criamos uma função onde so vamos precisar chama-la 
       BEGIN TRAN .. COMMIT TRAN - tudo  que esta entre o begin e o commit será executado de uma unica vez evitando perder parcialmente as querys (os dados podem ser visualizados localmente)
       GETDATE() - função para coletar a data e hora atual
       @nomevariavel - variaveis locais
       @@nomevariavel - variaveis globais
       
       system DataBase - master - coração onde contém todas as informações vitais (necessita de backup)
       system DataBase - model - contém modelos de DB, estruturas de tabelas internas, parametros basicos ("modelo") (backup opcional como é somente um modelo)
       system DataBase - msdb - contém as tabelas dos dados do Server Agent (jobs, logs e etc) (necessita de backup)
       system DataBase - tempdb - base de apoio temporaria (não necessita de backup pois sempre reseta ao iniciar) 
       
<h2>COMANDOS</h2>

                                         *******   CREATE   *******
                                   
              CREATE DATABASE nomebanco;                                  - criar um BD
              CREATE TABLE nometabela;                                    - criar uma tabela

                                         *******   ALTER   ********  
                                   
              ALTER TABLE nometabela ADD nome INT;                        - altera a tabela adicionando a coluna nome com valor INT

                                     ********   DROP , DELETE   ********
                            
              DROP TABLE nometabela;                                      - remover tabela
              DELETE FROM nometabela;                                     - deletar tabela (não pode estar vinculada a um  atabela filha)

                                 ********   INSERT , UPDATE   ********   
                            
              INSERT into [nometabela] (campo1, …) values (dado1, …);     - inserir dados nos campos             
              UPDATE nometabela SET campo1 = 'dado1' WHERE id = dado2;    - editar dados de um campo com restrições            

                                       ********   SELECT   ********
                                   
              SELECT * FROM nometabela;                                   - pesquisa de todos os dados  (evitar devido a perfomarce)
              SELECT campo1 FROM nometabela;                              - pesquisa as colunas selecionadas  
              SELECT campo1, campo2 FROM nometabela ORDER BY campo1       - pesquisa os dados e ordena conforme a campo1
              SELECT campo1, campo2 FROM nometabela ORDER BY campo1 DESC  - pesquisa os dados e ordena o campo1 de forma decrescente
              SELECT * FROM nometabela WHERE campo = valorx               - pesquisa todos os dados que possuam valorx
              SELECT TOP 10 * FROM nometabela                             - pesquisa os 10 primeiros valores da tabela
              SELECT DISTINCT campo1 FROM nometabela ORDER BY valorx      - apresenta somente 1 vez cada valor mesmo que alguns se repitam
              SELECT MIN (campo1) FROM tabela                             - apresenta o menor valor da coluna 
              SELECT MAX (campo1) FROM [tabela] WHERE campo1 = 'valorx'   - pesquisa o maior valor quando campo1 = valorx
              SELECT COUNT (campo1) FROM tabela                           - informa quantos linhas há no campo1
              SELECT SUM [...] FROM [...]                                 - soma dos valores da coluna
              SELECT AVG [...] AS media FROM [...]                        - traz as media dos valores da coluna 
              SELECT [...] FROM [...] WHERE [...] AND | OR, IN | NOT      - pesquisa valores com condições E, OU, e NÃO 
              SELECT [...] FROM [...] WHERE campo1 BETWEEN 10 AND 20      - todos os valores entre 10 e 20 (BETWEEN) inclusive 10 e 20
              SELECT [...] FROM [...] WHERE campo1 LIKE 'Ca%'             - todos os valores que comecem com as letras Ca (não importa a proxima letra) 
              SELECT [...] FROM [...] WHERE campo1 LIKE '%Ca%'            - todos os valores que contenha as letras Ca (não importa onde)                        - 
              SELECT [...] FROM [...] WHERE campo1 LIKE 'Ca_'             - todos os valores que contenha apenas as letras Ca e mais um caractere 
              SELECT [...] FROM [...] WHERE campo1 IS NULL | IS NOT NULL  - todos os valores que possuam valor nulo | valores não nulos 
              SELECT [...], COUNT (ID) FROM [...] GROUP BY [...]          - vai contar quantos ID possuem valores iguais 

                       ********   INNER JOIN  | JOIN (é a interseção entre duas tabelas ou seja, o que possui o mesmo valor em ambas)********
                       
              SELECT [...] FROM tabela1 INNER JOIN tabela2 ON tabela1.pk = tabela2.fk - retorna os valores iguais em ambas as tabelas que tiverem ligadas atraves de primary key e foreign key 

                      ********   LEFT JOIN  (são todos os valores da primeira tabela + os valores comuns entre a primeira e a segunda)********

              SELECT [...] FROM tabela1 INNER JOIN tabela2 ON tabela1.pk = tabela2.fk - retorna todos os valores da primeira tabela = interseção que tiverem ligadas atraves de primary key e foreign key
                     
                      ********   RIGHT JOIN  (são todos os valores da segunda tabela + os valores comuns entre a primeira e a segunda)********

              SELECT [...] FROM tabela1 INNER JOIN tabela2 ON tabela1.pk = tabela2.fk - retorna todos os valores da segunda tabela = interseção que tiverem ligadas atraves de primary key e foreign key

                       ********   SQL UNION  (realiza  a junção das colunas desejadas desde que possuam a mesma quantidade e tipo de dados)********

              SELECT 'cliente' AS type , nome + ' ' + sobrenome  AS NomeCompleto FROM [...] - criará uma coluna chamado "type" onde terá o valor cliente, e a coluna nomecompleto onde esta a junção nome+sobrenome
              SELECT 'cliente' AS type , nome + ' ' + sobrenome  AS NomeCompleto FROM [...] UNION SELECT 'fornecedor', nome + ' ' + sobrenome  AS NomeCompleto FROM [...] - irá colocar a tabela fornecedor pós o cliente

                                                        ********   SQL HAVING  ********

              SELECT (..), COUNT(ID) AS quant FROM (..) WHERE [...] <> 'BRASIL' GROUP BY [...]  HAVING COUNT (ID) =>9 
                     - se executarmos a pesquisa ate o GROUP será feito a contagem e junção de todos os paises DIFERENTES de Brasil, e a função do HAVING e filtrar para aparecer somente paises com numero >= 9  

                                                        ********   SQL SELECT INTO  ********

                     SELECT * INTO NovoNomeTabela FROM [...] WHERE [...] = 'Exemplo' - ao realizar a pesquisa os resultados encontrados serão salvos em uma nova tabela com o nome NovoNomeTabela

                     
                                                               ********  VIEWS  ********
              
              CREATE VIEW [...] AS SELECT * FROM [...] WHERE id = 5 - será criado uma view com o nome escolhido onde irá conter somente os valores com id = 5
              SELECT * FROM (nomedaview) - retorna os dados somente dessa view
              CREATE OR ALTER VIEW [...] AS SELECT YEAR(vendasdata) AS ano, month(vendasdata) AS mes, day(vendasdata) AS dia, quant * valor AS vendas FROM [...] podendo usar JOIN's
              
                                                                 ********  TRIGGER  ********

              CREATE TRIGGER [dbo].[...] ON [dbo].[...] AFTER INSERT, DELETE AS BEGIN (o que irá ocorrer apóso gatilho) - Criação do Trigger que fará alguma ação após ocorrer um INSERT ou DELETE
              ALTER TABLE [...] ENABLE TRIGGER [...]- Comando necessario para ativar o TRIGGER
              ALTER TABLE [...] DISABLE TRIGGER [...]- Comando necessario para desativar o TRIGGER 
              ENABLE TRIGGER ALL ON [...] - ativa todas as TRIGGERS da tabela
              DISABLE TRIGGER ALL ON [...] - desativa todas as TRIGGERS da tabela
              SELECT * FROM sys.triggers WHERE TYPE = 'TR' - tabela do propio SQL que nos mostra todas as TRIGGERS que possuimos e em quais tabelas
              DROP TRIGGER IF EXISTS [...]
              
                                                                 ********  FUNCTIONS  ********

              CREATE FUNCTIONS nomefuncao( variaveis ) RETURNS (variavel) AS BEGIN RETURN (EX: variavel1 * variavel3 - variavel3) END; - Criando uma function
              SELECT nomefuncao (variavel1, variavel2, variavel3) nomecoluna - Chamando a função e passando os parametros que serão usados na function o resultado sairá na coluna nomecoluna

  
<H2>SEGURANÇA</h2>

       Se mesmo com a senha do "sa", não estiver conseguindo abrir o banco deve-se permitir o acesso a essa porta pelo firewall do dc

       GRANT - Atribui previlegios de acesso a objetos do banco de dados
       REVOK - Remove os previlegios de acesso aos objetos obtidos atraves do comando GRANT
       DENY  - Nega permissão a um usuario ou grupo para realizar operações a objetos
