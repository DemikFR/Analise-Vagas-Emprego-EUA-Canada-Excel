<!-- PROJECT LOGO -->
<br />
<div align="center">
  <h1 align="center">Análise de Dados das Vagas de Emprego dos EUA, Canadá e África</h1>

  <p align="center">
    Análise dos Dados das vagas de emprego dos EUA, Canadá e África para o desafio <a href="https://www.linkedin.com/feed/hashtag/?keywords=5dataglowup">5-data-glow-up</a> do <a href="https://www.linkedin.com/in/heitorsasaki">Heitor Sasaki</a>.
  </p>
  <p align="center">
    Os dados usados se encontram em uma base de dados do <a href="https://www.kaggle.com/datasets/cedricaubin/linkedin-data-analyst-jobs-listings">Kaggle</a>.
  </p>
</div>


<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#sobre-o-projeto">Sobre o Projeto</a>
      <ul>
        <li><a href="#ferramentas">Ferramentas</a></li>
      </ul>
    </li>
    <li><a href="#iniciar-o-projeto">Iniciar o Projeto</a></li>
    <li>
      <a href="#análise-dos-dados">Análise dos Dados</a>
      <ul>
        <li><a href="#requisitos-de-negócios">Requisitos de Negócios</a></li>
      	<li><a href="#processo-etl">Processo ETL</a></li>
        <li><a href="#analise-de-dados">Analise de Dados</a></li>
      </ul> 
    </li>
    <li><a href="#apresentação-e-storytelling">Apresentação e Storytelling</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>



<!-- Sobre o Projeto -->
## Sobre o Projeto

Após ver em diversos lugares pessoas discutindo quais serviços de cloud são os maiores requisitados pelas empresas, eu decidi aproveitar o momento para satisfazer essa curiosidade e levar uma informação utíl aos stakeholders.



### Ferramentas

Para realizar este projeto, foi usado as seguintes ferramenta:


* [![Microsoft-Excel][Microsoft-Excel.xlsx]][Microsoft-Excel-url]



<!-- Iniciar o Projeto -->
## Iniciar o Projeto

1. Clone este Repositório
   ```sh
   git clone https://github.com/DemikFR/Analise-Vagas-Emprego-EUA-Canada-Excel.git
   ```
2. Com os arquivos, será possível abrir o projeto no Microsoft Excel.



## Análise dos Dados

Antes de prosseguir com a análise de dados, é essencial compreender e entender os requisitos do negócio, juntamente com as perguntas que precisam ser respondidas para depois realizar a etapa de preparação dos dados e, assim, dar início à análise propriamente dita. Dessa forma, resultará em um projeto mais preciso e bem-sucedido.

### Requisitos de Negócios

Em geral, a pergunta principal que deve ser feita é: qual é o serviço em nuvem mais utilizado nos países mencionados? Para responder a essa pergunta de forma mais detalhada, é necessário fazer outras perguntas relevantes que possam fornecer informações úteis.

Assim, as perguntas feitas, são:

1. Qual é a proporção de vagas de Analista de Dados que exigem ou mencionam o uso de serviços em nuvem em relação ao total de vagas disponíveis para essa função?

2. Quais são os serviços mais utilizados individualmente, considerando as quantidades dos serviços que estão agrupados?

3. Qual é a utilização de cada serviço por país ou região, considerando os agrupamentos?

4. Qual é a proporção de cada país ou região para o uso de cloud?

5. Considerando a quantidade de vagas disponíveis, quais são as funções que mais exigem ou mencionam o uso de serviços em nuvem em sua descrição?


### Processo ETL

Para este projeto, foi decidido que o processo ETL será realizado utilizando o Power Query e a sua linguagem M, que foi implementada no em algumas versões do Excel.

Após importar os arquivos obtidos no Kaggle e carrega-los no Power Query, foi realizada a primeira análise dos dados, essa para conhecer a base de uma maneira geral, para assim realizar a transformação necessária.


1. Etapa:

	A primeira etapa consiste em retirar as linhas completamente vazias da tabela. Em todas elas, as linhas pares contém linhas em branco, que de nada servem para a análise.
	
	Além disso, todos os registros em que a descrição estavam vazias, foram excluídas para manter o rigor da análise.

2. Etapa:

	Para responder as questões de negócio, precisará saber de qual país é cada vaga, para isso, foi verificado que no campo de localização tem a cidade, estado e país separados por vírgula, alguns casos, está apenas a cidade ou estado e país precisando de mais um processo.

	Para esta etapa, no Canadá, foi usado o <i>separador de colunas por delimitador (vírgula)</i> e depois usada o comando <i>preenchimento para baixo</i>, assim todos os registros terão o nome do país para uso posterior na análise.

	Nos EUA, os registros que tem o nome do país estão em inglês e há os que tem apenas cidade e estado, conforme mencionado anteriormente. Para colocar um campo informando o país foi necessário apenas usar a opção de adicionar <i>coluna personalizada</i> recebendo uma string "Estados Unidos".

	Para tratar os dados referentes à África, utilizou-se inicialmente o <i>separador de colunas por delimitador (vírgula)</i>. Em seguida, foi criada uma nova coluna utilizando uma fórmula que verificava se a coluna de país, criada a partir do separador, estava nula. Caso isso ocorresse, o campo receberia o conteúdo da coluna de estado. Caso a coluna de estado também estivesse nula, seria adicionado o conteúdo da coluna de cidade.
	
   ```r
   = Table.AddColumn(#"Separar Cidade, Estado e País", "country", each if [country_1] = null and [state] <> null then [state] 
	else if [state] = null and [city] <> null then [city]
	else [country_1])
   ```
   
3. Etapa:

	Nesta etapa, serão excluídas todas as colunas que não serão utilizadas na análise, são elas: "onsite_remote", "salary", "criteria", "link", "city", "state" e "country_1" (esta última coluna foi criada anteriormente)


4. Etapa:

	A fim de identificar se a vaga requer conhecimento em Cloud Computing e, em caso afirmativo, especificar qual plataforma é necessária, foi utilizada a técnica de criação de coluna personalizada. Essa coluna foi criada por meio da fórmula 'Text Contains', a qual busca por palavras-chave relacionadas às plataformas de Cloud mais comuns. Quando a palavra-chave é encontrada, a respectiva plataforma é atribuída ao campo correspondente na coluna criada. Vale ressaltar que muitas vagas exigem conhecimentos em Cloud Computing, sem especificar qual plataforma é necessária. Para esses casos, foram considerados os maiores players do mercado em Cloud Computing como possíveis requisitos.
	
   ```r
	= Table.AddColumn(#"Valor Substituído", "Cloud", each if Text.Contains([description], "Azure") and Text.Contains([description], "AWS") and (Text.Contains([description], "GCP") or Text.Contains([description], "Google Cloud")) then "Azure, AWS e GCP"
	else if Text.Contains([description], "Azure") and (Text.Contains([description], "Google Cloud") or Text.Contains([description], "GCP")) then "Azure e GCP"
	else if Text.Contains([description], "AWS") and (Text.Contains([description], "Google Cloud") or Text.Contains([description], "GCP")) then "AWS e GCP"
	else if Text.Contains([description], "Azure") and Text.Contains([description], "AWS") then "Azure e AWS"
	else if Text.Contains([description], "Azure") then "Azure"
	else if Text.Contains([description], "AWS") then "AWS"
	else if Text.Contains([description], "GCP") or Text.Contains([description], "Google Cloud") or Text.Contains([description], "Google Cloud Platform") then "Google Cloud Platform"
	else if Text.Contains([description], "Oracle Cloud") then "Oracle Cloud"
	else if Text.Contains([description], "IBM Cloud") then "IBM Cloud"
	else if Text.Contains([description], "Salesforce") then "Salesforce"
	
	# Estas condições apenas para o Canada
	else if Text.Contains([description], "Redshift") then "AWS"
	else if Text.Contains([description], "Cloud") then "Azure, AWS e GCP"
	else null)
   ```
   
	Para garantir a precisão dos dados analisados, foi necessária uma etapa adicional para verificar às vagas que mencionavam apenas "Cloud" sem especificar qual tipo, seguida da análise individual de cada ocorrência para identificar o motivo.

   ```r
	= Table.AddColumn(#"Valor Substituído", "Cloud", each if Text.Contains([description], "Cloud") then "Cloud"
   ```

	Em alguns casos, há um nome genérico para se referir a nuvem (por exemplo, Cloud Technologies), mas existe um serviço preferível disponível. Nesses casos, foi decidido utilizar o serviço preferível como o solicitado.
	
	Com base no primeiro script mencionado, observou-se que, em alguns casos no Canadá, a habilidade de trabalhar com serviços em nuvem era referenciada apenas como "cloud", sem especificar o provedor. No entanto, foram considerados os três maiores provedores de serviços em nuvem. Além disso, foi identificada uma vaga que especificava o uso de um serviço da AWS, o Redshift. Para capturar adequadamente essa informação, foi realizada uma busca pelo nome "Redshift" e adicionado o serviço à lista de habilidades exigidas para essa vaga específica.

	Na África, foi identificado um Google Cloud Platform que não pôde ser encontrado, pois estava junto com outra palavra, assim, foi necessário adicionar um espaço entre às duas palavras usando a fórmula da linguagem M.

   ```r
	= Table.ReplaceValue(#"Colunas Removidas","PythonGoogle","Python Google",Replacer.ReplaceText,{"description"})
   ```	
   
5. Etapa:

	Para responder a quarta pergunta, foi criado uma nova coluna buscando padrões no título das vagas, por exemplo, todas as palavras que tem relação com "Analista" é considerado Analista de Dados, é necessário salientar que profissionais de BI, foram unidos com o Analista de Dados ficando "Analista de Dados ou BI", assim como os Desenvolvedores de Dados foram considerados "Engenheiro de Dados", que conforme as descrições de vaga, realizam atividades muito parecidas ou até igual à categoria que foi considerada.
	
   ```r
	= Table.AddColumn(#"Coluna Cloud Adicionada", "expertise", each if Text.Contains([title], "Analyst") or Text.Contains([title], "ANALYST") or Text.Contains([title], "analyst") or Text.Contains([title], "analysis") or Text.Contains([title], "Analysis") or Text.Contains([title], "Analytics") or Text.Contains([title], "BI") or Text.Contains([title], "Business Intelligence") or Text.Contains([title], "Researcher") then "Analista de Dados ou BI"
	else if Text.Contains([title], "Data Specialist") then "Especialista de Dados"
	else if Text.Contains([title], "Data Engineer") or Text.Contains([title], "Developer") then "Engenheiro de Dados"
	else if Text.Contains([title], "Data Intern") then "Estagiário de Dados"
	else null)
   ```	
  
6. Etapa:

	A última etapa será unir os dados de todas as tabelas em uma só, assim facilitando o processo de análise. 
	
	Para isso, foi realizada uma nova consulta em branco no Power Query e inserida a fórmula <code>=Excel.CurrentWorkbook()</code>. Essa fórmula busca e une todas as tabelas do Excel por colunas.

	Todo este processo ETL resultou na tabela, conforme o exemplo abaixo:
	
| title | company | description | posted_date | country | cloud | expertise | region name | 
|-------|---------|-------------|-------------|---------|-------|-----------|-------------|
Group Data Analyst | 60 Degrees Ltd | The opportunity that awaits you: A multinational International FMCG... | 12/11/2022	|  Botswana |  | Analista de Dados ou BI | Africa | 
| Data Analyst | Clutch | DATA ANALYST Overview of Opportunity If you enjoy collaborating... | 08/11/2022	| United States | Azure | Analista de Dados ou BI | United States | 
| Senior Data Analyst, APAC Marketplace | Hopper | About The JobDespite the challenges of the pandemic, Hopper managed to have triple... | 21/11/2022	|  Canada |   Google Cloud Platform | Analista de Dados ou BI | Canada |
| Data Analyst (Credit Risk)	|	Kuda	|	Kuda is a fintech on a mission to make financial services accessible, affordable and...	|	21/11/2022	| South Africa	|	|	Analista de Dados ou BI	|	Africa

	
	

### Analise de Dados

Após a etapa de ETL, é possível realizar a análise com base nas perguntas pré-definidas.

1. Pergunta - Qual é a proporção de vagas de Analista de Dados que exigem ou mencionam o uso de serviços em nuvem em relação ao total de vagas disponíveis para essa função?

	Para responder a 1° pergunta, foi usado um gráfico de pizza em que há duas fatias, uma para representar as vagas que não e a outra para a que menciona cloud. 
	
	![image](https://user-images.githubusercontent.com/102700735/235042456-1367f84c-0584-407d-888b-08fe9a32f7ec.png)
	
	Para todas as vagas disponíveis, foi identificado que apenas 1/5 delas pedem ou ao menos mencionam o uso de cloud em suas descrições.
	
2. Pergunta - Quais são os serviços mais utilizados individualmente, considerando as quantidades dos serviços que estão agrupados?

	A partir do gráfico apresentado abaixo, é possível verificar que o serviço AWS é o mais frequentemente mencionado, com um total de 162 aparições a mais do que o segundo colocado, o Azure. Em seguida, na terceira posição, está o GCP, sendo que os três juntos somam 93% das aparições nas vagas. A quarta posição é ocupada pelo Salesforce, com 159 citações, enquanto o IBM Cloud aparece em último lugar, com apenas duas menções.

	![image](https://user-images.githubusercontent.com/102700735/235056263-25bd64cf-2fad-4134-b9b8-cf268b29c7c2.png)
	
3. Pergunta - Qual é a utilização de cada serviço por país ou região, considerando os agrupamentos?

	A partir da análise realizada considerando as diferentes categorias de serviços de cloud, é possível destacar algumas tendências interessantes. Ao avaliar as citações que mencionam mais de um serviço de cloud na mesma vaga, é possível observar que a categoria "AWS e GCP" se destaca no Canadá, com um total de 101 aparições. Além disso, a categoria "Azure e AWS" foi mencionada em todos os países e regiões analisados, com uma média de aproximadamente 37 menções.

	Ao avaliar as categorias de clouds de forma isolada, nota-se que o Azure se destaca na África, embora seja o segundo menor nos Estados Unidos, ficando atrás do Salesforce. O AWS, por sua vez, é o maior serviço de cloud nos EUA e mantém uma boa posição e constância de 150 a 220 aparições em todos os países analisados. Já o GCP é o menor nos Estados Unidos, mas vence o Salesforce em todos os outros países e regiões, apresentando uma média de 85 aparições.
	
	![image](https://user-images.githubusercontent.com/102700735/235039923-a1ed1b15-91c9-471a-8ba5-1af0a7e3b4df.png)

4. Pergunta - Qual é a proporção de cada país ou região para o uso de cloud?

	Entre as regiões analisadas, foi possível observar que o Canadá apresentou a maior proporção de vagas com a menção de serviços de cloud na descrição, correspondendo a 43% do total de vagas. Em seguida, a África apareceu com uma proporção aproximadamente 7% menor que o Canadá. Já os Estados Unidos apresentaram a menor proporção de vagas com cloud na descrição, correspondendo a apenas 21% do total, o que representa a metade da quantidade de vagas do Canadá.
	
	![image](https://user-images.githubusercontent.com/102700735/235039870-742bfa39-5426-4ba9-875a-a32d36ff952e.png)

5. Pergunta - Considerando a quantidade de vagas disponíveis, quais são as funções que mais exigem ou mencionam o uso de serviços em nuvem em sua descrição?

	Para esta questão, foi utilizado o gráfico de barras empilhadas, pois com ele, é possível verificar cada vaga e a proporção de menções aos serviços de cloud. 
	
	Com isso, é possível perceber que em nenhuma vaga de Estagiário de Dados foi especificado algum serviço na descrição, enquanto em todas as vagas de Especialista de Dados, houve a ocorrência de cloud, mas vale resaltar, que existem apenas 2 vagas para este cargo. Com 192 vagas analisadas, o Engenheiro de Dados tem 45% de vagas que citam cloud, apesar de ser uma amostra pequena em relação ao mercado americano que tem mais de 92 mil vagas abertas no LinkedIn, no momento, é possível perceber que cloud é forte neste mercado. Para as vagas de Analista de Dados, 21% mencionaram cloud, isto é, um percentual significativamente menor do que as vagas para Engenheiro de Dados. Porém, ainda assim, indica uma presença relevante do uso de cloud nessa posição.

	![image](https://user-images.githubusercontent.com/102700735/234728552-2e3dc4bf-97d1-40bd-82a7-087ebd0bf70b.png)
	
	
	
## Apresentação e Storytelling	

Com base na análise realizada e nos insights obtidos, foi decidido criar dois relatórios para apresentação aos stakeholders. Um deles destacará o desempenho de cada serviço nas vagas em dados, enquanto o outro mostrará a relação dos países e regiões analisados com os serviços cloud, além de determinar a proporção em que cada cargo analisado mencionou algum serviço cloud em sua descrição.											
																	
![image](https://user-images.githubusercontent.com/102700735/235055898-2ec21e39-dd32-44c9-9870-95c376e1db6d.png)



![image](https://user-images.githubusercontent.com/102700735/235039707-8887bd27-1abf-45ef-b0bb-5c9fdf91fa7a.png)


	
<!-- LICENSE -->
## License

Distributed under the BSD 2-Clause License. See `LICENSE.txt` for more information.



<!-- CONTACT -->
## Contact

Demik Freitas - [Linkedin](https://www.linkedin.com/in/demik-freitas/) - demik.freitast2d18@gmail.com

Project Link: [https://github.com/DemikFR/Analise-Vagas-Emprego-EUA-Canada-Excel](https://github.com/DemikFR/Analise-Vagas-Emprego-EUA-Canada-Excel)



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[Microsoft-Excel.xlsx]: https://img.shields.io/badge/Microsoft_Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white
[Microsoft-Excel-url]: https://www.microsoft.com/pt-br/microsoft-365/excel?&ef_id=_k_CjwKCAjwue6hBhBVEiwA9YTx8L8HZ4aL6EyiDeOqaTjqnBHuVhAfb9qJWDlBZzaa2aYzJum7Dti7lhoCTH8QAvD_BwE_k_&OCID=AIDcmm409lj8ne_SEM__k_CjwKCAjwue6hBhBVEiwA9YTx8L8HZ4aL6EyiDeOqaTjqnBHuVhAfb9qJWDlBZzaa2aYzJum7Dti7lhoCTH8QAvD_BwE_k_&gclid=CjwKCAjwue6hBhBVEiwA9YTx8L8HZ4aL6EyiDeOqaTjqnBHuVhAfb9qJWDlBZzaa2aYzJum7Dti7lhoCTH8QAvD_BwE
