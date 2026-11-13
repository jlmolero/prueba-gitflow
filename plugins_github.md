# Plugin necesario para trabajar con Gitflow

Por el momento, el único plugin que se debe instalar en Visual Studio Code para este flujo es **GitHub Pull Requests and Issues**, publicado por GitHub.

## Instalación

1. Abre la vista **Extensions** en VS Code (`Ctrl+Shift+X`).
2. Busca `GitHub Pull Requests and Issues`.
3. Comprueba que el editor sea **GitHub** y selecciona **Install**.

También puedes instalarlo desde la [página de la extensión en Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github) o desde una terminal:

```bash
code --install-extension GitHub.vscode-pull-request-github
```

Al usarlo por primera vez, inicia sesión y autoriza a VS Code para acceder a tu cuenta de GitHub.

## Para qué se utiliza

La extensión permite consultar y trabajar con issues y Pull Requests de GitHub desde VS Code. En este repositorio se utiliza para acompañar el flujo de Pull Requests de Gitflow; la creación y el cambio entre ramas también pueden hacerse con Git desde la terminal o desde las funciones integradas de VS Code.

No es necesario instalar una extensión adicional de Gitflow. Git y VS Code son herramientas necesarias para el trabajo, pero no son plugins de VS Code.
