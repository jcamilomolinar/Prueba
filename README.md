# Implementación de herramienta SAST dentro del repositorio de devsecops-engine-tools

  

Se investigaron diferentes opciones priorizando dos caracteristicas esenciales, que estas herramientas fueran gratuitas/open source y que soportaran los lenguajes Java y Javascript.

Se consultaron herramientas de distintas fuentes incluida la pagina oficial del OWASP, alli tienen una [larga lista](https://owasp.org/www-community/Source_Code_Analysis_Tools) de herramientas recomendadas para el análisis de código.

  

## _Posibles opciones_

Determiné las siguientes herramientas como posibles candidatas, teniendo en cuenta la herramienta recomendada.

  

-  [SonarQube](https://github.com/SonarSource/sonarqube)

-  [Semgrep](https://github.com/semgrep/semgrep)

-  [Fluid Attacks Scanner](https://docs.fluidattacks.com/tech/scanner/plans/foss/) (Herramienta recomendada)

-  [Bearer](https://github.com/Bearer/bearer)

- [BetterScan](https://github.com/marcinguy/betterscan-ce)

- [Horusec](https://github.com/ZupIT/horusec)

## _¿Como probar la efectividad de estas herramientas?_

  

Para este fin se usaran dos valiosos recursos, uno es el [benchmark de OWASP](https://owasp.org/www-project-benchmark/) que se trata de una serie de test en Java para evaluar la efectividad, cubrimiento y velocidad de herramientas automatizadas de detección de vulnerabilidades.

  

Por otro lado tambien se usara el proyecto [OWASP Juice Shop](https://github.com/juice-shop/juice-shop), que basicamente cumple la misma funcion que el benchmark solo que aqui se evaluará con código escrito en Javascript (y Typescript).

  

## _Resultados_

| Herramienta                 | Lenguajes soportados                                                                                 | Interfaz gráfica                                                             | Integración CI/CD | Documentación                                   | Comunidad activa                                                                            | Vulnerabilidades encontradas en el proyecto BenchmarkJava  | Vulnerabilidades encontradas en el proyecto The Juice Shop | Facilidad de usar                                                                                                                                           |
|-----------------------------|------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------|-------------------|-------------------------------------------------|---------------------------------------------------------------------------------------------|------------------------------------------------------------|------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SonarQube Community Edition | Soporta 19 lenguajes, ademas soporta nativamente proyectos de Java compilados con Maven y Gradle     | Si, desplegada localmente y de facil entendimiento                           | Si                | Si, cuenta con una amplia documentación         | Si, cuenta con mas de 8.7k estrellas en GitHub y segun la web lo usan mas de 400k compañias | 1124 en 7 minutos                                          | 264 en 3 minutos                                           | Un poco engorrosa de utilizar y configurar manualmente                                                                                                      |
| Bearer                      | Soporta totalmente javascript/typescript, ruby y PHP, java y go estan soportados parcialmente (beta) | No, se maneja a traves de un cliente en terminal                             | Si                | Si, cuenta con documentación                    | Si, cuenta con mas de 1.6k estrellas en GitHub                                              | 2252 en 3 minutos                                          | 331 en 1 minuto                                            | Muy facil de utilizar con un  simple comando ya esta corriendo el escaneo en las carpetas requeridas                                                        |
| Semgrep                     | Soporta totalmente 13 lenguajes, y mas de 30 lenguajes son soportados parcialmente                   | Si, requiere registrarse  en su pagina, tambien tiene un cliente en terminal | Si                | Si, cuenta con documentación                    | Si, cuenta con mas de 9.5k estrellas en GitHub                                              | 6498 en 7 minutos                                          | 80 en 3 minutos                                            | Facil de usar, se debe loggear en su web para acceder a todas las reglas, ademas al hacer un escaneo apareceran alli todas las vulnerabilidades encontradas |
| Fluid Attacks Scanner       | La herramienta SAST soporta un total de 18 lenguajes                                                 | No, se maneja a través de un cliente en terminal                             | Si                | Si, aunque no es muy extensa es de fácil manejo | Si, cuenta con mucha actividad en GitLab                                                    | 1758 en 15 minutos                                         | No fue posible ejecutar                                    | Fácil de usar, la documentación tiene algunas inconsistencias.                                                                                              |

El benchmark tiene 1415 vulnerabilidades según la documentación y la Juice Shop tiene alrededor de 106 vulnerabilidades según la documentación del proyecto.