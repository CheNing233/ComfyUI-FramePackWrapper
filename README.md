# ComfyUI Wrapper for [FramePack by lllyasviel](https://lllyasviel.github.io/frame_pack_gitpage/)

A fork of https://github.com/kijai/ComfyUI-FramePackWrapper

# Notes

## This fork is not updated frequently

如果追求稳定，请使用原分支

该分支用于个人尝鲜，优先添加一些不稳定的、未经确认的功能，并且不会经常更新

同时这里有个人使用 RTX 3050 Laptop 4G 和 RTX 2080 Ti 11G 的一些测试

## Modifications on this fork (2025.05.05 update)

No changes. (Already sync with the original)

## Work in 20 series GPU

如果你需要运行在 2080ti 11G 等不支持 bf16 的 GPU

你可以尝试使用 https://huggingface.co/Kijai/HunyuanVideo_comfy/blob/main/hunyuan_video_vae_fp32.safetensors

并将 `base_precision` 更改为 `fp32`

## OOM

我已经成功在 RTX 3050 Laptop 4G 和 RTX 2080 Ti 11G 上测试通过

尽管要求的显存降到 4G，但你仍然需要大量的运存（物理运存+虚拟运存），幸运的是虚拟运存可以调，最好设置 60G 以上的虚拟运存

如果你在 VAE 解码爆显存，那么你可以把 VAE 解码分块大小从 256 降到 128 甚至更低

## About Error

### FramePackSampler.process() got an unexpected keyword argument 'image_end_embeds'

该fork以前的首尾帧和当前官方首尾帧的实现方式不一样，更换新的工作流即可解决

## Other useful

- [支持了多帧渲染的fork](https://github.com/nirvash/ComfyUI-FramePackWrapper)

# WORK IN PROGRESS

Mostly working, took some liberties to make it run faster.

Uses all the native models for text encoders, VAE and sigclip:

https://huggingface.co/Comfy-Org/HunyuanVideo_repackaged/tree/main/split_files

https://huggingface.co/Comfy-Org/sigclip_vision_384/tree/main

And the transformer model itself is either autodownloaded from here:

https://huggingface.co/lllyasviel/FramePackI2V_HY/tree/main

to `ComfyUI\models\diffusers\lllyasviel\FramePackI2V_HY`

Or from single file, in `ComfyUI\models\diffusion_models`:

https://huggingface.co/Kijai/HunyuanVideo_comfy/blob/main/FramePackI2V_HY_fp8_e4m3fn.safetensors
https://huggingface.co/Kijai/HunyuanVideo_comfy/blob/main/FramePackI2V_HY_bf16.safetensors
