# git-training
Ejercicio de Git — Sistemas de Big Data

Material docente para el curso de especialización en Inteligencia Artificial y Big Data.

Este ejercicio está basado en el material original de Mario Carbonell, disponible en su repositorio git-training: https://github.com/mariocarbonelliesabastos/git-training
## Contexto
En este ejercicio se van realizar las acciones más comunes en el trabajo diario con un repositorio git.
Vamos a considerar que la rama main que existe en el repositorio remoto es la rama que únicamente contiene el código que esta en producción, es decir, código testeado y estable. Se va a crear una rama develop, que contendrá los evolutivos que se han terminado pero que no están listos para pasar a producción. Se crearán diversas ramas feature, que estan destinadas a almacenar el desarrollo de una funcionalidad concreta y atómica, lo que implica que este desarrollo no depende de otro ni ningún otro desarrollo depende de este. Por último se realizarán ramas release con sus tags correspondientes para indicar cuando se ha generado una versión del software.

En este ejercicio se va a utilizar una nomenclatura standard para las ramas y mensajes de los commits, esto facilíta la comprensión del histórico del repositorio.

Nombre de rama:
- feature/[nombre]: para ramas feature
- release/[version]: para ramas release

Mensaje de commit:
- feat:[mensaje]: para commits que crean funcionalidad
- fix:[mensaje]: para commits que corrigen funcionalidades

## Pasos

- - acceder a https://github.com/alfonsjoan/git-training y clonar el repositorio en el equipo local

        git clone https://github.com/alfonsjoan/git-training.git

- mostrar las ramas del repositorio

        git branch

- mostrar las ramas del repositorio incluyendo las ramas remotas

        git branch -a

- crear una rama local para develop

        git branch develop
        git checkout develop

- crear la primera rama feature, en el que se creará un fichero de texto. Este comando crea una rama y realiza el checkout a la misma.

        git checkout -b feature/create-txt-file

- crear un fichero de texto llamado commands.txt, y escribir en la primera línea "init command"

- mostrar el estado del repositorio

        git status

- añadir el fichero al stash

        git add commands.txt

- realizar el primer commit

        git commit -m "feat: first command"

- cambia a develop

        git checkout develop

- realiza el merge de la rama feature

        git merge feature/create-txt-file

- elimina la rama feature

        git branch -d feature/create-txt-file

- crea una feature para el segundo comando

        git checkout -b feature/run_command

- escribe el segundo comando en la linea siguiente del fichero commands.txt: run
- añade los cambios al stage y realiza el commit
- pasa a develop
- crea una feature para el tercer comando

        git checkout -b feature/write_command

- escribe el tercer comando en la linea siguiente del fichero commands.txt: write
- añade los cambios al stage y realiza el commit
- pasa a develop
- realiza el merge de la rama feature/run_command a develop y observa que git ha gestionado la fusión de los cambios
- pasa a la rama feature/write_command
- Pasar los cambios de develop a write ya que siempre se debe trabajar con una rama actualizada para evitar conflictos o desarrollos erroneos

        git merge develop

- Esta vez como en la rama feature y la rama develop hay cambios en la misma linea, git muestra un conflicto. Se debe resolver antes de seguir, para ello se debe tener en cuenta la funcionalidad concreta y se deben hacer pruebas del codigo para comprobar que se ha resuelto el conflicto correctamente.

Se puede observar que en la consola gitbash el nombre de la rama parece con el sufijo "|MERGE", esto es porque en este momento se esta trabajando en un punto intermedio dentro de una operación de merge.

el contenido del fichero commands debería ser el siguiente:

    init command
    <<<<<<< HEAD
    write
    =======
    run
    >>>>>>> develop

Por cada conflicto, y puede haber varios dentro de un mismo fichero, se verá el símbolo "<<<<<<<" indicando el inicio del conflicto y el contenido de la rama actual, es decir, la destinataria de los cambio, en este caso "HEAD". El símbolo que indica el final del conflicto y el nombre de la rama de donde provienen los cambios externos es ">>>>>>>", en este caso los cambios externos vienen de develop. Entre las dos secciones esta el símbolo "=======" que indica la division de ambas partes.

Para resolver los cambios se deben eliminar los tres símbolos y realizar la selección manual de las líneas de código que se deseen. En este caso el contenido del fichero debería quedar así: 

    init command
    run
    write

- añadimos la resolución del conflicto al stage

    git add commands.txt

- realizamos el commit, y se abrirá el editor de texto de la consola, si es el editor vi se debe escribir ":q"

    git commit

- una vez realizado el merge se deben pasar los cambios a la rama develop

## Ejercicio

Para realizar la entrega se debe crear un fichero pdf, a partir de un docx o cualquier editor de texto, donde se indique cada paso y una captura de pantalla de cada comando ejecutado, la captura debe mostrar el comando y una parte parcial de la respuesta del mismo.

En estos momentos se considera que se el desarrollo esta estable y se desea lanzar una versión, lo cual requiere de los siguientes pasos:

- pasar los cambios a la rama main
- crear una rama release siguiendo la nomenclatura indicada al principio, para la version 0.1.0
- crear un tag con el nombre "0.1.0"
- a partir de develop, crear una rama para añadir un comando más al fichero commands.txt, el comando será "finish", esta rama debe pasarse a develop.
