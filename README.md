React Redux Starter Kit
=======================

[![Join the chat at https://gitter.im/davezuko/react-redux-starter-kit](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/davezuko/react-redux-starter-kit?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Build Status](https://travis-ci.org/davezuko/react-redux-starter-kit.svg?branch=master)](https://travis-ci.org/davezuko/react-redux-starter-kit?branch=master)
[![dependencies](https://david-dm.org/davezuko/react-redux-starter-kit.svg)](https://david-dm.org/davezuko/react-redux-starter-kit)
[![devDependency Status](https://david-dm.org/davezuko/react-redux-starter-kit/dev-status.svg)](https://david-dm.org/davezuko/react-redux-starter-kit#info=devDependencies)


> ### This Project Recently Upgraded to Babel 6!
> Woohoo! If you'd like to try it out, you're welcome to build directly from the master branch. However, if troubleshooting issues with Babel isn't quite your thing, just pull the [stable v0.18.0 release](https://github.com/davezuko/react-redux-starter-kit/tree/v0.18.0) and continue on your way with Babel 5.

This starter kit is designed to get you up and running with a bunch of awesome new front-end technologies, all on top of a configurable, feature-rich webpack build system that's already setup to provide hot reloading, CSS modules with Sass support, unit testing, code coverage reports, bundle splitting, and a whole lot more.

The primary goal of this project is to remain as **unopinionated** as possible. Its purpose is not to dictate your project structure or to demonstrate a complete sample application, but to provide a set of tools intended to make front-end development robust, easy, and, most importantly, fun. Check out the full feature list below!

Table of Contents
-----------------
1. [Requirements](#requirements)
1. [Features](#features)
1. [Getting Started](#getting-started)
1. [Usage](#usage)
1. [Structure](#structure)
1. [Webpack](#webpack)
1. [Server](#server)
1. [Styles](#styles)
1. [Testing](#testing)
1. [Utilities](#utilities)
1. [Deployment](#deployment)
1. [Troubleshooting](#troubleshooting)

Requirements
------------

Node `^5.0.0`

Features
--------

* [React](https://github.com/facebook/react) (`^0.14.0`)
  * Includes react-addons-test-utils (`^0.14.0`)
* [Redux](https://github.com/gaearon/redux) (`^3.0.0`)
  * react-redux (`^4.0.0`)
  * redux-devtools
    * use `npm run dev:nw` to display in a separate window.
  * redux-thunk middleware
* [react-router](https://github.com/rackt/react-router) (`^1.0.0`)
* [redux-simple-router](https://github.com/jlongster/redux-simple-router) (`^0.0.10`)
* [Webpack](https://github.com/webpack/webpack)
  * [CSS modules!](https://github.com/css-modules/css-modules)
  * sass-loader
  * postcss-loader with cssnano for style autoprefixing and minification
  * Pre-configured folder aliases and globals
  * Separate vendor-only bundle for common dependencies
  * CSS extraction during production builds
  * Loader support for fonts and images
* [Express](https://github.com/strongloop/express)
  * webpack-dev-middleware
  * webpack-hot-middleware
* [Karma](https://github.com/karma-runner/karma)
  * Mocha w/ Chai, Sinon-Chai, and Chai-as-Promised
  * PhantomJS
  * Code coverage reports
* [Babel](https://github.com/babel/babel) (`^6.3.0`)
  * `react-transform-hmr` for hot reloading
  * `react-transform-catch-errors` with `redbox-react` for more visible error reporting
  * Uses babel runtime rather than inline transformations
* [ESLint](http://eslint.org)
  * Includes [eslint-config-defaults](https://github.com/walmartlabs/eslint-config-defaults) (uses airbnb by default)
  * Includes separate test-specific `.eslintrc` to work with Mocha and Chai

Getting Started
---------------

Just clone the repo and install the necessary node modules:

```shell
$ git clone https://github.com/davezuko/react-redux-starter-kit.git
$ cd react-redux-starter-kit
$ npm install                   # Install Node modules listed in ./package.json (may take a while the first time)
$ npm start                     # Compile and launch
```

Usage
-----

Before delving into the descriptions for each available npm script, here's a brief summary of the three which will most likely be your bread and butter:

* Doing live development? Use `npm start` to spin up the dev server.
* Compiling the application to disk? Use `npm run compile`.
* Deploying to an environment? `npm run deploy` can help with that.

**NOTE:** This package makes use of [debug](https://github.com/visionmedia/debug) to improve your debugging experience. To see all starter kit messages during the build process, set the `DEBUG` environment variable to `kit:*` (e.g. `DEBUG=kit:* npm start`).

Great, now that introductions have been made here's everything in full detail:

* `npm start` - Spins up express server to serve your app at `localhost:3000`. HMR will be enabled in development.
* `npm run compile` - Compiles the application to disk (`~/dist` by default).
* `npm run dev:nw` - Same as `npm start`, but opens the redux devtools in a new window.
* `npm run dev:no-debug` - Same as `npm start` but disables redux devtools.
* `npm run test` - Runs unit tests with Karma and generates a coverage report.
* `npm run test:dev` - Runs Karma and watches for changes to re-run tests; does not generate coverage reports.
* `npm run lint` - Runs ESLint against your source code.
* `npm run lint:tests` - Runs ESLint against your tests.
* `npm run deploy`- Runs linter, tests, and then, on success, compiles your application to disk.

**NOTE:** Deploying to a specific environment? Make sure to specify your target `NODE_ENV` so webpack will use the correct configuration. For example: `NODE_ENV=production npm run compile` will compile your application with `~/build/webpack/production.js`.

### Configuration

Basic project configuration can be found in `~/config/index.js`. Here you'll be able to redefine your `src` and `dist` directories, add/remove aliases, tweak your vendor dependencies, and more. For the most part, you should be able to make changes in here _without ever having to touch the webpack build configuration_. If you need environment-specific overrides, create a file with the name of target `NODE_ENV` prefixed by an `_` in `~/config` (see `~/config/_production.js` for an example).

Common configuration options:

* `dir_src` - application source code base path
* `dir_dist` - path to build compiled application to
* `server_host` - hostname for the express server
* `server_port` - port for the express server
* `compiler_css_modules` - whether or not to enable CSS modules
* `compiler_source_maps` - whether or not to generate source maps
* `compiler_vendor` - packages to separate into to the vendor bundle

Structure
---------

The folder structure provided is only meant to serve as a guide, it is by no means prescriptive. It is something that has worked very well for me and my team, but use only what makes sense to you.

```
.
├── bin                      # Build/Start scripts
├── build                    # All build-related configuration
│   └── webpack              # Environment-specific configuration files for webpack
├── config                   # Project configuration settings
├── server                   # Express application (uses webpack middleware)
│   └── app.js               # Server application entry point
├── src                      # Application source code
│   ├── components           # Generic React Components (generally Dumb components)
│   ├── containers           # Components that provide context (e.g. Redux Provider)
│   ├── layouts              # Components that dictate major page structure
│   ├── redux                # Redux-specific pieces
│   │   └── modules          # Collections of reducers/constants/actions
│   ├── routes               # Application route definitions
│   ├── styles               # Application-wide styles (generally settings)
│   ├── utils                # Generic utilities
│   ├── views                # Components that live at a route
│   └── app.js               # Application bootstrap and rendering
└── tests                    # Unit tests
```

### Components vs. Views vs. Layouts

**TL;DR:** They're all components.

This distinction may not be important for you, but as an explanation: A **Layout** is something that describes an entire page structure, such as a fixed navigation, viewport, sidebar, and footer. Most applications will probably only have one layout, but keeping these components separate makes their intent clear. **Views** are components that live at routes, and are generally rendered within a **Layout**. What this ends up meaning is that, with this structure, nearly everything inside of **Components** ends up being a dumb component.

Webpack
-------

### Configuration
The webpack compiler configuration is located in `~/build/webpack`. Here you'll find configurations for each environment; `development`, `production`, and `development_hot` exist out of the box. These configurations are selected based on your current `NODE_ENV`, with the exception of `development_hot` which will _always_ be used during live development.

**Note**: There has been a conscious decision to keep development-specific configuration (such as hot-reloading) out of `.babelrc`. By doing this, it's possible to create cleaner development builds (such as for teams that have a `dev` -> `stage` -> `production` workflow) that don't, for example, constantly poll for HMR updates.

So why not just disable HMR? Well, as a further explanation, enabling `react-transform-hmr` in `.babelrc` but building the project without HMR enabled (think of running tests with `NODE_ENV=development` but without a dev server) causes errors to be thrown, so this decision also alleviates that issue.

### Vendor Bundle
You can redefine which packages to treat as vendor dependencies by editing `compiler_vendor` in `~/config/index.js`. These default to:

```js
[
  'history',
  'react',
  'react-redux',
  'react-router',
  'redux-simple-router',
  'redux'
]
```

### Webpack Root Resolve
Webpack is configured to make use of [resolve.root](http://webpack.github.io/docs/configuration.html#resolve-root), which lets you import local packages as if you were traversing from the root of your `~/src` directory. Here's an example:

```js
// current file: ~/src/views/some/nested/View.js

// What used to be this:
import SomeComponent from '../../../components/SomeComponent';

// Can now be this:
import SomeComponent from 'components/SomeComponent'; // Hooray!
```

### Globals

These are global variables available to you anywhere in your source code. If you wish to modify them, they can be found as the `globals` key in `~/config/index.js`.

* `process.env.NODE_ENV` - the active `NODE_ENV` when the build started
* `__DEV__` - True when `process.env.NODE_ENV` is `development`
* `__PROD__` - True when `process.env.NODE_ENV` is `production`

Server
------

This starter kit comes packaged with an Express server. It's important to note that the sole purpose of this server is to provide `webpack-dev-middleware` and `webpack-hot-middleware` for hot module replacement. Using a custom Express app in place of webpack-dev-server will hopefully make it easier for users to extend the starter kit to include functionality such as back-end API's, isomorphic/universal rendering, and more -- all without bloating the base boilerplate. Because of this, it should be noted that the provided server is **not** production-ready. If you're deploying to production, take a look at [the deployment section](#deployment).

Styles
------

Both `.scss` and `.css` file extensions are supported out of the box and are configured to use [CSS Modules](https://github.com/css-modules/css-modules). After being imported, styles will be processed with [PostCSS](https://github.com/postcss/postcss) for minification and autoprefixing, and will be extracted to a `.css` file during production builds.

**NOTE:** If you're importing styles from a base styles directory (useful for generic, app-wide styles), you can make use of the `styles` alias, e.g.:

```js
// current file: ~/src/components/some/nested/component/index.jsx
import 'styles/core.scss'; // this imports ~/src/styles/core.scss
```

Furthermore, this `styles` directory is aliased for sass imports, which further eliminates manual directory traversing; this is especially useful for importing variables/mixins.

Here's an example:

```scss
// current file: ~/src/styles/some/nested/style.scss
// what used to be this (where base is ~/src/styles/_base.scss):
@import '../../base';

// can now be this:
@import 'base';
```

Testing
-------

To add a unit test, simply create a `.spec.js` file anywhere in `~/tests`. Karma will pick up on these files automatically, and Mocha and Chai will be available within your test without the need to import them.

Coverage reports will be compiled to `~/coverage` by default. If you wish to change what reporters are used and where reports are compiled, you can do so by modifying `coverage_reporters` in `~/config/index.js`.

Utilities
---------

This boilerplate comes with a simple utility (thanks to [StevenLangbroek](https://github.com/StevenLangbroek)) to help speed up your Redux development process. In `~/client/utils` you'll find an export for `createReducer` designed to expedite the creation of reducers when they're defined via an object map rather than switch statements. As an example, what once looked like this:

```js
import { TODO_CREATE } from 'constants/todo';

const initialState = [];
const handlers = {
  [TODO_CREATE] : (state, payload) => { ... }
};

export default function todo (state = initialState, action) {
  const handler = handlers[action.type];

  return handler ? handler(state, action.payload) : state;
}
```

Can now look like this:

```js
import { TODO_CREATE }   from 'constants/todo';
import { createReducer } from 'utils';

const initialState = [];

export default createReducer(initialState, {
  [TODO_CREATE] : (state, payload) => { ... }
});
```

Deployment
----------

Out of the box, this starter kit is deployable by serving the `~/dist` folder generated by `npm run compile` (make sure to specify your target `NODE_ENV` as well). This project does not concern itself with the details of server-side rendering or API structure, since that demands an opinionated structure that makes it difficult to extend the starter kit. However, if you do need help with more advanced deployment strategies, here are a few tips:

If you are serving the application via a web server such as nginx, make sure to direct incoming routes to the root `~/dist/index.html` file and let react-router take care of the rest. The Express server that comes with the starter kit is able to be extended to serve as an API or whatever else you need, but that's entirely up to you.

Have more questions? Feel free to submit an issue or join the Gitter chat!

Troubleshooting
---------------

### `npm run dev:nw` produces `cannot read location of undefined.`

This is most likely because the new window has been blocked by your popup blocker, so make sure it's disabled before trying again.

Reference: [issue 110](https://github.com/davezuko/react-redux-starter-kit/issues/110)
