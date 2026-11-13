# Configuración de GitHub para trabajar con Gitflow

Esta guía configura el repositorio para usar Gitflow con GitHub y Pull Requests. El flujo usa dos ramas permanentes:

- `main`: versiones estables que se pueden publicar.
- `develop`: integración del trabajo que formará parte de la siguiente versión.

Las ramas de trabajo son temporales y siguen estos nombres:

- `feature/<nombre>`: nuevas funcionalidades; nacen y se integran en `develop`.
- `release/<version>`: preparación de una versión; nace en `develop` y se integra en `main` y `develop`.
- `hotfix/<nombre>`: correcciones urgentes de producción; nacen en `main` y se integran en `main` y `develop`.

## 1. Preparar las ramas

1. En GitHub, abre **Settings → General → Default branch** y establece `main` como rama predeterminada. Si todavía no existe, crea y publica `main` primero.
2. Crea `develop` a partir de `main` y publícala:

   ```bash
   git switch main
   git pull
   git switch -c develop
   git push -u origin develop
   ```

3. Conserva `main` como rama predeterminada. Las Pull Requests de funcionalidades se dirigirán explícitamente a `develop`.

## 2. Proteger `main` y `develop`

En **Settings → Rules → Rulesets**, crea un ruleset de ramas activo para cada rama y selecciona como destino el nombre exacto (`main` o `develop`). Si los rulesets no están disponibles en este repositorio, usa **Settings → Branches → Branch protection rules**.

Activa en ambas ramas:

- **Require a pull request before merging**: no permitir cambios directos.
- **Require conversation resolution**: resolver comentarios de revisión antes de integrar.
- **Block force pushes** y **Restrict deletions**: evitar reescrituras y borrados accidentales.
- Permitir a los administradores quedar sujetos a las mismas reglas, si se quiere que la protección no tenga excepciones.

En un equipo, exige al menos una aprobación y descarta aprobaciones obsoletas cuando se suben cambios nuevos. Para una persona trabajando sola, no exijas aprobación: conserva el requisito de Pull Request y revisa los cambios antes de integrarlos.

Activa **Require status checks to pass** solo después de que el repositorio tenga una acción de CI que publique comprobaciones de estado. Selecciona las comprobaciones necesarias para compilar y probar el proyecto; no marques comprobaciones que no existan o que no se ejecuten en cada Pull Request.

## 3. Configurar la integración de Pull Requests

En **Settings → General → Pull Requests**:

- Mantén habilitado **Allow merge commits**. Gitflow utiliza ramas de integración y el merge commit conserva el historial de la rama.
- Deshabilita **Allow squash merging** y **Allow rebase merging** si quieres que todas las integraciones respeten esa convención.
- Habilita **Automatically delete head branches** para limpiar las ramas temporales una vez integradas.

Si el repositorio ya tiene una política de integración acordada, aplícala de forma consistente en vez de cambiarla sin revisar el historial existente.

## 4. Flujo de trabajo diario

### Funcionalidad

1. Crea `feature/<nombre>` desde `develop`.
2. Publica la rama y abre una Pull Request con destino `develop`.
3. Revisa y pasa las comprobaciones requeridas; integra la PR y elimina la rama temporal.

```bash
git switch develop
git pull
git switch -c feature/nombre
# realizar y confirmar los cambios
git push -u origin feature/nombre
```

### Preparar una versión

1. Crea `release/<version>` desde `develop` cuando el conjunto de cambios esté listo.
2. En esa rama, limita los cambios a estabilización, correcciones y metadatos de versión.
3. Abre una PR de `release/<version>` a `main`. Tras integrarla, crea un tag de versión (por ejemplo, `v1.2.0`) en el commit publicado.
4. Integra también la rama de release en `develop` para conservar allí las correcciones realizadas durante la preparación.

### Corrección urgente

1. Crea `hotfix/<nombre>` desde `main`.
2. Abre una PR hacia `main`; tras integrarla, publica un nuevo tag de versión.
3. Integra la misma corrección en `develop` (mediante otra PR o incorporando el cambio de `main`), para que no se pierda en la próxima versión.

## 5. Comprobación inicial

- `main` y `develop` existen y están protegidas.
- Las PR de funcionalidades tienen como destino `develop`; las de release y hotfix tienen como destino `main`.
- No se exige una comprobación de CI hasta que exista y se ejecute en las PR.
- Las personas colaboradoras conocen la convención de nombres y el destino de cada tipo de rama.