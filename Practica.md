# Introducción a la integración continua
Para realizar la tareas podemos escoger el sistema de integración continúa que queramos: travis, gitlab, github actions, …

### Tarea 1: Despliegue de una página web estática (build, deploy)
En esta práctica investiga como generar una página web estática con la herramienta que elegiste en la práctica 1 de la asignatura y desplegarla en el servicio que utilizaste en esa práctica.
- En el repositorio GitHub sólo tienen que estar los ficheros markdown.
- La página se debe generar en el sistema de integración continúa, por lo tanto debemos instalar las herramientas necesarias.
- Investiga si podemos desplegar de forma automática en el servicio elegido (si es necesario cambia el servicio de hosting para el despliegue).

Esta tarea se va a llevar a cabo con Jeckyll y Github Pages.

### Tarea 2: Integración continúa de aplicación django (Test + Deploy)
Vamos a trabajar con el repositorio de la aplicación django_tutorial. Esta aplicación tiene definidas una serie de test, que podemos estudiar en el fichero tests.py del directorio polls.

Para ejecutar las pruebas unitarias, ejecutamos la instrucción python3 manage.py test.

Estudia las distintas pruebas que se han realizado, y modifica el código de la aplicación para que al menos una de ella no se ejecute de manera exitosa.

A continuación vamos a configurar la integración continúa para que cada vez que hagamos un commit se haga la ejecución de test en travis.

Crea un fichero .travis.yml para realizar de los tests en travis. Entrega el fichero .travis.yml, una captura de pantalla con un resltado exitoso de la IC y otro con un error.

Siguiendo la guía de esta página: Continuous delivery of a Django app from Travis CI to PythonAnywhere. Para además de realizar los tests, se haga un despliegue al servicio pythonanyhere.

Entrega un breve descripción de los pasos más importantes para realizar el despliegue desde travis.





