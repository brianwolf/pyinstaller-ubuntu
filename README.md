# :card_index_dividers:	pyinstaller-ubuntu

> Imagen de Ubuntu 18.04 con Python 3.8 y Pyinstaller 3.6

Esta imagen se creó debido a que la version de python oficial tiene una version de *gcc* diferente a la usada en Ubuntu, esto hace que pyinstaller genere un ejecutable que no funciona en SO basadas en Ubuntu

![alt text](docs/img/ubuntu.jpg)
![alt text](docs/img/python.png)

---

## :tada: Uso

Se ejecuta con **docker run** seguido de **pyinstaller**

```\
docker run -it --rm \
-v $(pwd):/usr/src \
brianwolf94/pyinstaller-ubuntu \
  pyinstaller app.py \
    --clean \
    --onefile \
    --name app-script \
    --add-data="resources/version.txt:resources"
```

## :scroll: Scripts

Se dejan scripts para facilitar el manejo del proyecto, la cual contiene scripts para docker, heroku, python, etc.
Para ejecutarlos hay que pararse en la ruta raiz del proyecto y llamar el script desde ahi, ejemplo:
`./scripts/docker/build.sh`

## :package: Despliegue

La aplicacion se despliega de forma automatica utilizando *CircleCI* cada vez que se realiza un merge a la rama *master*,
para ello utiliza los scripts dentro de la carpeta `scripts/`, es decir que ejecutar los scripts manualmente es similar a lo que ejecutan las tasks dentro de los jobs del pipeline de circleci

Este despliegue consiste en:

* Construir una nueva imagen de docker
* Crear un tag para la imagen con la version acortada del commit de *github*
* Subir la imagen a *docker hub*
* Actualizar la version *latest* existente en docker hub a esta ultima

## :earth_americas: Paginas

* [Docker Hub Generado](https://hub.docker.com/repository/docker/brianwolf94/pyinstaller-ubuntu)
* [CircleCI](https://circleci.com/)
* [Emoticones del Readme](https://github.com/ikatyang/emoji-cheat-sheet)

## :grin: Autor

> **Brian Lobo**

* Github: [brianwolf](https://github.com/brianwolf)
* Docker Hub:  [brianwolf94](https://hub.docker.com/u/brianwolf94)
