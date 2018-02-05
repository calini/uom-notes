<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=UA-113560131-1"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'UA-113560131-1');
</script>

# Transformations

## Table of Contents?
* Types of geometrical transformation
* Vector and matrix representations
* Homogenous coordinates
* Using transformations in OpenGL
* Some handy vector geometry


## 3D Cartesian coordonates
* **Rene Descartes** 1595-1650 was the inventor of the cartesian coordinates

* A **coordinate** represents a point in space, measured with respect to an origin and set of X,Y,Z axes

## Vectors
* Direction in space with respect of X, Y, Z axes
* Has characteristic length
* A vector of length 1 is known as a "unit vector"

### Two different representations
* Both coordinates and vectors can be represented by a triple of x, y, z values.
* In computer graphics we usually write these in column format. OpenGL uses **column** vectors. Some use rows (Kind of Wrong)

## Geometrical transformations
* Define geometry as sets of vertices
* Apply transformations to vertices to change them
* Examples: translation, scaling, rotation
* To transform a whole shape, we transform all its vertices

## Translation
![](transformation.png)
* Applies a 3D shift (tx, ty, tz) to all coordinates
```
x' = x + tx
y' = y + ty
z' = z + tz
```

# Scaling 
![](scaling.png)
* Applies a 3D scale (sx, sy, sz) to all coordinates
(with respect to the origin

```
x' = x . sx
y' = y . sy
z' = z . sz
```

# Rotations TODO AFTER

## Matrix trasformations recap
* The transformation T1 changes point P to P'

###### Play with ./transformations4 

## Composite transformations, 2D examples
* M1 moves object to origin
* M2 transforms
* M3 moves object back (undoing what M1 does)

M1 and M3 are matrix inverses to one another

```math
f(x) = sin(x) + x^2
```