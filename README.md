# Py2Exe Builder

Private source backup for a Windows-focused Tkinter GUI that assembles and runs PyInstaller build commands for Python applications.

## Capabilities

- one-file or one-folder builds;
- console or windowed mode;
- output name, icon, destination, resources, hidden imports, and extra paths;
- clean build, UPX, manifest/DPI, UAC, and Windows version metadata options;
- interpreter selection and PyInstaller install/upgrade support;
- queued builds with a live log; and
- user settings under the Windows application-data directory.

The implementation is currently one approximately 48 KB Python file: `Py2EXE - V4.py`.

Read [`PROJECT_CONTEXT.md`](PROJECT_CONTEXT.md) for command-injection, untrusted-project, signing, test, packaging, and product boundaries.

## Run on Windows

```powershell
py "Py2EXE - V4.py"
```

Use a disposable sample project for initial testing. Do not build untrusted source or pass unreviewed extra PyInstaller arguments.
