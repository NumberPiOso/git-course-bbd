
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
en los archivos. Por ejemplo, cuando se editó un archivo, quién
lo hizo, cuál fue la razón y nos permiten volver a versiones anteriores de
código. Esto sin tener que recurrir a copias innecesarias de archivos tipo 
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
son hermosos y pueden ser fácilmente entendidos. Por eso es importante entender
los comandos y no utilizarlos como magia negra. Como revela el siguiente meme.

![](imgs/how_works.png){: .center-image }


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
