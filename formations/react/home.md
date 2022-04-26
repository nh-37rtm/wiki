---
title: Untitled Page
description: This is the short description
published: true
date: 2021-02-19T23:20:10.150Z
tags: 
editor: undefined
dateCreated: 2020-11-19T23:20:10.150Z
---

# Project creation

## initialise the project using

````
npx create-react-native-app xperience-react-native
````
## add the typescrpit tools to the project

````
pnpm add -D typescript @types/jest @types/react @types/react-native @types/react-test-renderer
````
you can also create explicit configurations inside ``tsconfig.json`` and ``jest.config.js``

## references
 - https://reactnative.dev/docs/typescript
  

## Start the react packager inside vscode

you can use F1 + ``>packager``
with the react native tools extension installed you should have the ``React Native: Start Packager`` proposition

## Attach debugger to packager

in the ``{project}/.vscode/launch.json`` you can have for exemple :
````
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach to packager",
            "request": "attach",
            "type": "reactnative",
            "cwd": "${workspaceFolder}"
        },
    ]
}
````
the default packager should listen on the 8081 port, you can see the packager output logs in the Output tab ( F1 + ``output`` should show the Focus action)

if the step works you should see that the connexion state is established in the debug console output associated to you project


## Run the application

````
pnpm android
````
# References
- https://reactnative.dev/docs/typescript