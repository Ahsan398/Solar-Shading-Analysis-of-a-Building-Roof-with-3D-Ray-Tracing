# PVlib_with_shading


This project calculates annual solar shading on the roof of a selected building.

It uses 3D building data, tree data, solar position calculations, and ray tracing. The result shows whether roof sample points are shaded or sunlit at different times of the year.

## Workflow

Run the notebooks in this order:

1. `GeoData_my.ipynb`
2. `TreeData.ipynb`
3. `RayTracing.ipynb`

## Notebooks

### `GeoData_my.ipynb`

This notebook prepares the building data.

It:

- Loads LoD2 building data.
- Reads building geometry and building attributes.
- Handles coordinate reference systems.
- Selects the target building.
- Extracts the roof surfaces of the target building.
- Prepares nearby building data for the shading analysis.
- Creates maps and visualizations of the building data.

### `TreeData.ipynb`

This notebook prepares the tree data.

It:

- Loads the tree GeoPackage file.
- Reads tree locations, ground elevation, and tree height.
- Selects trees near the target building.
- Creates values for tree height and tree crown radius.
- Represents trees as cone-shaped objects for the 3D shading model.
- Creates maps and visualizations of the selected trees.

### `RayTracing.ipynb`

This notebook performs the solar shading calculation.

It:

- Loads the prepared building, roof, and tree data.
- Creates a 3D obstacle model from surrounding buildings and trees.
- Creates sample points on the target roof surfaces.
- Calculates the Sun position for each time step.
- Creates a ray from every roof sample point toward the Sun.
- Checks whether the ray hits a building or tree.
- Marks a roof point as `sunlit` when no obstacle is hit.
- Marks a roof point as `shaded` when the ray hits an obstacle.
- Calculates the shading percentage for each roof surface.
- Runs the analysis for all daylight time steps during the year.
- Displays the total number of ray-tracing checks and the runtime.
- Creates an example 3D ray-tracing plot for 19 June 2026 at 12:00 local time.

The target building is not included in the obstacle mesh. This avoids a ray intersecting its own roof or walls.

## Supporting File

### `LoD2BuildingFunctions.py`

This Python file contains lookup tables for:

- LoD2 building function codes.
- LoD2 roof shape codes.

It is used by `GeoData_my.ipynb`.

## Installation

Install the required Python libraries before running the notebooks:

```bash
pip install -r requirements.txt
```

## Input Data

The notebooks use local LoD2 building data and a local tree GeoPackage file.

Before running the notebooks, check that the file paths inside the notebooks match the folder structure on your computer.
```