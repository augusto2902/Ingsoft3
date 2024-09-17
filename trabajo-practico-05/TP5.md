## Trabajo Práctico 5 - Despliegue de aplicaciones con Azure Devops Release Pipelines

### 1- Objetivos de Aprendizaje
 - Adquirir conocimientos acerca de las herramientas de despliegue y releases de aplicaciones.
 - Configurar este tipo de herramientas.
 - Comprender el concepto de recurso en Azure
 - Comprender los conceptos básicos de Release Pipelines en Azure DevOps.
 - Configurar un Release Pipeline para automatizar despliegues en diferentes entornos-

### 2- Unidad temática que incluye este trabajo práctico
Este trabajo práctico corresponde a la unidad Nº: 3 (Libro Continuous Delivery: Cap 10)

### 3- Consignas a desarrollar en el trabajo práctico:
 - Los despliegues (deployments) de aplicaciones se pueden realizar en diferentes tipos de entornos
   - On-Premise (internos) es decir en servidores propios.
   - Nubes Públicas, ejemplo AWS, Azure, Gcloud, etc.
   - Plataformas como servicios (PaaS), ejemplo Heroku, Google App Engine, AWS, Azure WebApp, etc
 - En este práctico haremos despliegue a Plataforma como Servicio utilizando Azure Web Apps

### 4- Desarrollo:
4.1\. Crear una cuenta en Azure
![image](https://github.com/user-attachments/assets/a425f412-7337-49d7-88ff-5ac50abe9c37)

4.2\. Crear un recurso Web App en Azure Portal y navegar a la url provista
uso MiWebApp01UCC porque el otro no estaba disponible
![image](https://github.com/user-attachments/assets/a02b0422-cb6e-44f3-9cf0-7e0bd241cfc7)
![image](https://github.com/user-attachments/assets/f0fe35e3-b4ab-4041-ab5b-8a2fe41022bb)


4.3\. Actualizar Pipeline de Build para que use tareas de DotNetCoreCLI@2 como en el pipeline clásico, luego crear un Pipeline de Release en Azure DevOps con CD habilitada
![image](https://github.com/user-attachments/assets/5988ad40-92eb-4565-930a-d7fa339ceea6)




4.4\. Optimizar Pipeline de Build
![image](https://github.com/user-attachments/assets/52016a09-d94e-4ee7-b231-03f5871e6441)


4.5\. Verificar el deploy en la url de la WebApp /weatherforecast
![image](https://github.com/user-attachments/assets/4aa96dd0-8add-4a03-b2ae-0afa020966b3)

![image](https://github.com/user-attachments/assets/a13d5fb6-99d9-40bd-8349-09f5217e3915)

4.6\. Realizar un cambio al código del controlador para que devuelva 7 pronósticos, realizar commit, evaluar ejecución de pipelines de build y release, navegar a la url de la webapp/weatherforecast y corroborar cambio
![image](https://github.com/user-attachments/assets/c8cb3850-58f3-4f2e-88c1-93db68517b81)
![image](https://github.com/user-attachments/assets/70a7e686-82a3-40b0-bb5b-2348c559cb60)


4.7\. Clonar la Web App de QA para que contar con una WebApp de PROD a partir de un Template Deployment en Azure Portal y navegar a la url provista para la WebApp de PROD.


4.8\. Agregar una etapa de Deploy a Prod en Azure Release Pipelines 
![image](https://github.com/user-attachments/assets/a46efab9-64ce-4260-b2ec-51558d9ff0a4)

4.9\.  Realizar un cambio al código del controlador para que devuelva 10 pronósticos, realizar commit, evaluar ejecución de pipelines de build y release, navegar a la url de la webapp/weatherforecast y corroborar cambio, verificar que en la url de la webapp_prod/weatherforecast se muestra lo mismo.
![image](https://github.com/user-attachments/assets/10b596d1-b6bb-4074-86f5-a9c0ddd20346)
![image](https://github.com/user-attachments/assets/43cda2f8-abb4-4059-8dcc-85472029aa59)
![image](https://github.com/user-attachments/assets/8c0bf6e5-53f3-4573-bdab-6c6996dac3d5)


4.10\. Modificar pipeline de release para colocar una aprobación manual para el paso a Producción.
![image](https://github.com/user-attachments/assets/e122ea25-fa19-49c7-a283-0e4a6811c9fc)

4.11\. Realizar un cambio al código del controlador para que devuelva 5 pronósticos, realizar commit, evaluar ejecución de pipelines de build y release, navegar a la url de la webapp/weatherforecast y corroborar cambio, verificar que en la url de la webapp_prod/weatherforecast aun se muestra la versión anterior.
![image](https://github.com/user-attachments/assets/c479f55d-9220-4f4f-a76a-a18bd7b55ec7)
![image](https://github.com/user-attachments/assets/9d6f4efe-f67b-4422-8933-10b3770b0df1)

4.12\. Aprobar el pase ya sea desde el release o desde el mail recibido. 

![image](https://github.com/user-attachments/assets/f1fcc304-0992-490b-bc3a-82e58b175e08)


4.13\. Esperar a la finalización de la etapa de Pase a Prod y luego corroborar que en la url de la webapp_prod/weatherforecast se muestra la nueva versión coinicidente con la de QA.
![image](https://github.com/user-attachments/assets/a821270f-bb76-4d49-9353-ec704992cc37)
![image](https://github.com/user-attachments/assets/d6581ac9-1a77-46d4-b625-567e5427f093)


4.14\. Realizar un pipeline (no release) que incluya el deploy a QA y a PROD con una aprobación manual. El pipeline debe estar construido en YAML sin utilizar el editor clásico de pipelines ni el editor clásico de pipelines de release.
