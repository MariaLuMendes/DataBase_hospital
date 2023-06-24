<p align="center"><img src= "https://user-images.githubusercontent.com/102841560/238230794-47244cbd-9b83-43fe-9a39-c5600da13a73.png"></p>

<h3> Banco de dados para o hospital fundamental </h3>

## Parte 1 - Diagrama Entidade Relacionamento

<p>Um pequeno hospital local busca desenvolver um novo sistema que atenda melhor às suas necessidades. Por isso, fui contratada para desenvolver um banco de dados funcional para otimizar suas consultas.<br>
Para começar, apresento o modelo conceitual do nosso banco.</p>
<br>

<p align="center"><img src= "https://user-images.githubusercontent.com/102841560/238229550-d291ce8a-7518-4885-9980-7b293317bedb.png"></p>

<br>
<p>O modelo acima está organizado da seguinte forma: temos a entidade médicos, que apresentam especialidade e cadastro, onde os eles realizam N consultas. As consultas tem algumas caracteristicas, como valor, data e hora, especialidade, nome/número do convênio, médico e paciente. Uma consulta gera N receita médica, onde apresentam instruções de uso, médicamentos e a quantidade. <br> Médicos atendem N pacientes, que apresentam cadastro e documentos, 1 paciente pode ter N convênios, que apresentam CNPJ, nome e carência. Pacientes adquirem N receitas médicas ao fim de uma consulta.</p> 
<br>

## Parte 2 - Diagrama Entidade Relacionamento (ER)
No hospital, as internações têm sido registradas por meio de formulários eletrônicos que gravam os dados em arquivos.

<ul>
  
<li>Para cada internação, são anotadas a data de entrada, a data prevista de alta e a data efetiva de alta, além da descrição textual dos procedimentos a serem realizados.</li>
  
<br>

<li>As internações precisam ser vinculadas a quartos, com a numeração e o tipo.</li>

<br> 
  
<li>Cada tipo de quarto tem sua descrição e o seu valor diário (a princípio, o hospital trabalha com apartamentos, quartos duplos e enfermaria).</li>

<br> 
  
<li>Também é necessário controlar quais profissionais de enfermaria estarão responsáveis por acompanhar o paciente durante sua internação. Para cada enfermeiro(a), é necessário nome, CPF e registro no conselho de enfermagem (CRE).</li>

<br>  
  
<li>A internação, obviamente, é vinculada a um paciente – que pode se internar mais de uma vez no hospital – e a um único médico responsável.</li>

<br>  
  
<li>Por último, crie um script SQL para a geração do banco de dados.</li>
  
<br>  

![DiagramaER pt2](https://github.com/GoncalvessLeo/DataBase-Hospital/assets/125033731/a09604d1-9966-421d-a043-5a638e2fd69d)
</ul> 

## Parte 3 - Alimentando o banco de dados  
  
Crie scripts de povoamento das tabelas desenvolvidas na atividade anterior. Observe as seguintes atividades:

<ul>
  
<li>Inclua ao menos dez médicos de diferentes especialidades.</li>

<br>
  
<li>Ao menos sete especialidades (considere a afirmação de que “entre as especialidades há pediatria, clínica geral, gastrenterologia e dermatologia”).</li>

<br>   
  
<li>Inclua ao menos 15 pacientes.</li>

<br>   
  
<li>Registre 20 consultas de diferentes pacientes e diferentes médicos (alguns pacientes realizam mais que uma consulta). As consultas devem ter ocorrido entre 01/01/2015 e 01/01/2022. Ao menos dez consultas devem ter receituário com dois ou mais medicamentos.</li>

<br>   
  
<li>Inclua ao menos quatro convênios médicos, associe ao menos cinco pacientes e cinco consultas.</li>

<br>   
  
<li>Criar entidade de relacionamento entre médico e especialidade.</li>

<br>   
  
<li>Criar Entidade de Relacionamento entre internação e enfermeiro.</li> 

<br>   
  
<li>Arrumar a chave estrangeira do relacionamento entre convênio e médico.</li>

<br>   
  
<li>Criar entidade entre internação e enfermeiro.</li>

<br>   
  
<li>Colocar chaves estrangeira dentro da internação (Chaves Médico e Paciente).</li>

<br>   
  
<li>Registre ao menos sete internações. Pelo menos dois pacientes devem ter se internado mais de uma vez. Ao menos três quartos devem ser cadastrados. As internações devem ter ocorrido entre 01/01/2015 e 01/01/2022.</li>

<br> 
  
<li>Considerando que “a princípio o hospital trabalha com apartamentos, quartos duplos e enfermaria”, inclua ao menos esses três tipos com valores diferentes.</li>

<br>   
  
<li>Inclua dados de dez profissionais de enfermaria. Associe cada internação a ao menos dois enfermeiros.</li>

<br>   
  
<li>Os dados de tipo de quarto, convênio e especialidade são essenciais para a operação do sistema e, portanto, devem ser povoados assim que o sistema for instalado.</li>
  
</ul> 

## Parte 4 - Alterando o banco de dados 
<p>Pensando no banco que já foi criado para o Projeto do Hospital, realize algumas alterações nas tabelas e nos dados usando comandos de atualização e exclusão:

Crie um script que adicione uma coluna “em_atividade” para os médicos, indicando se ele ainda está atuando no hospital ou não.</p> 
![AlterandoTabela](https://github.com/GoncalvessLeo/DataBase-Hospital/assets/125033731/c1744455-2005-4ba2-9947-b6c5435af947)

## Parte 5 - Consultas
<p>Crie um script e nele inclua consultas que retornem:</p>

* Todos os dados e o valor médio das consultas do ano de 2020 e das que foram feitas sob convênio.
  ```
  select *, AVG(valor_consulta) from consulta group by year(dt_consulta) = 2020;
  ```
<br>  

* Todos os dados das internações que tiveram data de alta maior que a data prevista para a alta.
  ```
  select * from internacao where dt_efetiva_alta > dt_prevista_alta; 
  ```
<br>  
  
* Receituário completo da primeira consulta registrada com receituário associado.
  ```
  select * from consulta inner join receita on consulta.id_consulta = receita.id_consulta inner join
  paciente on paciente.id_paciente = consulta.id_paciente order by receita.id_receita limit 1;
  ```
<br>  
  
* Todos os dados da consulta de maior valor e também da de menor valor (ambas as consultas não foram realizadas sob convênio). 
  ```
  select *, MAX(valor_consulta), MIN(valor_consulta) from consulta;
  ```
<br>  

* Todos os dados das internações em seus respectivos quartos, calculando o total da internação a partir do valor de diária do quarto e o número de dias entre a entrada e a alta.
  ```
  select *, DATEDIFF(dt_efetiva_alta, dt_entrada) dias_internado, tipos_quarto.valor_diario,
  DATEDIFF(dt_efetiva_alta, dt_entrada) * tipos_quarto.valor_diario
  valor_total from internacao inner join quartos on internacao.quarto_id = quartos.id_quarto inner join
  tipos_quarto on quartos.tipo_id = tipos_quarto.id_tipo;</code>
  ```
<br>  
  
* Data, procedimento e número de quarto de internações em quartos do tipo “apartamento”.
  ```
  select i.id_internacao, i.dt_entrada, i.desc_procedimentos, q.numero_quarto
  from internacao i inner join quartos q on q.id_quarto = i.quarto_id where q.tipo_id = 1; 
  ```
<br> 
  
* Nome do paciente, data da consulta e especialidade de todas as consultas em que os pacientes eram menores de 18 anos na data da consulta e cuja especialidade não seja “pediatria”, ordenando por data de realização da consulta.
  ```
  select p.nome_paciente, c.dt_consulta, e.nome_especialidade from consulta c inner join
  paciente p on p.id_paciente = c.id_paciente inner join
  especialidade e on e.id_especialidade = c.id_especialidade where c.id_especialidade<> 1 and year(c.dt_consulta)
  - year(p.dt_nasc_paciente) < 19 and year(c.dt_consulta) - year(p.dt_nasc_paciente) > 0 order by c.dt_consulta;
    ```
<br>
    
* Nome do paciente, nome do médico, data da internação e procedimentos das internações realizadas por médicos da especialidade “gastroenterologia”, que tenham acontecido em “enfermaria”.
    ```
    select p.nome_paciente, m.nome_medico, i.dt_entrada, i.desc_procedimentos, q.id_quarto from internacao
    i inner join medico m on m.id_medico = i.medico_id inner join paciente p on p.id_paciente = i.paciente_id inner join
    quartos q on q.id_quarto = i.quarto_id where q.tipo_id = 3 and m.id_especialidade = 3;
    ```
<br>
    
* Os nomes dos médicos, seus CRMs e a quantidade de consultas que cada um realizou.</li>
    ```
    select m.nome_medico, count(c.id_medico) as 'Qntd de consultas' from medico m inner join
    consulta c on c.id_medico = m.id_medico group by c.id_medico;
  ```
<br>
    
* Todos os médicos que tenham "Gabriel" no nome. 
   ```
  insert into medico(nome_medico, cpf_medico, crm, email_medico, cargo_medico, id_especialidade, em_atividade)
  values('Gabriel Augusto', 45679312, 123456, 'gabriel.augusto@gmail.com', 'Especialista', 3, 'Ativo');
  select * from medico where nome_medico like '%Gabriel%';
   ```
<br>
    
* Os nomes, CREs e número de internações de enfermeiros que participaram de mais de uma internação.
 ```
select enf.nome_enfermeiro, enf.cre, COUNT(i.id_enfermeiro) as Participacao from enfermeiros enf
inner join internacao_enfermeiro i on i.id_enfermeiro = enf.id_enfermeiro group by enf.id_enfermeiro having Participacao > 1;
 ```

<p align="center"><img src="https://user-images.githubusercontent.com/102841560/238230797-746bb32f-48e1-4e13-b19a-ccdc7e7b4375.png"></p>
