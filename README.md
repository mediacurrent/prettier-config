# @mediacurrent/prettier-config
Make sure all of your code is run through Prettier when you commit it to git. We achieve this by configuring prettier to run on git hooks using husky and lint-staged.

- [Install](#install)
- [Extend](#extend)
- [Ignore File](#ignore-file)
- [Pre-commit hook](#pre-commit-hook)
- [IDE Configuration](#ide-configuration)

## Install

`npm install --save-dev prettier @mediacurrent/prettier-config`

## Extend
Can be extended two ways:

### package.json

Add the following to you `package.json`

`"prettier": "@mediacurrent/prettier-config"`

This method *does not* allow overrides.  If overrides are needed, use the next method.

### .prettierrc.js

```javascript
module.exports = {
  ...require("@mediacurrent/prettier-config"),
  // Override here
  semi: false,
};
```

## Ignore File
Unfortunately, Prettier does not have a way to extend a shared `.prettierignore` file so the one in this repo must be copied and pasted in to a new `.prettierignore` file at the root of your project.

## Pre-commit Hook
To have prettier format all files before commit (to prevent unformatted files from being committed), follow these steps.

### Install packages

`npm install --save-dev husky lint-staged`

### Add hooks to `package.json`
This will affect `.js`, `.md`, `.mdx`, `.json`, and `.scss` files.  For this to work properly, [eslint](https://github.com/mediacurrent/eslint-config-react) and [stylelint](https://github.com/mediacurrent/stylelint-config) need to have been configured properly.

Add the following `husky` and `lint-staged` commands to your `package.json`.

```json
{
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "*.{js,md,mdx,json}": "['prettier --write']",
    "*.scss": "npm run lint:sass",
  }
}
```
The `npm run lint:sass` command is tied to the stylelint config and the jest test running suite.

## IDE Configuration

### VSCode

A developer may or may not like having Prettier auto format when a file is saved.  The pre-commit hook will always format the file, so that choice can be controlled the following way in VSCode:

`Settings -> Text Editor -> Formatting -> Format on Save`
