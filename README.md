# home-improvement

Exterior design using stable-diffusion 🏡 → General [install instructions](https://github.com/hlky/stable-diffusion/wiki/Installation).

#### References

1. `CompVis` Stable Diffusion  
   [High-Resolution Image Synthesis with Latent Diffusion Models](https://github.com/CompVis/stable-diffusion)

2. `Basujindal` fork optimisation for lesser VRAM  
   [Optimized Stable Diffusion (Sort of)](https://github.com/basujindal/stable-diffusion)

3. `ControlNet`  
https://github.com/lllyasviel/ControlNet



</br>  



# 🖼️→🖼️ `img2img` with custom images

```py
pstring = "An fantasy english family home, dog in the foreground, fantasy, illustration, trending on artstation"
input_img = "../inputs/halle_at_home_2021_s.JPG"

strength = range(30, 75, 5)
for s in strength:
    !python optimizedSD/optimized_img2img.py --prompt "{pstring}" --init-img {input_img} --strength {s*0.01} --seed 200 --outdir {outdir}
```

![home example](media/home_pic_dog.JPG)



# 🎨→🖼️ `controlnet` concept generation

* 🏠 Exterior design with stable diffusion with [controlnet](https://github.com/lllyasviel/ControlNet), canny-fp16 edge detection.  


```py
prompt = "modern english front garden, with traditional lush green lawn and striking architectural design"
```

![controlnet home example](media/controlnet_home.png)
</br>  

* Alternative edge control, using `hed-fp16`  
![controlnet backyard example](media/controlnet_backyard.png)


# 🎨→🖼️ Generation from scratch with `MidJourney` + `controlnet` 
1. **Midjourney** generation from prompt
```py
line art drawing of top down landscape 
architectural plan of a classic english garden --s 1 --v 4 --q 2 --s 5000
```
2. **Stable Diffusion** + **ControlNet** with canny-fp16
```py
landscape garden with flowers, professional photograph, acurate, intricate
```
![midjourney example](media/controlnet_midjourney.png)



</br>  


</br>  </br>  

# 🌐 Stable Diffusion
</br>


# 🖼️→🖼️ `img2img` iterative improvements

Example from [`argaman123`](hhttps://old.reddit.com/r/StableDiffusion/comments/wzlmty/its_some_kind_of_black_magic_i_swear/) 🔗

- Using the output of one image to generate a new image.
- This iterative process can make increasingly complex and customizable images.

> _A distant futuristic city full of tall buildings inside a huge transparent glass dome, In the middle of a barren desert full of large dunes, Sun rays, Artstation, Dark sky full of stars with a shiny sun, Massive scale, Fog, Highly detailed, Cinematic, Colorful_

</br>

![img2img_given_example](inputs/011_iterative_design.JPG)

![img2img_given_example](inputs/021_iterative_design.JPG)

```py
!python optimizedSD/optimized_img2img.py --prompt "{pstring}" --init-img {input_img} --strength 0.8 
--n_iter 2 --n_samples 3 --H 512 --W 512 --seed 12 --outdir {outdir} --ddim_steps 200
```

</br>
</br>


# 🖼️→🖼️ `img2img` with `strength` variation

Using an input image to create unlimited variations.

- Img from [`jansteffen` on r/stablediffusion](https://www.reddit.com/r/StableDiffusion/comments/wwmjih/converting_a_minecraft_screenshot_into_a_painting/)

![img2img example](media/img2img_examples.JPG)

</br>


</br>

# 🖼️→🖼️ Inpainting with `diffusers`

Inpainting allows applying a layer mask to an area of interest – and then running `img2img` with a `text prompt` to generate new content.

   - 📹 Tutorial from [1littlecoder](https://www.youtube.com/watch?v=N913hReVxMM) on youtube and accompanying [Colab Notebook](https://colab.research.google.com/drive/1R2HJvufacjy7GNrGCwgSE3LbQBk5qcS3?usp=sharing#scrollTo=BnobY4zi0Pjs).

   - 🤗 Uses [Huggingface `diffusers` library](https://github.com/huggingface/diffusers).

Example: Adding a dragon to the castle `(1)` and then adding flaming rubble to the gate `(2)`.

![Inpainting_given_example](media/castle_inpainting.png)

```py
prompt = "A fantasy castle with a dragon defending. Trending on artstation, 
          precise lineart, award winning, divine"

with autocast("cuda"):
    images = pipe(prompt=prompt, init_image=init_image, mask_image=mask_image, strength=0.7)["sample"]
```


</br>
</br>


# 📱🖼️ Gradio WebUI by `hlky` 

Gradio webui by hlky https://github.com/sd-webui/stable-diffusion-webui

* Clone repo
* Run `webui.bat` from windows explorer


</br>
</br>

# Training Data Visualisations

`LAION-Aesthetics v2 6+` on Datasette:

From [this blog post](https://waxy.org/2022/08/exploring-12-million-of-the-images-used-to-train-stable-diffusions-image-generator/), and [Hackernews](https://news.ycombinator.com/item?id=32655497) conversation.

1. Top Artists  
   https://laion-aesthetic.datasette.io/laion-aesthetic-6pls/artists?_sort_desc=image_counts

2. Search by Artist  
   https://laion-aesthetic.datasette.io/laion-aesthetic-6pls/images?_search=%22Thomas+Kinkade%22&_sort=rowid


</br>
</br>

