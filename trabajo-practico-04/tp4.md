## Trabajo Práctico 4 - Azure Devops Pipelines

#### 4- Pasos del TP
 - 4.1 Verificar acceso a Pipelines concedido
   ![image](https://github.com/user-attachments/assets/4590d0dd-39e1-4bbf-8354-8ee1a1bb3880)

 - 4.2 Agregar en pipeline YAML una tarea de Publish.
   ![image](https://github.com/user-attachments/assets/7511e20e-97c4-4760-a1a7-0fb4cb19c602)

 - 4.3 Explicar por qué es necesario contar con una tarea de Publish en un pipeline que corre en un agente de Microsoft en la nube.
 - Es necesario para almacenar los artefactos generados en el pipeline
 - 4.4 Descargar el resultado del pipeline y correr localmente el software compilado.
 - ![image](https://github.com/user-attachments/assets/1532ebf7-8eb2-45e6-a2da-a15427f77da1)
![image](https://github.com/user-attachments/assets/85d3b475-bc62-4628-8df1-eb927e3f615a)

 - 4.5 Habilitar el editor clásico de pipelines. Explicar las diferencias claves entre este tipo de editor y el editor YAML.
 - la differencia es que l editor clásico es más accesible para principiantes o para configuraciones simples, mientras que el editor YAML ofrece una mayor flexibilidad y control para usuarios más avanzados o para proyectos más complejos.
 - Ademas de que el editor clasico no es portable.

 - 4.6 Crear un nuevo pipeline con el editor clásico. Descargar el resultado del pipeline y correr localmente el software compilado.
 - ![image](https://github.com/user-attachments/assets/12bd8ca2-1790-4e55-8b53-d2b5e05f6e84)
 - ![image](https://github.com/user-attachments/assets/457c9474-dfa8-4495-a37f-0c19e03cddd3)

 - 4.7 Configurar CI en ambos pipelines (YAML y Classic Editor). Mostrar resultados de la ejecución automática de ambos pipelines al hacer un commit en la rama main.
   ![image](https://github.com/user-attachments/assets/e4f9fe24-bbe4-41fe-be7d-3770e1b45e9d)
   en el yaml viene habilitado por default
   ![image](https://github.com/user-attachments/assets/20307423-c0aa-4239-bbb7-eb8678493798)
   al commitear un cambio al main se ejecutan las 2
   ![image](https://github.com/user-attachments/assets/178ea65e-7d54-4ade-84d7-5d0649ff1299)



 - 4.8 Explicar la diferencia entre un agente MS y un agente Self-Hosted. Qué ventajas y desventajas hay entre ambos? Cuándo es conveniente y/o necesario usar un Self-Hosted Agent?
 - Agentes Microsoft-hosted (MS)= Microsoft se encarga de la configuración, el mantenimiento y las actualizaciones de los agentes. Son mas faciles de configurar y auyoescalables pero no manejas demasiado control sobre el entorno del agente
 - Se usan cuando deseas simplicidad y no necesitas configuraciones personalizadas en el entorno de ejecución. Para tareas generales y pipelines que no requieren configuraciones específicas del entorno.
 - 
 -Agentes Self-hosted= Tenes control total sobre el entorno del agente, puedes tener agentes dedicados para tus pipelines,aparte de que tienen configuraciones Personalizadas. El problema es que el usuario es completamente responsable del mantenimiento, actualizacion y configuracion de este y se necesitan gestionar los recursos para utilizarlos.
 -Se usan cuando se necesita un entorno personalizado o herramientas específicas que no están disponibles en los agentes Microsoft-hosted. Para reducir tiempos de espera o tener un mayor control sobre el entorno de ejecución.
 - 4.8 Crear un Pool de Agentes y un Agente Self-Hosted
   ![image](https://github.com/user-attachments/assets/ffa23079-ec89-416a-9b38-1f99046ce478)

