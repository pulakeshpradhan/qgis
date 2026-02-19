# Raster Operations

Automating raster processing is essential for remote sensing and terrain analysis.

## 1. Raster Information

```python
raster = iface.activeLayer()

print(f"Raster Dimensions: {raster.width()} x {raster.height()}")
print(f"Data Provider: {raster.dataProvider().name()}")
```

## 2. Band Calculations (The Fast Way)

Instead of iterating pixels, use the `QgsRasterCalculator`.

```python
from qgis.analysis import QgsRasterCalculator, QgsRasterCalculatorEntry

# Setup Band 1
entry1 = QgsRasterCalculatorEntry()
entry1.ref = 'band1@1'
entry1.raster = raster
entry1.bandNumber = 1

entries = [entry1]

# Apply expression (e.g., Simple threshold)
# Thresholding pixel values above 100
expression = 'band1@1 > 100'

calc = QgsRasterCalculator(
    expression, 
    '/path/to/output.tif', 
    'GTiff', 
    raster.extent(), 
    raster.width(), 
    raster.height(), 
    entries
)
calc.processCalculation()
```

## 3. Zonal Statistics

Calculating averages of raster values within vector boundaries.

```python
from qgis.analysis import QgsZonalStatistics

zone_layer = QgsProject.instance().mapLayersByName('Districts')[0]
raster_layer = QgsProject.instance().mapLayersByName('LST')[0]

zonal_stats = QgsZonalStatistics(zone_layer, raster_layer, 'prefix_', 1)
zonal_stats.calculateStatistics(None)
```
