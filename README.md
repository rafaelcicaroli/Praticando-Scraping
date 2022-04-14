# Praticando **_WEBSCRAPING_**

![GitHub repo size](https://img.shields.io/github/repo-size/iuricode/README-template?style=for-the-badge)
![GitHub language count](https://img.shields.io/github/languages/count/iuricode/README-template?style=for-the-badge)
![GitHub forks](https://img.shields.io/github/forks/iuricode/README-template?style=for-the-badge)

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
</br> <img src="jsonsemtratamento.PNG">

Após a extração dos dados, acrescentei no código um método de tratamento simples em todas as linhas apenas do arquivo .json, retirando as informações circuladas em vermelho que não seriam úteis para uma visualização limpa dos dados
<br/>(_**clique**_ na imagem para uma melhor resolução)</br>

</br> <img src="tratamentomudar.png">

</br>
</br>

    def clean_text(text):
    text = text.strip(u'\u201c')
    text = text.strip(u'\u201d')
    return text

    class QuotesSpider(scrapy.Spider):
        name = "quotes"
        start_urls = [ "http://quotes.toscrape.com/page/1/" ]

         def parse(self, response):
            for quote in response.css('div.quote'):
                yield {
                     'text': clean_text(quote.css('span.text::text').get()),
                     'author': quote.css('small.author::text').get(),
                     'tags': quote.css('div.tags a.tag::text').getall()}
            next_page = response.css('li.next a::attr(href)').get()
             if next_page is not None:
                yield response.follow(next_page, callback=self.parse)

_________________
</br>
Arquivo .json tratado:

<br/>(_**clique**_ na imagem para uma melhor resolução)</br>
</br>

</br> <img src="tratamentoquotes.png">


</br>
</br>

Dessa forma finalizo o meu _**WEBSCRAPING**_ onde _coletei_ dados específicos de todas as páginas de um site, _limpei_, _tranformei_ em um arquivo de fácil leitura para consumo em várias ferrmantas e uma melhor visualização.

Estou praticando, há muito campo para melhora, porém estou satisfeito por realizei o que me propus fazer

Um abraço, 

_**Rafael Cicaroli**_
___
</br>

### _**Quer falar comigo?**_ Aponte a câmera no QR Code
</br>
<img src="sendtorafaelcicaroli.png" alt="drawing" width="200"/>



    
[⬆ Voltar ao topo](#rafaelcicaroli/Praticando-Scraping)<br>








<div style="display: inline_block"></br><img align="center" alt="html5"src="http://ForTheBadge.com/images/badges/made-with-python.svg"/><div><div style="display: inline_block"></br><img align="center" alt="html5"src="https://img.shields.io/badge/pycharm-143?style=for-the-badge&logo=pycharm&logoColor=black&color=black&labelColor=green"/>
<div>
