---
title: Real-time Glow Effect
date: 2019-09-01
feed: show
showhomefeed: true
image_path: assets/images/2019/572_glow_effect/Glow.PNG
tags:
  - Computer Graphics
  - C++
---

In this project, I implement a lighting technique to create the effect of objects glowing in the scene.

## Pipeline
1. Render scene to two textures: color and glow mask
	![Color Texture](assets/images/2019/572_glow_effect/ColorTexture.PNG)
![Glow Mask](assets/images/2019/572_glow_effect/GlowMaskTexture.PNG)

2. Blur the glow mask using Gaussian Blur.
![Glow mask with Gaussian Blur](assets/images/2019/572_glow_effect/GlowMaskBlurredTexture.PNG)
3. Blend the color texture with the glow mask texture using additive blending
![Blended color texture and glow mask](assets/images/2019/572_glow_effect/Glow.png)
## Resources
- [LearnOpenGL: Bloom](https://learnopengl.com/Advanced-Lighting/Bloom)
- [GPU Gems: Real-Time Glow](http://developer.download.nvidia.com/books/HTML/gpugems/gpugems_ch21.html)
- [Unreal Engine: Bloom Post Process Effect](https://docs.unrealengine.com/en-US/Engine/Rendering/PostProcessEffects/Bloom/index.html)