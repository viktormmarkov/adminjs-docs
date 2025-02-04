# Getting started

The "Getting started" section is an overview and quick explanation of AdminJS ecosystem. Detailed instructions for setting up your AdminJS application and connecting it to your database(s) are described in separate guides (scroll down to [Setup](getting-started.md#setup) for quick links).

### Overview

An AdminJS application consists of:

* a core package
* a plugin (for a framework of your choice)
* an adapter for (for a ORM/ODM of your choice)

### ESM & CJS Support

As of version 7, AdminJS only supports ESM and will no longer work with CommonJS syntax. When setting up your project you should follow the guidelines from Node.js documentation: [https://nodejs.org/docs/latest-v18.x/api/esm.html](https://nodejs.org/docs/latest-v18.x/api/esm.html)

In the most basic scenario, the steps to get started with ESM are:

* setting `type` to `"module"` in your `package.json` file,
* using `import`/`export` syntax with explicit `.js` extensions instead of `require`s,
* if using Typescript, you should set `moduleResolution` and `module` to `"nodenext"` and `target` to `"esnext"` in your `tsconfig.json`

{% hint style="warning" %}
If you use `@adminjs/nestjs` do not update to ESM as NestJS doesn't support ESM as of 2023/04. Instead, please see the [updated guide for NestJS plugin](plugins/nest.md) so that you can import updated AdminJS packages into your CJS NestJS app.
{% endhint %}

### Quickstart

`@adminjs/cli` provides `adminjs create` command which you can use to quickly create your AdminJS application.

#### Installation

**NPM:**

```bash
$ npm i -g @adminjs/cli
```

**Yarn:**

```bash
$ yarn global add @adminjs/cli
```

#### Usage

```bash
$ adminjs create
```

You may also set up your AdminJS application manually by following the rest of this documentation.

### Packages

First of all, install the core package:

```bash
$ yarn add adminjs
```

Next, install one of our plugins:

```bash
$ yarn add @adminjs/express                # for Express server
$ yarn add @adminjs/nestjs                 # for Nest server
$ yarn add @adminjs/hapi                   # for Hapi server
$ yarn add @adminjs/koa                    # for Koa server
$ yarn add @adminjs/fastify                # for Fastify server
```

Finally, install an adapter:

```bash
$ yarn add @adminjs/typeorm                # for TypeORM
$ yarn add @adminjs/sequelize              # for Sequelize
$ yarn add @adminjs/mongoose               # for Mongoose
$ yarn add @adminjs/prisma                 # for Prisma
$ yarn add @adminjs/mikroorm               # for MikroORM
$ yarn add @adminjs/objection              # for Objection
$ yarn add @adminjs/sql                    # for raw SQL, currently supports only Postgres
```

### Setup

After you have installed AdminJS dependencies, proceed to:

* [Plugins](plugins/) section for instructions on how to setup AdminJS with your framework.
* [Adapters](adapters/) section for instructions on how to connect your AdminJS instance to your database.

### Frontend bundling

AdminJS needs to generate its own frontend. In the production environment, you would bundle all frontend files during build step of your deployment process, but that would be quite annoying to do in development.

For this reason you should add `adminJS.watch()` function call after setting up all plugins and adapters. This only affects development environment (`process.env.NODE_ENV === 'development'`) and launches a separate bundling process in the background.

```typescript
import AdminJS from 'adminjs'

const adminJS = new AdminJS({
    // ...
})

adminJS.watch()
```

Without this step in development, AdminJS will start but won't display anything useful in the browser (except for some parsing errors in the console).
