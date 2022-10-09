# **NX micro-frontend setup guide**

This guide will provides step by step to build a web micro-frontend application structured with NX workspace. There are two different templates. One for application and one for library. Your project will most likely be splitted into multiple workspaces that are managed by different team building up their own micro-frontend applications and libraries to interface with the host.

## **Create workspace**

We will use the `create-nx-workspace` package to generate the workspace. Refers to the [NX website](https://nx.dev/nx/create-nx-workspace) for additional information.

```bash
npx create-nx-workspace mylib --name MyLib --style scss --preset core --nxCloud false --skipGit true --ci github
```

> TIP: Run the command without arguments to have the interactive mode on.

> TIP: Using something like `@MyOrg/MyLib` as first parameter will create a nested folder structure, but the application name wil be MyLib.

## **Create Host/Remote application**

To create the `host` application and optional libraries specific to the application, We will use the `@nrwl/angular` nx plugin generator.

First, install the NX angular generator plugin.

```bash
npm install @nrwl/angular@13 -D
```

## **Create first library**

Architecturing a micro-frontend is no more different than any other application. As such, we can create libraries that will be componsed of services, model, api (interfaces) and even components.

```bash
nx g @nrwl/angular:lib SomeLib --prefix=portal-somelib --importPath=@portal/somelib --publishable --strict
```

> TIP: Add `--dry-run` to validate the options will generate what´d you expect.

> TIP: run `nx g rm SomeLib` to remove the application or library.

## **Create first service**

To add a service within the newly created `MyLib` library. run the following commmand.

```bash
nx g @nrwl/angular:service MyService --project=portal-somelib
```

## **Create first component**

To add a componet within the newly created `MyLib` library. run the following commmand.

```bash
nx g @nrwl/angular:component MyComponent --project=portal-somelib
```

# Powered by

``` 
Powered by
  _   _ _            _                  ______               _____                      
 | \ | (_)          | |                |  ____|             / ____|                     
 |  \| |_ _ __   ___| |_ ___  ___ _ __ | |__ ___  _   _ _ _| (___   _____   _____ _ __  
 | . ` | | '_ \ / _ \ __/ _ \/ _ \ '_ \|  __/ _ \| | | | '__\___ \ / _ \ \ / / _ \ '_ \ 
 | |\  | | | | |  __/ ||  __/  __/ | | | | | (_) | |_| | |  ____) |  __/\ V /  __/ | | |
 |_| \_|_|_| |_|\___|\__\___|\___|_| |_|_|  \___/ \__,_|_| |_____/ \___| \_/ \___|_| |_|
```
