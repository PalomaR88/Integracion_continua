# Introducción a la integración continua
Para realizar la tareas podemos escoger el sistema de integración continúa que queramos: travis, gitlab, github actions, …

### Tarea 1: Despliegue de una página web estática (build, deploy)
En esta práctica investiga como generar una página web estática con la herramienta que elegiste en la práctica 1 de la asignatura y desplegarla en el servicio que utilizaste en esa práctica.
- En el repositorio GitHub sólo tienen que estar los ficheros markdown.
- La página se debe generar en el sistema de integración continúa, por lo tanto debemos instalar las herramientas necesarias.
- Investiga si podemos desplegar de forma automática en el servicio elegido (si es necesario cambia el servicio de hosting para el despliegue).

Para el despliegue de la página estática se ha utilizado Jekyll y GitHub-Pages. A coninuación se va a implementar travis. Para ello, se crear un nuevo repositorio en GitHub con todos los ficheros de configuración de Jekyll, en él, se crea una rama para alojar los html.

En este repositorio además se añade un fichero de configuración, **.travis.yml** con el siguiente contenido:
~~~
language: ruby
rvm:
  - 2.5.5

before_install:
#  - gem update --system
  - gem install bundler
  -
script:
  - bundle install
  - bundle exec jekyll build

branches:
  only:
  - master				

env:
  global:
  - NOKOGIRI_USE_SYSTEM_LIBRARIES=true	
sudo: false				

addons:
  apt:
    packages:
    - libcurl4-openssl-dev

cache: bundler

notifications:				
  email: false				

deploy:					
  provider: pages			
  skip_cleanup: true			
  local_dir: _site		
  github_token: $github_token
  on:					
    repo: PalomaR88/palomar88.github.io
    on:					
      branch: master			
  fqdn: palomar88.github.io
~~~

En travis-ci.com se seleccionan los repositorios que queramos que se utilicen, en nuestro caso solo un.
[imagen](imagen/aimg.png)

En el repositorio hay que crear el token en la siguiente ventana en el apartado setting:
[imagen](imagen/bimg.png)

Con las siguientes opciones:
[imagen](imagen/cimg.png)

Y en travis se introduce la clave del token que se ha creado:
[imagen](imagen/dimg.png)

[Pincha aquí para ver la página creada](https://palomar88.github.io/)

### Tarea 2: Integración continúa de aplicación django (Test + Deploy)
Vamos a trabajar con el repositorio de la aplicación django_tutorial. Esta aplicación tiene definidas una serie de test, que podemos estudiar en el fichero tests.py del directorio polls.

Para ejecutar las pruebas unitarias, ejecutamos la instrucción python3 manage.py test.

Estudia las distintas pruebas que se han realizado, y modifica el código de la aplicación para que al menos una de ella no se ejecute de manera exitosa.

A continuación vamos a configurar la integración continúa para que cada vez que hagamos un commit se haga la ejecución de test en travis.

Crea un fichero .travis.yml para realizar de los tests en travis. Entrega el fichero .travis.yml, una captura de pantalla con un resltado exitoso de la IC y otro con un error.

Siguiendo la guía de esta página: Continuous delivery of a Django app from Travis CI to PythonAnywhere. Para además de realizar los tests, se haga un despliegue al servicio pythonanyhere.

Entrega un breve descripción de los pasos más importantes para realizar el despliegue desde travis.





