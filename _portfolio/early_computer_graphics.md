---
title: "Computer Graphics Series"
excerpt: "A series of projects showcasing computer graphics techniques."
image_path: assets/images/calpoly/474_bunny.png
# header:
#   image: /assets/images/calpoly/474_bunny.png
# sidebar:
#   - title: "Role"
#     image: http://placehold.it/350x250
#     image_alt: "logo"
#     text: "Developer"
#   - title: "Responsibilities"
#     text: " "
gallery:
  - url: /assets/images/calpoly/474_face_blend.gif
    image_path: assets/images/calpoly/474_face_blend.gif
    alt: "Mesh blend while parsing text"
  - url: /assets/images/calpoly/471_bunny.gif
    image_path: assets/images/calpoly/471_bunny.gif
    alt: "Geomtry Shader to create exploding effect"
  - url: /assets/images/calpoly/474_plane_curve.gif
    image_path: assets/images/calpoly/474_plane_curve.gif
    alt: "B-spline interpolations for path animations"
  - url: /assets/images/calpoly/474_fbx_slomo_animation.gif
    image_path: assets/images/calpoly/474_fbx_slomo_animation.gif
    alt: "FBX slomo animation"    
  - url: /assets/images/calpoly/572_ssao.PNG
    image_path: assets/images/calpoly/572_ssao.PNG
    alt: "SSAO"
tags:
  - ComputerGraphics
  - C++
  - OpenGL  
  - Animation
---

## Small Projects
_This series of short projects were created for Computer Graphics courses at Cal Poly: Intro to Computer Graphics & Computer Graphic Animation._

{% include gallery caption="" %}

## Animation Final Project: Flying Dragon and Path Editor
Our final project features a combination of computer graphics techniques used in animation. This project was created in a team of two with cross platform development (Windows & Mac). 

### FBX Dragon 
- Loaded into the rendering pipeline using Autodesk's FBX SDK. 
- Interpolate between two animations (running and flying) using mesh blending
### Path Editor
- Paths are created using a sequence of control points, which contain position and orientation information in 3D space. 
- Add new control points in-game and update the path in real-time

### Key Technologies
- B-spline interpolation
- Mesh blending

<figure>
    <a href="/assets/images/calpoly/474_fbx_dragon.gif"><img src="/assets/images/calpoly/474_fbx_dragon.gif"></a>
	<figcaption>Final Project. Features an animated mesh (.fbx) that </figcaption>
</figure>