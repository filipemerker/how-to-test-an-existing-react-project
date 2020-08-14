# How to test an existing React project

First thing when contibuting to public projects on github should be creating an `issue`.

There you can use a very objective template:

**Title**: Add tests

**Description**: Hey @owner, great lib!

I could help you by adding tests, how about that? `jest` + `react-testing-library`?

From there, if the woner approves, fork the repo and go ahead:

# React Native

First step should be adding libraries. Standard for me is:

`yarn add -D jest @testing-library/react-native react-test-renderer`

Next, add this to `jest.config.js` or `package.json`:

```js
module.exports = {
  testEnvironment: 'jsdom',
  preset: 'react-native',
  transform: {
    '^.+\\.(js)$': '<rootDir>/node_modules/react-native/jest/preprocessor.js'
  },
  transformIgnorePatterns: [
    'node_modules/(?!(jest-)?react-native)'
  ]
}
```

Than, go ahead and create a `__test__` folder and add a `View.test.js`

```js
import React from 'react';
import { View } from 'react-native';
import { render, cleanup } from '@testing-library/react-native';

afterEach(cleanup);

describe('View', () => {
  it('renders correctly', () => {
    const { baseElement } = render(<View />);

    expect(baseElement).toMatchSnapshot();
  });
});

```

If it's a `TypeScript` project, you should also do:

`yarn add -D @types/jest`

and add this to `tsconfig.json`:

```json
"types": [
	"@types/jest"
]
```

After that, you can add a new script to `package.json`:

```json
"test": "jest"
```

Now, go to the terminal and hit that `yarn test`!
