# **NX micro-frontend setup guide**

This guide will provides step by step to build a web micro-frontend application structured with NX workspace. There are two different templates. One for application and one for library. Your project will most likely be splitted into multiple workspaces that are managed by different team building up their own micro-frontend applications and libraries to interface with the host.

## **Setup environment**

Refers to the [Environment documentation](https://github.com/NineteenSevenFour/template-portal-lib/blob/main/ENVIRONMENT.md) to ensure you have the correct toolchain installed before carrying out this guide.

## **Create your library**

### **Initialize the workspace**

We will use the `create-nx-workspace` package to generate the workspace. Refers to the [NX website](https://nx.dev/nx/create-nx-workspace) for additional information.

```bash
npx create-nx-workspace mylib --name MyLib --style scss --preset core --nxCloud false --skipGit true --ci github
```

> TIP: Run the command without arguments to have the interactive mode on.

> TIP: Using something like `@MyOrg/MyLib` as first parameter will create a nested folder structure, but the application name wil be MyLib.

### **Scaffold the library**

Architecturing a micro-frontend is no more different than any other application. As such, we can create libraries that will be componsed of services, model, api (interfaces) and even components.

To create the `host` application and optional libraries specific to the application, We will use the `@nrwl/angular` nx plugin generator.

First, install the NX angular generator plugin.

```bash
npm install @nrwl/angular@13 -D
```

Once the angular plugin is installed, we can generate the library.

```bash
nx g @nrwl/angular:lib SomeLib --prefix=portal-somelib --importPath=@portal/somelib --publishable --strict
```

> TIP: Add `--dry-run` to validate the options will generate what´d you expect.

> TIP: run `nx g rm SomeLib` to remove the application or library.

### **Create first service**

To add a service within the newly created `MyLib` library. run the following commmand.

```bash
nx g @nrwl/angular:service MyService --project=portal-somelib
```

Once the service has been added, ensure to add it to the `provider` section of your library module as well as to the `index` or `public-api` file to ensure your service is accessible when referenced by other applications or libraries.

### **Create first component**

To add a componet within the newly created `MyLib` library. run the following commmand.

```bash
nx g @nrwl/angular:component MyComponent --project=portal-somelib
```

Once the component has been added, ensure to add it to the `declaration` and `export` sections of your library module as well as to the `index` or `public-api` file to ensure your component is accessible when referenced by other applications or libraries.

## **Setup Pre-commit validation**

While working alone or in a team, it is good practice to setup pre-commit validation of the code and commit message. This ensure that your project has constant buildable codebase and consistant commit.

[CGit Hooks](https://github.com/NineteenSevenFour/template-portal-lib/blob/main/CGITHOOKD.md)

## **Setup CI / CD**

Different team uses different process adapted for their needs, but typically, you will have some sort of `SDLC` that include `Brnaching` and `Pull request`. Following this workflow, you will most likely use also `Continuous integration` and in case you don´t, then you should !

The following guide will helps you setup a [CI / CD](https://github.com/NineteenSevenFour/template-portal-lib/blob/main/CI-CD.md) pipeline with `Github actions`. Refers to github for more information if this doesn´t fit your needs.

## **Packages upgrade**

From time to time, you will need to update / upgrade your packages to a newer version due to security fixes, support changes or new features adoption. The [Packages migration](https://github.com/NineteenSevenFour/template-portal-lib/blob/main/MIGRATION.md) guide provides exemples of commands to upgrade the workspace, runtime and dev packages.

## **Wants to learn mode ?**

While this guide is tailored for our needs, this is based on many good blog articles and tools documentation listed in a [Reading list](https://github.com/NineteenSevenFour/template-portal-lib/blob/main/REFERENCES.md).

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
