# Guía de Setup — DataCore Workspace Centralizado

## Requisitos previos
- VS Code con extensión Claude Code instalada
- Obsidian instalado (https://obsidian.md — gratis)
- Git configurado
- Node.js instalado
- Tus 5 repos clonados en algún lugar de tu máquina

---

## Paso 1: Crear la carpeta raíz

Elegí dónde va a vivir todo. Recomiendo tu home o Documents:

```bash
# Opción A: en home
mkdir ~/datacore

# Opción B: en Documents
mkdir ~/Documents/datacore
```

---

## Paso 2: Extraer el workspace descargado

```bash
# Ir a donde descargaste el .tar.gz
cd ~/Downloads

# Extraer (esto crea datacore/ con toda la estructura)
tar -xzf datacore-workspace.tar.gz

# Copiar el contenido a tu carpeta elegida
cp -r datacore/* ~/datacore/
cp -r datacore/.claude ~/datacore/

# Verificar que .claude se copió (es carpeta oculta)
ls -la ~/datacore/.claude/
# Deberías ver: agents/ y skills/
```

---

## Paso 3: Mover tus repos existentes

La carpeta `projects/` tiene los CLAUDE.md de cada proyecto. Ahora necesitás
meter tus repos reales ahí. Tenés dos opciones:

### Opción A: Mover los repos (más limpio)
```bash
# Ajustá las rutas a donde tengas tus repos actualmente
mv ~/ruta/landing-datacore/* ~/datacore/projects/landing/
mv ~/ruta/landing-datacore/.git ~/datacore/projects/landing/

mv ~/ruta/marketing-studio/* ~/datacore/projects/studio/
mv ~/ruta/marketing-studio/.git ~/datacore/projects/studio/

mv ~/ruta/DataCore_Workspace/* ~/datacore/projects/workspace/
mv ~/ruta/DataCore_Workspace/.git ~/datacore/projects/workspace/

mv ~/ruta/sistema_gestion/* ~/datacore/projects/pos/
mv ~/ruta/sistema_gestion/.git ~/datacore/projects/pos/

mv ~/ruta/PortfolioMathias/WebMathias/* ~/datacore/projects/portfolio/
mv ~/ruta/PortfolioMathias/.git ~/datacore/projects/portfolio/
```

**Importante**: El CLAUDE.md que ya existe en cada `projects/{nombre}/` NO se 
sobreescribe porque tus repos no tienen ese archivo. Si alguno sí tiene un 
CLAUDE.md, renombrá el del repo a `CLAUDE-original.md` y mantené el nuevo.

### Opción B: Symlinks (si no querés mover repos)
```bash
# Borrar las carpetas placeholder
rm -rf ~/datacore/projects/landing
rm -rf ~/datacore/projects/studio
rm -rf ~/datacore/projects/workspace
rm -rf ~/datacore/projects/pos
rm -rf ~/datacore/projects/portfolio

# Crear symlinks
ln -s ~/ruta/landing-datacore ~/datacore/projects/landing
ln -s ~/ruta/marketing-studio ~/datacore/projects/studio
ln -s ~/ruta/DataCore_Workspace ~/datacore/projects/workspace
ln -s ~/ruta/sistema_gestion ~/datacore/projects/pos
ln -s ~/ruta/PortfolioMathias/WebMathias ~/datacore/projects/portfolio

# Después copiar el CLAUDE.md de cada proyecto al repo real
cp ~/Downloads/datacore/projects/landing/CLAUDE.md ~/ruta/landing-datacore/CLAUDE.md
cp ~/Downloads/datacore/projects/studio/CLAUDE.md ~/ruta/marketing-studio/CLAUDE.md
cp ~/Downloads/datacore/projects/workspace/CLAUDE.md ~/ruta/DataCore_Workspace/CLAUDE.md
cp ~/Downloads/datacore/projects/pos/CLAUDE.md ~/ruta/sistema_gestion/CLAUDE.md
cp ~/Downloads/datacore/projects/portfolio/CLAUDE.md ~/ruta/PortfolioMathias/CLAUDE.md
```

**Recomendación**: Opción A es mejor para el flujo centralizado. Con symlinks 
hay edge cases donde Claude Code no sigue bien los links.

---

## Paso 4: Verificar estructura

```bash
# Desde la raíz
cd ~/datacore
find . -name "CLAUDE.md" -o -name "STATE.md" | sort
```

Deberías ver:
```
./.claude/agents/analyst.md
./.claude/agents/auditor.md
./.claude/agents/developer.md
./.claude/agents/memory-keeper.md
./.claude/agents/orchestrator.md
./.claude/agents/tester.md
./.claude/skills/change-classifier.md
./.claude/skills/compact-strategy.md
./.claude/skills/token-efficient.md
./CLAUDE.md
./projects/landing/CLAUDE.md
./projects/studio/CLAUDE.md
./projects/workspace/CLAUDE.md
./projects/pos/CLAUDE.md
./projects/portfolio/CLAUDE.md
./vault/proyectos/landing/STATE.md
./vault/proyectos/studio/STATE.md
./vault/proyectos/workspace/STATE.md
./vault/proyectos/pos/STATE.md
./vault/proyectos/portfolio/STATE.md
```

---

## Paso 5: Configurar Obsidian

### 5.1 Abrir vault
1. Abrir Obsidian
2. Click en "Open folder as vault" (o "Abrir carpeta como bóveda")
3. Seleccionar: `~/datacore/vault/`
4. Obsidian va a indexar los archivos

### 5.2 Configuración recomendada
1. **Settings → Files & Links**:
   - Default location for new notes: `In the folder specified below`
   - Folder: `diario` (así las notas rápidas van al diario)
   - New link format: `Relative path to file`

2. **Settings → Templates** (core plugin):
   - Template folder location: `templates`
   - Esto te permite insertar templates con `Ctrl+T`

3. **Settings → Daily Notes** (core plugin, activar si no está):
   - Date format: `YYYY-MM-DD`
   - New file location: `diario`
   - Template file: `templates/diario-template`

### 5.3 Plugins recomendados (opcionales)
- **Dataview**: para queries tipo "todos los pendientes de todos los proyectos"
- **Calendar**: para navegar el diario por fecha
- **Templater**: para templates más dinámicos (reemplaza {{date}} automáticamente)

### 5.4 Verificar que funciona
1. En Obsidian, navegá a `proyectos/pos/STATE.md`
2. Deberías ver el estado del POS con sus pendientes
3. Probá crear una daily note (Ctrl+T o Command+T)
4. Debería crearse en `diario/` con el template

---

## Paso 6: Configurar VS Code

### 6.1 Abrir el workspace
```bash
code ~/datacore
```

### 6.2 Workspace settings recomendados
Crear `~/datacore/.vscode/settings.json`:
```json
{
  "files.exclude": {
    "**/.git": true,
    "**/node_modules": true,
    "**/__pycache__": true,
    "**/.venv": true
  },
  "search.exclude": {
    "**/node_modules": true,
    "**/dist": true,
    "**/.next": true
  },
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true
}
```

### 6.3 Extensiones útiles
- Claude Code (ya lo tenés)
- Markdown Preview Enhanced (para ver STATE.md bonito)
- GitLens (para ver git de múltiples repos)

---

## Paso 7: Primer arranque con Claude Code

### 7.1 Abrir terminal en VS Code
```bash
# Asegurate de estar en la RAÍZ del workspace
cd ~/datacore
```

### 7.2 Lanzar Claude Code
```bash
claude
```

### 7.3 Primer mensaje (copiar y pegar)
```
Lee CLAUDE.md y vault/proyectos/. Confirmá que ves los 5 proyectos 
y sus estados. Listá cada uno en 1 línea.
```

Claude debería responder con algo como:
```
- landing: producción, pendiente conectar dominio y demo_requests
- studio: desarrollo, pendiente verificar migración a composition
- workspace: operativo, en migración al centralizado
- pos: v1.2.2 producción, próximo v2.0.0 facturación electrónica
- portfolio: producción, pendiente contenido real y proyectos DataCore
```

### 7.4 Empezar a trabajar
```
Necesito trabajar en {proyecto}. Lee vault/proyectos/{proyecto}/STATE.md 
y decime los pendientes ordenados por prioridad.
```

---

## Paso 8: Flujo diario (rutina)

### Al empezar el día
1. Abrir Obsidian → revisar último diario para contexto rápido (visual)
2. Abrir VS Code → `cd ~/datacore` → `claude`
3. Pegar prompt de arranque de `vault/templates/session-prompts.md`

### Durante el trabajo
- Un proyecto a la vez
- Si necesitás cruzar contexto: usar prompt de cruce
- Si Claude sugiere compactar: usar prompt de compactación

### Al terminar (ANTES de que se agoten tokens)
1. Pegar prompt de cierre de sesión
2. Esperar que el memory-keeper actualice el vault
3. Verificar en Obsidian que STATE.md se actualizó
4. Si no alcanzaron los tokens para el cierre: abrir Obsidian y 
   actualizar STATE.md manualmente con lo que recuerdes

### Si se cortó por tokens sin cerrar
1. Nueva sesión de Claude Code
2. Pegar: "La sesión anterior se cortó. Lee vault/proyectos/{proyecto}/STATE.md 
   y continuá con el primer pendiente."

---

## Paso 9: Git para el workspace (opcional pero recomendado)

El workspace en sí puede tener su propio repo para versionar la memoria:

```bash
cd ~/datacore

# Inicializar repo del workspace
git init

# .gitignore del workspace raíz
cat > .gitignore << 'EOF'
# Repos de proyectos tienen su propio git
projects/*/node_modules/
projects/*/.next/
projects/*/dist/
projects/*/.expo/

# Archivos de sistema
.DS_Store
*.swp

# No versionar el .obsidian config (es local)
vault/.obsidian/
EOF

# Primer commit
git add .
git commit -m "feat: workspace centralizado DataCore con agentes y vault"
```

Esto te permite versionar:
- Los agentes y skills (`.claude/`)
- El vault completo (estados, decisiones, diario)
- Los CLAUDE.md de cada proyecto
- Sin versionar el código de los proyectos (cada uno tiene su repo)

---

## Troubleshooting

### Claude Code no lee el CLAUDE.md
- Verificá que estás lanzando `claude` desde `~/datacore/`, no desde un subdirectorio
- Claude Code lee el CLAUDE.md de la carpeta donde se lanza

### Obsidian no muestra los archivos
- Verificá que el vault apunta a `~/datacore/vault/`, no a `~/datacore/`
- Si apuntás a la raíz, Obsidian indexa todo incluyendo node_modules

### Los repos no hacen git push desde el workspace
- Cada repo dentro de `projects/` mantiene su propio `.git`
- Hacé `cd projects/landing && git push` normalmente
- El workspace raíz tiene su propio `.git` separado

### Claude improvisa en vez de leer STATE.md
- Es probable que no haya leído el CLAUDE.md raíz
- Forzá: "Antes de hacer cualquier cosa, lee CLAUDE.md y vault/proyectos/{proyecto}/STATE.md"
