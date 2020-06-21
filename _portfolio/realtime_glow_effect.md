---
title: "Real-time Glow Effect"
excerpt: "An implementation of a glow effect."
image_path: assets/images/calpoly/572_glow_effect/Glow_img_2.PNG
# header:
#   image: /assets/images/calpoly/572_glow_effect/Glow_img_2.PNG
# sidebar:
#   - title: "Role"
#     image: http://placehold.it/350x250
#     image_alt: "logo"
#     text: "Developer"
#   - title: "Responsibilities"
#     text: " "   
tags:
  - ComputerGraphics
  - C++
  - OpenGL  
  - Lighting
---

In this project, I implement a lighting technique to create the effect of objects glowing in the scene.

## Pipeline
1. Render scene to two textures: color and glow mask

<figure>
    <a href="/assets/images/calpoly/572_glow_effect/ColorTexture.PNG"><img src="/assets/images/calpoly/572_glow_effect/ColorTexture.PNG"></a>
	<figcaption>Color Texture </figcaption>
</figure>

<figure>
    <a href="/assets/images/calpoly/572_glow_effect/GlowMaskTexture.PNG"><img src="/assets/images/calpoly/572_glow_effect/GlowMaskTexture.PNG"></a>
	<figcaption>Glow Mask</figcaption>
</figure>


2. Blur the glow mask using 2D Gaussian Blur

<figure>
    <a href="/assets/images/calpoly/572_glow_effect/GlowMaskBlurredTexture.PNG"><img src="/assets/images/calpoly/572_glow_effect/GlowMaskBlurredTexture.PNG"></a>
</figure>

3. Blend the color texture with the glow mask texture using additive blending

<figure>
    <a href="/assets/images/calpoly/572_glow_effect/Glow_img_1.PNG"><img src="/assets/images/calpoly/572_glow_effect/Glow_img_1.PNG"></a>
</figure>

<figure>
    <a href="/assets/images/calpoly/572_glow_effect/Glow_img_2.PNG"><img src="/assets/images/calpoly/572_glow_effect/Glow_img_2.PNG"></a>
</figure>

## Resources
- [LearnOpenGL: Bloom](https://learnopengl.com/Advanced-Lighting/Bloom)
- [GPU Gems: Real-Time Glow](http://developer.download.nvidia.com/books/HTML/gpugems/gpugems_ch21.html)
- [Unreal Engine: Bloom Post Process Effect](https://docs.unrealengine.com/en-US/Engine/Rendering/PostProcessEffects/Bloom/index.html)