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

## Que es Robots.txt

> Revisarlo para definir que puedes ver o que no puedes ver.

- User-Agent: hace referencia al bot que está haciendo la petición al sitio, * (son todos)
- Disallow: las rutas q estan deshabilitados
- Allow: lo que esta permitido(excepcción, no puedes visualizar lo que esta disallow pero si puedes los q estan en allow)

**Entrar al archivo robots.txt**

En la url del sitio poner `https://sitio.com/robots.txt`

## Scrapy

> Framework open source

**Conceptos**

- shell: terminal para probar scrapy y python(pre-scrapping)
- selectores: expresiones regulares para seleccionar html o css
- items: da formato de salida y se accede como a un diccionario
- spiders: extraen los datos estructurados.

## PASOS

1. Inspeccionar la web para saber la estructura del contenido y en que etiquetas se encuentra la información que necesitamos
2. Probar con la shell de scrapy(dentro de nuestro entorno virtual)
```shell
#scrapy shell quotes.toscrape.com fijarse en la respuesta que codigo nos retorna
$ scrapy shell <urldelsitio>

# sugar syntax extraer mediante etiquetas y clases css(los hijos se separa con espacio)
$ nameVar = response.css("div.row div.col-md-8 div.quote span.text::text").getall()
$ import pprint
$ pprint.pprint(nameVar)

# mediante regex
$ response.xpath("//div[@class='row']//div[@class='col-md-8'] /div[@class='quote']/ span[@class='text']/text()").extract()
```
3. Crear el proyecto
```sh
$ scrapy startproject <nameProject>
$ cd <nameProject>
$ scrapy genspider <nameSpider>
```
**Genera la siguiente [estructura](https://ascii-tree-generator.com/)**

```tree
nameProject/
├─ __pycache__/
├─ __init__.py
├─ items.py
├─ middleware.py
├─ settings.py
├─ pipelines.py
├─ Spiders/
│  ├─ jobs
```

**El archivo `<nameSpider>` contiene**
    
![scrapy](https://lh4.googleusercontent.com/MstoqWfPU0cLZPV8ZsYieHtAGtlwAcGRjDLlV7iPZJGdyGq1qUd_kZC7ZXI8FNgcuaVUVI9gphORf5WwwRiyyKjaI81rpHBj-af0WeIcVL74fE2qnLRofM0g9uC2JdQ08LVPm7vY)

> La clase JobsSpider es con la cual declaramos nuestra araña, y está heredando de scrapy.Spider, este es la araña por default que tiene scrapy

Dentro del método parse es donde escribimos lo que probamos en la shell scrapy

```py
import pprint
    ...
    def parse(self, response):
        nameVar = response.css("div.row div.col-md-8 div.quote span.text::text").getall()
        pprint.pprint(nameVar) 
```
4. Ejecutar la araña
```sh
$ scrapy crawl <nameAraña>
```
5. crear nuestros items : abrir el archivo items.py

En la clase agregamos nuestros items como nos muestra el ejemplo
```py
class ...
    nameVar = scrapy.Field()
```
6. usar los items en archivo `<nameSpider>`

Primero importamos los items 

```py
from <nameProject>.items import <nameProject>Item
```

En el método parse agregamos y modificamos las variables donde guardamos los resultados

```py
 def parse(self, response):
    item = PythonJobItem()
    item['job'] = response.css("div.row div.col-md-8 div.quote span.text::text").getall()
    yield item #se usa para iterar la respuesta
```

7. guardamos en un archivo
```sh
$ scrapy crawl -o <nameArchivo.extension> <nameAraña>
```

## Pipelines

procesos que se ejecutan después de la extracción de datos que hizo la araña.

**principales usos**

- Limpiar datos HTML
- validando datos raspados (verificando que los elementos contengan ciertos campos)
- buscando duplicados (y eliminarlos)
- almacenar el elemento raspado en una base de datos

usar postgress, istalar y crear una base de datos e instalar en nuestro env
```sh
$ pip3 install psycog2-binary
```
    

