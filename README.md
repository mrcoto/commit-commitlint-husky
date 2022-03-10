# Commit Convencionales

## Paso 1: Instalar Commitizen + Commitlint + Husky

```bash
npm i -D husky @commitlint/cli @commitlint/config-conventional commitizen
```

- Commitizen: Herramienta para dar formato estándar a un commit.
- Commitlint: Linter que valida un commit.
- Husky: Permite realizar una validación con commitlint al realizar git commit

## Paso 2: Crear archivo commitlint.config.js
Añadir el siguiente contenido:
```javascript
module.exports = {
	extends: ['@commitlint/config-conventional'],
};
```

## Paso 3: Crear archivo .huskyrc
Añadir el siguiente contenido:
```json
{
	"hooks": {
		"commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
	}
}
```

**Nota:** Si es la primera vez que se instalan estos paquetes,
ejecutar:
```bash
npx husky install # Crea directorio .husky
yarn husky add .husky/commit-msg "yarn commitlint --edit $1" # Genera archivo .husky/commit-msg
```

## Paso 4: Configurar commitizen en package.json

```bash
npx commitizen init cz-conventional-changelog --save-dev --save-exact
```

## Paso 5: Añadir el script para ejecutar commitizen en package.json
Ahora se podrá ejecutar commitizen con `npm run commit`
```json
"scripts": {
    ...
    "commit": "cz",
    ...
}
```

## Paso 6: Añadir npx husky install a postinstall de script
Esto ejecutará el comando npx husky install después de instalar los paquetes con `npm install`
```json
"scripts": {
    ...
    "postinstall": "npx husky install",
    ...
}
```

## Paso 7: Listo!

Solo basta con ejecutar `npm run install` y estará todo configurado.
Cada commit deberá generarse con `npm run commit`