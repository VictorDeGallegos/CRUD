# Como crear un CRUD con Django y MySQL 🐍🐬

## Instalar herramientas necesarias 🧰

### Instalar python

```bash
sudo apt install python3
```

sitio oficial: <https://www.python.org/downloads/>

### Instalar django

Consola:

```bash
python3 -m pip install Django
```

Otra forma:

```bash
pip3 install Django
```

Consola python:

```python
print(django.get_version())
```

sitio oficial: <https://www.djangoproject.com/>

### Instalar mysql workbench

```bash
sudo apt install mysql-workbench
```

sitio oficial: <https://www.mysql.com/products/workbench/>

### Instalar Visual Studio Code

```bash
sudo snap install --classic code
```

sitio oficial: <https://code.visualstudio.com/>

### Descargar extensiones para VSCode

- [Bootstrap 5 Quick Snippets](https://marketplace.visualstudio.com/items?itemName=AnbuselvanRocky.bootstrap5-vscode)
- [Github copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)
- [Error Lens](https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens)
- [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
- [Trailing Spaces](https://marketplace.visualstudio.com/items?itemName=shardulm94.trailing-spaces)
- [Tabine](https://marketplace.visualstudio.com/items?itemName=TabNine.tabnine-vscode)
- [Shades of Purple](https://marketplace.visualstudio.com/items?itemName=ahmadawais.shades-of-purple)
- [Color the tag name](https://marketplace.visualstudio.com/items?itemName=jzmstrjp.color-the-tag-name)
- [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python)

## Crear proyecto 🚀

### Crear una carpeta vacia llamada **CRUD**

En esta carpeta se creara una nueva carpeta llamada **sistema** el cual tendrá la estructura de carpetas y archivos necesarios para el funcionamiento de django.

```bash
django-admin startproject sistema
```

### Iniciar servidor para probar el proyecto en CRUD/sistema

```bash
python3 manage.py runserver
```

Imagén de la pagina de inicio de django en la ruta <http://127.0.0.1:8000/>

![Servidor en linea](https://user-images.githubusercontent.com/41756950/198696290-f48833df-ac65-462a-967f-0eda9363f760.png)

## Crear primera apicacion 📱

Este sera el crud que deseamos construir y sera nombrado de acuerdo al contexto de la app en este caso lo llamaremos libreria.

Y sera creada dentro de la carpeta CRUD/**sistema**.

```bash
python3 manage.py startapp libreria
```

Una vez creada la app se debe registrar en la lista de apps en el archivo *settings.py* de la carpeta CRUD/**sistema**.

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'libreria' #aqui se registra la app
]
```

## Creando una vista 👁️

### Creando el primer inicio 👋🏻

En la carpeta CRUD/sistema/**libreria** se encuentra el archivo *views.py* el cual se encarga de manejar las vistas de la app.

Aqui se creara una funcion que retornara un inicio.

```python
def inicio(request):
    return HttpResponse("Hola mundo")
```

### Creando la ruta de la vista 🛣️

En la carpeta CRUD/sistema/**libreria**  se debe crear un archivo llamado *urls.py* el cual se encarga de manejar las rutas de la app.

Aqui se creara una ruta que apunte a la vista creada anteriormente.

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio, name='inicio'),
]
```

Ahora se debe registrar la ruta en el archivo *urls.py* de la carpeta CRUD/sistema/**sistema** .

```python
from django.conf.urls import include
from django.contrib import admin
from django.urls import path, include #importar include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('libreria.urls')) #aqui se registra la ruta
]
```

Si se ejecuta el servidor y se ingresa a la ruta <http://127.0.0.1:8000/> se debera mostrar el inicio.

![Hola mundo](https://user-images.githubusercontent.com/41756950/198713593-e14c8efe-48db-47be-9ab8-72a7531a6195.png)

## Vista HTML de libreria 🖼️

Ahora nos concentraremos en *urls.py* y *views.py* de la carpteta CRUD/sistema/**libreria** .

### Crear carpeta templates 🖌️

En la carpeta CRUD/sistema/**libreria**  se debe crear una carpeta llamada **templates**.

En esta carpeta se crearan las vistas de la aplicacion.

Debtro de templates se creara una nueva carpeta llamada **paginas** aqui crearemos archivos html que seran las vistas de la aplicacion por ejemplo crear la vista nosotros.html utilizando el signo `!` para que emmet nos porporcione el código HTML.

- nosotros.html:

  ```html
        <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Nosotros</title>
    </head>
    <body>
        Seccion de nosotros
    </body>
    </html>
    ```

Y acceder mediante las vistas en CRUD/sistema/libreria/**views.py** para generar una funcion render que retornara el html.

```python
def nosotros(request):
    return render(request, 'paginas/nosotros.html')
```

Posteriormente se debe registrar la ruta o acceso en el archivo *urls.py* de la carpeta CRUD/sistema/**libreria** .

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio, name='inicio'),
    path('nosotros/', views.nosotros, name='nosotros'), #aqui se registra la ruta
]
```

Si se ejecuta el servidor y se ingresa a la ruta <http://127.0.0.1:8000/nosotros> se debera mostrar la vista.

![Nosotros](https://user-images.githubusercontent.com/41756950/198713843-a470b457-3d5c-428f-9a04-d59c078f461b.png)

## Plantilla base HTML 🌱

Ahora crearemos una plantilla base para que todas las vistas hereden de ella.

La plantilla base se creara en la carpeta CRUD/sistema/libreria/**templates**  en la carpeta **templates**.

Al crear la plantilla utilizar el comando `!bs5` para generar el codigo HTML de bootstrap considerando que tendra un *MENU* y un *CONTENEDOR* se debe considerar agregar `{% load static %}` al inicio por tratarse una plantilla y asignar `{block + 'algo'}`  *espacio* `{% endblock %}` a los datos dinámicos.

```html
{% load static %}
<!DOCTYPE html>
<style>
  footer {
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    color: black;
    text-align: center;
  }
</style>
<html lang="en">
  <head>
    <title>{% block titulo%} {% endblock %}</title>
    <!-- Required meta tags -->
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no" />

    <!-- Bootstrap CSS v5.2.1 -->
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.1/dist/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-iYQeCzEYFbKjA/T2uDLTpkwGzCiq6soy8tYaI1GyVh/UjpbCx/TYkiZhlZB6+fzT"
      crossorigin="anonymous"
    />
  </head>

  <body>
    <header>
      <nav class="navbar navbar-expand navbar-light bg-light">
        <div class="nav navbar-nav">
          <a class="nav-item nav-link" href="{% url 'inicio' %}">Inicio</a>
          <a class="nav-item nav-link" href="{% url 'libros' %}">Libros</a>
          <a class="nav-item nav-link" href="{% url 'nosotros' %}">Nosotros</a>
        </div>
      </nav>
    </header>
    <main>
      <div class="container">
        <div class="row">
          <div class="col-12">
            <!-- <h1>Bienvenidos</h1> -->
            {% block contenido%} {% endblock %}
          </div>
        </div>
      </div>
    </main>
    <footer>
      <div class="container">
        <div class="row">
          <div class="col">
            <br />
            <p style="text-align: center">Hecho con ❤️</p>
          </div>
        </div>
      </div>
    </footer>
    <!-- Bootstrap JavaScript Libraries -->
    <script
      src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.11.6/dist/umd/popper.min.js"
      integrity="sha384-oBqDVmMz9ATKxIep9tiCxS/Z9fNfEXiDAYTujMAeBAsjFuCZSmKbSSUnQlmh/jp3"
      crossorigin="anonymous"
    ></script>

    <script
      src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.1/dist/js/bootstrap.min.js"
      integrity="sha384-7VPbUDkoPSGFnVtYi0QogXtr74QeVeeIs99Qfg5YCF+TidwNdjvaKZX19NZ/e6oz"
      crossorigin="anonymous"
    ></script>
  </body>
</html>


```

Para verlo en funcionamiento en necesario implementarlo en CRUD/sistema/libreria/templates/paginas/**nosotros.html**

- Editar el archivo **nosotros.html** y agregar `{% extends 'base.html' %}` para indicar que hereda de la plantilla base.

```html
{% extends 'base.html'%} {% block titulo%} Nosotros {% endblock %} {% block contenido%}
<div class="row">
  <div class="col-12">
    <h2 style="text-align: center">¿Quien soy?</h2>
    <br />
    <!-- Tarjeta contacto -->
    <div class="card" style="width: 18rem; margin: 0px auto">
      <img src="https://avatars.githubusercontent.com/u/41756950?v=4" class="card-img-top" alt="..." />
      <div class="card-body">
        <h5 class="card-title text-center">Victor Hugo Gallegos Mota</h5>
        <p class="card-text text-center">Estudiante de Ciencias de la Computación en Universidad Nacional Autónoma de México</p>
        <!-- redes sociales -->
        <div class="row">
          <div class="col-12 text-center">
            <a href="https://github.com/VictorDeGallegos  " target="_blank">
              <img src="https://img.icons8.com/ios-filled/50/000000/github.png" />
            </a>
            <a href="https://mx.linkedin.com/in/victor-hugo-gallegos-mota-462102253?trk=profile-badge" target="_blank">
              <img src="https://img.icons8.com/ios-filled/50/000000/linkedin.png" />
            </a>
          </div>

          {% endblock %}
        </div>
      </div>
    </div>
  </div>
</div>

```

Y así se vera en el navegador.

![Nosotros](https://user-images.githubusercontent.com/41756950/198937188-fd76de07-a0e6-44f1-8e1e-4c44d362263d.png)

## Vista del CRUD de libros 📚

Vamos a crear la aprte donde se van a gestionar los datos del CRUD  de libros, para ello vamos a crear una carpeta llamada **libros** en CRUD/sistema/libreria/templates. y dentro de esta carpeta vamos a crear los siguientes archivos

- **index.html:** el cual servirá para msotrar todos los registros y poder editarlos.
- **crear.html:** el cual servirá para crear un formulario y crear los libros.
- **editar.html** el cual servirá para editar la informacion del libro seleccionado.
- **form.html** el cual servirá para crear un formulario y poder reutilizarlo en los archivos crear.html y editar.html.

### Vista index.html

Procedemos a poner la misma estructura como en sistema/libreria/templates/paginas/**nosotros.html** modificando el titulo y el contenido utilizando `bs5-card-head-foot` y debajo del titulo de la tarjeta utilizamos el comando `bs5-table-default` para generar una tabla donde mostrar los libros.

```html
{% extends 'base.html'%} {% block titulo%} Lista de libros {% endblock %} {% block contenido%}
<div class="row">
  <div class="col-12">
    <div class="card">
      <div class="card-header">Listar libros</div>
      <div class="card-body">
        <h4 class="card-title">Libros</h4>

        <div class="table-responsive">
          <table class="table table-striped">
            <thead>
              <tr>
                <th scope="col">ID</th>
                <th scope="col">Titulo</th>
                <th scope="col">Imagen</th>
                <th scope="col">Descripcion</th>
                <th scope="col">Acciones</th>
              </tr>
            </thead>
            <tbody>
              <tr class="">
                <td>1</td>
                <td>Django con python</td>
                <td>libro.png</td>
                <td>Como aprender django en 5 minutos</td>
                <td>Editar | Eliminar</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <!-- <div class="card-footer text-muted">Escrito con ❤️</div> -->
    </div>
  </div>
  {% endblock %}
</div>
```

### Vista crear.html

Procedemos a poner la misma estructura como en sistema/libreria/templates/paginas/**nosotros.html** modificando el titulo y el contenido.

```html
{% extends 'base.html'%} {% block titulo%} Agregar nuevo libro {% endblock %} {% block contenido%} Formulario para agregar nuevo libro {%
endblock %}
```

### Vista editar.html

Procedemos a poner la misma estructura como en sistema/libreria/templates/paginas/**nosotros.html** modificando el titulo y el contenido.

```html
{% extends 'base.html'%} {% block titulo%} Editar libro {% endblock %} {% block contenido%} Formulario para editar libro {%
endblock %}
```

## Accediendo a la tabla de libros 📚🛹

Ahora tendremos que dirigirnos al archivo CRUD/sistema/libreria/**views.py** y renderizar las vistas que acabamos de crear.

```python
from django.shortcuts import render
from django.http import HttpResponse
# Create your views here.


def inicio(request):
    return HttpResponse('<h1>Hola mundo</h1>')


def nosotros(request):
    return render(request, 'paginas/nosotros.html')


def libros(request):
    return render(request, 'libros/libros.html') #Agregamos esta linea para renderizar la vista libros.html
```

Ahora debemos de crear una ruta para poder acceder a la vista libros.html, para ello debemos de dirigirnos al archivo CRUD/sistema/libreria/**urls.py** y agregar la siguiente linea.

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio, name='inicio'),
    path('nosotros/', views.nosotros, name='nosotros'),
    path('libros/', views.libros, name='libros'), #Agregamos esta linea para poder acceder a la vista libros.html
]
```

## Creando el menu de navegacion 🏄🏻‍♂️

Es necesario modificar la pagina de inicio pues solo imprimia un texto al inicio copiando el template de la pagina nosotros.html y modificando el titulo y el contenido el cual se genera con el comando `bs5-jumbutron-default`.

```html
{% extends 'base.html'%} {% block titulo%} Inicio {% endblock %} {% block contenido%}

<div class="row align-items-md-stretch">
  <div class="col-md-12">
    <div class="h-100 p-5 bg-white border rounded-3">
      <h1>Bienvenido a mi CRUD</h1>
      <!-- agregar linea  -->
      <hr />
      <p>
        Un crud es un sistema de gestión de datos que permite crear, leer, actualizar y eliminar datos de una base de datos, este programa
        se realizo en mi framework favorito Django utilizando MySQL
      </p>
      <button class="btn btn-dark" type="button">Comenzar</button>
    </div>
  </div>
</div>

{% endblock %}

```

Despues de generar el HTML se debe hacer el cambio en CRUD/sistema/libreria/**views.py**

```python
def inicio(request):
    return render(request, 'paginas/inicio.html') #Agregamos esta linea para renderizar la vista libros.html


def nosotros(request):
    return render(request, 'paginas/nosotros.html')


def libros(request):
    return render(request, 'libros/index.html')
```

Ahora en la **base.html** debemos modificar las rutas para que se pueda navegar de una pestaña a otra.

```html
    <header>
      <nav class="navbar navbar-expand navbar-light bg-light">
        <div class="nav navbar-nav">
          <a class="nav-item nav-link" href="{% url 'inicio' %}">Inicio</a>
          <a class="nav-item nav-link" href="{% url 'libros' %}">Libros</a>
          <a class="nav-item nav-link" href="{% url 'nosotros' %}">Nosotros</a>
        </div>
      </nav>
    </header>
```

## Acceso a la vista 🔓👁️

Dedemos modificar el archivo sistema/libreria/templates/libros/**index.html** y agregar un boton con el comando `bs5-button-a`

Remmplazar

```html
<div class="card-header">Listar libros</div>
```

Por

```html
      <a name="" id="" class="btn btn-primary" href="#" role="button">Button</a>
```

Despues debemos agregar la vista en CURD/sistema/libreria/**views.py**

```python
from django.shortcuts import render
from django.http import HttpResponse
# Create your views here.


def inicio(request):
    return render(request, 'paginas/inicio.html')


def nosotros(request):
    return render(request, 'paginas/nosotros.html')


def libros(request):
    return render(request, 'libros/index.html')


def crear(request):
    return render(request, 'libros/crear.html') #Agregamos esta linea para renderizar la vista libros.html

```

Ahora debemos de crear una ruta para poder acceder a la vista libros.html, para ello debemos de dirigirnos al archivo CRUD/sistema/libreria/**urls.py** y agregar la siguiente linea.

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio, name="inicio"),
    path('nosotros', views.nosotros, name="nosotros"),
    path('libros', views.libros, name="libros"),
    path('libros/crear', views.crear, name="crear"), #Agregamos esta linea para poder acceder a la vista libros.html
]
```

Modificamos sistema/libreria/templates/libros/**index.html** agregando la ruta en el boton

```html
    <a name="" id="" class="btn btn-primary" href="{% url 'crear' %}" role="button">Button</a>
```

Probamos la ruta y nos muestra la siguiente pagina

![libros index](https://user-images.githubusercontent.com/41756950/198752225-50054014-8194-4669-93b1-698b77650db6.png)

## Crear formulario vista 📝

Debemos de crear un formulario para poder crear un libro, para ello debemos de dirigirnos al archivo sistema/libreria/templates/libros/**form.html** y agregar el siguiente codigo, primero declarar el formulario usando comando `bs5-form-input` y editar

```html
<form enctype="multipart/form-data" method="post">
  <div class="mb-3">
    <label for="" class="form-label">Nombre</label>
    <input type="text" class="form-control" name="" id="" aria-describedby="helpId" placeholder="Nombre" />
  </div>
</form>

```

Posteriormente ir a sistema/libreria/templates/libros/**crear.html** y usar el comando `bs5-card-head-foot`

```html
{% extends 'base.html'%} {% block titulo%} Agregar nuevo libro {% endblock %} {% block contenido%}
<div class="card">
  <div class="card-header">Crear un libro</div>
  <div class="card-body">
    <h4 class="card-title">Datos del libro</h4>
    {% include 'libros/form.html' %}
  </div>
</div>
{%endblock %}
```

## Accediendo a la vista 👁️

Al igual que **crear.html** tiene como estructura la creacion de un libro se le pasara la misma a **editar.html**

Por lo tanto pasara de
```html
{% extends 'base.html'%} {% block titulo%} Editar Libro {% endblock %} {% block contenido%} 
Formulario para editar libro
{% endblock %}
```

a esto:

```html
{% extends 'base.html'%} {% block titulo%} Editar Libro {% endblock %} {% block contenido%}
<div class="card">
  <div class="card-header">Editar informacion del libro</div>
  <div class="card-body">
    <h4 class="card-title">Datos del libro</h4>
    {% include 'libros/form.html' %}
  </div>
</div>
{% endblock %}
```

Posteriormente debos regresar a sistema/libreria/templates/libros/**index.html** y modificar en Acciones el boton de editar usando el siguiente comando `bs5-button-a`

```html

```html
<td><a name="" id="" class="btn btn-warning" href="#" role="button">Editar</a> | Eliminar</td>
```

Del mismo modo que se agrego el boton de editar se agrega el boton de eliminar

```html
<td>
    <a name="" id="" class="btn btn-warning" href="#" role="button">Editar</a>
    <a name="" id="" class="btn btn-danger" href="#" role="button">Eliminar</a>
</td>
```

Si todo esta bien deberia de verse asi

![Libros con botones](https://user-images.githubusercontent.com/41756950/198754159-0e9dd575-1c2f-453c-8b05-b611d3761332.png)

Luego de crear los botones debemos ir a CRUD/sistema/libreria/**views.py** y agregar las siguientes lineas

```python
from django.shortcuts import render
from django.http import HttpResponse
# Create your views here.


def inicio(request):
    return render(request, 'paginas/inicio.html')


def nosotros(request):
    return render(request, 'paginas/nosotros.html')


def libros(request):
    return render(request, 'libros/index.html')


def crear(request):
    return render(request, 'libros/crear.html')


def editar(request):
    return render(request, 'libros/editar.html') #Agregamos esta linea para poder acceder a la vista editar.html
```

Y en CRUD/sistema/libreria/**urls.py** debemos de agregar la ruta para poder acceder a la vista editar.html

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio, name="inicio"),
    path('nosotros', views.nosotros, name="nosotros"),
    path('libros', views.libros, name="libros"),
    path('libros/crear', views.crear, name="crear"),
    path('libros/editar', views.editar, name="editar"), #Agregamos esta linea para poder acceder a la vista editar.html
]
```

Volvemos a sistema/libreria/templates/libros/**index.html** para asignarle la ruta al boton de editar

```html
<a name="" id="" class="btn btn-warning" href="{% url 'editar' %}" role="button">Editar</a>
```

## Conexión a la base de datos 📊

Primero debemos de crear una base de datos en MySQL, para ello debemos abrir MySQL Workbench y crear una base de datos llamada **libreria** con el siguiente comando en mysql

```sql
CREATE schema libreria;
```

Para poder conectar la base de datos debemos detener el servidor y dirigirnos a a CRUD/sistema/sistema/**settings.py** y remplazar lo siguiente

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```

por esto

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'libreria',
        'USER': 'root',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '3306'
    }
}
```

Despues de esto debemos de ejecutar el siguiente comando en la terminal para poder instalar el paquete `PyMySQL` el cual nos permitira conectarnos a la base de datos

```bash
pip3 install PyMySQL
```

Y con el siguiente comando se podran hacer la carga de las imagenes a la base de datos

```bash
pip3 install Pillow
```

con el siguiente comando listamos los paquetes que estan descargados

```bash
pip3 list
```

posteriormente demos ir a CRUD/sistema/sistema/**__init__.py** y agregar la siguiente linea

```python
import pymysql
pymysql.install_as_MySQLdb()
```

## Modelo y migraciones 📦

### Modelo 📋

El modelo es una tabla donde se almacenan los datos, para poder crear el modelo debemos de ir a CRUD/sistema/libreria/**models.py** y agregar el siguiente codigo

```python
from tabnanny import verbose
from django.db import models

# Create your models here.


class Libro(models.Model):
    id = models.AutoField(primary_key=True)
    titulo = models.CharField(max_length=50, verbose_name="Titulo")
    imagen = models.ImageField(
        upload_to='imagenes/', verbose_name="Imagen", null=True)
    descripcion = models.TextField(verbose_name="Descripción", null=True)
```

### Migraciones 📦

En este paso se crean las tablas en la base de datos, para ello debemos de ir a la terminal y ejecutar el siguiente comando

```bash
python3 manage.py makemigrations
```

```bash
python3 manage.py migrate
```

Esto nos va permitir subir la informacion

## Modificando la base de Datos 📊

si llegase a existir algun problema con algun campo de la base de datos se debe de actualizar el archivo CRUD/sistema/libreria/**models.py** y VOLVER a ejecutar los comandos de migraciones

## Accediendo al Admin de Django 🛠️

debemos acceder a CRUD/sistema/sistema/**admin.py** para poder controlar la base de datos desde el admin de Django como estamos trabajando con modelos debemos de importar el modelo que creamos anteriormente y registrar el modelo en el admin

```python
from django.contrib import admin
from .models import Libro #importamos el modelo Libro

# Register your models here.
admin.site.register(Libro) #registramos el modelo Libro
```

Despues de esto debemos de crear un superusuario para poder acceder al admin de Django

```bash
python3 manage.py createsuperuser
```

si exite un error instalar 'cryptography' con el siguiente comando

```bash
pip install cryptography
```

## Propiedades en modelo y admin 📋👤

Primero debemos de ir a CRUD/sistema/libreria/**models.py** y agregar la instrccion __str__(self) para devolver una lista de los datos del libro en el admin de Django

```python
from tabnanny import verbose
from django.db import models

# Create your models here.


class Libro(models.Model):
    id = models.AutoField(primary_key=True)
    titulo = models.CharField(max_length=50, verbose_name="Titulo")
    imagen = models.ImageField(
        upload_to='imagenes/', verbose_name="Imagen", null=True)
    descripcion = models.TextField(verbose_name="Descripción", null=True)

    def __str__(self):
        fila = "Titulo: " + self.titulo + " Descripcion: " + self.descripcion
        return fila #devuelve una lista de los datos del libro en el admin de Django

```

Para poder eliminar permanentemente la imagen de la base de datos debemos de agregar las siguientes lineas de código
  
  ```python
    def delete(self, using=None, keep_parents=False):
        self.imagen.storage.delete(self.imagen.name)
        super().delete()
  ```

  ## Mostrando los libros en el index 📋📚

  Tenemos que dirigirnos a CRUD/sistema/sistema/**views.py** y debemos identificar el elemento que nos ayuda a recibir informacion de la base de datos y mostrarla en el index, `def libros(request):` es el elemento que nos ayuda a recibir informacion de la base de datos y mostrarla en el index, para ello debemos de agregar el siguiente codigo

  ```python
from .models import Libro #importamos el modelo Libro
```

Posteriormente debemos modificar la funcion `def libros` de la siguiente manera

```python
def libros(request):
    # mostrar todos los libros en la tabla
    libros = Libro.objects.all()
    return render(request, 'libros/index.html', {'libros': libros})enviamos los libros a la vista index.html
```

y debemos ir a sistema/libreria/templates/libros/**index.html** y modificar la tabla para ver los datos de la bd utilizando el ciclo for y los atributos de los modelos de la siguiente forma:

```html
<tbody>
  <!-- ciclo for -->
  {% for libro in libros %}
  <tr class="">
    <td>{{libro.id}}</td>
    <td>{{libro.titulo}}</td>
    <td>{{libro.imagen}}</td>
    <td>{{libro.descripcion}}</td>
    <td>
      <a name="" id="" class="btn btn-warning" href="{% url 'editar' %}" role="button">Editar</a>
      <a name="" id="" class="btn btn-danger" href="#" role="button">Eliminar</a>
    </td>
  </tr>
  {% endfor %}
</tbody>
```

## URL para mostrar imagenes en la vista 📋📷

Primero debemos ir a sistema/libreria/templates/libros/**index.html** y modificar el campo donde se muestra la imagen indicando que es una imagen

```html
<td><img src="{{libro.imagen.url}}" height="100px" /></td>
```

Ahora debemos dirigirnos a CRUD/sistema/sistema/**settings.py** y debemos importar las utilerias del sistema operativo

```python
import os
```

Diriginos al final del archivo y agregamos la siguiente linea de codigo

```python
MEDIA_ROOT = os.path.join(BASE_DIR, '')
MEDIA_URL = '/imagenes/'
```

Despues debemos dirigirnos a CRUD/sistema/libreria/**urls.py**  y demeos importar clases que nos van ayudar a acceder a las imagenes

```python
from django.conf import settings
from django.contrib.staticfiles.urls import static
```

y agregar al final del corchete de urlpatterns la siguiente linea de codigo

```python
from django.urls import path
from . import views

from django.conf import settings
from django.contrib.staticfiles.urls import static

urlpatterns = [
    path('', views.inicio, name="inicio"),
    path('nosotros', views.nosotros, name="nosotros"),
    path('libros', views.libros, name="libros"),
    path('libros/crear', views.crear, name="crear"),
    path('libros/editar', views.editar, name="editar"),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT) #agregamos esta linea de codigo
```

## Crear estructura del formulario 📋📝

Para crear un formulario es necesario crear un archivo en la siguiente ruta CRUD/sistema/libreria/**forms.py** y debemos de importar la clase `forms` y el modelo `Libro` de la siguiente manera

```python
from django import forms
from .models import Libro
```

Luego debemos crear una clase libro para poder mapear todos los campos del formulario con los campos del modelo de la siguiente manera

```python
class LibroForm(forms.ModelForm):
    class Meta:
        model = Libro
        fields = '__all__'
```

Una vez hecho esto nos debemos dirigir a sistema/libreria/**views.py** e importar la clase `LibroForm` de la siguiente manera

```python
from .forms import LibroForm
```

Y modificar la funcion `def crear` para identificar todos los elementos que nos estan enviando a traves del formulario de la siguiente manera

```python
def crear(request):
    formulario = LibroForm(request.POST or None)
    return render(request, 'libros/crear.html', {'formulario': formulario})
```

Luego debemos ir a sistema/libreria/templates/libros/**form.html** para añadir un token de seguridad para evitar ataques CSRF y para poder enviar los datos del formulario a la vista `def crear` de la siguiente manera

```html
<form enctype="multipart/form-data" method="post">
{% csrf_token %} {% for campo in formulario %}
  <div class="mb-3">
    <label for="" class="form-label">Nombre</label>
    <input type="text" class="form-control" name="" id="" aria-describedby="helpId" placeholder="Nombre" />
  </div>
  {% endfor %}
</form>
```

## Mostrando el formulario en la vista 📋📝👀

En este punto debemos modificar el mismo formulario editando el tipo de dato por cada campo por ejemplo `{{ campo.field.widget.input_type}}` de la siguiente forma

A parte debemos modificar la etiqueta `label` para que muestre el nombre del campo de la siguiente manera `<label for="" class="form-label">{{ campo.label }}</label>`

Tambien debemos identificar la etiqueta `name` para modificar el nombre del campo de la siguiente manera `name="{{ campo.name }}"`

Y por ultimo identificar la etiqueta `placeholder` donde tambien debemos poner el `label`

Si existe algun error en el formulario podemos mostrarlo de la siguiente manera

```html
  <div class="col-12 help-text">{{campo.errors}}</div>
```

Y por ultimo necesitamos agregar un boton para enviar los datos del formulario de la siguiente manera

Todo junto quedaría de la siguiente manera

```html


<form enctype="multipart/form-data" method="post">
  {% csrf_token %} {% for campo in formulario %}
  <div class="mb-3">
    <label for="" class="form-label">{{ campo.label }}</label>
    <input
      type="{{ campo.field.widget.input_type}}"
      class="form-control"
      name="{{ campo.name }}"
      id=""
      aria-describedby="helpId"
      placeholder="{{ campo.label }}"
    />
  </div>
  <div class="col-12 help-text">{{campo.errors}}</div>
  {% endfor %}

  <input name="" id="" class="btn btn-success" type="submit" value="Enviar informacion" />
</form>

```

Y se mostraria de la siguiente manera

![Formulario](https://user-images.githubusercontent.com/41756950/198917704-52c949cc-cd08-4424-8030-c2115a1a2b67.png)

## Guardando libro ✅📗

Para lograr redireccionar la informacion primero debemos ir a CRUD/sistema/libreria/**views.py** y modificar la funcion `def crear` de la siguiente manera

Primero debemos importar redirect de la siguiente manera

```python
from django.shortcuts import render, redirect
```

luego modificamos la funcion `def crear` de la siguiente manera

```python
def crear(request):
    formulario = LibroForm(request.POST or None, request.FILES or None)
    if formulario.is_valid():
        formulario.save()  # guardar en la base de datos
        return redirect('libros')  # redireccionar a la vista libros
    return render(request, 'libros/crear.html', {'formulario': formulario})
```

## Borrando libro ❌📕

Para hacer esto debemos crear la funcion que nos permita eliminar el registro del libro seleccionado para esto debemos dirigirnos a CRUD/sistema/libreria/**views.py**

Aqui crearemos una funcion `def eliminar` de la siguiente manera la cual buscara por id el libro y lo eliminara devolviendo a la vista libros

```python
def eliminar(request, id):
    libro = Libro.objects.get(id=id)
    libro.delete()  # eliminar el libro
    return redirect('libros')   # redireccionar a la vista libros
```

Despues de crear la funcion se debe declarar el path en CRUD/sistema/libreria/**urls.py** de la siguiente manera

```python
path('eliminar/<int:id>', views.eliminar, name='eliminar'),
```

Despues volvemos al CRUD/sistema/libreria/templates/libros/**index.html** y editamos el boton para eliminar el libro de la siguiente manera

```html
<a
  name=""
  id=""
  class="btn btn-danger"
  href="{% url 'eliminar' libro.id %}"
  role="button"
  onclick="return confirm('¿Estas seguro de eliminar el libro?')"
  >Eliminar</a>
```

## Editando libro 📝📔

Para poder editar la informacion de un libro es necesario recuperar los datos del libro seleccionado enviando un parametro a treves de la url que le pueda decirr a la app que info se esta seleccioando para editar.

Primero debemos ir a CRUD/sistema/libreria/**urls.py** y agregar el path de la siguiente manera

```python
path('libros/editar/<int:id>', views.libros, name='editar'),
```

Posteriormente debemos ir a CRUD/sistema/libreria/**views.py** y modificar la funcion `def libros` de forma similar a eliminar para obtener por id solo que aqui recuperaremos la informacion de la siguiente manera

```python
def editar(request):
    libro = Libro.objects.get(id=id)
    formulario = LibroForm(request.POST or None,
                           request.FILES or None, instance=libro)
    return render(request, 'libros/editar.html', {'formulario': formulario})
```

Despues debemos ir a CRUD/sistema/libreria/templates/libros/**index.html** para mostrar la infromacion del libro seleccionado para editar por id

```html
<a name="" id="" class="btn btn-warning" href="{% url 'editar' libro.id %}" role="button">Editar</a>
```

Por ultimo debemos ir a CRUD/sistema/libreria/**views.py** y agregar id a los parametros que recibe la funcion `def editar` de la siguiente manera

```python
def editar(request, id):
    libro = Libro.objects.get(id=id)
    formulario = LibroForm(request.POST or None,
                           request.FILES or None, instance=libro)
    return render(request, 'libros/editar.html', {'formulario': formulario})
```

Despues debemos ir a CRUD/sistema/libreria/templates/libros/**form.html** para mostrar los datos en el input donde se muestra el valor
si no hay informacion en el input se mostrara default o vacio todo esto debajo de placeholder

```html
<form enctype="multipart/form-data" method="post">
  {% csrf_token %} {% for campo in formulario %}
  <div class="mb-3">
    <label for="" class="form-label">{{ campo.label }}</label>
    <input
      type="{{ campo.field.widget.input_type}}"
      class="form-control"
      name="{{ campo.name }}"
      id=""
      aria-describedby="helpId"
      placeholder="{{ campo.label }}"
      value="{{ campo.value | default:'' }}"
    />
  </div>
  <div class="col-12 help-text">{{campo.errors}}</div>
  {% endfor %}

  <input name="" id="" class="btn btn-success" type="submit" value="Enviar informacion" />
</form>
```

### Mostrar la imagen al editar 🖼✍🏼

Debemos ir a CRUD/sistema/libreria/templates/libros/**form.html** y debemos preguntar si se trata de un campo de tipo file para mostrarla de la siguiente manera

```html
<form enctype="multipart/form-data" method="post">
  {% csrf_token %} {% for campo in formulario %}
  <div class="mb-3">
    <label for="" class="form-label">{{ campo.label }}</label>
    {% if campo.field.widget.input_type == 'file' and campo.value %}
    <br />
    <img src="{{MEDIA_URL}}/imagenes/{{campo.value}}" width="100px" alt="" />
    {% endif %}
    <input
      type="{{ campo.field.widget.input_type}}"
      class="form-control"
      name="{{ campo.name }}"
      id=""
      aria-describedby="helpId"
      placeholder="{{ campo.label }}"
      value="{{ campo.value | default:'' }}"
    />
  </div>
  <div class="col-12 help-text">{{campo.errors}}</div>
  {% endfor %}

  <input name="" id="" class="btn btn-success" type="submit" value="Enviar informacion" />
</form>
```

Una vez hecho esto ya podemos editar la informacion de un libro y se veria de la siguiente manera

![Editar informacion](https://user-images.githubusercontent.com/41756950/198928451-1433e484-baee-4308-bd7d-72a970fc5ef3.png)

## Actualizando la informacion del registro 📝📔

Para actualizar la informacion de forma correcta debemos ir a CRUD/sistema/libreria/**views.py** y modificar la funcion `def editar` para crear un condicional que nos valide y guarde la informacion de la siguiente manera

```python
def editar(request, id):
    libro = Libro.objects.get(id=id)
    formulario = LibroForm(request.POST or None,
                           request.FILES or None, instance=libro)
    if formulario.is_valid() and request.POST:
        formulario.save()
        return redirect('libros')
    return render(request, 'libros/editar.html', {'formulario': formulario})
```
