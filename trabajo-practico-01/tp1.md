## Trabajo Práctico 1 - Git Básico

#### 1- Instalar Git
  ![image](https://github.com/user-attachments/assets/6dc228da-abe1-4d54-b914-5fcc942ed274)

#### 2- Crear un repositorio local y agregar archivos
  ![image](https://github.com/user-attachments/assets/11b15487-3eb7-4b93-975d-d9a73d3f0502)
  
#### - Creación de Repos 01 -> Crearlo en GitHub, clonarlo localmente y subir cambios
  - Crear una cuenta en https://github.com
  - Crear un nuevo repositorio en dicha página con el Readme.md por defecto
  - ![image](https://github.com/user-attachments/assets/87dfd794-3737-4458-85d7-4009de4a3e2a)

  - Clonar el repo remoto en un nuevo directorio local
  - Editar archivo Readme.md agregando algunas lineas de texto
  - Editar (o crear si no existe) el archivo .gitignore agregando los archivos *.bak
  - Crear un commit y porveer un mensaje descriptivo
  - Intentar un push al repo remoto
  - En caso de ser necesario configurar las claves SSH requeridas y reintentar el push.
![image](https://github.com/user-attachments/assets/6ce8fe9f-6f81-42d8-842a-82193ae03310)
![image](https://github.com/user-attachments/assets/3df1e435-5ac0-47ce-a100-cd4483bfe9a4)
![image](https://github.com/user-attachments/assets/1d9ed4c6-8a40-43b0-8ce9-32176268896d)

#### 5- Creación de Repos 02-> Crearlo localmente y subirlo a GitHub
 uso el repo local del punto 1
 
  - Crear repo remoto en GitHub
  - Asociar repo local con remoto
  - Crear archivo .gitignore
  - Crear un commit y proveer un mensaje descriptivo
  - Subir cambios.
![image](https://github.com/user-attachments/assets/8e3fde90-0b0e-454a-932f-ef94354b5729)

#### 6- Ramas
  - Crear una nueva rama
  - Cambiarse a esa rama
  - Hacer un cambio en el archivo Readme.md y hacer commit
  - Revisar la diferencia entre ramas
![image](https://github.com/user-attachments/assets/1af3b788-d96a-4c5b-83d5-cebd0253b1ed)

#### 7- Merges
  - Hacer un merge FF
  ![image](https://github.com/user-attachments/assets/b1e4e37e-b389-4b73-a8b5-4d18dc21450f)

  - Borrar la rama creada
  - Ver el log de commits
  - ![image](https://github.com/user-attachments/assets/0eb4a794-4b43-4b92-b470-ea0d16fcaa98)

  - Repetir el ejercicio 6 para poder hacer un merge con No-FF
![image](https://github.com/user-attachments/assets/e6067907-cbf7-4eb9-aa5f-91d58ebc665e)

#### 8- Resolución de Conflictos
  - Instalar alguna herramienta de comparación. Idealmente una 3-Way:
    - P4Merge https://www.perforce.com/downloads/helix-visual-client-p4v:
![alt text](p4merge.png)
    - Se puede omitir registración. Instalar solo opción Merge and DiffTool.
 - ByondCompare trial version https://www.scootersoftware.com/download.php
    - Configurar Tortoise/SourceTree para soportar esta herramienta.
    - https://www.scootersoftware.com/support.php?zz=kb_vcs
    - https://medium.com/@robinvanderknaap/using-p4merge-with-tortoisegit-87c1714eb5e2
  - Crear una nueva rama conflictBranch
  - Realizar una modificación en la linea 1 del Readme.md desde main y commitear
  - En la conflictBranch modificar la misma línea del Readme.md y commitear
  - ![image](https://github.com/user-attachments/assets/e6a5a160-491c-4e9d-a69f-b82d05656205)

  - Ver las diferencias con git difftool main conflictBranch
  - ![image](https://github.com/user-attachments/assets/e3e8608a-43c0-40dc-92a0-019913066781)

  - Cambiarse a la rama main e intentar mergear con la rama conflictBranch
    ![image](https://github.com/user-attachments/assets/14fe69b7-8c39-478e-a93c-a51015c2f297)

  - Resolver el conflicto con git mergetool
  - ![image](https://github.com/user-attachments/assets/5c8419dd-14f1-4b57-9038-c2cfe7c85324)
  ![image](https://github.com/user-attachments/assets/8555b28a-f10b-4e4f-a5e9-a255993331d1)

  - Agregar .orig al .gitignore
  - Hacer commit y push
![image](https://github.com/user-attachments/assets/37213fe3-6c9d-4700-bd64-5fb10a484c15)

#### 9- Familiarizarse con el concepto de Pull Request

  - Explicar que es un pull request.
Es una solicitud para hacer un pull a un repositorio,  para que los mantenedores de un proyecto revisen y, potencialmente, fusionen cambios propuestos desde una rama específica en un repositorio hacia otra rama, comúnmente la rama principal o main.
  - Crear un branch local y agregar cambios a dicho branch.
  ![image](https://github.com/user-attachments/assets/3556dbdc-4ed1-4b7b-a742-2887a0c537f9)

  - Subir el cambio a dicho branch y crear un pull request.
  - Completar el proceso de revisión en github y mergear el PR al branch master.

![image](https://github.com/user-attachments/assets/ce032e40-ac17-4af1-ac03-937acbd0df16)
![image](https://github.com/user-attachments/assets/da33a58d-db97-49b4-aadc-cdcd6cde9eec)
![image](https://github.com/user-attachments/assets/4dd37e92-1bc7-4fcb-be3d-ae02dcab68dd)

10- Algunos ejercicios online
Entrar a la página https://learngitbranching.js.org/
Completar los ejercicios Introduction Sequence
Realizado

