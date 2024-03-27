# Implementación de herramienta SAST dentro del repositorio de devsecops-engine-tools

  

Se investigaron diferentes opciones priorizando dos caracteristicas esenciales, que estas herramientas fueran gratuitas/open source y que soportaran los lenguajes Java y Javascript.

Se consultaron herramientas de distintas fuentes incluida la pagina oficial del OWASP, alli tienen una [larga lista](https://owasp.org/www-community/Source_Code_Analysis_Tools) de herramientas recomendadas para el análisis de código.

  

## _Posibles opciones_

Determiné las siguientes herramientas como posibles candidatas, teniendo en cuenta la herramienta recomendada.

  

-  [SonarQube](https://github.com/SonarSource/sonarqube)

-  [Semgrep](https://github.com/semgrep/semgrep)

-  [Fluid Attacks Scanner](https://docs.fluidattacks.com/tech/scanner/plans/foss/) (Herramienta recomendada)

-  [Bearer](https://github.com/Bearer/bearer)

-  [Horusec](https://github.com/ZupIT/horusec)

## _¿Como probar la efectividad de estas herramientas?_

  

Para este fin se usaran dos valiosos recursos, uno es el [benchmark de OWASP](https://owasp.org/www-project-benchmark/) que se trata de una serie de test en Java para evaluar la efectividad, cubrimiento y velocidad de herramientas automatizadas de detección de vulnerabilidades.

  

Por otro lado tambien se usara el proyecto [OWASP Juice Shop](https://github.com/juice-shop/juice-shop), que basicamente cumple la misma funcion que el benchmark solo que aqui se evaluará con código escrito en Javascript (y Typescript).

  

## _Resultados_


| Herramienta                 	| Lenguajes soportados                                                                                             	| Interfaz gráfica                                                             	| Integración CI/CD 	| Documentación                                                            	| Comunidad activa                                                                                                                                	| Vulnerabilidades encontradas en el proyecto BenchmarkJava         	| Vulnerabilidades encontradas en el proyecto The Juice Shop 	| Facilidad de usar                                                                                                                                                	|
|-----------------------------	|------------------------------------------------------------------------------------------------------------------	|------------------------------------------------------------------------------	|-------------------	|--------------------------------------------------------------------------	|-------------------------------------------------------------------------------------------------------------------------------------------------	|-------------------------------------------------------------------	|------------------------------------------------------------	|------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| SonarQube Community Edition 	| Soporta 19 lenguajes, ademas soporta nativamente proyectos de Java compilados con Maven y Gradle                 	| Si, desplegada localmente y de facil entendimiento                           	| Si                	| Cuenta con una amplia documentación                                      	| Cuenta con mas de 8.7k estrellas en GitHub y segun la web lo usan mas de 400k compañias                                                         	| 1124 en 7 minutos                                                 	| 264 en 3 minutos                                           	| Un poco engorrosa de utilizar y configurar manualmente                                                                                                           	|
| Bearer                      	| Soporta totalmente java, javascript/typescript, ruby y PHP, python y go estan soportados parcialmente (beta)     	| No, se maneja a traves de un cliente en terminal                             	| Si                	| Cuenta con documentación                                                 	| Cuenta con mas de 1.7k estrellas en GitHub                                                                                                      	| 2252 en 3 minutos                                                 	| 331 en 1 minuto                                            	| Muy facil de utilizar con un  simple comando ya esta corriendo el escaneo en las carpetas requeridas                                                             	|
| Semgrep                     	| Soporta totalmente 13 lenguajes, y mas de 30 lenguajes son soportados parcialmente                               	| Si, requiere registrarse  en su pagina, tambien tiene un cliente en terminal 	| Si                	| Cuenta con documentación                                                 	| Cuenta con mas de 9.6k estrellas en GitHub                                                                                                      	| 6498 en 7 minutos                                                 	| 80 en 3 minutos                                            	| Facil de usar, se debe loggear en su web para acceder a todas las reglas, ademas al hacer un escaneo apareceran alli todas las vulnerabilidades encontradas      	|
| Fluid Attacks Scanner       	| Soporta un total de 18 lenguajes, como Java, Javascript, C, entre otros.                                         	| No, se maneja a traves de un cliente en terminal                             	| Si                	| Cuenta con documentación que aunque no es muy extensa es de fácil manejo 	| Cuenta con mas de 75k commits en su repositorio de GitLab (aclarando que es para todo su core, no solamente para su escaner Machine Standalone) 	| 1758 en 15 minutos                                                	| No fue posible ejecutar                                    	| Facil de usar, la documentación tiene algunas inconsistencias.                                                                                                   	|
| Horusec                     	| Soporta un total de 18 lenguajes e integra alrededor de 20 herramientas distintas para incrementar la seguridad. 	| Si, requiere registrarse en su pagina, tambien tiene un cliente en terminal  	| Si                	| Cuenta con documentación                                                 	| Cuenta con mas de 1.1k estrellas en GitHub                                                                                                      	| No fue posible ejecutar, despues de cierto tiempo mata el proceso 	| 501 en 1 minuto                                            	| Relativamente fácil de usar, se debe indagar dentro de los issues del repositorio para arreglar un problema de la detección de la versión de docker del sistema. 	|


El benchmark tiene 1415 vulnerabilidades según la documentación y la Juice Shop tiene alrededor de 106 vulnerabilidades según la documentación del proyecto.