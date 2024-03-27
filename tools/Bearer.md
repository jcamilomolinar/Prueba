# Proceso para usar la herramienta Bearer

La manera mas eficiente para empezar a usar el escaner de Bearer en el cliente es ejecutando en consola el script de instalación


```
curl -sfL https://raw.githubusercontent.com/Bearer/bearer/main/contrib/install.sh | sh
```

Para empezar el escaneo se ejecuta el comando con el nombre del directorio del proyecto


```
bearer scan MyProyect
```

Existen una gran cantidad de opciones para personalizar el escaneo segun las necesidades del momento, especificada en la [documentación](https://docs.bearer.com/guides/configure-scan/) tambien se puede hacer uso del archivo ```bearer.yml``` para especificar cada preferencia. Por ejemplo se puede indicar que se quiere ignorar un directorio o archivo con la bandera ```--skip-path``` seguido de las rutas separadas por coma.


```
bearer scan MyProyect --skip-path path/*.js, /users
```

## Integración CI/CD

### Uso en Github Actions
Se integra facilmente con esta herramienta, es posible usar la llave ```with``` para especificar las banderas del escaneo por ejemplo se puede especificar un ```bearer.yml``` para personalizar el escaneo con la llave ```config-file```. El siguiente YML es una versión ligeramente modificada de la recomendada en la [documentación](https://docs.bearer.com/guides/github-action/).


```
on:
  push:
    branches:
      - master
  pull_request:
    types: [opened, synchronize, reopened]

permissions:
  contents: read

jobs:
  rule_check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Bearer
        uses: bearer/bearer-action@v2
        with:
          diff: true
          config-file: "/some/path/bearer.yml"
```