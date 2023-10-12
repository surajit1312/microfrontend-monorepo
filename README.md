# Microfrontend-Monorepo

This application is having monorepo structure to demo how to build microfrontend apps using module federation.

# Creation of workspace using a specific angular/cli version

```
npx @angular/cli@15.2.10 new <workspace-name> --create-application=false

```

# Creation of application inside mono-repo-workspace

```
cd mono-repo-workspace

```

## Created host-app

```
ng g application host-app --routing --style=scss

```

## Created mfe-app

```
ng g application mfe-app --routing --style=scss

```
