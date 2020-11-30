# prettier-config
Make sure all of your code is run through Prettier when you commit it to git. We achieve this by configuring prettier to run on git hooks using husky and lint-staged.

## Install

`npm install --save-dev @mediacurrent/prettier-config`

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
