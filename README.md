# Praticando **_WEBSCRAPING_**

### _Neste projeto estou realizando a **Extração** de dados do site [Quotes to Scrape](https://quotes.toscrape.com/), convertendo-os em informação estruturada para posterior análise_

</br>

**Nas páginas do site encontramos:** </br>
- Citações de grandes nomes da história 
_(Albert Einstein, J.K Roulling, Jane Austen, Thomas Edison entre outros)_
- Biografias </br></br>

Foram coletadas as _**frases**_, os _**autores**_ de cada frase, e as _**tags**_ relacionadas </br>
</br>
___
</br>

Na classe _QuotesSpyder_ eu dou um nome ao projeto, e criei uma outra variável que recebe a url chamada de _stars_urls_
</br>
</br>

    class QuotesSpider(scrapy.Spider):
        name = "quotes"
        start_urls = [ "http://quotes.toscrape.com/page/1/" ]

</br>

Dentro da classe _QuotesSpider_ eu criei o método que faz o _scrapy_ das informações que determinei para esta solução com uma laço de repetição:

- Texto, Autor da Frase e as tags Relacionadas de _**todas as páginas do site**_ graças ao _callback_ 

</br>

     def parse(self, response):
         for quote in response.css('div.quote'):
             yield {
                'text': quote.css('span.text::text').get(),
                'author': quote.css('small.author::text').get(),
                'tags': quote.css('div.tags a.tag::text').getall()
             }
         next_page = response.css('li.next a::attr(href)').get()
         if next_page is not None:
             yield response.follow(next_page, callback=self.parse)

### Executando o código
_Aqui estou rodando o código **quotes**, nome esse que foi atribuído ao projeto na variável _**name**_ lá no começo do código. E ao mesmo tempo estou dando o comando para criar um novo arquivo .json para consumo e tratamento desses dados em sequência_


    scrapy crawl quotes -O quotes.json

O arquivo .json ficou da seguinte forma: 
<br/>(_**clique**_ na imagem para uma melhor resolução)</br>
</br> <img src="jsonsemtratamento.png">

Após a extração dos dados eles foram tranformados em json
Depois de tranformados foi feito o tratamento rertirando caracteres ou informações que não seria úteis para uma visualização limpa dos dados 

<div style="display: inline_block"></br>
<img align="center" alt="html5"
src="http://ForTheBadge.com/images/badges/made-with-python.svg"/>
<div>
