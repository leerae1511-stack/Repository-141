# Tool Pocket Generator V141 — Release Notes

## Provenance
Built directly from `Tool_Pocket_Generator_V140_FINAL.zip`. V140 is the sole source build.

## Problem addressed
In the prior build, Curve points were used as quadratic control handles. Those handles generally do not lie on the resulting black outline, so the visible dots could appear detached from the tool shape. The edit canvas and sampled geometry also used separate path-generation routines.

## V141 changes
- Curve points are now treated as points ON the outline, rather than off-curve quadratic handles.
- A segment is smoothed with Catmull–Rom interpolation when either endpoint is marked Curve.
- Straight-to-Straight segments remain straight.
- The editable canvas now draws from the same `sampled()` function used by the final sampled geometry, so the drawn line passes through the listed points and shares one curve calculation.
- The existing master-envelope normalization from V140 remains in place for this diagnostic build.

## Process / order
Import JSON → inspect/confirm the physical grid and detected outline → edit point positions and Straight/Curve modes → confirm profile editing → Close Profile → Geometry Check → export JSON/STL.

## What was not changed
- Master-dimension normalization logic introduced in V140.
- Workspace sizing and import/export data structure.
- Finger Relief feature controls and depth settings.
- Geometry Check validation criteria and STL triangulation/export pipeline.
- Existing point list, IDs, and undo behaviour.

## Verification performed
- V140 ZIP used directly as source.
- Replaced only the shared `sampled()` curve routine and the edit-canvas path renderer.
- Confirmed the resulting source uses the same sampler for edit drawing and sampled geometry.
- ZIP integrity checked and exactly one README included.

## Retest required
This is a geometry-behaviour change and needs visual verification in Safari/iPad:
1. Import the same JSON.
2. Confirm the master dimensions show 132.59 × 35.63 mm.
3. Inspect the dots: the black line should pass through every point.
4. Check both Finger Relief arcs and the full silhouette against the intended tool.
5. Compare the edit view with the closed profile and Geometry Check.
6. Export STL and measure it in Bambu Studio.

## Important
The new interpolation can change the contour compared with V140 because the Curve dots are now on-curve points. Do not treat a passed geometry check or correct bounding dimensions as proof of a correct tool silhouette. Visually compare against the physical tool/photo before using the STL.
