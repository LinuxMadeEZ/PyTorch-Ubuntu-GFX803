# PyTorch-Ubuntu-GFX803
Torch, TorchVision and TorchAudio compiled on Ubuntu 22.04 LTS for GFX803 arch.

## Video on YouTube to help you configure everything.
- https://youtu.be/lCOk6Id2oRE

## 💻 Requirements

This is what I recommend. If you want to use anything other than this, you will be on your own.

- Ubuntu 22.04 LTS
- Python 3.10(Default)


## AMDGPU and ROCm Repositories

Download keys:

```
wget https://repo.radeon.com/rocm/rocm.gpg.key -O - | gpg --dearmor | sudo tee /etc/apt/keyrings/rocm.gpg > /dev/null
```


Add AMDGPU repo:

```
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/rocm.gpg] https://repo.radeon.com/amdgpu/6.2/ubuntu jammy main" | sudo tee /etc/apt/sources.list.d/amdgpu.list
```


Add ROCm repo:

```
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/rocm.gpg] https://repo.radeon.com/rocm/apt/5.7.3 jammy main" | sudo tee --append /etc/apt/sources.list.d/rocm.list
```

Set ROCm repo priority:
```
echo -e 'Package: *\nPin: release o=repo.radeon.com\nPin-Priority: 600' | sudo tee /etc/apt/preferences.d/rocm
```


## AMDGPU and ROCm Packges

AMDGPU and other necessary packages(You may need to run "sudo apt update" first):
```
sudo apt install amdgpu-dkms google-perftools python3-virtualenv python3-pip python3.10-venv git
```

ROCm packages:
```
sudo apt install rocm-hip-sdk5.7.3 rocminfo5.7.3 rocm-smi-lib5.7.3 hipblas5.7.3 rocblas5.7.3 rocsolver5.7.3 roctracer5.7.3 miopen-hip5.7.3
```


## ROCm Post-installation

```
sudo tee --append /etc/ld.so.conf.d/rocm.conf <<EOF
/opt/rocm/lib
/opt/rocm/lib64
EOF
sudo ldconfig
```
```
export PATH=$PATH:/opt/rocm-5.7.3/bin
```

## Get Stable Diffusion WebUI
```
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
```

## Options for low-vram(WebUI)
```
--precision full --no-half --lowvram --opt-split-attention-v1 --upcast-sampling
```

## Get ComfyUI
```
git clone https://github.com/comfyanonymous/ComfyUI.git
```
