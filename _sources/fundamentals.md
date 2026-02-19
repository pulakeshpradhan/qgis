# PyQGIS Fundamentals

---

jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: myst
      format_version: 0.13
      jupytext_version: 1.14.4
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

In this chapter, we cover the core classes of the QGIS API.

## 1. The `QgsProject` Class

Every layer, print layout, and project-wide setting is managed here.

```{code-cell} python
from qgis.core import QgsProject

# Access the project instance
project = QgsProject.instance()

# Check total layer count
print(f"Total Layers: {project.count()}")
```

## 2. Layers: Vector and Raster

Loading layers programmatically is a core skill.

### Loading a Shapefile

```python
from qgis.core import QgsVectorLayer
path_to_shp = "data/rivers.shp"
layer = QgsVectorLayer(path_to_shp, "Rivers", "ogr")

if not layer.isValid():
    print("Layer failed to load!")
else:
    QgsProject.instance().addMapLayer(layer)
```

## 3. Map Canvas Integration

The `QgsMapCanvas` class allows you to control the view: zooming, panning, and rendering.

```python
canvas = iface.mapCanvas()
canvas.setCanvasColor(Qt.white)
canvas.refresh()
```
