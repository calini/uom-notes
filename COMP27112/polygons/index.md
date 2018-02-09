## Polygons

## What is a poligon
* Ordered set of verteces (V1, ..., Vn)

OpenGL polygons are convex
* Convex = all interior angles < 180°

## Tesselation
* GLU Provides functions to tesselate polygons
    * Before: Concave polygon
    * After: Set of **convex** polygons 

## Polygon attributes

* The **surface normal** is a vector perpendicular to the plane of the polygon
* (We use this to distinguish front from back)
* Also to describe it's **orientation** in 3d space
* Orientation is essential in
    * Lighting calculations
    * Collisions
    * Culling

## The cross product
* Is a **vector** define as follows:
![](cross-product.png)


## Finding the surface normal

1. Choose a pair of sequential edges E1 and E2, compute their vectors
2. Invert the direction of the first so they now emanate from their shared vertex
3. Their cross product is the surface normal
`N = E2 x -E1`
4. We then almost always normalize N (make its length 1)

## Representing things with polygons

* **Polygon soup** = Huge list of individual polygons, colored individually, drawn in order

* Huge waste of storage space... most models contain “surfaces” not individual polygons, so we could share vertices rather than replicate them per polygon
* Complete loss of semantics: 
    * Does a polygon belong to a cow... or a table...?
* Leads to ‘brute force’ rendering, and makes interaction with the model complex

## Polygon meshes
* Use linked groups of polygons, or meshes, to represent surfaces
* Retains semantics of “surface” but reduces storage by sharing vertices and edges
* Helps with structuring the model so we can manipulate it more easily

![](cow.png)
