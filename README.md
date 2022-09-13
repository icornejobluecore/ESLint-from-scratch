# Ejecución de ESLint al momento de hacer commit sólo a los archivos modificados.

# Instalación de dependecias

Dependencias de desarrollo requeridas: 
* [ESLint](https://www.npmjs.com/package/eslint) 
* [@typescript-eslint/parser](https://www.npmjs.com/package/@typescript-eslint/parser)
* [husky](https://www.npmjs.com/package/husky)
* [lint-staged](https://www.npmjs.com/package/lint-staged)

### Instalación paquete por paquete
1. ESLint 
```sh
$ npm install --save-dev eslint@8.21.0
```
2. @typescript-eslint/parser
```sh
$ npm i --save-dev typescript @typescript-eslint/parser
```
> Nota: Validar en el `package.json` si ya existe esta dependecia.
3. husky
```sh
$ npx husky-init && npm install
```
4. husky
```sh
$ npm install --save-dev lint-staged@13.0.3
```

### Ruta rápida de instalación de paquetes
Copiar y pegar en el `package.json` en las dependencias de desarrollo (`devDependencies`)
```sh
 "eslint": "8.21.0",
 "@typescript-eslint/parser": "5.32.0",
 "husky": "8.0.0",
 "lint-staged": "13.0.3"
```
> :bulb: Nota: Al usar esta vía rápida es necesario iniciar el husky con el siguiente comando `npx husky-init`


***

# Configuración Husky
### Añadir script `prepare` en el `package.json`
```sh
  "prepare": "husky install .husky"
```
<img width="323" alt="image" src="https://user-images.githubusercontent.com/112881938/189396183-fee669de-a341-4b1d-b467-c8be67d518db.png">

> :bulb: Nota: Este script prepara al husky para ejecutar el ESLint. 

### Modificar el archivo `pre-comit` y reemplazar `npm test` por `npx lint-staged`

<img width="691" alt="image" src="https://user-images.githubusercontent.com/112881938/189398846-7537c967-d6dc-4087-bc88-d6335e09085c.png">

# Configuración ESLint
### Creación o modificación de archivo `.eslintrc.json`

Modificar el archivo `.eslintrc.json` añadiendo las siguientes reglas básicas:
> :bulb: Nota : Este archivo tiene una reglas básicas predefinidas. El objetivo de modificar el archivo, es para un flujo básico de configuración.

```sh
{
  "env": {
    "browser": true,
    "es2021": true
  },
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "sourceType": "module",
    "ecmaVersion": "latest"
  },
  "rules": {
    "no-console": [
      "error",
      {
        "allow": ["error"]
      }
    ]
  }
}
```
> :bulb: Nota : En este archivo se pueden añadir todas las reglas que se desean aplicar. [Ver más reglas](https://eslint.org/docs/latest/rules/)


### Creación de archivo `.eslintignore`

Creación de archivo .eslintignore al nivel raíz. En este archivo se especifican aquellas carpetas y extensiones donde no se requiera ejecutar el ESLint. 

```sh
*.spec.ts
**/node_modules
```
# Configuración lint-staged
### Creación de archivo `.lintstagedrc`
En este archivo se especifican a qué extensiones de archivos se desea ejecutar el ESLint.
Añadir el siguiente `.json` al archivo `.lintstagedrc`.
```sh
{
  "*.{js,ts,tsx}": ["eslint"]
}
```
# ✅ Ejecución
1. Añadimos un `console.log` a un archivo de prueba
2. Hacemos un commit `git commit -m ""`

<img width="525" alt="image" src="https://user-images.githubusercontent.com/112881938/189419361-7727ac35-9fb2-45be-bfc6-ae913c94e052.png">


