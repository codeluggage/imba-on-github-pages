_Bootstrapped with [imba-vite-template](https://github.com/imba/imba-vite-template)._

Welcome to the Imba Vite template! Let's get you set up and ready to code!

## Deploying to GitHub Pages

### 1) Set up GitHub Actions

Click the settings of your repository, and then click into **Pages** in the left sidebar:

![image](https://user-images.githubusercontent.com/1154150/189821341-3d227338-5bca-416e-b75d-7ed0224ac900.png)

### 2) Use the Node.js workflow

Browse the available workflows, and select the Node.js workflow.

### 3) Edit the node.js.yml file

```yml
# This workflow will do a clean installation of node dependencies, cache/restore them, build the source code and run tests across different versions of node
# For more information see: https://help.github.com/actions/language-and-framework-guides/using-nodejs-with-github-actions

name: Node.js CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:

    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [18.x]
        # See supported Node.js release schedule at https://nodejs.org/en/about/releases/

    steps:
    - uses: actions/checkout@v3
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
    - run: npm ci
    - run: npm run build --if-present
    - run: npm test
    - name: Deploy
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish: ./dist
```

### 4) Update the `base` of the Vite config

Depending on how you are deploying this, you'll need to modify the `base` Vite configuration in the `vite.config.js` file:

If you want your repo to be deployed on its own (for example <https://my-neat-website.github.io>), replace the `imba-on-github-pages` part with the name of your repository. 

If you want your repo to be your primary GitHub username website (for example <https://my-neat-username.github.io>), then delete the `base: "/imba-on-github-pages/",` line from the config completely.


## Code structure

### `main.imba`

In `src/main.imba` you see how [Imba styles](https://imba.io/docs/css) work. CSS is clearly scoped in Imba, so you can see [global CSS](https://imba.io/docs/css/syntax#selectors-global-selectors), tag level, and element level.

Both [assets](https://imba.io/docs/assets) and [components](https://imba.io/docs/components/) are imported and used. Finally, the web application is started by [mounting the tag](https://imba.io/docs/tags/mounting).

### `counter.imba`

In `src/components/counter.imba` you see more about how [tags](https://imba.io/docs/tags), [props](https://imba.io/docs/tags#setting-properties), [state management](https://imba.io/docs/state-management) (which is usually a big, complex topic - but is very lightweight in Imba), and inheriting from the web itself (in this case, the HTML button). There's also a [Vitest in-source component test](https://vitest.dev/guide/in-source.html), showing you how this tag is meant to be used.

### `app.css`

You don't need to use CSS files, because of the powerful scoping of [Imba styles](https://imba.io/docs/css), but this file shows how you can get the best of both worlds. It is imported and used in `src/main.imba`.

### `utils.imba`

To showcase logic without any front end interactions, there's a simple example `src/utils.imba` has in-source testing and 

### `tests/`

In `test/basic.test.imba` you see how terse and succinct the testing syntax is with Imba, using [Vitest](https://vitest.dev/). This test is in its own file with the `.test.imba` filename ending, but you can also use inline tests like in `src/components/counter.imba`.

## Recommended IDE

- [VS Code](https://code.visualstudio.com/).
- [Imba extension](https://marketplace.visualstudio.com/items?itemName=scrimba.vsimba) - which is automatically recommended if you open this repository in VSCode.

## Available Scripts

In the project directory, you can run:

### `npm dev`

Runs in development mode on `http://localhost:3000` with hot reloading, linting and detailed error output in the console, and source maps.

### `npm run build`

Builds the app for production to the `dist` folder. From here you can [deploy your app](https://imba.io/guides/deployment) to static hosting.

### `npm run preview`

_NOTE: Requires `npm run build` to have been run first._

Preview the production application from the `dist/` folder, just as it will be running on static hosting.

### `npm test`

Run and watch the tests.

### `npm run test:ui`

Run and watch the tests - and open the [Vitest UI](https://vitest.dev/guide/ui.html)

## Notes
- This app doesn't have a server. If you need a full stack web application with server logic you can use [imba base template](https://github.com/imba/imba-base-template) or check out [Vite's backend integration guide](https://vitejs.dev/guide/backend-integration.html)
- There is a temporary `src/main.js` file that is still necessary for Vite to work correctly. You don't have to do anything with this file. And this will probably be fixed in a future version of Vite.
