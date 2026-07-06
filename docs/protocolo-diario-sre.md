# Protocolo diario — Fase 1

Tu referencia para cada sesión. Ábrelo, síguelo, cierra sesión.

---

## La regla de oro

> Toda sesión termina en commit. Sin excepción.
> Si no hay commit, la sesión no existió.

---

## Día RHCSA (L, M, J, V)

### Antes de empezar (~2 min)

```bash
cd ~/sre-lab
git pull                    # por si tocaste algo desde otro sitio
```

Abre el libro de van Vugt en el capítulo que toque según el calendario.
Ten la VM de RHEL abierta (ssh o consola de Proxmox).

### Bloque 1 — Lectura activa (~20 min)

Lee el capítulo (o la sección que toque) con la terminal al lado.
NO copies y pegues los comandos del libro: escríbelos a mano.
Cuando algo te sorprenda o no lo entiendas, anótalo en tu fichero de notas.

El fichero de notas sigue esta plantilla:

```markdown
# Semana X · Cap Y — Título del capítulo

## Conceptos clave
- concepto 1: explicación breve con tus palabras
- concepto 2: ...

## Comandos nuevos
- `comando`: qué hace y cuándo usarlo
- `otro comando`: ...

## Lo que me ha costado
- cosa que no entendía y cómo la resolví

## Conexión con mi homelab
- "esto es lo que pasa cuando hago X en mis LXC"
```

Ruta del fichero: `fase1-linux/labs/semana-XX-tema.md`

### Bloque 2 — Lab práctico (~30-40 min)

Haz los ejercicios del capítulo en tu VM de RHEL.
El libro de van Vugt tiene ejercicios al final de cada capítulo: hazlos TODOS.
Si algo se rompe: bien. Diagnostica, arregla, y anota qué pasó.

Reglas del lab:
- Snapshot antes de romper cosas a propósito
- Si un comando no hace lo que esperas, investiga POR QUÉ antes de seguir
- Si terminas pronto, repite el ejercicio sin mirar el libro

### Bloque 3 — Commit (~5 min)

```bash
cd ~/sre-lab

# Ver qué has tocado
git status

# Añadir los ficheros que has creado/modificado
git add fase1-linux/labs/semana-01-herramientas.md

# Commit con mensaje descriptivo
git commit -m "lab(s1): cap2 - navegacion shell y ficheros"

# Subir
git push
```

### ¿Qué subo exactamente?

Tus notas del capítulo (el .md), siempre.
Si has creado scripts durante el lab, también.
Si has hecho una chuleta, también.

Lo que NO se sube: capturas de pantalla del libro, PDFs del libro,
contraseñas o tokens.

---

## Día de TICKET (cuando toca según calendario)

### El flujo del ticket (~45-60 min)

1. Lee el enunciado del ticket (pídelo a Claude si no lo tienes)
2. Pon un cronómetro visible
3. Prepara el sabotaje en tu VM (los comandos vienen con el ticket)
4. Intenta resolverlo SIN mirar la pista
5. Si te atascas >15 min, mira la pista
6. Resuélvelo
7. Documenta en `fase1-linux/tickets/ticket-XXX.md`:

```markdown
# TICKET-XXX · Nombre del ticket

## Tiempo: XX minutos (con/sin pista)

## Síntoma
Qué veías al empezar

## Diagnóstico
Qué comandos usaste para investigar y qué encontraste

## Solución
Los comandos exactos que lo arreglaron, en orden

## Verificación
Cómo confirmaste que funciona (reinicio, test, etc.)

## Lección
Qué me llevo: una frase que explique el "por qué"
```

### Commit del ticket

```bash
git add fase1-linux/tickets/ticket-001.md
git commit -m "ticket(s2): T-001 carpeta compartida - 18min sin pista"
git push
```

El tiempo en el mensaje de commit es un flex futuro: cuando un
recruiter vea tu historial, 50 tickets resueltos con tiempos
decrecientes es una señal brutal.

---

## Día Python (X, S)

### Antes de empezar (~2 min)

```bash
cd ~/sre-lab
git pull
```

### Si estás en Exercism (~45 min)

1. Abre exercism.org, elige un ejercicio
2. Resuélvelo en local (en `python/ejercicios/`)
3. Cuando funcione, súbelo a Exercism Y a tu repo

```bash
git add python/ejercicios/nombre-ejercicio.py
git commit -m "py(exercism): two-fer - listas y format strings"
git push
```

### Si estás en un proyecto (P1, P2, P3) (~45-60 min)

1. Antes de escribir código, define qué vas a hacer HOY
   (una función, un módulo, un test... algo concreto y pequeño)
2. Escríbelo
3. Pruébalo
4. Commit

```bash
git add python/backup-tool/backup.py
git commit -m "py(backup): funcion de rotacion con pathlib"
git push
```

### Estructura de un proyecto Python

```
python/backup-tool/
├── README.md          ← qué hace, cómo se usa, qué aprendí
├── backup.py          ← el código
├── requirements.txt   ← dependencias (si las hay)
└── test_backup.py     ← tests (opcional pero muy bien visto)
```

El README del proyecto sigue esta plantilla:

```markdown
# backup-tool

Script de backup para LXC containers de mi homelab.

## Qué hace
- Conecta a Proxmox via SSH
- Comprime los backups con tar
- Rota ficheros antiguos (>7 días)
- Notifica por Telegram

## Cómo se usa
python3 backup.py --containers 103,104,107

## Qué he aprendido
- subprocess vs os.system (y por qué subprocess)
- Manejo de errores con try/except específico
- Logging vs print (y por qué logging)
```

---

## Día de la mosca (domingos alternos, ~1h)

Abre tu lista de "cosas que me tientan" y elige UNA.
Puedes leer, ver un vídeo, trastear.
NO hace falta commit ni documentar — es exploración libre.

Si descubres algo que quieres recordar, un apunte rápido en
`docs/mosca.md` y commit.

---

## Chuletas — cuándo crearlas y dónde

Cuando un tema tenga comandos que sabes que vas a olvidar,
crea una chuleta en `fase1-linux/cheatsheets/`:

```
fase1-linux/cheatsheets/
├── permisos.md
├── lvm.md
├── selinux.md
├── systemd.md
├── firewalld.md
└── nfs.md
```

Una chuleta NO es una copia del libro. Es tu referencia rápida
personal: los comandos que TÚ necesitas con TUS notas.

Ejemplo de `selinux.md`:

```markdown
# SELinux — chuleta

## Ver estado
getenforce                      # Enforcing/Permissive/Disabled
sestatus                        # detalle completo

## Ver contexto de un fichero
ls -Z /ruta

## Cambiar contexto (temporal, se pierde con relabel)
chcon -t httpd_sys_content_t /ruta

## Cambiar contexto (permanente)
semanage fcontext -a -t httpd_sys_content_t "/ruta(/.*)?"
restorecon -Rv /ruta

## Booleans
getsebool -a | grep httpd       # listar
setsebool -P httpd_can_network_connect on   # -P = persistente

## Diagnosticar
ausearch -m avc -ts recent
sealert -a /var/log/audit/audit.log
```

Commit:

```bash
git add fase1-linux/cheatsheets/selinux.md
git commit -m "cheat: selinux - contextos, booleans, diagnostico"
git push
```

---

## Referencia rápida de commits

### Prefijos

| Prefijo | Cuándo | Ejemplo |
|---------|--------|---------|
| `lab(sX)` | Notas de un capítulo | `lab(s1): cap3 - gestion de ficheros` |
| `ticket(sX)` | Un ticket resuelto | `ticket(s2): T-001 permisos - 22min` |
| `py(nombre)` | Código Python | `py(backup): notificacion telegram` |
| `py(exercism)` | Ejercicio de Exercism | `py(exercism): resistor-color` |
| `cheat` | Chuleta nueva o actualizada | `cheat: lvm - crear, extender, reducir` |
| `docs` | Documentación general | `docs: decisiones fase1` |
| `fix` | Corrección de algo anterior | `fix: typo en chuleta de permisos` |

### Comandos git del día a día

```bash
git status              # qué hay pendiente
git add archivo.md      # meter al staging
git add .               # meter TODO lo pendiente
git commit -m "msg"     # sacar la foto
git push                # subir a GitHub
git log --oneline       # ver tu historial
git diff                # ver qué cambiaste antes de add
```

---

## Checklist semanal (viernes o domingo)

- [ ] ¿Hay al menos 4 commits esta semana?
- [ ] ¿Las notas de los capítulos están subidas?
- [ ] ¿Los tickets resueltos están documentados?
- [ ] ¿El código Python de la semana está subido?
- [ ] ¿Alguna chuleta nueva que crear?

Si la respuesta a todo es sí, la semana está cerrada.
