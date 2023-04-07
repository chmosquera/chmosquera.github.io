---
title: Computer Graphics Series
date: 2019-12-31
feed: show
showhomefeed: true
image_path: assets/images/2019/computer_graphics/474_bunny.png
tags:
  - Computer Graphics
  - C++
  - Animation
---

Various real-time rendering techniques developed on a custom renderer in C++ and OpenGL.

## Sinusoidal Explosion

For this project, I created a "sinusoidal explosion". To simulate the explosion, I translated the object's normal data in a geometry shader and used a sin wave to calculate the translation. 
![Sinusoidal Explosion](/assets/images/2019/computer_graphics/471_bunny.gif)

## SSAO
An implementation of screen space ambient occlusion.
![SSAO](/assets/images/2019/computer_graphics/572_ssao.PNG)


## Animation

### Face Blend
This face blending technique interpolates between four different geometries. Each letter of the alphabet is mapped to a geometry
![Face blend](/assets/images/2019/computer_graphics/474_face_blend.gif)

### Slow motion animation
![Slomo animation](/assets/images/2019/computer_graphics/474_fbx_slomo_animation.gif)

### Plane Curve
![B-spline curve demo](/assets/images/2019/computer_graphics/474_plane_curve.gif)

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
![Final Project. Features an animated mesh (.fbx) that travels along a b-spline path](/assets/images/2019/computer_graphics/474_fbx_dragon.gif)