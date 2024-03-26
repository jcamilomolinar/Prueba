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
