# INTRODUCCIÓN

Este proyecto contiene la configuración base de un proyecto que incluye Typescript.

## Pasos

Crear una carpeta que será el proyecto.

Crear una nueva carpeta llamada ‘src’ 

Crear, dentro de 'src', un archivo index.ts

Inicializar el proyecto con npm ``` npm init -y ```

Agregar typescript con npm ```npm i —save-dev typescript```

Agregar las siguientes librerias:
```npm i —save-dev ts-node```
```npm i —save-dev @types/node```
```npx tsc —init```

### Configuraciones

En el archivo ***package.json*** crear el script:
> “script:{ “build”: “npx tsc”}

Estar segura de incluir esta configuración en ***tsconfig.json***:
>“target”: “ES5”,

>“module”: “commonjs”,

>“lib”: [“ES6”, “DOM”]

También habilitar:
>“outDir”: “./build”

Asesurarse que las siguientes opciones estén configuradas así:
>“strict”: true,

>“noImplicityAny”: true,

Al final excluir lo siguiente:
>“exclude”: [“node_modules”]


Al finalizar compilar con el comando:

```npm run build```

## Test Jasmine

Instalar Jasmine

```npm i jasmine```

Instalar report Jasmine
``` npm i jasmine-spec-reporter```

Instalar difinición de type para Jasmine,
para trabajar con los archivos Jasmine y Typescript 

``` npm i --save-dev @types/jasmine```

Luego agregamos el script respectivo para correr el test, en este caso:

```"jasmine": "jasmine"```

## Sistema de archivos

En el directorio raíz crear la carpeta "spec" y en ella "support". Dentro de ella crear el archivo "jasmine.json".

En el directorio "src" crear la carpeta "tests", y en el un archivo (por cada archivo a testear), con el nombre del archivo a testear seguido por sufijo "Spec" y la extensión ".ts"

En el directorio "test" crear la carpeta "helpers", el que será revisado por spec reporter para buscar las configuraciones, para lo cual crearemos el archivo reporter.ts

La estructura de archivo quedaría de la siguiente forma:

├── node_modules
├── spec
│      └── support
│           └── jasmine.json
├── src
│     ├──  tests
│     │     ├── helpers
│     │     │      └── reporter.ts
│     │     └── indexSpec.ts
│     └── index.ts
├── package-lock.json
├── package.json
└── tsconfig.json


Agregar en el archivo "reporter.ts" la configuración básica:
import {DisplayProcessor, SpecReporter, StacktraceOption} from "jasmine-spec-reporter";
import SuiteInfo = jasmine.SuiteInfo;
```
class CustomProcessor extends DisplayProcessor {
    public displayJasmineStarted(info: SuiteInfo, log: string): string {
        return `${log}`;
    }
}
jasmine.getEnv().clearReporters();
jasmine.getEnv().addReporter(new SpecReporter({
    spec: {
        displayStacktrace: StacktraceOption.NONE
    },
    customProcessors: [CustomProcessor],
}));
```
Nota: En las siguientes configuraciones la referencia al directorio 'dist' puede ser cambiada a 'build' dependiendo si se agregó previamente o no el archivo "tsconfig.json", y como se configuró la opción "outDir": "./build" o "outDir": "./dist".

Agregar en "Jasmine.json" la siguiente configuración básica:

``` {
    "spec_dir": "dist/tests",
    "spec_files": [
        "**/*[sS]pec.js"
    ],
    "helpers": [
        "helpers/**/*.js"
    ],
    "stopSpecOnExpectationFailure": false,
    "random": false
} 
```
La opción ```"stopSpecOnExpectationFailure": false,````, nos permite correr el test de corrido, sin detenernos en cada error, pudiendo ver el test completo.

La opción ``` "random": false ```, nos permite ejecutar el test en forma ordenada, en el mismo orden que el test fue escrito.

Agregar a "tsconfig.json" la siguiente exclusión:

```  "exclude":["node_modules", "./dist", "spec"]```

Para este proyecto también se incluyó la opción ``` "allowJs": true, ```