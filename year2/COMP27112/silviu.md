# Graphics and Image Processing
 
## Graphics:
 
### Week 1.1:
- Images are formed from pixels; each pixel is about 0.2mm;
 
### Week 1.2: Introducing image synthesis
-  If the refresh rate is small, we have flickering effect on the monitor;
- Nowadays, Raster graphics display are used:
        - Raster graphics uses a 2D array of pixels (screens) or dots (printers)
        -  Images must be sampled
        - The more samples, the better fidelity, but always an approximation
- Basic graphics **system architecture**: Application program -> Graphics software -> Send pixels to GPU -> Store pixels into Framebuffer memory -> Pass them to DAC (digital analog converter) -> Show them on the screen
- **Fixed functionality pipeline:** (input: vertices)
        - Transformations and viewing
        - Lighting
        - Primitive assembly: primitives (bits of geometry) passed to the next layer
        - Rasterisation (aka scan conversion): (pixel candidates) fragments passed to the next layer
        - Fragment operations: blending, depth test, etc
        - Pixels for displaying
- By comparison, on the programmable pipeline, the first 2 operations and the fragment operations are programmable
- ***Triangles are used because they exist in only one plan and any shape can be approximated using triangles***
 
### Week 2.1: Transformations
- **Translation:** apply a 3D shift to all the coordinates: **x'=x+tx,** **y'=y+ty,** **z'=z+tz**
- **Scaling:** apply a 3D scale to all the coordinates: **x'=x*tx,** **y'=y*ty,** **z'=z*tz**
-  **2D Rotation:** rotate a point P about the origin, by angle **a**: if we note with R the distance from O to P and P', the distance is equal. Now, by expressing the x, y, x', y' by R and trigonometry, we get the relations.
- If we need to rotate about a specific point Q, we translate the system to have the origin in Q, rotate and translate back.
- In 3D rotations relative to an axis, a coordinate remains unchanged.
-  In order to use a consistent matrix for all linear transformations, we had to add an additional coordinate, w, to our usual coordinates. *This (x, y, z, w) form is called* **homogeneous**.
- **Rotation about an arbitrary 3D vector A:**
        - Transformation 1: shift vector A until it passes through the origin. Call the new vector A1
        - Transformation 2: rotate A1 until it is in the XY plane. Call the new vector A2
        - Transformation 3: rotate A2 about Z axis until is coincident with OX. Call the new vector A3
        - Transformation 4: rotate around OX axis
        - Undo the first 3 transformations
 
### Week 2.2: Polygons and pixels
- A polygon with all interior angles < 180 is convex.
- GLU provides functions to tessellate polygons (i.e. convert a concave polygon into a set of convex polygons).
- The **surface normal** is a vector perpendicular to the plane of the polygon and describes its orientation in 3D space.
- For two vectors, their **cross product** is a third vector, perpendicular to both of them.
- **Meshes:**
        -  Triangle strips: whenever we add a new point we get a new triangles: this save space, as for N triangles we need N+2 points.
        - Triangle fan: all triangles has a common point.
        - Quadratic strip: automatic tessellated to triangles.
- **Scan converting** means to find which pixels should we "turn on" to represent geometrical shapes. It is based on approximations.
- One of the ways to scan converting a triangle is to scan convert its lines and then fill the middle.
- Another way is the "sweep-line" algorithm: we start from a pair of edges and goes down, finding the start and end of each scanline and fill the pixels between them.
- **Hidden surface removal**: there are 2 approaches:
        - Solve it in world space: try to work out in geometrical space and then draw the result.
        - Solve it in display space: during scan conversion, determine for a pixel P if other 3D object closer to eye is also mapped to P. This is implemented using **The Z-Buffer**: for each pixel keep its color and depth. If it is represented again by other object and has smaller depth, override it. It can have problems because of the floating point precision.
 
### Week 3.1: Viewing and camera
- When viewing in 2D, the process is pretty simple; we need to specify to what we are looking and from where we want to see it.
- We need to transpose from the world coordinates to screen coordinates. We need to find a transformation to map the window of the world we want to see to the viewport. This is done by translating the left-bottom corner of the window to the origin, scale the window to have the same size as the viewport and then shift it to the viewport position.
- We also clip (trim) against the viewport to remove the parts of primitives whose coordinates are outside the window.
- In 3D viewing, there is a clear pipeline we follow:
Set Modelling Transformation-> Set Viewing Transformation-> Set Projection Transformation-> Set Viewport Transformation
- **Modeling and Viewing duality:**
        - We can create the same view from a camera at a certain location and orientation, by transforming the object.
        - To specify the camera, we need to specify the **eye point E** (where camera is located), **center of interest C** (the 3D point where camera is looking) and the **up direction V** of the camera.
        - We can use E, C, V and derive a transformation which, when applied to the model, would give the same view as we would really have the camera.
        - To translate the point/image in the camera coordinates system, we set a new system SUF. We can define F as E - C and then normalize it. to have length 1. If V is the up direction of the camera, we can **assume that V is perpendicular on F**, and so we have 2 axes and the 3rd one would be their cross product. But this assumption is not always true.
        - In order to avoid the errors of the assumption, we derive F as above, then we build the second coordinate as the product of F and V, normalized. The 3rd coordinate will simple be the product of the first 2.
        - **Observation:** if we apply a transformation on camera, it is the same thing as we apply its inverse on the object we look at.
 
### Week 3.2: Projections
- The mapping from 3D world to 2D coordinates is a projection; there are 2 classes of planar geometric projection:
        - Parallel projection: used in CAD and Engineering, allow precise measurements.
        - Perspective projection: used in computer graphics because of its realism sense.
- In **parallel projection**, the projection is the set of points at which the projectors intersect the projection plane. The projection plane is parallel with a world plane. Parallel edges remain parallel in the projection. Angles between edges may be distorted.
    - *Parallel projection: orthographic:* projectors are perpendicular to the projection plane; the projected image show only 2 of the 3 axes but there is no distortion of lengths and angles, so useful for CAD.
    - *Parallel projection: axonometric:* projectors are perpendicular to the projection plane, but the plane can have any orientation. We can see 3 axes but we have distortion of lengths and angles.
    - *Parallel projection: oblique:* the most general case of parallel projection, projectors can make any angle with the projection plane and the projection plane can have any orientation.
- **Perspective projection** models the way we see. The projection is the set of points at which the projectors intersect the projection plane. Center of projection, or "eye point", is a point, so projectors *converge*.
    - Objects further away become smaller, parallel edges may converge and angles between edges may be distorted.
    - 1 / 2 / 3 point perspective determines how many planes we can see.
- We define a 3D **view volume** which is the volume the camera can see.
- A view volume is a 3D shape, defined by 6 planes; for *parallel orthographic* projection, it's a cuboid, for perspective projection is a *frustum* (truncated pyramid).
- A problem for perspective projection is that after 1-point perspective transformation we lose data about depth (Z coordinate). The solution for this is **projection normalization**: it distorts the perspective to a unit cube and also the object in the perspective; however, the object is distorted in such a way that if we apply an orthographic projection on it, we get the same view as if we had applied perspective projection on the original object.
- **The viewport transformation:** after perspective division, we have 3D coordinates, in range [-1, 1], and we use X and Y to display them and Z to remove hidden surfaces.
 
### Week 4.1: Rendering
- We can model light-matter interaction in 2 ways:
    - **Locally:** we treat each object in a scene separately from any other object.
    - **Globally:** we treat all objects together and model their interactions.
- The might-matter interaction is very complex and we try to model (approximate) it.
- There are 3 broad classes of reflection:
    - **diffuse**: is absorption and uniform re-radiation (some wavelenghts are absorbed, other are reflected)
    - **perfect specular**: reflection is reflection at the air/surface interface (general definition for specular)
    - **imperfect specular**
- **Ambient illumination:** consider an environment with a light source; multiple reflections cause a general level of illumination in the scene; multiple reflections cause a general level of illumination in the scene.
- If the intensity of ambient is I, the amount of light diffusely reflected is **k * I** where k is *ambient reflection coefficient*, in range [0, 1]. On this model, each object is uniformly illuminated.
- **Directional lighting:** we need to model the effects of different angles of incidence and different distances from the light source. If the intensity if the source is I, the diffuse reflection has the intensity Ie = I * cos (a) where a is the angle of the light source with the surface.
- Local illumination **v2: I = ambient + diffuse = Ka * Ia + Ip * Kd * ( N * L)** where N * L is the vector product, the cos.
- Light intensity falls off with the square distance it traveled: for a distance d, the original intensity I becomes *Ie = I / 4 * pi * d^2* but for our pixel-space, a denominator which is a 2nd degree function on d works better. **V3 model also consider distance of the diffuse light.**
- *Modelling specular reflection*: V is vector pointing to the observer, L makes the angle a with N, and V makes the angle b with R, where R is the reflection of L. The wavelength is lambda. Then I specular is a function of a, b and lambda. This can be generalized to lights in different colors.
 
### Week 4.1: Rendering 2
- For a large angle of incidence, the Phong cos ^ n term is incorrect.
- For multiple light sources, we compute the illumination separately for each and sum.
- There are 3 shading methods:
    - Flat (constant): for each polygon, we compute color for one point and give that color to the whole polygon.
    - Gouraud (intensity): uses interpolation to smooth out the discontinuities between polygons. It approximates the normal of an underlying surface by computing the average of the normals where polygons share vertices. Edges must be tagged in the data structure to avoid interpolation across it![Algorithm](https://i.imgur.com/sAUcb9V.png)
    - Phong (normal-vector): as Gouraud, but instead of interpolating colors, we interpolate normal vectors along the scaleline. In this way we do not get any distortion highlights.![](https://i.imgur.com/8GM4ou3.png)
 
### Week 5: Textures
- We look at 2 methods for adding *surface detail* to rendered surfaces:
    - Texture mapping:
        - A texture is a 2D matrix of "texels".
        - We associate (u,v) texture coordinates with each vertex of a polygon, interpolate texture coordinates during scan-conversion and blend pixel color with texture color.
        - There is a problem which may occur: **resolution mismatches**
            - When pixel resolution > texture resolution (i.e. texels are bigger than pixels). If we do not filter, the image looks blocky. We can use **bilinear interpolation filter** which compute a texel color from adjacent texels, averaging horizontally and vertically.
            - When texture resolution > pixel resolution (i.e. pixels are bigger than texels). This lead to aliasing, as 2 consecutive pixels are mapped far apart. We can use **mipmap filtering**. The idea is that the further away from the viewpoint, the less detail we need. We use a set of texture maps and select which map to use, according to distance to to viewer.
            - *How to create a mipmap*: start with original texture and we create smaller versions of it, downsampling by 1/2, until reac a 1x1 texture. We keep each texture in memory. When rendering select one of the textures according to distance from viewpoint pr the two closest textures and do bilinear interpolation.
            - In both situations we need to **filter** the texture.
    - Textures can be used to add accurate illumination to a real-time scene: compute accurate diffuse illumination of the scene using a global model  and save rendered surfaces as textures (called **lightmaps**).
- Bump mapping: surfaces look bumpy because the surface normals change across the bumps so the top of the bumps appear brighter than sides.
    - Altering a surface normal: we introduce 2 unit vecotrs Nu and Nv, each orthogonal to the surface normal, scale them by *bu, bv* and then add them to normal.
    - We create the bump map by treating the value of each texel as a "height" which control the bumpiness of the surface.
 
## Image processing:
 
### Week 6.1: Introduction to image processing
- Anything that can generate a spatially coherent measurement of some propriety can be *imaged*.
 
### Week 6.2:
- Image resolution:
    - How many pixels: **spatial resolution**.
    - How many shades of grey/colors: **amplitude resolution**.
    - How many frames per second: **temporal resolution**.
- *Nyquist's theorem:* a periodic signal can be reconstructed if the sampling interval is half the period. Hence, an object can be detected if 2 samples span its smallest dimension, but we need more samples if we wan to recognise it.
- We can store each pixel on a byte, as we have 256 shades of gray.
- When we need to represent colors, we can use the fact that each color can be perceived as a mixture of shades of RGB.
 
 
# The real image processing (handbook)
## 1  Introduction
- **Sample applications:**
    - Character recognition
    - Biometry
    - Aerial photography
- A *computer vision* system has 3 important steps from the captured data to labeling it:
    - **Enhancement:** is any operation applied to the data to remove the degradations introduced by the capture process.
    - **Feature extraction:** operations to identify structures in the image that are useful for recognising the objects being analysed.
    - **Feature recognition:** processes will use the features just extracted to assign a label to the image or to parts of the image, by comparing the features against those derived from previously labeled objects.
## 2  Image representation
### 2.1 Introduction
- The starting point of our examination of computer vision systems is a captured digital image.
- There are some very important requirements of image capture:
    -  *Spatial and brightness resolutions*: this is what is required to capture images that contains our needed data.
    - *Factors that limit resolution*
    - *Representations of captured data*: monochrome image data is invariably represented using **one byte per pixel** whilst for color images we use **3 bytes, one for each color (RGB)**.
    - *Camera calibration*: is essentially the process of correcting the image data for the defects introduced by the camera's optical system.
### 2.2 The human visual system
- The eye regulate the amount of light entering in it, focus the rays of light on retina and retina encode data into nerve signals.
- Iris size is a fine control over eye adaption but the main control is for the retina, changing its sensitivity. Also, retina performs data reduction.
- Spatial and temporal differences are computed.
- There are 3 factors influencing the quality of the perceived data: angular resolution of the eyes, colur sensitivity and brightness sensitivity.
### 2.3 Image quality measurements
- The quantity of energy onto a photosensitive detector which is absorbed over a unit of time is measured digitally, and the measurements are assembled into an image. All these processes are subject to inaccuracies.
### 2.4 Sources of degradation
- Noise in the electronics that converts radiant energy to an electrical signal.
- The camera lens distort the image.
- Geometrical distortion: arises because the best focus of the scene is behind it. This is the problem of drawing a map.
- Scattering: occurs when rays of light reflected by the surface to be viewed are dispersed by material in their path to the detector. E.g. Fog
- The refractive index of the glass or plastic from which a lens is constructed.
- Blooming and saturation: the effect when a bright point source is imaged, the camera's optical system will blur the image on that point and on neighbouring cells.
- The sensitivity of the detector is not uniform.
- Overflow or clipping of a signal occurs whenever the signal is of excessive amplitude.
### 2.5 Signal to noise ratio
- Noise in an imaging system is defined as any deviation of the signal from its expected value. The most commonly seen type is Gaussian noise, described by uniform distribution.
- The consequence of the image being corrupted is that any pixel will have a different value from the expected one.
- By taking an uniform image and measure the variation in the image data, we can compute the noise amplitude (this procedure is called image histogram).
- **Signal to noise ratio** is the ratio of the signal's amplitude to the noise amplitude that we have measured. (Mathematically SNR = 20 * log10 (signal/noise) )
### 2.6 Image resolution
- When a vision system is being designed, the resolution of the images should be specified (useful to determine what objects can be seen in the data).
- The resolutions which must be defined are:
    - spatial (roughly the number of pixels), which is given by:
        - **Field of view**: the angle subtended by rays of light that hit the detector at the extreme edges of image.
        - **Angular resolution**: can be used to specify how close an object must be to be seen. It can be computed as the ratio of the smallest visible object to the range.
    - **Brightness and color** (the number of shades of grey or colors in the image)
        - The brightness resolution is defined as the number of shades of grey that may be discerned in a *monochrome image* or the number of distinct colors in a *color image*.
        - If the total brightness scale is divided into bins of 6 times noise amplitude, we can be sure that a sample falling into the center of a certain bin, it really belong to the bin. In other words, if we look at the formula for SNR, take the signal and divide by 6 we get the number of gray values camera can perceive.
    - temporal (the number of frames captured or processed per second)
        - the lower limit on the rate at which results should be calculated should be computed, in order to know if we need the appearance of real time processing.
### 2.7 Color representation model
- Colors are computed with the model C = rR +gG +bB
- A problem is that is it perceptually non linear; if we change a color's RGB value by a fixed amount, the perceived effect is dependent on original values.
- This problem led to adoption of perceptual color spaces: each pixel has a HSV where V is the intensity(brightness), H is underlying color and S is the saturation (depth).
## 3: Image transforms and feature extraction
###3.1 Introduction
- Feature extraction is defined as any operation that extracts information from an image.
- And image processing operation is an operation which manipulates the image without altering it size but it may alter the size of each pixel.
- A point transform manipulate the grey color value of an individual pixel without considering neighbouring values.
### Week 7.1:
## **Notes, observations, tricks:**
    - If we express 2 normalized vectors [x1 y1 z1 1], their dot product is their cosine.
    - 4 x 4 matrices are used for 3D transformations because with 3 x 3 cannot move the origin, which is required by rotations and translations.
    - In a graphics pipeline, a fragment is a candidate pixel, which may or may not be displayed.
    - A vector based display can draw lines, text and points.
    - In 2D we rotate with respect to a point; in 3D we rotate with respect to a 3D vector.
    - If we need to view a transformed model, fist we transform it and then model the view.
    - The main purpose of projection normalization is to keep the the z coordinates, which would otherwise be set to z-value of the projection plane.
    - The "n" paramether in Phong specular term tells how shiny the surface is: n small -> not very shiny.
    - Ks does not allow to render metals correctly, as it does not capture iteractions between light and metals.
    - Mach banding is the ilusion of changes in intensity greater than they really are.
    - Surfaces look bumpy because we alter the normals during rendering.