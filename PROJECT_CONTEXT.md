# Py2Exe Builder — Project Context

## Purpose

Py2Exe Builder is a Windows-oriented graphical front end for PyInstaller. It helps users configure common executable-build options, queue builds, install or upgrade PyInstaller for a selected interpreter, and inspect build logs without manually composing every command.

Despite the repository name, the tool uses PyInstaller rather than the separate `py2exe` package.

## Current reality

- The entire implementation is in `Py2EXE - V4.py`.
- It includes settings persistence, interpreter selection, UPX detection, temporary version-info and manifest generation, build command assembly, queued/background execution, logging, tooltips, and a themed Tkinter UI.
- It is explicitly Windows-focused; Linux syntax compilation cannot validate Windows manifests, UAC metadata, executable creation, icon/resources, or AppData behavior.
- No README, automated test suite, requirements file, license, release artifacts, or recorded clean Windows acceptance existed before this documentation update.

## Trust and build boundary

- Building a Python project executes PyInstaller hooks and imports/analysis against the selected source/dependencies. Treat untrusted projects, spec files, hooks, resources, and interpreters as code execution.
- Interpreter paths, extra arguments, hidden imports, resource mappings, output paths, and metadata must be passed as argument arrays without shell interpolation wherever possible.
- “Install/upgrade PyInstaller” changes the selected Python environment and requires an explicit confirmation showing the exact interpreter.
- UAC/admin manifests raise the privilege level of the built application; never enable them by default or imply they make software safer.
- UPX and one-file packaging can trigger antivirus heuristics. Signing, reputation, SBOM/dependency records, and reproducible release steps are separate concerns.
- Generated executables can embed source, secrets, config, data, and licenses. The GUI cannot certify that a project is safe to distribute.

## Source and backup boundaries

- The owner-designated working checkout is active source. This private GitHub repository is a secondary source/history backup.
- Selected projects, build/dist folders, spec files, icons/resources, interpreters, logs, temporary manifests/version files, settings, certificates, and signed artifacts do not belong in this source repository.
- Never store code-signing keys or passwords in the app, settings file, build command, or GitHub.

## Verification plan

Source syntax can be checked anywhere:

```bash
python3 -m py_compile 'Py2EXE - V4.py'
```

Release evidence must come from a clean supported Windows VM with a disposable fixture matrix: console/windowed, one-file/one-folder, spaces/unicode in paths, data files, hidden import, icon, version metadata, DPI manifest, optional UAC, cancel/failure, queue ordering, and output collision. Scan resulting binaries and verify they run without the source checkout.

## Maturity and product path

- **Current phase:** substantial single-file prototype, Windows acceptance unknown.
- **Website showcase:** after a clean Windows build/demo with synthetic fixtures.
- **Sellable-product potential:** moderate as a polished Windows packaging assistant, but competition is strong and signing/support/security expectations are high.
- **Public-source candidate:** feasible after modularization, argument-safety tests, a deliberate license, Windows CI/VM verification, dependency documentation, and signed release guidance.
- **SaaS fit:** poor; packaging should remain local because source, dependencies, secrets, and signing material are sensitive.

## Resume point

Refactor command construction and temporary-file handling into testable modules, add unit tests that assert exact argument arrays without invoking PyInstaller, then run the full disposable Windows fixture matrix before distributing an executable.
