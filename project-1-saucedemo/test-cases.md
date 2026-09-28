Casos de Prueba — Módulo de Login (SauceDemo)
Sitio bajo prueba: https://www.saucedemo.com/ 
Fecha: 13/09/2026
Ejecutado por: Julio Araujo M.
Técnicas aplicadas: Partición de equivalencia, valores límite, casos negativos y de seguridad
________________________________________
TC-01 — Login exitoso con credenciales válidas
•	Tipo: Positivo (Equivalencia válida)
•	Precondición: El usuario standard_user existe y está activo
•	Datos de prueba: usuario: standard_user / contraseña: secret_sauce
•	Pasos: 
1.	Ingresar a la URL de login
2.	Escribir el usuario en el campo "Username"
3.	Escribir la contraseña en el campo "Password"
4.	Hacer clic en "Login"
•	Resultado esperado: El sistema redirige correctamente a la página de productos (/inventory.html)
________________________________________
TC-02 — Login con usuario bloqueado
•	Tipo: Negativo
•	Precondición: El usuario locked_out_user está marcado como bloqueado en el sistema
•	Datos de prueba: usuario: locked_out_user / contraseña: secret_sauce
•	Pasos: 
1.	Ingresar a la URL de login
2.	Escribir usuario y contraseña indicados
3.	Hacer clic en "Login"
•	Resultado esperado: Se muestra un mensaje de error indicando que el usuario ha sido bloqueado. No se permite el acceso.
________________________________________
TC-03 — Login con usuario inexistente
•	Tipo: Negativo (Partición inválida)
•	Datos de prueba: usuario: usuario_random_255 / contraseña: secret_sauce
•	Pasos: 
1.	Ingresar a la URL de login
2.	Escribir un usuario que no existe en el sistema
3.	Escribir cualquier contraseña
4.	Hacer clic en "Login"
•	Resultado esperado: Se muestra un mensaje de error genérico ("Username and password do not match..."). El sistema NO debe indicar si el usuario existe o no (consideración de seguridad).
________________________________________
TC-04 — Login con contraseña incorrecta
•	Tipo: Negativo
•	Datos de prueba: usuario: standard_user / contraseña: password_incorrecto
•	Pasos: 
1.	Ingresar usuario válido
2.	Ingresar contraseña incorrecta
3.	Hacer clic en "Login"
•	Resultado esperado: Da un mensaje de: (“Username and password do not match..”) en vez de un error de credenciales inválidas. 
________________________________________
TC-05 — Campo "Username" vacío
•	Tipo: Negativo (Valor límite)
•	Datos de prueba: usuario: "" (vacío) / contraseña: secret_sauce
•	Pasos: 
1.	Dejar el campo usuario vacío
2.	Completar la contraseña
3.	Hacer clic en "Login"
•	Resultado esperado: Mensaje de error indicando que el campo "Username" es requerido.
________________________________________
TC-06 — Campo "Password" vacío
•	Tipo: Negativo (Valor límite)
•	Datos de prueba: usuario: standard_user / contraseña: "" (vacío)
•	Pasos: 
1.	Completar el usuario
2.	Dejar la contraseña vacía
3.	Hacer clic en "Login"
•	Resultado esperado: Mensaje de error indicando que el campo "Password" es requerido.
________________________________________
TC-07 — Ambos campos vacíos
•	Tipo: Negativo (Valor límite)
•	Datos de prueba: usuario: "" / contraseña: ""
•	Pasos: 
1.	Dejar ambos campos vacíos
2.	Hacer clic en "Login"
•	Resultado esperado: Mensaje de error solicitando usuario (prioriza el primer campo requerido, según comportamiento definido).
________________________________________
TC-08 — Usuario con espacios en blanco al inicio/final
•	Tipo: Negativo / Edge case
•	Datos de prueba: usuario: " standard_user " (con espacios) / contraseña: secret_sauce
•	Pasos: 
1.	Escribir el usuario con espacios antes y después del texto
2.	Completar contraseña válida
3.	Hacer clic en "Login"
•	Resultado esperado: Da el mensaje de: (“Username and password do not match..”). Idealmente el sistema debería recortar (trim) los espacios y loguear correctamente, o rechazar de forma clara. 
________________________________________
TC-09 — Sensibilidad a mayúsculas en el usuario
•	Tipo: Negativo / Edge case
•	Datos de prueba: usuario: STANDARD_USER (mayúsculas) / contraseña: secret_sauce
•	Pasos: 
1.	Escribir el usuario en mayúsculas
2.	Completar contraseña válida
3.	Hacer clic en "Login"
•	Resultado esperado: El sistema no permite avanzar, distingue mayúsculas/minúsculas en el campo usuario. Desde el punto de vista de UX/seguridad en el campo usuario se debería poder reconocer si se escribe tanto en minúsculas o en mayúsculas, pero en el campo de contraseña si debería diferenciarse. 
________________________________________

TC-10 — El campo contraseña oculta el texto ingresado
•	Tipo: Funcional / UI
•	Pasos: 
1.	Hacer clic en el campo "Password"
2.	Escribir cualquier texto
•	Resultado esperado: El texto ingresado se muestra enmascarado (puntos o asteriscos), nunca en texto plano.
________________________________________
Resumen de ejecución
Total de casos: 10
Pasaron: 8 (TC-01, 02, 03, 04, 05, 06, 07, 10)
Fallaron: 0
Bugs encontrados: 0
Observaciones/mejoras: 2 (Issue #1 — TC-08, Issue #2 — TC-09)


		

