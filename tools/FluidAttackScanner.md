# Proceso para usar la herramienta Fluid Attacks Scanner

La herramienta gratuita de esta empresa es llamada Machine Standalone que puede ser configurada segun las necesidades para analizar el codigo fuente, funciona a traves de su imagen oficial de docker, entonces primero se debe descargar para correrlo localmente


```
docker pull fluidattacks/cli
```

Luego se ejecuta un contenedor a partir de la imagen indicando la ruta del proyecto que funcionara con un volumen


```
docker run -v /dir/to/scan:/src fluidattacks/cli skims scan /src
```

Es posible personalizar la ejecución con un archivo ```config.yaml``` dentro del directorio raiz del proyecto, donde entre otras cosas se pueden especificar que carpetas excluir (o incluir)


```
docker run -v /your/local/dir:/working-dir fluidattacks/cli:arch skims scan /working-dir/config.yaml
```

Un ejemplo sencillo donde solo se usa el engine SAST de la herramienta es el siguiente la llave ```recursion-limit``` se utiliza para evitar largas esperas en los escaneos. Todas las opciones estan explicadas en la [documentación](https://docs.fluidattacks.com/tech/scanner/standalone/configuration/)


```
namespace: myapp
output:
  file_path: ./Fluid-Attacks-Results.csv
  format: CSV
working_dir: .
language: EN
sast:
  include:
    - .
  exclude:
    - glob(**/node_modules/**)
    - glob(**/test/**)
  recursion-limit: 1000
```

## Integración CI/CD

### Uso en Github Actions

La herramienta se integra facilmente con este proveedor, se ilustra un ejemplo de archivo YML donde se analizan tanto los push como los pull request del repositorio, por supuesto tambien es posible personalizarlo con un archivo ```config.yaml``` y agregarle la llave ```strict``` para hacer que se rompa el pipeline

```
name: Standalone CLI
on: [push, pull_request]
jobs:
   machineStandalone:
      runs-on: ubuntu-latest
      steps:
         - uses: actions/checkout@f095bcc56b7c2baf48f3ac70d6d6782f4f553222
         - uses: docker://docker.io/fluidattacks/cli:latest
           name: machineStandalone
           with:
             args: skims scan ./dir/to/scan
```