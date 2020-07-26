iniciando um projeto node express typescript

```bash
yarn init projectName -y
cd projectName

yarn add express
yarn add typescript -D
yarn add @types/express -D
yarn add ts-node-dev -D
yarn add eslint -D
yarn add eslint-import-resolver-typescript -D
yarn add prettier eslint-config-prettier eslint-plugin-prettier -D

yarn tsc --init
```

crie na raiz a pasta src para abrigar seu codigo ts e configure o tsconfig para ler dessa pasta e colocar o codigo buildado na pasta dist

```json
"outDir": "./dist",
"rootDir": "./src",
```

adicione ao package.json os scripts

```json
"scripts": {
  "build": "tsc",
  "dev:server": "ts-node-dev --transpile-only --ignore-watch node_modules src/server.ts"
},
```

instale no seu editor de codigo a extensão editorconfig
crie um arquivo na raiz chamado .editorconfig com o seguinte conteudo

```
root = true

[*]
end_of_line = lf
indent_style = space
indent_size = 2
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

```

isso fara com que todos os diferentes editores de codigo nos diferentes SOs respeitem as mesmas regras de estilo de escrita do codigo, charset, final de linha e etc.

instale no seu editor a extensão eslint, execute

yarn eslint --init

responda as perguntas que aparecerão na ordem abaixo

1- How would you like to use ESLint?
To check syntax, find problems, and enforce code style

2- What type of modules does your project use?
JavaScript modules (import/export)

3- Which framework does your project use?
None of these

4- Does your project use TypeScript?
yes

5- Where does your code run?
[ ] Browser
[x] Node

6- How would you like to define a style for your project?
Use a popular style guide
AirBnB

7- What format do you want your config file to be in?
JSON

8- Would you like to install them now with npm?
no
aqui vc respondeu n pq vc ta usando o yarn, copie a linha de codigo que foi gerada com as dependencias acima da pergunta para instalar com o yarn add, so remova dessa linha a parte do eslint pois ele ja esta instalado
o comando ficara parecido com esse

```
yarn add @typescript-eslint/eslint-plugin@latest eslint-config-airbnb-base@latest eslint-plugin-import@^2.21.2 @typescript-eslint/parser@latest
```

para o eslint formatar seu codigo a cada save adicione as configurações do seu vscode as seguintes configurações

```json
  "[javascript]": {
    "editor.codeActionsOnSave": {
      "source.fixAll.eslint": true
    }
  },
  "[javascriptreact]": {
    "editor.codeActionsOnSave": {
      "source.fixAll.eslint": true
    }
  },
  "[typescript]": {
    "editor.codeActionsOnSave": {
      "source.fixAll.eslint": true
    }
  },
  "[typescriptreact]": {
    "editor.codeActionsOnSave": {
      "source.fixAll.eslint": true
    }
  },
```

### removendo erros de importação typescript acusados pelo eslint

abra o arquivo .esint.json e adicione em rules (import/extensions) and settings (import/resolver)

```json
  "rules": {
    "import/extensions": [
      "error",
      "ignorePackages",
      {
        "ts": "never"
      }
    ]
  },
  "settings": {
    "import/resolver": {
      "typescript": {}
    }
  }
```

### configurando prettier
abra seu arquivo .eslintrc.json e mescle as seguintes configurações

```json
  "extends": [
    "airbnb-base",
    "plugin:@typescript-eslint/recommended",
    "prettier/@typescript-eslint",
    "plugin:prettier/recommended"
  ],
  "plugins": [
    "@typescript-eslint",
    "prettier"
  ],
  "rules": {
    "prettier/prettier": "error",
  },
```

adicione na raiz o arquivo prettier.config.js com o conteudo

```javascript
module.exports = {
  singleQuote: true,
  trailingComma: "all",
  arrowParens: "avoid",
};
```

adicione na raiz o arquivo .eslintignore com o conteudo

```
/*.js
node_modules
dist
```
