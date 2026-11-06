---
name: fdd-git-sync
description: Sincroniza ramas de trabajo con los remotos y publica cambios siguiendo el flujo del repositorio FDD Otoño 2026 (fork `origin`, curso base `upstream`). Úsalo para hacer pull, push o preparar la actualización de una rama de tarea.
---

# Sincronizar y publicar cambios de FDD

En este repositorio, `origin` es el fork personal y `upstream` es `raya-lucaria/fdd_o26`. Las tareas se trabajan en ramas `tarea-*`; la rama publicada normalmente va a `origin` y el PR se dirige a `upstream/main`.

## Antes de sincronizar

- Confirma el repositorio, la rama actual, los remotos y `git status --short --branch`.
- No cambies de rama ni descartes, guardes en stash o sobrescribas trabajo sin una razón concreta. Si hay cambios locales, conserva su estado y distingue los archivos del encargo de cualquier otro trabajo pendiente.
- No uses `git pull` sin remoto y rama explícitos: primero consulta y descarga referencias con `git fetch` para saber qué se va a integrar.

## Traer cambios del curso

En una rama `tarea-*`, actualiza referencias y revisa la diferencia antes de integrar:

```bash
git fetch upstream
git log --oneline HEAD..upstream/main
```

Si hay commits nuevos de curso que deban entrar a la tarea, intégralos conservando el historial del repositorio:

```bash
git merge upstream/main
```

Resuelve conflictos solo en el contexto de la tarea y revisa el resultado con `git status` y `git diff`. No uses rebase, reset, force-push ni `git pull` con estrategias que reescriban el historial publicado.

Si necesitas traer commits que ya existen en la copia remota de tu rama, haz `git fetch origin` y compara `HEAD` con `origin/<rama>` antes de fusionar. Integra esa rama únicamente cuando tenga commits remotos que no estén en local.

## Publicar una tarea

Antes de publicar, confirma que estás en la rama esperada y que solo vas a incluir los archivos de la tarea. No agregues cambios ajenos con `git add .` o `git add -A`; usa rutas explícitas. Revisa el diff staged antes del commit.

Para publicar la rama en tu fork:

```bash
git push -u origin HEAD
```

En actualizaciones posteriores, `git push origin HEAD` publica los nuevos commits de la rama actual. Nunca fuerces el push por rutina. Si Git rechaza el push porque el remoto avanzó, trae `origin/<rama>`, revisa la divergencia, integra los commits y vuelve a publicar.

Las ramas de tareas ordinarias se proponen mediante PR hacia `upstream/main`. Respeta las excepciones del curso: `clase-10-apis` y `clase-11-computo` se conservan sin PR; sigue las instrucciones vigentes si el alcance de la rama cambió.

## Rama `main` y otras clases

No publiques cambios de trabajo directamente en `main`. No supongas que todas las ramas `clase-*` requieren PR: las instrucciones del curso definen excepciones y deben prevalecer. Antes de actualizar una rama de clase, confirma su remoto y destino en las instrucciones actuales.

## Cierre

Después de integrar o publicar, informa qué remoto y rama se usaron, qué se integró o publicó y si quedó algún cambio local sin incluir. Si hay conflictos o un push rechazado que no se puede resolver con seguridad, detente y explica el estado concreto; no reescribas historial para sortear el bloqueo.
