# Proceso para usar la herramienta SonarQube

Para usar el escaner en el cliente el primer paso es descargarlo de la [pagina oficial](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner/) y tambien descargar la version Community de la [pagina](https://www.sonarsource.com/products/sonarqube/downloads/) de descargas de SonarQube para ejecutar el server donde se presentan las vulnerabilidades encontradas dentro de los escaneos

Primero se enciende el servidor alojado en la descarga de la version Community de SonarQube


```
sonarqube/bin/linux-x86-64/sonar.sh console
```

Se debe navegar a ```localhost:9000``` e ingresar con login:admin y password:admin para acceder, luego se debe crear un proyecto segun las necesidades de cada uno. Luego se ejecuta el analisis desde la consola


```
sonar-scanner \
  -Dsonar.projectKey=MyProjectKey \
  -Dsonar.sources=MyProjectDirectory \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=MyAuthenticationToken
```

Para un proyecto de Java con Maven tienen su propio escaner, se ejecuta en la carpeta raiz del proyecto


```
mvn clean verify sonar:sonar \
  -Dsonar.projectKey=MyProjectKey \
  -Dsonar.projectName='MyProjectName' \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=MyAuthenticationToken
```

## Integración CI/CD

### Uso en Github Actions

La edición Community no soporta el análisis de multiples ramas, solo puede analizarse la rama main, Github debe tener acceso a la instancia local de SonarQube y desde alli generar un token y ambos agregarlos como secretos del repositorio con los nombres de ```SONAR_TOKEN``` y ```SONAR_HOST_URL```, el YAML recomendado por la [documentación](https://github.com/marketplace/actions/official-sonarqube-scan) es el siguiente


```
on:
  push:
    branches:
      - main
      - master
  pull_request:
      types: [opened, synchronize, reopened]

name: Main Workflow
jobs:
  sonarqube:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
      with:
        fetch-depth: 0
    - name: SonarQube Scan
      uses: sonarsource/sonarqube-scan-action@master
      env:
        SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
        SONAR_HOST_URL: ${{ secrets.SONAR_HOST_URL }}
```


Posteriormente los resultados se veran reflejados dentro de la instancia local de Sonar.