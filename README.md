<h1>SQL/SQLServer</h1>

 
  ***DOCUMENTAÇÃO*** --------> <a>https://learn.microsoft.com/en-us/sql/sql-server/?view=sql-server-ver16</a>

<h2>DEFINIÇÕES</h2>

       - Domain Controller - Servidor onde armazena todas as informações dos usuarios 
       - Management Studio SSMS - Ferramenta client que conecta o servidor do SQÇ Server e permite a administração do DB
       - Linked Server - possibilita a ligação entre dois servidores diferentes até mesmo remotos (baixa performace)
       - Query - Solicitação de informações a um banco de dados (consulta)
       - Procedures - São rotinas/processos que são definidos e podem ser chamados pelo seu nome
       - Concatenar - Juntar dados (EX: nome + '(espaço)' + sobrenome) vai resultar em nome sobrenome
       - Procedures - São procedimentos armazenados, onde são passados procedimentos a serem realizados diretamente no SQL 
       - Cast/Convert - função usada para converter valores de uma variavel
       - Output - ao declarar uam variavel e usarmos essa função, após o termino dos codigos digitados será retornado o valor desta variavel
       - @@ROWCOUNT - função que retorna a quantidade de linhas que foram afetadas após um SELECT
       - TRY Catch - função usada para informar o usuario em caso de erro , a função irá no TRY e a msg de erro no catch caso o try nao seja exec
       - Trigger - são gatilhos programaveis que podem ser acionandos quando ocorre alguma determinada situação
       - Check - função usada para realizar checagem (Ex: operação Insert ou Delete, so aceitará essas opções escolhidas)
       - Inserted - tabela temporaria propia do sql onde fica os dados que acabaram de ser inseridos (permitindo o uso do ROLLBACK)
       - Deleted - tabela temporaria propia do sql onde fica os dados que acabaram de ser deletados  (permitindo o uso do ROLLBACK)
       - Functions - Reutilizar por exemplo calculos que vamos usar muitas vezes, ou uma consulta, para isso criamos uma função onde so vamos precisar chama-la 
       - Check Constraint - Usado para criar restrições de valores de uma tabela (EX: idade >= 18) 
       - Unique - Usado para criar valores unicos em uma tabela, esse valor nao pode ser repetido
       - BEGIN TRAN .. COMMIT TRAN - tudo  que esta entre o begin e o commit será executado de uma unica vez evitando perder parcialmente as querys (os dados podem ser visualizados localmente)
       - GETDATE() - função para coletar a data e hora atual
       - LIKE - utilizado para buscar por uma determinada string dentro de um campo com valores textuais.
       - @nomevariavel - variaveis locais
       - @@nomevariavel - variaveis globais
       
***SYSTEM DATABASE***

       - master - coração onde contém todas as informações vitais (necessita de backup)
       - model - contém modelos de DB, estruturas de tabelas internas, parametros basicos ("modelo") (backup opcional como é somente um modelo)
       - msdb - contém as tabelas dos dados do Server Agent (jobs, logs e etc) (necessita de backup)
       - tempdb - base de apoio temporaria (não necessita de backup pois sempre reseta ao iniciar) 
       
<h2>COMANDOS</h2>

***CREATE***
                                   
      - CREATE DATABASE nomebanco;                                  - criar um BD
      - CREATE TABLE nometabela;                                    - criar uma tabela

***IDENTITY***        ----------> (é um metodo para se auto incrementar um valor em uma tabela)

      - CREATE TABLE nometabela
      - (ID SMALLINT PRIMARY KEY IDENTITY (1 (valor inicial),1 (qtd incrementada)),

***ALTER***  
                                   
      - ALTER TABLE nometabela ADD nome INT;                        - altera a tabela adicionando a coluna nome com valor INT

***DROP , DELETE***
                            
      - DROP TABLE nometabela;                                      - remover tabela (não pode estar vinculada a uma tabela filha)
      - DELETE FROM nometabela WHERE condição;                      - deletar coluna 
      - TRUNCATE TABLE nometabela;                                  - paga todos os dados da TABELA, mas as colunas permanecem (sem dados)

***INSERT , UPDATE***   
                            
      - INSERT into [nometabela] (campo1, …) 
        VALUES (dado1, …);                                              - inserir dados nos campos             
      
      - UPDATE nometabela 
        SET campo1 = 'dado1', campo2 = 'dado2' 
        WHERE condição;                                                 - editar dados de um campo com restrições 
      
      - UPDATE DAN set coluna1 = coluna2 
        FROM tabela1 
        INNER JOIN tabela2 
             ON tabela1.pk = tabela2.fk 
        WHERE campo condição                                        - fazer UPDATE de uma coluna atraves de um JOIN (sempre usar BEGIN TRANSACTION / COMMIT TRANSACTION)

***SELECT***
                                   
      - SELECT * (campo)
        FROM nometabela;                                            - pesquisa de todos os dados  (evitar devido a perfomarce)
        

      - SELECT TOP 10 * 
        FROM nometabela                                            - pesquisa os 10 primeiros valores da tabela
        
      - SELECT DISTINCT campo1 
        FROM nometabela 
        ORDER BY valorx                                            - apresenta somente 1 vez cada valor mesmo que alguns se repitam
        
      - SELECT MIN (campo1) 
        FROM tabela                                                - apresenta o menor valor da coluna 
        
      - SELECT MAX (campo1) 
        FROM [tabela] 
        WHERE campo1 = 'valorx'                                   - pesquisa o maior valor quando campo1 = valorx
        
      - SELECT COUNT (campo1) ......                              - informa quantos linhas há no campo1
      
      - SELECT SUM [...] 
        FROM [...]                                                - soma dos valores da coluna
      
      - SELECT AVG [...] AS media 
        FROM [...]                                                - traz as media dos valores da coluna 
      
      - SELECT [...] 
        FROM [...] 
        WHERE [...] 
        AND | OR, IN | NOT                                       - pesquisa valores com condições E, OU, e NÃO 
      
      - SELECT [...] 
        FROM [...] 
        WHERE campo1 BETWEEN 10 AND 20                          - todos os valores entre 10 e 20 (BETWEEN) inclusive 10 e 20
      
      - SELECT [...] 
        FROM [...] 
        WHERE campo1 LIKE 'Ca%'                                 - todos os valores que comecem com as letras Ca (não importa a proxima letra) 
      
      - SELECT [...] 
        FROM [...] 
        WHERE campo1 LIKE '%Ca%'                                - todos os valores que contenha as letras Ca (não importa onde)                        - 
      
      - SELECT [...] 
        FROM [...] 
        WHERE campo1 LIKE 'Ca_'                                - todos os valores que contenha apenas as letras Ca e mais um caractere 
      
      - SELECT [...] 
        FROM [...] 
        WHERE campo1 IS NULL | IS NOT NULL                     - todos os valores que possuam valor nulo | valores não nulos 
      
      - SELECT [...], COUNT (ID) 
        FROM [...] 
        GROUP BY [...]                                          - vai contar quantos ID possuem valores iguais 

***SELF JOIN***        ----------> (é um metodo para se comparar itens da mesma tabela)
                       
       - SELECT A.coluna1, B.coluna1 
         FROM tabela1 A, tabela1 B 
         WHERE A.informação = B.informação                         - irá retornar todos os campos (EX: todas pessoas que moram e tal região) 

***INNER JOIN  | JOIN***         ----------> (é a interseção entre duas tabelas ou seja, o que possui o mesmo valor em ambas)
                       
       - SELECT [...] 
         FROM tabela1 
         INNER JOIN tabela2 
              ON tabela1.pk = tabela2.fk                           - retorna os valores iguais em ambas as tabelas que tiverem ligadas atraves de primary key e foreign key 

***LEFT OUTER JOIN |LEFT JOIN***  ----------> (são todos os valores da primeira tabela + os valores comuns entre a primeira e a segunda)

       - SELECT [...] 
         FROM tabela1 
         INNER JOIN tabela2 
              ON tabela1.pk = tabela2.fk                          - retorna todos os valores da primeira tabela = interseção que tiverem ligadas atraves de primary key e foreign key

***FULL OUTER JOIN |OUTER JOIN***    ----------> (Join mais completo, pois nos traz todos os valores de tabela, caso nao possua correspondentes ela traz o valor NULL para o valor.

       - SELECT [...] 
         FROM tabela1 
         INNER JOIN tabela2 
              ON tabela1.pk = tabela2.fk
       
***RIGHT OUTER JOIN |RIGHT JOIN***                ---------->(são todos os valores da segunda tabela + os valores comuns entre a primeira e a segunda)

       - SELECT [...] 
         FROM tabela1 
         INNER JOIN tabela2 
              ON tabela1.pk = tabela2.fk                         - retorna todos os valores da segunda tabela = interseção que tiverem ligadas atraves de primary key e foreign key

***UNION***           ---------->(realiza a combinação dos resultados de um ou mais SELECT em apenas um, remove dados duplicados)

      - SELECT coluna1(INT), coluna2(VARCHAR) 
        FROM tabela1 
        UNION 
        SELECT coluna1(INT), coluna2(VARCHAR) 
        FROM tabela2
        
      - SELECT 'cliente' AS type , nome + ' ' + sobrenome  AS NomeCompleto 
        FROM [...] 
        UNION 
        SELECT 'fornecedor', nome + ' ' + sobrenome  AS NomeCompleto 
        FROM [...]                                                             - irá colocar a tabela fornecedor pós o cliente

***HAVING***                 ---------->(usado para filtar o resultado de um agrupamento)

      - SELECT (..), COUNT(ID) AS quant 
        FROM (..) 
        WHERE [...] <> 'BRASIL' 
        GROUP BY [...]  
        HAVING COUNT (ID) =>9                                 - se executarmos a pesquisa ate o GROUP será feito a contagem e junção de todos os paises DIFERENTES de Brasil, e a função do HAVING e filtrar para aparecer somente paises com numero >= 9  
      

***SELECT INTO***            ---------->(usado para inserir informações em uma tabela atraves de uma consulta)                

      - SELECT * INTO NovoNomeTabela 
        FROM [...] 
        WHERE [...] = 'Exemplo'                                 - ao realizar a pesquisa os resultados encontrados serão salvos em uma nova tabela com o nome NovoNomeTabela

                     
***VIEWS***                   ----------> (usado para reaproveitar SELECT facilitando uma proxima consulta, salvando determinada consulta)    
              
     - CREATE VIEW [...] 
       AS 
           SELECT * 
           FROM [...] 
           WHERE id = 5                                        - será criado uma view com o nome escolhido onde irá conter somente os valores com id = 5
 
***PROCEDURES***              

     - SELECT name, modify_date 
       FROM sys.objects 
       WHERE type = 'P'                         -- 'P' representa stored procedures AND name = 'nome_procedure'; -- verificar ultima atualização/modificação realizad ana procedure
                 
***TRIGGER***                 ----------> (Uma forma de criar gatilho para determinda situações.   EX: backup, registro em log etc...)

     - CREATE TRIGGER nome_da_trigger
           ON nome_da_tabela
           FOR [AÇÃO]  -- Por exemplo, INSERT, UPDATE, DELETE
           AS
           BEGIN
                -- Corpo da trigger (código SQL a ser executado quando a trigger é acionada)
           END;

     - SELECT * 
       FROM sys.triggers 
       WHERE TYPE = 'TR' - tabela do propio SQL que nos mostra todas as TRIGGERS que possuimos e em quais tabelas
       
     - DROP TRIGGER IF EXISTS [...]
              
***FUNCTIONS***

    - CREATE FUNCTION nome_da_funcao
           (-- Parâmetros de entrada, @parametro1 tipo_de_dado, @parametro2 tipo_de_dado )
          RETURNS tipo_de_retorno
          AS
          BEGIN
              DECLARE @resultado tipo_de_retorno          
              -- Lógica da função, os parâmetros e realizar cálculos ou operações aqui
              RETURN @resultado
          END;

            
     - SELECT nomefuncao (variavel1, variavel2, variavel3) nomecoluna - Chamando a função e passando os parametros que serão usados na function o resultado sairá na coluna nomecoluna

***DATEPART***                 ----------> (Função usada para fragmentar uma data)
     
     - DATEPART ("year, day, month, minute, hour, etc....", coluna1)   
     
     - Possibilidades (https://learn.microsoft.com/en-us/sql/t-sql/functions/datepart-transact-sql?view=sql-server-ver16)

***OPERAÇÕES COM STRINGS***  ----------> ex: (LEN contagem de letras), (CONCAT concatenar)

     - SELECT coluna1, 
       SUBSTRING(coluna2, 1 - inicia de onde?, 5 -quantas letras?) 
       FROM tabela - FILTAR LETRAS - irá filtrar 5 letras iniciando da primeira
       
     - SELECT coluna1, 
       REPLACE(coluna2, ' 1 ' - busca o caractere 1, ' 2 ' -Substitui por 2) 
       FROM tabela - Substitui caracteres, nesse caso irá procurar o 1 e substituir por 2
     
     - Possibilidades ([https://learn.microsoft.com/en-us/sql/t-sql/functions/datepart-transact-sql?view=sql-server-ver16](https://learn.microsoft.com/en-us/sql/t-sql/functions/string-functions-transact-sql?view=sql-server-ver16))

***ROW_NUMBER***                 ----------> (Função usada para numerar um determinado resultado)
     
     - SELECT ROW_NUMBER() 
            OVER (ORDER BY alguma_coluna) 
            AS numero_da_linha,coluna1,coluna2 
            FROM sua_tabela;

***UNPIVOT***                 ----------> (Função usada para tranformar as colunas em linhas)
     
    - SELECT coluna_chave, coluna_valores
      FROM 
          (SELECT coluna_chave,coluna_origem1, coluna_origem2, ...
           FROM nome_da_tabela) AS TabelaFonte
      UNPIVOT 
              (coluna_valores FOR coluna_destino 
               IN (coluna_origem1, coluna_origem2, ...)) 
               AS nomeTabelaUnpivotada;


***PIVOT***                 ----------> (Função usada para tranformar as colunas em linhas)
     
     - SELECT coluna1, coluna2, ...
       FROM
           (SELECT coluna_de_pivot, coluna_para_agregacao, coluna_valor
            FROM nome_da_tabela) AS TabelaFonte
       PIVOT
            (funcao_agregacao(coluna_valor) FOR coluna_de_pivot 
             IN ([valor1], [valor2], ...)) 
             AS nomeTabelaPivotada;


***CASE***                 ----------> (Função usada para avaliar uma lista de condiçoes e retornar uma  das opções)
     
       CASE
         WHEN quando acontecer essa condição THEN entao sai esse resultado [ ...n ]
        [ ELSE senao sai esse resultado ]
       END


<H2>SEGURANÇA</h2>

     - Se mesmo com a senha do "sa", não estiver conseguindo abrir o banco deve-se permitir o acesso a essa porta pelo firewall do dc

       GRANT - Atribui previlegios de acesso a objetos do banco de dados
       REVOK - Remove os previlegios de acesso aos objetos obtidos atraves do comando GRANT
       DENY  - Nega permissão a um usuario ou grupo para realizar operações a objetos


<H2>ATALHOS</h2>

    - F1 - abre o navegador para ajuda com o comando desejado 
    - F2 - Renomear objetos/ tabelas/ views ....
    - F3 - Proxima vez que aparece a palavra / Shift + F3 Retorna a busca pela palavra
    - F4 - Exibe as propiedades
    - F5 - Executa 
    - F6 - Alterna entre os paineis 
    - F7 - Exibe a janela object explorer / abre uma aba com os itens selecionados
    - F8 - Abre e fecha a janela de object explorer
