# Microfrontend-Monorepo

This application is having monorepo structure to demo how to build microfrontend apps using module federation.

## Creation of workspace using a specific angular/cli version

```
npx @angular/cli@15.2.10 new <workspace-name> --create-application=false

```

## Creation of application inside mono-repo-workspace

```
cd mono-repo-workspace

```

### Created host-app

```
ng g application host-app --routing --style=scss

```
#### Running it on port 4200

```
ng serve host-app --port=4200 -o

```
### Created mfe-app

```
ng g application mfe-app --routing --style=scss

```

#### Running it on port 4300

```
ng serve mfe-app --port=4300 -o

```

## Adding Module Federation package from Webpack 5 which is available in angular v15. To explicitly allow angular to use the custom builder namely '@angular-architects/module-federation' to enable this Module Federation package from Webpack 5 we need to run the below commands for both the applications i.e. host-app and mfe-app

```
ng add @angular-architects/module-federation --project host-app --port 4200 --type host

```

```
ng add @angular-architects/module-federation --project mfe-app --port 4300 --type remote

```

## Creating a component inside host-app

```
ng g c home --project host-app

```

## Creating a module and component inside mfe-app to expose it to host-app

```
ng g m todo-list --project mfe-app

```

```
ng g c todo-list --project mfe-app

```


## Exposing remote application 'mfe-app' to host application 'host-app'
### In mfe-app, webpack.config.js modify 'exposes' attribute 'TodoListModule' as defined in host-app routes as shown below:

```

const { shareAll, withModuleFederationPlugin } = require('@angular-architects/module-federation/webpack');

module.exports = withModuleFederationPlugin({

  name: 'mfe-app',

  exposes: {
    './TodoListModule': './projects/mfe-app/src/app/todo-list/todo-list.module.ts',
  },

  shared: {
    ...shareAll({ singleton: true, strictVersion: true, requiredVersion: 'auto' }),
  },

});

```

### In host-app, webpack.config.js looks like below:

```

const { shareAll, withModuleFederationPlugin } = require('@angular-architects/module-federation/webpack');

module.exports = withModuleFederationPlugin({

  remotes: {
    "mfe-app": "http://localhost:4300/remoteEntry.js",    
  },

  shared: {
    ...shareAll({ singleton: true, strictVersion: true, requiredVersion: 'auto' }),
  },

});

```
