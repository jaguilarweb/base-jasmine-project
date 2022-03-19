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

