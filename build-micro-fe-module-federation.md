## What are micro frontends?

Divide a monolithic app into multiple smaller apps. each smaller app is responsible for a distinct feature of the product. with micro frontends, multiple engineering teams can work in isolation. each smaller app is easier to understand and make changes without accidentally breaking another part of our app.

## What is the Module Federation?

Introduced in Webpack 5, the Module Federation plugin gives developers a way to create multiple separate builds that form a single application. Any JavaScript application that is bundled with Webpack 5.0 or greater can dynamically load or share code and dependencies with any other at runtime.

## Why use Module Federation?

- A better way to share code

- Environment Independent

- Resolves Dependency Issues

## Module Federation Configuration

Module Federation is configuration-based, here basic configuration :
```
import {Configuration, container} from 'webpack';

export const webpackConfig: Configuration = {
  plugins: [
    new container.ModuleFederationPlugin({
      name: '',
      shared: []
    })
  ]
};
export default webpackConfig;
```
Here are the key configuration options need to know.

### Name

Name is the unique name for the exposed container. Module Federation uses the ContainerPlugin and when it is initialized, the name you entered will be used as the file name for the container’s relative path.
```
plugins: [
    new container.ModuleFederationPlugin({
      name: 'shop',
    })
  ]
};
```
### Filename

Filename is used to specify the file name for the output bundle that also serves as an entry point to the bundle.
```
plugins: [
  new container.ModuleFederationPlugin({
    filename: 'shop/remoteHome.js'
  })
]
```
### Remote

The remote option is a list of static remote modules that can be accessed by the local module. Remote can be an array or an object.
```
plugins: [
  new container.ModuleFederationPlugin({
   remotes: {
        ShopModule: 'ShopModule@http://localhost:3100/remoteHome.js'
        }
  })
]
```
### Exposes

This is the path to the module or files exposed by the container; it can be an object or an array.
```
plugins: [
  new container.ModuleFederationPlugin({
  exposes: {
    HomeComponent: './projects/app1-home/src/app/home/home.component.ts',
    ShopModule: './projects/app1-home/src/app/shop/shop.module.ts'
   }
  })
]
```
With Module Federation you can share not just modules, but other file types. The above configuration shows how to expose two different files.