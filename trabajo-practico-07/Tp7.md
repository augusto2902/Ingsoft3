## Trabajo Práctico 7 - Code Coverage, Análisis estático de Código y Pruebas de Integración



### 4- Desarrollo:
#### Prerequisitos:

#### 4.1 Agregar Code Coverage a nuestras pruebas unitarias de backend y front-end e integrarlas junto con sus resultados en nuestro pipeline de build.
- Desarrollo del punto 4.1: 
	- ##### 4.1.1 En el directorio raiz de nuestro proyecto Angular instalar el siguiente paquete:
  - ##### 4.1.2 Editar nuestro archivo karma.conf.js para que incluya reporte de cobertura
   	- ##### 4.1.3 En el dir raiz del proyecto EmployeeCrudApi.Tests ejecutar:
  
   	- ##### 4.1.4 Agregar a nuestro pipeline ANTES del Build de Back la tarea de test con los argumentos especificados y la de publicación de resultados de cobertura:

 	- ##### 4.1.5 Agregar a nuestro pipeline ANTES del Build de front la tarea de test y la de publicación de los resultados.

	
	- ##### 4.1.6 Ejecutar el pipeline y analizar el resultado de las pruebas unitarias y la cobertura de código.

![image](https://github.com/user-attachments/assets/7680f616-37fa-4782-934b-e85bcc389535)

![image](https://github.com/user-attachments/assets/3fd7208b-c024-4dfe-b019-0483008a6a02)

![image](https://github.com/user-attachments/assets/bff0129e-14b6-4f19-8a7c-850e439bd66e)

#### 4.2 Agregar Análisis Estático de Código con SonarCloud:

![image](https://github.com/user-attachments/assets/713d8d46-9111-4cc4-bbed-3085bbf1cb29)


 ##### 4.2.2 Vemos el resultado de nuestro pipeline, en extensions tenemos un link al análisis realizado por SonarCloud

 ![image](https://github.com/user-attachments/assets/fc999325-caca-48ef-a930-3c3a715c69dc)

  ![image](https://github.com/user-attachments/assets/e7cf2a79-ee1d-4a5c-92a4-5a342b36bc8a)
Basicamente nos muestra los problemas de nuestro codigo distribuido segun la categoria que tienen seguridad, mentanimiento, codigo limpio etc. Nos permite filtrar por estos atributos y tambien filtrar por la severidad del problema en mi caso subi un acceso a labase de datos de azure que es un problema grave y me lo indico sonar
![image](https://github.com/user-attachments/assets/d660081d-f23f-4cc0-a40b-558fc3a29782)



#### 4.3 Pruebas de Integración con Cypress:


- Desarrollo del punto 4.4: 
	- ##### 4.3.1 En el directorio raiz de nuestro proyecto Angular instalar el siguiente paquete:
  	```bash
	npm install cypress --save-dev
   	```
   	- ##### 4.3.2 Abrir Cypress:
  	```bash
   	npx cypress open
   	```
	- ##### 4.3.3 Inicializar Cypress en nuestro proyecto como se indica en el instructivo 5.2
  ![image](https://github.com/user-attachments/assets/c6770033-9b8b-42f3-9e43-d26720cf1c33)

  	- ##### 4.3.4 Crear nuestra primera prueba navegando a nuestro front.
 	En la carpeta cypress/e2e, crear un archivo con el nombre primer_test.js y agregar el siguiente código para probar la página de inicio de nuestro front:
  	```js
	  describe('Mi primera prueba', () => {
	  it('Carga correctamente la página de ejemplo', () => {
	    cy.visit('https://as-crud-web-api-qa.azurewebsites.net/') // Colocar la url local o de Azure de nuestro front
	    cy.get('h1').should('contain', 'EmployeeCrudAngular') // Verifica que el título contenga "EmployeeCrudAngular"
	  })
	})
   	```
	- ##### 4.3.5 Correr nuestra primera prueba
 	Si está abierta la interfaz gráfica de Cypress, aparecerá el archivo primer_test.cy.js en la lista de pruebas. Clic en el archivo para ejecutar la prueba.
  	<img width="1154" alt="image" src="https://github.com/user-attachments/assets/f34a9af2-1692-441a-b1f0-37055ae2d7a0">
   	<img width="1436" alt="image" src="https://github.com/user-attachments/assets/8758c000-2f40-4a05-8cb0-c5fa56d583f9">
	
	También es posible ejecutar Cypress en modo "headless" (sin interfaz gráfica) utilizando el siguiente comando:
	```bash
 	npx cypress run
 	```
 	![image](https://github.com/user-attachments/assets/78ecba2e-9e40-4eb0-a286-56908723dee1)


	- ##### 4.3.6 Modificar nuestra prueba para que falle.
	  - Editamos el archivo primer_test.cy.js y hacemos que espere otra cosa en el título
	  - Ejecutamos cypress en modo headless
	 ![image](https://github.com/user-attachments/assets/b431354b-0e4f-492e-8c40-2993991ac76d)

	Cypress captura automáticamente pantallas cuando una prueba falla. Las capturas de pantalla se guardan en la carpeta `cypress/screenshots`.
	<img width="1136" alt="image" src="https://github.com/user-attachments/assets/e6f26695-def4-4596-b5c6-152f5b95aa59">

 	- ##### 4.3.6 Grabar nuestras pruebas para que Cypress genere código automático y genere reportes:
    	 - Cerramos Cypress
	 - Editamos el archivo cypress.config.ts incluyendo la propiedad **experimentalStudio** en true y la configuración de reportería.
	      ```typescript
		import { defineConfig } from "cypress";

		export default defineConfig({
		  e2e: {
		    setupNodeEvents(on, config) {
		      // implement node event listeners here
		    },
		    reporter: 'junit',  // Configura el reporter a JUnit
		    reporterOptions: {
		      mochaFile: 'cypress/results/results-[hash].xml',  // Directorio y nombre de los archivos de resultados
		      toConsole: true,  // Opcional: imprime los resultados en la consola
		      },
		  },
		  experimentalStudio: true,
		});

		```
       - Corremos nuevamente Cypress con npx cypress open, una vez que se ejecute nuestra prueba tendremos la opción de "Add Commands to Test". Esto permitirá interactuar con la aplicación y generar automáticamente comandos de prueba basados en las interacciones con la página:
         
         <img width="748" alt="image" src="https://github.com/user-attachments/assets/73c287fc-de00-477d-abbf-d905eb11cdb3">

       - Por ejemplo, si agregamos un nuevo empleado y luego verificamos que esté en la lista, Cypress nos generará un código como este:
 	```typescript
  	escribe('Mi primera prueba', () => {
	  it('Carga correctamente la página de ejemplo', () => {
        cy.visit('https://as-crud-web-api-qa.azurewebsites.net/') // Colocar la url local o de Azure de nuestro front
        cy.get('h1').should('contain', 'EmployeeCrudAngular') // Verifica que el título contenga "EmployeeCrudAngular"
        /* ==== Generated with Cypress Studio ==== */
        cy.get('.btn').click();
        cy.get('.form-control').clear('O');
        cy.get('.form-control').type('Oso Pratto');
        cy.get('.btn').click();
        cy.get(':nth-child(15) > :nth-child(2)').click();
        cy.get(':nth-child(15) > :nth-child(2)').should('have.text', ' Oso Pratto ');
        /* ==== End Cypress Studio ==== */
      })
	})
 	```
  	- Por supuesto que habrá que hacerle ajustes, como por ejemplo que se fije siempre en la última fila de la grilla y no en la posición 15 como lo grabó, es ahí cuando consultando la documentación de Cypress debemos ver cómo modificar el código, en nuestro caso de ejemplo sería así:
  	  ```typescript
  	  cy.get('tr:last-child > :nth-child(2)').should('have.text', ' Oso Pratto ');
  	  ```
  	- ##### 4.3.7 Hacemos prueba de editar un empleado
    	 - Creamos en cypress/e2e/ un archivo editEmployee_test.cy.js con el siguiente contenido, guardamos y aparecerá en Cypress:
  	       
		```js
  		describe('editEmployeeTest', () => {
			  it('Carga correctamente la página de ejemplo', () => {
		        cy.visit('https://as-crud-web-api-qa.azurewebsites.net/') // Colocar la url local o de Azure de nuestro front
		      })
			})
  	  	```
  	
 	<img width="845" alt="image" src="https://github.com/user-attachments/assets/d37524a6-fcfc-431c-9a69-594bf4dbbc62">
	- Hacemos "Add command to the test" y empezamos a interactuar con la página
 	<img width="679" alt="image" src="https://github.com/user-attachments/assets/e7ad9389-3f68-42fc-95f2-68a7a79a029a">
  
  	- Hacemos algunos ajustes al código generado:
   
  	```js
	describe('editEmployeeTest', () => {
	  it('Edita correctamente un empleado', () => {
	    cy.visit('https://as-crud-web-api-qa.azurewebsites.net/') // URL del front
	
	    // Haz clic en el botón de editar empleado
	    cy.get(':nth-child(7) > :nth-child(4) > a > .fa').click();
	
	    // Asegúrate de que el campo de texto esté visible y habilitado
	    cy.get('.form-control')
	      .should('be.visible')
	      .should('not.be.disabled')
	
	    cy.wait(500);
	
	    cy.get('.form-control').type('{selectall}{backspace}')  // Selecciona todo el texto y lo elimina
	
	    cy.wait(500);
	
	    cy.get('.form-control').should('have.value', '');  // Verifica que el campo esté vacío
	
	    // Escribe el nuevo nombre 
	    cy.get('.form-control').type('Emilia Schwindt Modified');
	
	    // Envía el formulario
	    cy.get('.btn').click();
	
	    // Verifica que el nombre fue actualizado correctamente
	    cy.get(':nth-child(7) > :nth-child(2)').should('have.text', ' Emilia Schwindt Modified ');
	  });
	});

  	```



### 7-  Criterio de Calificación
Los pasos 4.1 al 4.3 representan un 60% de la nota total, los pasos 4.4 y subsiguientes representan el 40% restante.



