See https://github.com/storybookjs/storybook/issues/35186 

In this commit:

[e1d7c0e#diff-5886c929f94f7b3459d0df077761ab4992bb59c282d8ecc8701fb2c82edce0edR45-R58](https://github.com/storybookjs/storybook/commit/e1d7c0e2b84080401cad0c3bf3af625102449dd4#diff-5886c929f94f7b3459d0df077761ab4992bb59c282d8ecc8701fb2c82edce0edR45-R58)

@storybook/react-dom-shim had react 19 added as acceptable for peer dependencies, but it's marked as an optional dependency.

This causes any project with strict-peer-deps=true and using @types/react 18 to fail, due to npm/cli#8416, where optional dependencies end up hoisting the latest peer dep with strict peer deps on, thus colliding with actual @types/react being used

While this requires specific setup, it cost us much of the morning when going from 10.4.4 -> 10.4.5/10.4.6 of storybook.

Is this really optional? the issue would go away if they weren't marked as optional, but just regular peer deps.

Reproduction link
* https://github.com/broksonic21/storybook-optional-dependencies/tree/main

Reproduction steps
* Clone repo
* `npm install` - get peer dependency issues
* run with `npm install --no-strict-peer-deps`, see that it passes
