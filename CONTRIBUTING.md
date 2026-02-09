# Contributing / Contribuciones

## English

### Scope

This document defines minimum technical requirements for contributions to DisableWinTracking.

### Change Conventions

- Keep changes focused and atomic.
- Use explicit commit messages.
- Do not mix unrelated refactors with behavioral changes.
- If behavior changes, update docs in the same change set.

### Required Local Validation

Run at least:

```powershell
python -m py_compile dwt.py dwt_util.py dwt_about.py dwt_i18n.py
python -m unittest discover -s tests -p "test_*.py" -v
powershell -NoProfile -ExecutionPolicy Bypass -File .\scripts\windows_smoke.ps1 -PythonVersion 3.12
powershell -NoProfile -ExecutionPolicy Bypass -File .\scripts\windows_smoke.ps1 -PythonVersion 3.14
```

Validate CLI behavior when touching silent flow:

```powershell
python dwt.py -silent
python dwt.py -silent-revert
```

### Build Validation (if packaging/build changed)

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File .\build.ps1
```

Expected outputs:

- `dist/DisableWinTracking.exe`
- `public/dwt-<version>-<pyTag>-win_amd64.zip`

### Documentation Policy

Any functional change affecting behavior, setup, validation, build, or troubleshooting must update docs in the same PR, at least:

- `README.md`
- `.github/ISSUE_TEMPLATE.md` (if issue diagnostics changed)
- `CONTRIBUTING.md` (if contributor workflow changed)

### PR Quality Checklist

- [ ] No break in declared compatibility (Python 3.12/3.14).
- [ ] `-silent` and `-silent-revert` behavior validated if touched.
- [ ] Tests and smoke checks executed and reported.
- [ ] Docs and code are consistent.

## Espanol

### Alcance

Este documento define requisitos tecnicos minimos para contribuciones a DisableWinTracking.

### Convenciones de cambios

- Mantener cambios acotados y atomicos.
- Usar mensajes de commit explicitos.
- No mezclar refactors no relacionados con cambios de comportamiento.
- Si cambia el comportamiento, actualizar documentacion en el mismo set de cambios.

### Validacion local requerida

Ejecutar como minimo:

```powershell
python -m py_compile dwt.py dwt_util.py dwt_about.py dwt_i18n.py
python -m unittest discover -s tests -p "test_*.py" -v
powershell -NoProfile -ExecutionPolicy Bypass -File .\scripts\windows_smoke.ps1 -PythonVersion 3.12
powershell -NoProfile -ExecutionPolicy Bypass -File .\scripts\windows_smoke.ps1 -PythonVersion 3.14
```

Validar CLI cuando se toque flujo silencioso:

```powershell
python dwt.py -silent
python dwt.py -silent-revert
```

### Validacion de build (si cambia packaging/build)

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File .\build.ps1
```

Salidas esperadas:

- `dist/DisableWinTracking.exe`
- `public/dwt-<version>-<pyTag>-win_amd64.zip`

### Politica de documentacion

Todo cambio funcional que impacte comportamiento, setup, validacion, build o troubleshooting debe actualizar docs en el mismo PR, al menos:

- `README.md`
- `.github/ISSUE_TEMPLATE.md` (si cambian datos para reproducir issues)
- `CONTRIBUTING.md` (si cambia el flujo de contribucion)

### Checklist de calidad para PR

- [ ] No romper compatibilidad declarada (Python 3.12/3.14).
- [ ] Validar comportamiento de `-silent` y `-silent-revert` cuando aplique.
- [ ] Ejecutar tests y smoke checks y reportar resultados.
- [ ] Coherencia entre codigo y documentacion.
