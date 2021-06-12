<h1 align="center">🕷 Scraping con Python</h1>
<p align="center"> <a href="https://www.azulschool.net/courses/curso-bases-del-web-scraping-con-python/" target="_blank">Curso de Azul school</a> - rodrigo Urcino </p>

| Tecnología | Versión |
|------------|---------|
| python     | 3.7.3   |
| Scrapy     | 2.5.0   |

## Construccion proyecto

- Crear archivo requirements.txt
- crear un entorno virtual(venv asdf y pycharm)
- dentro del entorno virtual
    - pip3 install scrapy
    - pip3 freeze > requirements.txt
    
## Uso

- crear un env y dentro del entorno
- pip3 install -r requirements.txt

## Que es el Scrapping

> “El proceso de extracción de información automatizado de sitios web” Cabe mencionar que todo esto se basa en HTTP

## Scrapy

> Framework open source

**Conceptos**

- shell: terminal para probar scrapy y python(pre-scrapping)
- selectores: expresiones regulares para seleccionar html o css
- items: da formato de salida
- spiders: extraen los datos estructurados.

## PASOS

1. Inspeccionar la web para saber la estructura del contenido y en que etiquetas se encuentra la información que necesitamos
2. Probar con la shell de scrapy(dentro de nuestro entorno virtual)
```shell
#scrapy shell quotes.toscrape.com
$ scrapy shell <urldelsitio>
# sugar syntax extraer mediante etiquetas y clases css(los hijos se separa con espacio)
$ response.css("div.row div.col-md-8 div.quote span.text::text").getall()
# mediante regex
$ response.xpath("//div[@class='row']//div[@class='col-md-8'] /div[@class='quote']/ span[@class='text']/text()").extract()

```