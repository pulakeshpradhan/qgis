# Standalone PyQGIS Scripts

Sometimes you want to process data without opening the QGIS GUI.

## 1. The Script Skeleton

To run QGIS code in a standard Python environment, you must initialize the `QgsApplication`.

```python
import sys
from qgis.core import QgsApplication, QgsProject, QgsVectorLayer

# 1. Provide the path to the QGIS installation
# On Windows: C:/OSGeo4W/apps/qgis
QgsApplication.setPrefixPath("/path/to/qgis/installation", True)

# 2. Initialize the application (False = no GUI)
qgs = QgsApplication([], False)
qgs.initQgis()

# 3. Your Processing Logic
layer = QgsVectorLayer("data.shp", "Layer", "ogr")
print(f"Is layer valid? {layer.isValid()}")

# 4. Clean up and exit
qgs.exitQgis()
```

## 2. Automating Data Migration

Example: Converting 100 Shapefiles to GeoPackage via a script.

```python
import os
import processing

input_dir = "data/shapefiles"
output_gpkg = "consolidated.gpkg"

for file in os.listdir(input_dir):
    if file.endswith(".shp"):
        path = os.path.join(input_dir, file)
        processing.run("native:package", {
            'LAYERS': [path],
            'OUTPUT': output_gpkg,
            'OVERWRITE': False
        })
```
