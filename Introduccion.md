
# Introducción a la integración continúa y despliegue continuo
## Objetivos
- Conocer el software de integración continúa más utilizados
- Tener una primera experiencia con travis para realizar la integración continúa (en este caso simplemente realizar de forma automática que todos los cambios en nuestra página web estática es válida)
- Despliegue manual de nuestra página en el servicio surge.sh
- Entender el concepto de despliegue continúo y comprobar la función de despliegue de travis sobre surge.sh

## Contenidos
- Integración continua: La integración continua requiere que cada vez que alguien haga un commit se construya la aplicación entera y que se ejecuten una serie de tareas automatizados: Las pruebas y el despliegue se automatizan.
- Integración continua: Práctica de desarrollo software donde los miembros del equipo integran su trabajo frecuentemente, al menos una vez al día. Cada integración se verifica con un build automático (que incluye la ejecución de pruebas) para detectar errores de integración tan pronto como sea posible.

Procesos que se realizan en la IC:
- Se recoge el código fuente de un repositorio compartido.
- Se analiza el código
- Se compila o transforma el código necesario (build)
- Se ejecutan los test (unitarios, integrales y funcionales)
- Se generan informes y documentación

Es un cambio de paradigma. Es necesario la aceptación de los miembros del equipo, puesto que la integración continua es una práctica y no una herramienta.

## Integración continua
- **Entrega continua (EC)**: Es el siguiente paso de IC, y consiste en preparar la aplicación web para su puesta en producción. El paso a producción se hace de forma manual.
- **Despliegue continuo (DC)**: Es similar a la anterior pero en este caso también se automatiza el despliegue final en producción.

Herramientas
- Jenkins
- Travis
- gitlab
- github actions
- CircleCi
- Semaphore
- Codeship
- Shippable
- Go-Ci
- appveyor

## Prácticas
#### Ejercicio 1: Corrector ortográfico de documentos markdown (test)

#### Ejercicio 2: Comprobación de html5 válido y despliegue en surge.sh (test y deploy)
En este ejercicio queremos desplegar una página html5 en el servicio surge.sh, además queremos comprobar si el código html5 es válido. Estas dos operaciones: comprobar si el html5 es válido (test) y el despliegue en surge.sh (deploy) lo vamos a hacer con travis de forma automática (IC y DC).

Antes de empezar vamos a aprender a trabajar con surge.sh:
- Siguiendo las instrucciones de esta página instala NodeJS y npm.
~~~
vagrant@servidor:~$ sudo apt install curl
vagrant@servidor:~$ curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
vagrant@servidor:~$ sudo apt install nodejs
vagrant@servidor:~$ node -v
v10.18.0
vagrant@servidor:~$ sudo apt install build-essential libssl-dev
vagrant@servidor:~$ npm install express
~~~

- Instala surge.sh
~~~
vagrant@servidor:~$ npm install surge
vagrant@servidor:~$ sudo npm install --global surge
~~~

- Despliega una pequeña página web en el dominio tunombre.surge.sh.
~~~
vagrant@servidor:~$ surge

   Welcome to surge! (surge.sh)
   Login (or create surge account) by entering email & password.

          email: palomagarciacampon08@gmail.com
          password: 
          project: /home/vagrant/
          domain: palomagarciacampon.surge.sh
          upload: [] 100% eta: 0.0s (1 files, 57106 bytes)
            CDN: [====================] 100%
             IP: 45.55.110.124

   Success! - Published to palomagarciacampon.surge.sh
~~~



Vamos a añadir la funcionalidad de IC y DC con travis, para ello:
- Realiza un fork del repositorio de GitHub: https://github.com/josedom24/ic-travis-html5
~~~
vagrant@servidor:~$ git clone https://github.com/PalomaR88/ic-travis-html5.git
~~~

- Activa la IC en travis de tu repositorio.
En la página de Travis:
~~~
https://travis-ci.com/
~~~

- Comprueba la prueba y el despliegue que vamos a realizar estudiando el fichero .travis.yml.

- Modifica el fichero .travis.yml para poner el nombre de dominio que vas a utilizar.
~~~
deploy:
  provider: surge
  project: /home/vagrant
  domain: palomagarciacampon.surge.sh
  skip_cleanup: true
~~~

- Para que travis pueda hacer el despliegue en surge le tenemos que indicar un TOKEN. Genera el token:
~~~
  surge token
~~~
- Crea dos variables de entorno en settings del proyecto travis:
**SURGE_LOGIN**: Indica el correo electrónico que has utilizado como lógin en surge
**SURGE_TOKEN**: Indica el TOKEN que has obtenido en el paso anterior.


- Realiza cambios en el fichero index.html del directorio _build y comprueba, que si el código html5 es válido se despliega y puedes acceder a la página web. Si el código html5 no es válido no se realiza el despliegue y te mandan un correo informando de la incidencia.

Para seguir profundizanod en la integración continúa investiga y realiza el mismo ejercicio usando gitlab o github actions.