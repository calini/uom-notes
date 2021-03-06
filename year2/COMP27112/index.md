<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=UA-113560131-1"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'UA-113560131-1');
</script>

# COMP27112 - Computer Graphics and Image Processing

## Links

* [Course Material](https://online.manchester.ac.uk/webapps/blackboard/content/listContent.jsp?course_id=_49989_1&content_id=_5832582_1)
* [OpenGL Reference Manual](https://online.manchester.ac.uk/bbcswebdav/pid-5832611-dt-content-rid-20615314_1/xid-20615314_1)
* [Image Processing Notes](https://online.manchester.ac.uk/bbcswebdav/pid-5832611-dt-content-rid-20615313_1/xid-20615313_1)

Other useful links:
* [OpenGL Support](http://studentnet.cs.manchester.ac.uk/ugt/COMP27112/OpenGL/) (Get it working on Mac, Windows or Linux)
* [GLUT Reference Manual](http://studentnet.cs.manchester.ac.uk/ugt/COMP27112/doc/glut-reference.pdf)
* [OpenGL (2.1) Reference](https://www.khronos.org/registry/OpenGL-Refpages/gl2.1/)

Examples and simulations:
* [WebGL Water](http://madebyevan.com/webgl-water/)
* [For the Birds - Pixar](https://www.youtube.com/watch?v=AkFuvTHaMUE)

Lecturers: [Toby Howard](mailto:toby.howard@manchester.ac.uk) (course leader), [Tim Morris](mailto:tim.morris@manchester.ac.uk)

## Table of contents

* Interactive Computer Graphics "synthetic" (Toby)
    * [Introduction, history and pipelines](1-intro/index.md)
    * [Transformations](2-transformations/index.md)
    * [Polygons and pixels](3-polygons/index.md)
    * [3D Viewing](4-3d-viewing/index.md)
        * [The Camera](4-3d-viewing/index.md#camera)
        * [Projections](4-3d-viewing/index.md#projections)
    * [Rendering]()
        * [Local Illumination](5-rendering/index.md/#illumination)
        * [Shading and Interpolation](5-rendering/index.md/#shading-interpolation)
        * [Surface Detail](5-rendering/index.md/#shading)
* Image Processing "analytic" (Tim)
    * [Image Processing](6-image-processing/index.md)
    * [Point Processing](7-point-processing/index.md)
    * [Region Processing](8-region-processing/index.md)
    * [Region Detection and Description](9-region-detection/index.md)
	
## Timetable

* Labs
	* Thursdays 9:00, Week A in *LF31*
    * 5 x 2 hour lab sessions + marking session (10 May 9:00)
    * Deadline before start of next lab
    * No further extensions
	* 20% of course mark
* Coursework Assignments
    * 5 exercises (Scheduled for Week B)
    * 5% of course mark
* Weekly quizzes
    * Self-assessment quizzes
    * Do not count towards mark
    * Check Blackboard
* Lectures
	* Mondays 14:00 in *Kilburn LT1.1*
	* Thursdays 14:00 in *Kilburn LT1.1*
* Exam
    * 2 Hours
    * No optional parts
    * Everything is examinable
    * Online (2016/17 onwards)
    * 75% of course mark

## Labs

1. [x] [Kwake World](https://online.manchester.ac.uk/bbcswebdav/pid-5832612-dt-content-rid-20614199_1/xid-20614199_1) (1 session)
2. [ ] [The Orrey](https://online.manchester.ac.uk/bbcswebdav/pid-5832612-dt-content-rid-20614200_1/xid-20614200_1) (2 sessions)
3. [x] [Point Processing Transformations](https://online.manchester.ac.uk/bbcswebdav/pid-5832612-dt-content-rid-20615301_1/xid-20615301_1) - 26 April 9:00
4. [x] [Image Enhacement](https://online.manchester.ac.uk/bbcswebdav/pid-5832612-dt-content-rid-20615302_1/xid-20615302_1) - 10 May 9:00

* Can I use C++? Yes
* Can I use C#/Objective C? Yes, but:
    * Keep it to the C family
    * TA help not guaranteed, Pp **OpenGL** not recommended

## Coursework
1. [x] [Introducing OpenGL](https://online.manchester.ac.uk/bbcswebdav/pid-5832613-dt-content-rid-20614193_1/xid-20614193_1) - 16 February 17:00 
2. [x] [3D modelling and viewing](https://online.manchester.ac.uk/bbcswebdav/pid-5832613-dt-content-rid-20614194_1/xid-20614194_1) - 2 March 17:00 
3. [x] [Lighting and texture](https://online.manchester.ac.uk/bbcswebdav/pid-5832613-dt-content-rid-20614196_1/xid-20614196_1) - 16 March 17:00
4. [x] [Read, modify and save an image](https://online.manchester.ac.uk/bbcswebdav/pid-5832613-dt-content-rid-20614197_1/xid-20614197_1) - 30 March 17:00
5. [x] [Region Based Processing](https://online.manchester.ac.uk/bbcswebdav/pid-5832613-dt-content-rid-20614198_1/xid-20614198_1) - 4 May 17:00

## Course aims

* To introduce the theory and practice of interactive 3D computer graphics and image processing
* To be able to:
    * Describe the principles of interactive computer graphics
    * Design systems using fixed-pipeline OpenGL
    * Apply the mathematics of 3D transformations and viewing
    * Describe principles of the rendering pipeline
    * Describe principles of image processing
    * Implement fundamental image processing algorithms

## Recommended textbooks

* [*OpenGL Programmer's Guide*](http://www.glprogramming.com/red/) *aka "The Red Book"* - Dave Shreiner
* *Interactive Computer Graphics: A Top-Down Approach Using OpenGL (4th Edition)* - Edward Angel
* *Open GL: A primer* - Edward Angel
* *Image Processing, Analysis and Machine Vision* - Hlavac and Sonka
* *The Image Processing Cookbook* - John C. Russ
* *Computer Vision and Image Processing* - Tim Morris
