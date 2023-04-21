<!-- PROJECT LOGO -->
<br />
<div align="center">
  <h1 align="center">Análise de Dados das Vagas de Emprego do EUA e Canadá</h1>

  <p align="center">
    Análise dos Dados das vagas de emprego dos EUA e Canadá para o desafio <a href="https://www.linkedin.com/feed/hashtag/?keywords=5dataglowup">5-data-glow-up</a> do <a href="https://www.linkedin.com/in/heitorsasaki">Heitor Sasaki</a>.
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
        <li><a href="#processo-etl">Processo ETL</a></li>
        <li><a href="#existe-alguma-possibilidade-desses-gêneros-serem-os-mais-alugados-por-terem-mais-filmes">Existe alguma possibilidade desses gêneros serem os mais alugados por terem mais filmes?</a></li>
        <li><a href="#quais-foram-os-5-filmes-mais-alugados">Quais foram os 5 filmes mais alugados?</a></li>
        <li><a href="#quais-foram-os-5-filmes-menos-alugados">Quais foram os 5 filmes menos alugados?</a></li>
        <li><a href="#existe-algum-filme-que-não-foi-alugado">Existe algum filme que não foi alugado?</a></li>
        <li><a href="#por-ordem-decrescente-qual-foi-o-lucro-que-cada-loja-recebeu">Por ordem decrescente, qual foi o lucro que cada loja recebeu?</a></li>
        <li><a href="#quem-são-os-10-maiores-clientes">Quem são os 10 maiores clientes?</a></li>
        <li><a href="#quais-são-as-cidades-onde-residem-os-10-maiores-clientes">Quais são as cidades onde residem os 10 maiores clientes?</a></li>
	<li><a href="#quais-são-as-cinco-cidades-com-o-maior-número-de-clientes-exceto-as-que-já-possuem-lojas">Quais são as cinco cidades com o maior número de clientes, exceto as que já possuem lojas?</a></li>
        <li><a href="#quem-é-o-ator-que-tem-mais-filmes-alugados">Quem é o ator que tem mais filmes alugados?</a></li>
        <li><a href="#qual-foi-o-lucro-médio-de-cada-ano">Existe algum filme que não foi alugado?</a></li>
      </ul> 
    </li>
    <li><a href="#agradecimentos">Agradecimentos</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>



<!-- Sobre o Projeto -->
## Sobre o Projeto

Após ver em diversos lugares as pessoas discutindo quais serviços de cloud são os maiores requisitados pelas empresas, eu decidi aproveitar o momento para matar essa curiosidade.



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

Para este projeto, foi decidido que o processo ETL será realizado utilizando o Power Query e sua linguagem M, que já vem implementada no Excel desde a versão 2010. Em seguida, será realizada a etapa de análise dos dados.

### Processo ETL

Após importar os arquivos obtidos no Kaggle e carrega-los no Power Query, foi realizada a primeira análise dos dados, essa para conhecer a base de uma maneira geral, para assim realizar a transformação necessária.





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
