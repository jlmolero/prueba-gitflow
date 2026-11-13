# Workflow del Project Manager en GitHub

Tutorial para coordinar Gitflow desde la interfaz web de GitHub.

## 1. Preparar el trabajo

1. En **Issues → New issue**, crea una tarea con objetivo y criterios de aceptación.
2. Asigna responsable y etiquetas; agrega el issue al milestone de la versión y al GitHub Project, si se usan.
3. En **Settings → Branches** o **Rules → Rulesets**, confirma que `main` y `develop` estén protegidas y requieran Pull Requests.

## 2. Coordinar una funcionalidad

1. En **Branches → New branch**, crea `feature/<issue>-<nombre>` desde `develop`.
2. Pide al responsable que abra una Pull Request desde esa rama hacia `develop`.
3. En la PR, verifica que la base sea `develop`, que enlace el issue, cumpla sus criterios y pase las revisiones y comprobaciones requeridas.
4. Cuando esté aprobada, integra la PR según las reglas del repositorio y mueve el issue a revisión o completado, según el flujo del equipo. No lo marques como publicado hasta que el cambio llegue a `main`.

## 3. Coordinar una versión

1. Confirma que el alcance acordado esté integrado en `develop` y crea `release/<version>` desde **Branches → New branch**, usando `develop` como origen.
2. Revisa la PR de `release/<version>` a `main`; comprueba revisiones, verificaciones y notas de versión. Intégrala cuando esté aprobada.
3. Abre y revisa una PR de `main` a `develop` para devolver a desarrollo las correcciones de la release; intégrala.
4. En **Releases → Draft a new release**, crea el tag (por ejemplo, `v1.2.0`), selecciona `main` como destino, completa las notas y publica.
5. Actualiza el milestone y el Project; cierra los issues incluidos una vez publicados y aceptados.

## 4. Coordinar un hotfix

1. Crea `hotfix/<issue>-<nombre>` desde `main` en **Branches → New branch**.
2. Revisa y prioriza la PR de esa rama a `main`; intégrala cuando pase las revisiones y comprobaciones.
3. Abre una PR de `main` a `develop` e intégrala para conservar la corrección en el próximo desarrollo.
4. Crea el tag y publica el release desde **Releases** con destino `main`; actualiza el issue y el Project.

## Comprobación rápida

- Funcionalidad: `feature/*` → `develop`.
- Release y hotfix: primero → `main`; después sincronizar `main` → `develop`.
- No integrar PR con destino incorrecto, revisiones pendientes o comprobaciones fallidas.
- Mantener issues y milestones al día; cerrar el trabajo cuando cumpla sus criterios y esté publicado.
