# Proceso para usar la herramienta Semgrep

El escaner SAST gratuito de Semgrep es su versión open-source software (OSS), se puede instalar a traves del sistema de gestión de paquetes pip de Python
```
python3 -m pip install semgrep
```

Para iniciar el escaneo se debe navegar hasta el directorio raiz del proyecto y ejecutar el comando para escanearlo
```
semgrep scan
```

Es posible iniciar sesión en su plataforma [Semgrep Cloud Platform](https://semgrep.dev/login/) donde disponen de muchas mas reglas para los escaneos y se almacenan las vulnerabilidades encontradas
```
semgrep login
semgrep ci
```

Es posible personalizar el escaneo con banderas especificadas en la [documentación](https://semgrep.dev/docs/cli-reference-oss/) ademas de ignorar directorios dentro de un archivo ```.semgrepignore``` que funciona con la misma sintaxis que un archivo ```.gitignore```, este es el ejemplo básico
```
# Common large paths
node_modules/
build/
dist/
vendor/
.env/
.venv/
.tox/
*.min.js
.npm/
.yarn/

# Common test paths
test/
tests/
*_test.go

# Semgrep rules folder
.semgrep

# Semgrep-action log folder
.semgrep_logs/
```

## Integración CI/CD

### Uso en Github Actions

La versión Semgrep OSS Se integra facilmente con esta herramienta, el YML recomendado por la documentación para un escaneo básico es el siguiente
```
name: Semgrep OSS scan

on:
  pull_request: {}
  workflow_dispatch: {}
  push:
    branches: ["master", "main"]

jobs:
  semgrep:
    name: semgrep-oss/scan
    runs-on: ubuntu-latest

    container:
      image: semgrep/semgrep

    # Skip any PR created by dependabot to avoid permission issues:
    if: (github.actor != 'dependabot[bot]')

    steps:
      - uses: actions/checkout@v4
      - run: semgrep scan --config auto
```