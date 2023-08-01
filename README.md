<h2>SQLServer</h2>

<h5>Definições</h5>

       Domain Controller - Servidor onde armazena todas as informações dos usuarios 
       Management Studio SSMS - Ferramenta client que conecta o servidor do SQÇ Server e permite a administração do DB
       Linked Server - possibilita a ligação entre dois servidores diferentes até mesmo remotos (baixa performace)
       Query - Solicitação de informações a um banco de dados (consulta)
       Procedures - São rotinas/processos que são definidos e podem ser chamados pelo seu nome

       system DataBase - master - coração onde contém todas as informações vitais (necessita de backup)
       system DataBase - model - contém modelos de DB, estruturas de tabelas internas, parametros basicos ("modelo") (backup opcional como é somente um modelo)
       system DataBase - msdb - contém as tabelas dos dados do Server Agent (jobs, logs e etc) (necessita de backup)
       system DataBase - tempdb - base de apoio temporaria (não necessita de backup pois sempre reseta ao iniciar) 
       
<h5>Comandos</h5>


<h5>Segurança</h5>

       Se mesmo com a senha do "sa", não estiver conseguindo abrir o banco deve-se permitir o acesso a essa porta pelo firewall do dc
