<p align="center"><img src= "https://user-images.githubusercontent.com/102841560/238230794-47244cbd-9b83-43fe-9a39-c5600da13a73.png"></p>

<h3> Diagrama ER do hospital fundamental </h3>

<p>Um pequeno hospital local busca desenvolver um novo sistema que atenda melhor às suas necessidades. Por isso, fui contratada para desenvolver um banco de dados funcional para otimizar suas consultas.<br>
Para começar, apresento o modelo conceitual do nosso banco.</p>
<br>

<p align="center"><img src= "https://user-images.githubusercontent.com/102841560/238229550-d291ce8a-7518-4885-9980-7b293317bedb.png"></p>

<br>
<p>O modelo acima está organizado da seguinte forma: temos a entidade médicos, que apresentam especialidade e cadastro, onde os eles realizam N consultas. As consultas tem algumas caracteristicas, como valor, data e hora, especialidade, nome/número do convênio, médico e paciente. Uma consulta gera N receita médica, onde apresentam instruções de uso, médicamentos e a quantidade. <br> Médicos atendem N pacientes, que apresentam cadastro e documentos, 1 paciente pode ter N convênios, que apresentam CNPJ, nome e carência. Pacientes adquirem N receitas médicas ao fim de uma consulta.</p> 
<br>
<p align="center"><img src="https://user-images.githubusercontent.com/102841560/238230797-746bb32f-48e1-4e13-b19a-ccdc7e7b4375.png"></p>
