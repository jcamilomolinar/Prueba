# Proceso para usar la herramienta Horusec

Es una herramienta para analizar de forma estatica el codigo para detectar posibles vulnerabilidades de seguridad en el, hay un detalle y es que se debe instalar la ultima version en beta para aprovechar todo el potencial ya que la ultima version estable posee problemas al detectar la version de docker del sistema


```
curl -fsSL https://raw.githubusercontent.com/ZupIT/horusec/master/deployments/scripts/install.sh | bash -s latest-beta
```

Para iniciar con el escaneo se debe desplazar hasta la carpeta raiz del proyecto y ejecutar el siguiente comando


```
horusec start -p .
```

Por supuesto es posible personalizar el escaneo mediante banderas en el comando base, las cuales estan especificadas en la [documentación](https://docs.horusec.io/docs/cli/commands-and-flags/) o tambien es posible crear un archivo ```horusec-config.json``` dentro de la carpeta raiz para especificar mas facilmente cada configuración deseada, el siguiente es el ejemplo base de la documentación


```
{
    "horusecCliCertInsecureSkipVerify": false,
    "horusecCliCertPath": "",
    "horusecCliContainerBindProjectPath": "",
    "horusecCliCustomImages": {
        "c": "",
        "csharp": "",
        "dart": "",
        "elixir": "",
        "generic": "",
        "go": "",
        "hcl": "",
        "java": "",
        "javascript": "",
        "kotlin": "",
        "leaks": "",
        "php": "",
        "python": "",
        "ruby": "",
        "shell": "",
        "yaml": ""
    },
    "horusecCliCustomRulesPath": "",
    "horusecCliDisableDocker": false,
    "horusecCliEnableCommitAuthor": false,
    "horusecCliEnableGitHistoryAnalysis": false,
    "horusecCliEnableInformationSeverity": false,
    "horusecCliEnableOwaspDependencyCheck": false,
    "horusecCliFalsePositiveHashes": [],
    "horusecCliLogFilePath": "./tmp",
    "horusecCliFilesOrPathsToIgnore": 
    [
        "*tmp*",
        "**/.vscode/**"
    ],
    "horusecCliEnableShellcheck": false,
    "horusecCliFilterPath": "",
    "horusecCliHeaders": {},
    "horusecCliHorusecApiUri": "http://0.0.0.0:8000",
    "horusecCliJsonOutputFilepath": "",
    "horusecCliMonitorRetryInSeconds": 15,
    "horusecCliPrintOutputType": "text",
    "horusecCliProjectPath": "./",
    "horusecCliRepositoryAuthorization": "00000000-0000-0000-0000-000000000000",
    "horusecCliRepositoryName": "",
    "horusecCliReturnErrorIfFoundVulnerability": false,
    "horusecCliRiskAcceptHashes": [],
    "horusecCliSeveritiesToIgnore": [
        "INFO"
    ],
    "horusecCliTimeoutInSecondsAnalysis": 600,
    "horusecCliTimeoutInSecondsRequest": 300,
    "horusecCliToolsConfig": {
        "Bandit": {
            "istoignore": false
        },
        "Brakeman": {
            "istoignore": false
        },
        "Eslint": {
            "istoignore": false
        },
        "Flawfinder": {
            "istoignore": false
        },
        "GitLeaks": {
            "istoignore": false
        },
        "GoSec": {
            "istoignore": false
        },
        "HorusecCsharp": {
            "istoignore": false
        },
        "HorusecDart": {
            "istoignore": false
        },
        "HorusecJava": {
            "istoignore": false
        },
        "HorusecKotlin": {
            "istoignore": false
        },
        "HorusecKubernetes": {
            "istoignore": false
        },
        "HorusecLeaks": {
            "istoignore": false
        },
        "HorusecNodeJS": {
            "istoignore": false
        },
        "NpmAudit": {
            "istoignore": false
        },
        "PhpCS": {
            "istoignore": false
        },
        "Safety": {
            "istoignore": false
        },
        "SecurityCodeScan": {
            "istoignore": false
        },
        "Semgrep": {
            "istoignore": false
        },
        "ShellCheck": {
            "istoignore": false
        },
        "TfSec": {
            "istoignore": false
        },
        "YarnAudit": {
            "istoignore": false
        },
        "DotnetCli": {
            "istoignore": false
        },
         "Nancy": {
            "istoignore": false
        }
    },
    "horusecCliWorkDir": {
    "go": [],
    "csharp": [],
    "ruby": [],
    "python": [],
    "java": [],
    "kotlin": [],
    "javaScript": [],
    "leaks": [],
    "hcl": [],
    "php": [],
    "c": [],
    "yaml": [],
    "generic": [],
    "elixir": [],
    "shell": [],
    "dart": [],
    "nginx": []
    }
}
```

## Integración CI/CD

### Uso en Github Actions

Se puede integrar esta herramienta a este proceso, el YML recomendado por la documentación (ligeramente modificado) es el siguiente


```
name: SecurityPipeline

on: [push, pull_request]

jobs:
  horusec-security:
    name: horusec-security
    runs-on: ubuntu-latest
    steps:
    - name: Check out code
      uses: actions/checkout@v4
      with: # Required when commit authors is enabled
        fetch-depth: 0
    - name: Running Horusec Security
      run: |
        curl -fsSL https://raw.githubusercontent.com/ZupIT/horusec/main/deployments/scripts/install.sh | bash -s latest-beta
        horusec start -p="./" -e="true"
```