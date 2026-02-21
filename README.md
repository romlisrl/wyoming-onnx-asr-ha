[![Buy Me a Coffee](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://buymeacoffee.com/romlis)
## Wyoming ONNX ASR container for Home Assistant on [ONNX ASR](https://github.com/istupakov/onnx-asr)
### STT (Speech-to-Text) service for Home Assistant using ONNX ASR models
This project provides a Wyoming protocol-compatible Automatic Speech Recognition (ASR) server powered by ONNX models. It is designed to be used with voice integrations such as Home Assistant’s Wyoming ecosystem, enabling local speech-to-text processing without relying on external APIs.

### 🚀 Features

- 🧠 Automatic Speech Recognition (ASR) server for Wyoming-compatible voice systems
- 🗣️ Supports a variety of ONNX models (e.g., Parakeet, GigaAM, Whisper, etc.)
- ⚡ Includes optimized pipelines for CPU or GPU inference
- 📦 Can be run standalone or inside Docker
- 🏡 Integrates with Home Assistant Voice Assistants via the Wyoming protocol

### 🐳 Using Docker

A compose.yaml is included for easy container deployment:
```
services:
  asr:
    image: ghcr.io/romlisrl/wyoming-onnx-asr-ha:latest
    container_name: wyoming-onnx-asr
    restart: unless-stopped
    ports:
      - 10305:10305
    command: --model gigaam-v3-ctc --uri tcp://0.0.0.0:10305 --quantization int8 --debug
    volumes:
      - ./data:/data
    environment:
      - HF_HOME=/data
```
### 🧩 Recommended Models
Different ONNX models are supported. Examples:

Model	Description

`gigaam-v3-ctc`	Efficient and accurate English/Russian ASR

`nemo-parakeet-tdt-0.6b`	Nvidia Parakeet TDT English

`onnx-community/whisper-base`	Whisper baseline model

Model choice affects latency and accuracy. Larger models require more memory.

### 🛠️ Configuration Options
You can fine-tune:

URI: network address to serve (e.g., tcp://0.0.0.0:xxxx)

Quantization: reduce model size/speed trade-off

Device: CPU or CUDA GPU

Debug logging: for troubleshooting

### 📦 Docker / Deployment Notes
The included compose.yaml can be customized with environment variables, mount points, and model paths.
Be sure to expose ports correctly for Home Assistant’s Wyoming integration.

### ❓ Integration with Home Assistant
Once the server runs and listening:

Add Wyoming Protocol integration in Home Assistant
Provide the server URI (e.g., host:10305)
Home Assistant will send audio and receive text responses

### 🙏 Credits & License
Forked from mitrokun/wyoming_stt_onnxasr and adapted for broader usage.
