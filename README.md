# home-improvement

Exterior design using stable-diffusion 🏡

#### References

1. `CompVis` Stable Diffusion  
   [High-Resolution Image Synthesis with Latent Diffusion Models](https://github.com/CompVis/stable-diffusion)

2. `Basujindal` fork optimisation for lesser VRAM  
   [Optimized Stable Diffusion (Sort of)](https://github.com/basujindal/stable-diffusion)

# 🖼️→🖼️ `img2img`

Using an input image to create unlimited variations.

- Img from [`jansteffen` on r/stablediffusion](https://www.reddit.com/r/StableDiffusion/comments/wwmjih/converting_a_minecraft_screenshot_into_a_painting/)

![img2img example](media/img2img_examples.JPG)

# 🖼️→🖼️ `img2img` with custom images

```py
pstring = "An fantasy english family home, dog in the foreground, fantasy, illustration, trending on artstation"
input_img = "../inputs/halle_at_home_2021_s.JPG"

strength = range(30, 75, 5)
for s in strength:
    !python optimizedSD/optimized_img2img.py --prompt "{pstring}" --init-img {input_img} --strength {s*0.01} --seed 200 --outdir {outdir}
```

![home example](media/home_pic_dog.JPG)

</br>  
</br>

# 🖼️→🖼️ `img2img` with `hand-drawn` sketch

[Example shown on `CompVis` project page](https://github.com/CompVis/stable-diffusion#image-modification-with-stable-diffusion) 🔗

![img2img_given_example](media/img2img_given_example.JPG)
