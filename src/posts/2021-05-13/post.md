# ESLint and stylelint with code formatting in VSCode

![linter](./assets/2021-05-13.jpeg)

Good project has consistent code rules. To enforce them good practice is to use linters and formaters. For JS/TS the best linter is [ESLint](https://eslint.org/) and for CSS/Sass/Less - [stylelint](https://stylelint.io/). For code formating common choice is [Prettier](https://prettier.io/).

But Prettier often conflicts with linter. So how to set them up correctly?

## Extensions

Install two extensions:
- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [stylelint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)

There is also available [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) extension, but we won't use it.

Next update VSCode settings (in `.json` format) and add following lines:

```json
{
  ...

  "editor.codeActionsOnSave": {
    "source.fixAll": true
  },
  "editor.formatOnSave": true,
  "eslint.format.enable": true
}
```

## Project related stuff

Now in every project that you want to lint and format code - do following things.

### For ESLint

Instal packages:

```sh
npm i -D 
```

Next create `.eslintrc` file in the project's root folder with following content:

```json
{
  "ignorePatterns": [
    "node_modules",
    "dist",
    "build"
  ],
  "extends": [
    "react-app",
    "react-app/jest",
    "airbnb-typescript",
    "airbnb/hooks",
    "plugin:@typescript-eslint/recommended",
    "plugin:jest/recommended",
    "plugin:prettier/recommended"
  ],
  "plugins": [
    "react",
    "@typescript-eslint",
    "jest"
  ],
  "env": {
    "browser": true,
    "es6": true,
    "jest": true
  },
  "globals": {
    "Atomics": "readonly",
    "SharedArrayBuffer": "readonly"
  },
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaFeatures": {
      "jsx": true
    },
    "ecmaVersion": 2018,
    "sourceType": "module",
    "project": "./tsconfig.json"
  },
  "rules": {
    "linebreak-style": "off",
    "prettier/prettier": [
      "error",
      {
        "endOfLine": "auto",
        "singleQuote": true,
        "semi": false,
        "tabWidth": 2
      }
    ],
    "no-console": "off",
    "no-param-reassign": "off",
    "react/require-default-props": "off"
  },
  "overrides": [
    {
      "files": [
        "*.test.ts{,x}"
      ],
      "rules": {
        "react/jsx-props-no-spreading": "off"
      }
    }
  ]
}
```

### For stylelint

Instal packages:

```sh
npm i -D stylelint stylelint-config-standard stylelint-config-sass-guidelines
```

`stylelint-config-sass-guidelines` is for sass and scss files.

Next create `.stylelintrc` file in the project's root folder with following content:

```json
{
  "extends": "stylelint-config-sass-guidelines"
}
```

That's it. Code is linted when you are typing. Now every time you hit ctrl+s code will be fixed and formatted as it should be.
