# DisableWinTracking (Fork)

Living fork of the original archived project: <https://github.com/10se1ucgo/DisableWinTracking>

Current upstream repository: <https://github.com/Potencial/DisableWinTracking>
Current app version: `v3.3.0`

![screenshot](web/dwt-screenshot.png)

## English

### Download

- Releases: <https://github.com/Potencial/DisableWinTracking/releases>

### Platform and Python Support

- Target OS: Windows 10 (some behavior may also work on Windows 11).
- Supported Python versions for source/runtime validation:
- Python `3.12`
- Python `3.14`

### Dependencies

Runtime dependency model:

- `requirements.lock.py312.txt`: reproducible runtime set for Python 3.12
- `requirements.lock.py314.txt`: reproducible runtime set for Python 3.14
- `requirements.txt`: editable runtime base (ranges)
- `requirements.build.txt`: build tooling (`PyInstaller` and hooks)

Install runtime dependencies (recommended):

```powershell
py -3.12 -m pip install -r requirements.lock.py312.txt
py -3.14 -m pip install -r requirements.lock.py314.txt
```

### Running the App

Run GUI (as Administrator):

```powershell
py -3.14 dwt.py
```

Apply the balanced silent profile:

```powershell
py -3.14 dwt.py -silent
```

Revert the silent profile:

```powershell
py -3.14 dwt.py -silent-revert
```

### GUI Workflow (v3.3.0)

The GUI now uses a categorized layout with presets:

- Tabs:
- `Core` (legacy controls)
- `Privacy+` (new policy-based controls)
- `Network` (HOSTS/IP blocking)
- Presets:
- `Balanced` (recommended)
- `Custom`
- Before execution, the app shows a confirmation summary with risk labels (`Low` / `Medium`).

### Language Selection (UI)

- Available languages: `English`, `Espanol`.
- Open `File -> Settings` and choose the language in `Language`.
- Language preference is persisted.
- Restart is recommended after changing language to refresh every label.

### Features

Core features:

- Services (`Disable` / `Delete`) + startup policy
- Clear DiagTrack log
- Telemetry policy
- HOSTS domain blocking (+ extra list)
- Firewall IP blocking
- WifiSense policy
- OneDrive privacy/uninstall flow
- Xbox DVR policy

Privacy+ features (new):

- Disable Advertising ID
- Disable Activity History feed/publish/upload
- Disable cross-device clipboard
- Disable input personalization
- Disable tailored experiences with diagnostic data
- Disable feedback notifications

### Silent Mode Scope

`-silent` now applies `Core + Privacy+ (Balanced)` by default:

- Includes: services policy, telemetry, WifiSense, OneDrive, Xbox DVR, and all Privacy+ controls
- Includes setup actions: clear DiagTrack + stop tracking services
- Excludes by design: HOSTS domain blocking and firewall IP blocking

`-silent-revert` reverts the same policy scope (excluding non-reversible DiagTrack clear action).

### Validation and CI

Local smoke validation script:

```powershell
./scripts/windows_smoke.ps1 -PythonVersion 3.12
./scripts/windows_smoke.ps1 -PythonVersion 3.14
```

From WSL:

```bash
powershell.exe -NoProfile -ExecutionPolicy Bypass -Command "Set-Location 'D:\DisableWinTracking'; .\scripts\windows_smoke.ps1 -PythonVersion 3.14"
```

Unit tests:

```powershell
python -m unittest discover -s tests -p "test_*.py" -v
```

CI workflow:

- `.github/workflows/windows-smoke.yml`
- Runs smoke validation on Python `3.12` and `3.14`.

### Build and Release Artifacts

Build command:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File .\build.ps1
```

Expected outputs:

- `dist/DisableWinTracking.exe`
- `public/dwt-<version>-<pyTag>-win_amd64.zip`

### Historical Notes

- This fork preserves the NCSI fix and avoids adding these HOSTS entries:
- `0.0.0.0 msftncsi.com`
- `0.0.0.0 www.msftncsi.com`

### Cyrillic Path Warning

The app may fail when executed from paths containing Cyrillic characters. Use a non-Cyrillic path (for example `C:\`).

## Espanol

### Descarga

- Releases: <https://github.com/Potencial/DisableWinTracking/releases>

### Plataforma y soporte de Python

- SO objetivo: Windows 10 (parte del comportamiento puede funcionar en Windows 11).
- Versiones soportadas para validacion de runtime:
- Python `3.12`
- Python `3.14`

### Dependencias

Modelo actual de dependencias:

- `requirements.lock.py312.txt`: entorno reproducible para Python 3.12
- `requirements.lock.py314.txt`: entorno reproducible para Python 3.14
- `requirements.txt`: base editable de runtime
- `requirements.build.txt`: tooling de build (`PyInstaller`)

Instalacion recomendada:

```powershell
py -3.12 -m pip install -r requirements.lock.py312.txt
py -3.14 -m pip install -r requirements.lock.py314.txt
```

### Ejecucion

Modo GUI (Administrador):

```powershell
py -3.14 dwt.py
```

Aplicar perfil silencioso balanceado:

```powershell
py -3.14 dwt.py -silent
```

Revertir perfil silencioso:

```powershell
py -3.14 dwt.py -silent-revert
```

### Flujo GUI (v3.3.0)

La GUI ahora se organiza por categorias y presets:

- Pestañas:
- `Core` (controles clasicos)
- `Privacidad+` (controles nuevos por politicas)
- `Red` (bloqueo HOSTS/IP)
- Presets:
- `Balanceado` (recomendado)
- `Personalizado`
- Antes de ejecutar se muestra un resumen de acciones con nivel de riesgo (`Bajo` / `Medio`).

### Seleccion de idioma

- Idiomas: `English`, `Espanol`.
- Ir a `Archivo -> Configuracion` y elegir idioma.
- La preferencia queda guardada.
- Se recomienda reiniciar para refrescar todas las etiquetas.

### Funcionalidades

Core:

- Servicios (`Disable` / `Delete`) + politica de inicio
- Limpieza de log DiagTrack
- Politica de telemetria
- Bloqueo de dominios HOSTS (+ lista extra)
- Bloqueo de IP por firewall
- Politica de WifiSense
- Flujo de privacidad/desinstalacion de OneDrive
- Politica de Xbox DVR

Privacidad+ (nuevo):

- Deshabilitar Advertising ID
- Deshabilitar Activity History (feed/publicacion/subida)
- Deshabilitar portapapeles entre dispositivos
- Deshabilitar personalizacion de entrada
- Deshabilitar experiencias personalizadas con datos de diagnostico
- Deshabilitar notificaciones de feedback

### Alcance de modo silencioso

`-silent` ahora aplica `Core + Privacidad+ (Balanceado)`:

- Incluye: politica de servicios, telemetria, WifiSense, OneDrive, Xbox DVR y todos los controles Privacidad+
- Incluye acciones de preparacion: limpiar DiagTrack y detener servicios de rastreo
- Excluye por diseno: bloqueo HOSTS y bloqueo IP por firewall

`-silent-revert` revierte ese mismo alcance (excepto limpieza de DiagTrack, que no es reversible automaticamente).

### Validacion y CI

Script smoke local:

```powershell
./scripts/windows_smoke.ps1 -PythonVersion 3.12
./scripts/windows_smoke.ps1 -PythonVersion 3.14
```

Desde WSL:

```bash
powershell.exe -NoProfile -ExecutionPolicy Bypass -Command "Set-Location 'D:\DisableWinTracking'; .\scripts\windows_smoke.ps1 -PythonVersion 3.14"
```

Tests unitarios:

```powershell
python -m unittest discover -s tests -p "test_*.py" -v
```

Workflow CI:

- `.github/workflows/windows-smoke.yml`

### Build y artefactos

Comando de build:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File .\build.ps1
```

Salidas esperadas:

- `dist/DisableWinTracking.exe`
- `public/dwt-<version>-<pyTag>-win_amd64.zip`

### Nota historica

Este fork conserva la correccion de NCSI y evita agregar en HOSTS:

- `0.0.0.0 msftncsi.com`
- `0.0.0.0 www.msftncsi.com`

### Advertencia de rutas con caracteres cirilicos

La app puede fallar si se ejecuta desde rutas con caracteres cirilicos. Usar una ruta sin cirilico (por ejemplo `C:\`).

## License

This project remains under GPLv3 (see `COPYING`).
