# Processing Toolbox Automation

QGIS has hundreds of built-in algorithms. You can run them all via Python using the `processing` module.

## 1. Finding Algorithms

To see all available tools:

```python
import processing
for alg in QgsApplication.processingRegistry().algorithms():
    print(alg.id(), "->", alg.displayName())
```

## 2. Running a Tool

Let's run a 'Fixed Distance Buffer'.

```python
import processing

input_layer = "rivers.shp"
output_layer = "buffered_rivers.shp"

params = {
    'INPUT': input_layer,
    'DISTANCE': 250,
    'SEGMENTS': 5,
    'END_CAP_STYLE': 0,
    'JOIN_STYLE': 0,
    'MITER_LIMIT': 2,
    'DISSOLVE': False,
    'OUTPUT': output_layer
}

result = processing.run("native:buffer", params)
# The result is a dictionary containing the path to the output
print(f"Output saved at: {result['OUTPUT']}")
```

## 3. Chaining Tools (Workflows)

You can use the output of one tool as the input for another.

```python
# Step 1: Buffer
buffer_res = processing.run("native:buffer", {'INPUT': 'points.shp', 'DISTANCE': 100, 'OUTPUT': 'memory:buff'})

# Step 2: Centroids on the buffer
centroid_res = processing.run("native:centroids", {'INPUT': buffer_res['OUTPUT'], 'OUTPUT': 'memory:cents'})

# Add the final result to the project
QgsProject.instance().addMapLayer(centroid_res['OUTPUT'])
```
