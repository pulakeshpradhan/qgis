# Getting Started with PyQGIS

To begin automating QGIS, you need a working environment where Python and QGIS are correctly linked.

## The QGIS Python Console

The easiest way to start is the built-in console.

1. Open QGIS.
2. Press `Ctrl + Alt + P`.

## Running your first script in QGIS

```python
from qgis.utils import iface

# Get current project title
print(f"Project Title: {iface.mainWindow().windowTitle()}")

# Add a message to the UI
iface.messageBar().pushMessage("Success", "Welcome to PyQGIS Automation", level=0)
```

## Setting up a Python Environment for QGIS

If you want to use VS Code or PyCharm, you must use the Python interpreter provided by QGIS (usually inside the `apps\Python39` or similar folder in your QGIS installation).

### Critical Environment Variables

- `PYTHONPATH`: Must include `qgis\python`.
- `PATH`: Must include `qgis\bin`.
- `QGIS_PREFIX_PATH`: Path to your QGIS installation.
