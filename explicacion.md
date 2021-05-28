
<style type="text/css">
  .center-image
    {
        margin: 0 auto;
        display: block;
    }
</style>

# Explicacion

Los sistemas de control de versiones *VCS* (por sus siglas en inglés)
son herramientas que facilitan hacer un seguimiento sobre cambios
"*proyecto.txt*", "*proyecto1.txt*", "*proyectofinal.txt*", 
"*proyectofinalestesi.txt*" ...

![](imgs/drake.jpeg){: .center-image }

¿Por qué se considera tan valioso? Cuando se está trabajando solo se guardan
*capturas* del proyecto, guardando una serie de notas de por qué se hicieron 
ciertos cambios, permite trabajar en paralelo en rutas de desarrollo diferentes
y más. Pero son especialmente importantes cuando se trabajan con múltiples 
personas, permitiendo escribir la historia de código entre todos, ver 
sencillamente los cambios de los otros y resolver conflictos cuando dos
usuarios están cambiando las mismas lineas de un archivo.  
Aunque existen múltiples *VCS*, Git es el más usado actualmente. Sin embargo, 
Git es conocido por lo dificl que es aprenderlo, pero sus conceptos más básicos

![](imgs/how_works.png){: .center-image }

Entonces git es un sistema de versionamiento de versiones, ¿pero es lo mismo
que *GitHub*, absolutamente NO. Git es un programa que se instala dentro de tu
computador (no en la nube). GitHub es un _hosting_ de repositorios git,
es decir, si bien nosotros decidimos guardar una copia de nuestro repositorio
git en GitHub, también podríamos utilizar cualquier otro servicio como 
BitBucket, GitLab, o hasta
[crear uno privado](https://git-scm.com/book/en/v2/Git-on-the-Server-The-Protocols)
con nuestros propios protocolos de seguridad en la organización.

## Conceptos

Git modela la historia de una colección de carpetas y archivos como una serie
de Snapshots (instantáneas) en git llamados **commit**.
En terminología Git, un archivo es un **blob**
y son simplemente bytes. Un directorio se conoce como **tree** y en su definición
incluye referencias a blobs o a otros trees.  En la siguiente figura se muestra un
ejemplo.

```console
<root> (tree)
|
+- foo (tree)
|  |
|  + bar.txt (blob)
|
+- baz.txt (blob)
```

### Commits

Una manera relativamente sencilla e ingenua de modelar los snapshots sería una historia lineal.
Gráficamente sería algo así:

```console
A1 <-- A2 <-- A3 <-- A4
```

En este diagrama, las `A#` representan los commits, y la flecha apunta al commit anterior,
es decir, el commit más a la derecha es el último y el commit anterior
(que a veces se llama padre) es el que esta consecutivamente a su izquierda.  
Pero en git, un commit no está limitado a contener un solo padre, puede tener
múltiples esto representaría trabajar bajo dos tareas en paralelo y después
unir su trabajo. Algo así:

```console
A1 <-- A2 <-- A3 <-- A3B2
       ^             /
        \           v
        B1  <----  B2
```

En git los commits son inmutables. Esto no significa que los errores
no se puedan borrar de la historia, simplemente que editarlos implicaría
crear nuevos commits. 

### Referencias

Para git, todos los objetos (**commit**, **blob**, **tree**) están
referenciados por su [SHA-1](https://en.wikipedia.org/wiki/SHA-1)
esto puede ser estorboso, ya que los seres humanos no son buenos memorizando
40 carácteres hexadecimales. Por esto, se crean las referencias, las
referencias se hacen a los commits, entre las más generales están
`main` antes llamada `master`, que suele representar el último commit
del código "estable". También a modo de ejemplo, podemos ver la
referencia al commit actual, llamada `HEAD`.


## Configuracion por primera vez

Una vez teniendo git en nuestro computador. Hay que hacer unas pocas
cosas para configurarlo. En general usaremos el comando _git config_
para hacer esto. Las variables de entorno se encuentran en 3 diferentes
niveles.
- `[path]/etc/gitconfig` (`$HOME/.gitconfig` en Windows):
        Variables del sistema, en general no quisieramos tocar este.
- `~/.gitconfig` o `~/.config/git/config`: Variables de usuario.
- `config` archivo que está en cada repositorio git en la ruta `.git/config`.

Puedes ver tus configuraciones y de que ruta vienen utilizando el comando
```console
git config --list --show-origin
```

### Configuraciones básicas

#### Identidad
Git necesita usar un nombre y correo para hacer los commits. Se configuran
para el sistema de la siguiente manera.

```console
git config --global user.name "Pablo Osorio"
git config --global user.email pablo.osorio@bigbangdata.com.co
```

Y si por ejemplo, yo quisiese utilizar un correo diferente para un proyecto
en particular, me puedo meter a la carpeta de ese proyecto y correr los mismos
comandos sin `--global`. Esto sería:

```console
git config user.email pablo.osorio@empresa.com
```

Donde este correo solo se utilizaría para este proyecto y para el resto
seguiría usando el predefinido en global.

#### Editor de texto
Git necesita usar un editor de texto para escribir los mensajes.
Entre los más comunes están _notepad_ (recomendado para iniciar),
_code_ (vscode), _vim_, _emacs_.

Basta con el siguiente comando
```console
git config --global core.editor notepad
```


### Crear repositorio (git)
En git, tu carpeta de archivos incluyendo toda su historia y configuraciones
se llama repositorio. Para crear un respositorio hay que seguir los siguientes
pasos:

- Ve al directorio donde quieras guardar el proyecto.
- Escribe en la consola `git init`.
- `git add <nombre archivo>` para incluir en el repositorio los archivos que queremos.
- `git commit` y se escribe un mensaje normalmente como `first commit` o
  algo describiendo el trabajo hecho.


### .gitignore

El archivo `.gitignore`, es un archivo de texto que le dice a Git qué archivos
o carpetas ignorar en un proyecto.  

Tiene ciertos carácteres especiales utiles de conocer
- `*` se utiliza como una coincidencia comodín.
- `/` se usa para ignorar las rutas relativas al archivo .gitignore.
- `#` Comentarios

Es importante incluir archivos que no sean código acá, por ejemplo, imágenes
generadas por código, copias de seguridad creadas por nuestro editor de texto,
resultados generados de correr un script o datos sensibles.
Como una "regla de dedo" podemos tener la regla de que si no es código o texto,
probablemente no debería ir en el repositorio git.  

Github propone unos genéricos cuando vamos a crear un proyecto y a la gente
también le gusta publicar algunos que van mejorando en la web


```console

# Carpetas con archivos de datos
data/

# Ignorar archivos creados por Jupyter
.ipynb_checkpoints

# Sphinx documentation
docs/_build/

# Configuraciones editories
.vscode/
.idea/

# Ignorar todos los archivos .csv
*.csv
```



