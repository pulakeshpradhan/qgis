# Vector Operations

Manipulating vector data is the heart of GIS automation.

## 1. Accessing Features and Attributes

You can iterate through all features of a layer to perform calculations.

```python
layer = iface.activeLayer() # Get selected vector layer

# Get layer fields
fields = layer.fields()
for field in fields:
    print(f"Field: {field.name()}, Type: {field.typeName()}")

# Iterate through features
for feature in layer.getFeatures():
    # Access attribute by name
    name = feature['NAME']
    # Access geometry
    geom = feature.geometry()
    print(f"Feature: {name}, Area: {geom.area()}")
```

## 2. Spatial Queries

Find which features in 'Layer A' intersect with 'Layer B'.

```python
layer_a = QgsProject.instance().mapLayersByName('Airports')[0]
layer_b = QgsProject.instance().mapLayersByName('Regions')[0]

for feature_a in layer_a.getFeatures():
    for feature_b in layer_b.getFeatures():
        if feature_a.geometry().intersects(feature_b.geometry()):
            print(f"Airport {feature_a['name']} is in {feature_b['region_name']}")
```

## 3. Modifying Geometry

Smoothing, buffering, or simplifying geometries via code.

```python
layer.startEditing()
for feature in layer.getFeatures():
    # Create a 500m buffer
    buffered_geom = feature.geometry().buffer(500, 5)
    layer.changeGeometry(feature.id(), buffered_geom)
layer.commitChanges()
```
