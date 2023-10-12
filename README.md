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
