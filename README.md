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

<img width="848" height="142" alt="image" src="https://github.com/user-attachments/assets/c6243d20-2f3d-4505-b83e-830a2b507f9c" />

- mostrar las ramas del repositorio

        git branch

  <img width="610" height="52" alt="image" src="https://github.com/user-attachments/assets/2fc3b8bb-7699-44d7-8dae-fc8993b2c0e4" />


- mostrar las ramas del repositorio incluyendo las ramas remotas

        git branch -a

<img width="624" height="179" alt="image" src="https://github.com/user-attachments/assets/af1e399b-c187-42f7-9452-cecd5f3aa5b9" />

- crear una rama local para develop

        git branch develop
        git checkout develop
  <img width="610" height="52" alt="image" src="https://github.com/user-attachments/assets/2fc3b8bb-7699-44d7-8dae-fc8993b2c0e4" />


- crear la primera rama feature, en el que se creará un fichero de texto. Este comando crea una rama y realiza el checkout a la misma.

        git checkout -b feature/create-txt-file

  <img width="812" height="51" alt="image" src="https://github.com/user-attachments/assets/aaf2593d-98e7-4a73-897e-982cb41fd2ea" />


- crear un fichero de texto llamado commands.txt, y escribir en la primera línea "init command"
<img width="812" height="213" alt="image" src="https://github.com/user-attachments/assets/3a53f748-965c-4381-9aaa-5de9e1ad49e9" />

- mostrar el estado del repositorio

        git status
  
<img width="955" height="269" alt="image" src="https://github.com/user-attachments/assets/9327a234-673b-48a2-afc6-b0b84f10e51e" />

- añadir el fichero al stash

        git add commands.txt

- realizar el primer commit

        git commit -m "feat: first command"

  <img width="733" height="100" alt="image" src="https://github.com/user-attachments/assets/285af8b2-4b14-4cd2-8408-c5966a4199f5" />


- cambia a develop

        git checkout develop

  <img width="646" height="71" alt="image" src="https://github.com/user-attachments/assets/074e96ef-fb54-44c1-830c-b2e974538bfd" />


- realiza el merge de la rama feature

        git merge feature/create-txt-file

  <img width="749" height="185" alt="image" src="https://github.com/user-attachments/assets/cfebaa1d-86f0-4596-9deb-4cf85c34e1bf" />

- elimina la rama feature

        git branch -d feature/create-txt-file
<img width="749" height="185" alt="image" src="https://github.com/user-attachments/assets/614d93c8-bae7-4a1d-a0a2-22ef5c3be4a8" />

- crea una feature para el segundo comando

        git checkout -b feature/run_command
<img width="749" height="185" alt="image" src="https://github.com/user-attachments/assets/615ceb33-0ef2-48c6-a2df-82d99fd3f915" />

- escribe el segundo comando en la linea siguiente del fichero commands.txt: run
- añade los cambios al stage y realiza el commit
- pasa a develop
- crea una feature para el tercer comando

        git checkout -b feature/write_command


  <img width="928" height="326" alt="image" src="https://github.com/user-attachments/assets/0aa094e1-dc74-4285-90f7-214b5f6b5dc5" />


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

  <img width="928" height="326" alt="image" src="https://github.com/user-attachments/assets/3f6a017e-2fa2-40ae-b9d6-b7e37cf7068e" />


## Ejercicio

Para realizar la entrega se debe crear un fichero pdf, a partir de un docx o cualquier editor de texto, donde se indique cada paso y una captura de pantalla de cada comando ejecutado, la captura debe mostrar el comando y una parte parcial de la respuesta del mismo.

En estos momentos se considera que se el desarrollo esta estable y se desea lanzar una versión, lo cual requiere de los siguientes pasos:

- pasar los cambios a la rama main
<img width="616" height="552" alt="image" src="https://github.com/user-attachments/assets/b54f54c5-b058-4c57-833d-a703e351843c" />

- crear una rama release siguiendo la nomenclatura indicada al principio, para la version 0.1.0
  <img width="704" height="69" alt="image" src="https://github.com/user-attachments/assets/f1f7f7bc-78ca-4c01-bfc1-2c54b80bbb2f" />

- crear un tag con el nombre "0.1.0"

<img width="704" height="69" alt="image" src="https://github.com/user-attachments/assets/ad8fc6df-6e60-4d5b-aa3e-a9c93056aa16" />

- a partir de develop, crear una rama para añadir un comando más al fichero commands.txt, el comando será "finish", esta rama debe pasarse a develop.

  <img width="762" height="782" alt="image" src="https://github.com/user-attachments/assets/8253806a-05ab-4b8b-8943-f184f983af79" />

